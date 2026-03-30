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

I call these comands on the standard print end and start macros
