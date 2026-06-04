---
created: 2026-06-04
tags:
  - diary
  - programming
---
## a quick rambling
So this is my setup:![[Pasted image 20260604084645.png]]
(Yes i space larp)
As you can see here, i have some a5 sheets between me and the keyboard, which i very much love, just to scribe, land my ideas instead of just making them float in my head. This is getting out of hand, i'm wasting so much paper while the graphic tablet is right there gathering dust. I might also add that the bottom screen does not get much use, i keep mainly just coms there and other stuff i don't need to look at very often, not even music gets there, and so i thought a fix for my paper problem is just staring at me (or better i have been staring at it). So i started to look up some sort of uncomplicated drawing app that made me able of just throw down some notes, without borders, without a complicated interface, not closed source, without a fucking subscription model (looking at you notion), without all of that bullshit.
Of course, as luck would have it, nothing that fit those criteria exists and so i took it as a challenge for myself

## What i did
What i decided to do was to challenge myself, lately i understood that my usage of llms made me dependent on that tool so what i set out to do was to make this project without generating any code (use is still allowed, YOU CAN'T MAKE ME READ DOCS).
I set myself some requirements:
- App should not have ANY ui elements besides the drawing surface
- Written in C++
- Works for my os
- Should have at least undo functionality
- Smooth experience, ease of use
Those are very reachable and not too crazy.
So i started looking at libraries and of course Gtk came up so i went with it (Gtkmm). I have to say, windows is not the best os to be doing this in. 
To be honest development went pretty decently, i'm pleasantly surprised i still got it, even though i got claude to help i treated it like a senior developer, asking implementation details, methods signature etc... Still feel like i've lost a lot of, let's call it, awareness, while writing code, especially when it comes to using libraries, i would like to blame IDEs, i would like to say that c++ is not my goto usually etc... Etc.. But i really feel like the immediacy of learning a framework has eroded away in this ai powered age, and also didn't, using a tool like claude or chatgpt to learn a library or framework can really make understanig it wayy easier to what it used to take, but then i also don't want to loose my ability to learn the same way i lost my affinity with coding. Also no damage is permanent, and i still think that using llms is a great way too bootstrap learning, and it makes it easier to get over the learning curves of anything STEM related.
Lastly
When it comes to teaching, especially programming, there's a specific threshold amount of code written by the teacher where teaching becomes babysitting, I personally think that llm usage should be treated the same way, you shouldn't demonize that tool the same way you shouldn't demonize a teacher lmao, it is just up to us to use it correctly.
And also generating staright code out of your arse in some situations is very understandable and even commendable, just don't get drunk with power

## github link
Https://github.com/fippolo/DesktopIt

## PS
That was quite the rambling i embarked on there, and you read through all that? Thank you for your time i guess. I'm very open to talk about this with anyone, you can find my e-mail at the top, any insight, criticism, opinions about llm usage will help us all get a clear picture on how we should use this new tool.