---
layout: post
title:  "BitMad about.... Commodore 64"
---


Growing up, I had a Commodore 64 (after a Dragon 32 and ZX Spectrum) and to this day it remains my favourite computer. That may be because I never had an Atari ST or Amiga back then so never knew what I was missing out on.
Regardless, I still love the humble C64 and have decided that the 30 years since I last used the machine is quite long enough and I should try to learn all the stuff I wasn't clever enough to understand back then…..not that I’m any more intelligent now mind.

There are so many great tools available these days for writing C64 code that you could be up and running at no cost in around 5-10 mins. IDEs, cross compilers, debuggers, everything you can think of is out there and can be used but for now, I'm going to use the "real" thing.
By that I mean either a real C64 or an emulator, not a PC based development tool.

The reason for this is because I feel that by using the C64 directly, I'll gain a better understanding of the machine. 

I actually started working on this article many weeks ago but kept on changing how I did things and then having to re-write parts. This is probably better for anyone wanting to follow along because at least now I have a fixed set of methods and tools whereas previously I would have been flicking between different applications.

I'll use the term C64 from now on as a blanket term. Obviously there are many ways to facilitate this, from real hardware, emulator, replicas, etc.
I have settled on 3 main methods for now (with a 4th planned) :-

Real Commodore C64c - My own machine, stock firmware, no mods. Custom PSU (DO NOT USE THE ORIGINAL - article coming soon to explain why).
[Kung Fu Flash cartridge](https://github.com/KimJorgensen/KungFuFlash) - Recently purchased. 
[Pi1541](https://cbm-pi1541.firebaseapp.com/) - Bare PCB arrived this morning so will be built by the time this is published.

[MiSTer FPGA](https://github.com/MiSTer-devel/Wiki_MiSTer/wiki) - I've had this for a few years now and absolutely love it. Expect some articles in the near future about it.
The C64 core on the MiSTer is simply amazing. Great accuracy and the framework features add so many quality of life improvements while working with C64 media.

Emulator - I tend to use [Vice](https://vice-emu.sourceforge.io/) or [Denise](https://sourceforge.net/projects/deniseemu/) when using an emulator. Both are great and they're to hand on my laptop when I'm out and about or want to lay on the sofa and code.

The C64 Maxi - I'm thinking of ordering one of these mainly for the keyboard.
When using the MiSTer or an emulator, I use a Corsair K65 and have put stickers on some keycaps to identify special keys. I'd likely use the Maxi most of all because it blends the keyboard with the QOL improvements of emulation.

Ok, on with the show.
If I were writing this back in the 80s or 90s on real hardware, I'd probably have to choose software that most users already had or include a listing for it.
I'm not. It's 2023 and emulators are filled to the brim with all the hardware you could wish for. The internet is awash with any software package you could imagine and you can find pretty much any information you desire either via web search or by downloading old C64 books.
Life is just god damn peachy!

Having owned an Action Replay mk6 cartridge back in the day, this was my first choice of utility cartridge. It was never unplugged from my machine in the 90s and it's always mounted when I run emulation.
This time, it's different. For reasons that I will explain in a different article, I've opted for the Super Snapshot V5 cartridge.

Regarding software, I've played with several different options but ultimately settled on Turbo Macro Pro (TMP).
Initially I was put off by the menu system. From the few YouTube videos that I saw, it looked to me like I'd have to learn complicated shortcuts and command which I didn't fancy.
Then I put my big boy pants on, looked at the docs and got stuck in.

I did spend some time using Mikro Assembler by Supersoft and got on really well with it.
I just found that TMP helped me to keep my code more organised.
I had a quick look at the PAL assembler too but decided against it.

Blank disks. I always keep a blank.d64 file handy and make copies when I need new disks. Some emulators have a feature to create a new blank disk and insert it which is nice. MiSTer doesn’t have this feature hence the files.

Documentation is another thing I've taken into account. I keep copies of these files with me while working with the C64 :-

C64 User Manual
C64 Programmers Reference Manual
Super Snapshot V5 manual
TMP Documentation

This list will no doubt grow over time but it's what I consider the bare minimum for the time being. I did think about providing a zip file with everything included but quite honestly, these things are so easy to find that it's just not worth it. 

Most software / documentation can be found here :-\
[CSDB](https://csdb.dk/)\
[Internet Archive](https://archive.org/)\

Obviously this is just my choice and you are free to substitute any of the above should you choose to follow along.
Many people nowadays use JiffyDOS / DolphinDOS or their own choice of utility cartridge. That is fine as most of what I will be covering will transfer between different methods.

To each their own and may their C64 journey be eventful.

