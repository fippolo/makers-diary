---
tags:
  - electronics
  - network
  - diary
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
#### private bluetooth
Using that IRK 
