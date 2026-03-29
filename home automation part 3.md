---
created: 2026-03-29
tags:
  - network
---
## 14:42
Yesterday i was able to make everything work and now i'm able to sync my phone alarm to the homeassistant server.
The flow is actually quite simple, it is made of 3 parts:
- A node-RED flow that just have 2 http inputs and parses them
- On the Hass side i just have 2 helper entities a datetime and a switch to enable the alarms, then i can just use blueprints for the parabolic sunrise
- And then 2 shortcuts and an automation on ios Shortcuts
I also have to mention that the esp32 device that controls the overhead light on my desk already have a parabolic wake up function, so i just need to pass it the same values

### node-RED
These are the two flows
![[Pasted image 20260329144655.png]]
Very easy, i know i could have made them with scripts on Hass but i couldn't be bothered.

### Hass
![[Pasted image 20260329145640.png]]
These are the helpers, again very basic
And then i used [this](https://community.home-assistant.io/t/simple-light-wake-up-alarm-with-parabolic-sunrise-effect/673747) blueprint.

### ios
The ios side took some time to nail down correctly, what i did are two shortcuts one that sends the state of an alarm with a certain tag to the node-RED endpoints:![[Pasted image 20260329150048.png]]
![[Pasted image 20260329150103.png]]
This as to use a return because for some reason the alternative flow did'n trigger the get URL content block so i couldn't actually send the post to the node-RED endpoint.
And then another script to send the time to wake me up at:
![[Pasted image 20260329150220.png]]
This also chains the execution of sending the state at the end because for some reason ios didn't want to execute those 2 scripts separately on the same trigger so it has to be like that... But hey, if it works it's not stupid.
Than i just trigger these scripts whenever i close the clock app, i did this instead of doing it periodically assuming that whenever i open the clock i change the alarm time. Besides this does not cover the possibility that i could change my alarm while not connected to the wifi (either not using it or not in the house) so this is actually quite dangerous, hey at least everything should work perfectly as long as i respect this constraint. I might add also a daily execution at like 1:00 AM to avoid accidentally waking me up.

### results:
Here's the desk light (unfortunatly this is linear)
![[Pasted image 20260329150752.png]] 

