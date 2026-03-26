---
created: 2026-03-21
tags:
  - 3d
  - diary
  - electronics
  - keyboard
---
##  11:14
Today i will be working on a esp32-c3 powered keypad since my aliexpress package has arrived with 5 of them, the design is pretty basic with just 9 switches, the controller, a 1 cell bms to handle a 18650, using the battery itself to angle itself.
![[Pasted image 20260321111618.png]]

## 15:03
I finalised the design adding some mounting point for the eventual back cover and soldered the whole system i powered it up and there looks to be no shorts
Let's quickly go over how it works:
The switches are not connected each to a gpio but they are arranged into a matrix where each column and each row are connected together like this
![[Pasted image 20260321150549.png]]
The problem with this is that if you press both (r1,c1) and (r2,c2) both (r1,c2) and (r2,c1) will result as pressed, this is called ghosting, we can avoid this behavior by making the grid "one way" by adding diodes on the rowes like this:![[Pasted image 20260321150920.png]]
Then i can connect every raw and column to the micro controller like this
![[Pasted image 20260321151009.png]]![[Pasted image 20260321151017.png]]
The power side is wired like this ![[Pasted image 20260321151054.png]]
I suggest to check out [golem](https://golem.hu/guide/keyboard-matrix/) for further reading

So now i can start to think about the firmware, i would like to run [KMK firmware](https://github.com/KMKfw/kmk_firmware) since i have it on my main keyboard and i am very pleased with it.

I was able to load circuit python through [this guide](https://learn.adafruit.com/circuitpython-with-esp32-quick-start/overview) 

## 17:00
With the heavy use of codex i was able to adapt an implementation of kmk firmware to work with the limited memory this micro controller has available the full firmware is available at this [github repository](https://github.com/fippolo/kmk-esp)  and now everything works and i should be able to start making macros as i see fit

:warning: the firmware fork was unstable so i took it down for now, I will write a custom firmware once i get the time to go around it