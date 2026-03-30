---
tags:
  - electronics
  - network
  - diary
created: 2026-03-30
---

# poor mans presence sensor 

Today i tackled the classic automation use-case to turn on and off stuff depending on the state of some presence sensors. This in my experience is what makes up the majority of the [ROI](https://it.wikipedia.org/wiki/Return_on_investment) of a automation system. Granted for now it's just the workbench, a light and some screens, so it does not cut down on wasted energy that much, the real magic is when we factor in HVAC and window sensors, but i'm very much not there yet.
On that note let me quickly write down what i did today:
- Made esphome work on the cheap esp32-c3 devboards (unrelated)
- I extracted my IRK code from my phone
- I integrated my phone as a private BLE device
- Using Bermuda i can now know the distance between the server (in my room) and my phone
- Made a helper template switch for manual operation of the system
- Interacting with my 3d printer to avoid removing power while printing
- Using node-RED i can then implement the logic for sensing and actuation 

#### ESPHome
You can read this [[misc 1]] to check out what was wrong
#### IRK
I was able to use ESPHome and a specific irk extraction firmware to get the irk code of my phone, specifically used [Derek Seaman irk-capture ](https://github.com/DerekSeaman)firmware, very nice, worked nicely first try, well done mr. Seaman.
#### private BLE device
Using that IRK i am just able to integrate it as a private BLE device on stock hass
#### Bermuda
This is where it gets interesting. Using [HACS](https://www.hacs.xyz/) i am able to install Bermuda that instantly gets the private BLE device and have a fast refresh distance entity for my phone
#### manual override
Just a basic switch template:
![[Pasted image 20260330233747.png]]
This is basically acts as a global variable between node-RED and home assistant

# 3d printer
The 3d printer setup actually is quite convoluted, and it also does introduce a circular usage dependency. That's the reason we are going to look at node-RED in here:
![[Pasted image 20260330234517.png]]
(Yes i know i am using GET)
This just set global variables based on the 3d printer state, where i defined macros to actually use these endpoint using gcode shell commands and curl:
```ini
[gcode_shell_command _notify_printing]
command: curl -s "http://192.168.1.22:1880/printer/printing"
timeout: 10.
verbose: False

[gcode_shell_command _notify_done]
command: curl -s "http://192.168.1.22:1880/printer/done"
timeout: 10.
verbose: False

[gcode_shell_command _poweroff_via_nodered]
command: curl -s "http://192.168.1.22:1880/printer/off"
timeout: 10.
verbose: False

[gcode_macro _AUTO_POWEROFF]
description: Stores whether printer should power off after print
variable_enabled: 0
gcode:
    RESPOND MSG="Auto poweroff is {'ON' if printer['gcode_macro _AUTO_POWEROFF'].enabled|int == 1 else 'OFF'}"

[gcode_macro _AUTO_POWEROFF_ON]
description: Enable auto poweroff at end of print
gcode:
    SET_GCODE_VARIABLE MACRO=_AUTO_POWEROFF VARIABLE=enabled VALUE=1
    RESPOND MSG="Auto poweroff enabled"

[gcode_macro _AUTO_POWEROFF_OFF]
description: Disable auto poweroff at end of print
gcode:
    SET_GCODE_VARIABLE MACRO=_AUTO_POWEROFF VARIABLE=enabled VALUE=0
    RESPOND MSG="Auto poweroff disabled"
```
I call these comands on the standard print end and start macros
```ini
[gcode_macro START_PRINT]
gcode:
  {% set BED = params.VALUE|default(60)|float %}
  RUN_SHELL_COMMAND CMD=_notify_printing
  M190 S{BED}
  
  G90 ; use absolute coordinates
  M83 ; extruder relative mode
  G4 S30 ; allow partial nozzle warmup
  {% if printer.toolhead.homed_axes != "xyz" %}
    G28
  {% endif %}
  BED_MESH_CALIBRATE
  SMART_PARK
  
[gcode_macro END_PRINT]
gcode:
    # Turn off bed, extruder, and fan
    M140 S0
    M104 S0
    M106 S0
    # Move nozzle away from print while retracting
    G91
    G1 X-2 Y-2 E-3 F3000
    # Raise nozzle by 10mm
    G1 Z10 F3000
    G90
    G1 Y200
    RUN_SHELL_COMMAND CMD=_notify_done
    {% if printer["gcode_macro _AUTO_POWEROFF"].enabled|int == 1 %}
      RESPOND MSG="Auto poweroff is enabled, shutting down soon"
      RUN_SHELL_COMMAND CMD=_poweroff_via_nodered
    {% else %}
      RESPOND MSG="Auto poweroff is disabled"
    {% endif %}
```
Here is where thing get weird, the "turn off when done printing" logic sits on the printer firmware, since that's the best place to determine when a print is done, but the presence logic sits on node-RED, so the printer notifies the state to it, hence the circular dependency (i'm ok with this since it just reflects on the added feature and not on both systems functionalities).

#### Node-RED logic
![[Pasted image 20260330235503.png]]
This 