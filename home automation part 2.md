---
created: 2026-03-28
tags:
  - electronics
  - network
  - diary
---
## 11:03
Ok so today i have some stuff to take care of, firstly i need to invert the logic of the mqtt relays so that they actually match the real behavior of the actual devices, luckily i predicted this and actually statically defined the on and off values of relays at the top of the code for the firmware so its just a matter of flipping this:
![[Pasted image 20260328110922.png]]
## 11:48 
It turns out it was a bit more difficult than that since i had to actually refer to this values in the startup logic since for some reason i didn't do that before, so now it is actually flipped, it defaults to not energizing the coils, and it posts the correct state to mqtt. That was harder than i thought, how did i let this little thing firmware get 340 lines long? I should limit my LLM usage, they tend to turn even the simplest projects into a architectural nightmare lmao.  
## 12:18
So now it's time for the screen and light to get mqtt'd
This one i actually need to plug a usbc into since no fancy circuitpython. This one actually scares me a little, i better set up version control before touching it.
## 12:34
Wow that was unexpected, the codex code worked!! First try!!
Man these agents some time are so unpredictable, like it struggled with inverted logic in PYTHON of all thing, but then when asked to translate a whole ass 700 line project that used a web interface to a mqtt in the arduinoFramework for an esp32, it's done it first try, this is incredibly unexpected.
So here it is![[Pasted image 20260328123711.png]]
I wonder if i can actually make it sync with my phone alarm
