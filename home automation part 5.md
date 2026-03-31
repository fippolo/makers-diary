---
created: 2026-03-31
tags:
  - diary
  - electronics
  - network
---
## 11:11
Today i was looking at my workbench light. I like this light a lot, its nicely diffused, i can move it around however i want, and it is a nice color and bright:

![[Pasted image 20260331111355.png]]

It is a usb light and it is controlled by a very "un-complex" controller inline with the usb cable![[Pasted image 20260331111531.png]]
And so i begin to wonder, how hard could it be to hook the button and have a microcontroller interact with the pcb board.
So i opened up the pcb and took a look at it ![[Pasted image 20260331112151.png]]
(did not take a foto of the other side) Unfortunately the controller inside is not labeled so i got to probing, it looks like the button shorts a pin of the controller to ground so it must be using a pull-up resistor to read the button state, and the voltage across the button terminals when idling is oddly enough 2.5 V, being USB 5 V i suspect there is some in series shenanigans going on here, but that does not matter to me, all i need to know is that the voltage 