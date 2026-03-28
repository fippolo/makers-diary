---
created: 2026-03-28
tags:
  - electronics
  - network
---
## 11:03
Ok so today i have some stuff to take care of, firstly i need to invert the logic of the mqtt relays so that they actually match the real behavior of the actual devices, luckily i predicted this and actually statically defined the on and off values of relays at the top of the code for the firmware so its just a matter of flipping this:
![[Pasted image 20260328110922.png]]
## 11:48 