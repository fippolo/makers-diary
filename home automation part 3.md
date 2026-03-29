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
