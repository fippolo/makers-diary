---
created: 2026-03-27
tags:
  - diary
  - electronics
---
Today i wanted to talk about how i recently got into automation. I have a "server", which is just a laptop without a screen, glued on the underside of my desk (i know, i know), linked to my network using a 10/100 24 port switch that a friend of mine generously gave to me (also glued to my desk).
![[Pasted image 20260327092150.png]]i had quite some time to think about what to host in this server, and i came up with the idea to host a homeassistnat instance using docker and not the official image, and so i did. I later integrate the very few smart devices i have in my home (2 smart lights and a smart socket). But that wasn't enough for me since i wanted to control more stuff, mainly powering my desk setup and my workbench, since when i go to sleep i have to power off a lot of devices that light pollute my room in order to actually sleep. And so i made this:
![[Pasted image 20260327094045.png]]
That is just an electrical box with a [3 relay module](https://it.aliexpress.com/item/1005005721397678.html?spm=a2g0o.order_list.order_list_main.152.19e11802UOo3go&gatewayAdapt=glo2ita) and a [esp32-c3](https://it.aliexpress.com/item/1005007663345442.html?spm=a2g0o.order_list.order_list_main.29.19e11802UOo3go&gatewayAdapt=glo2ita) from aliexpress.
It has 4 cables coming out of it, one has a male electrical socket at the end, to take power in and the other 3 have some female electrical sockets to give power out. The schematic is as follow![[Pasted image 20260327095728.png]]
And of cource the relays 