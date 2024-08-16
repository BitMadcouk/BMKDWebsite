# The Greaseweazle

## Intro

I've always liked the idea of the [Greaseweazle](https://github.com/keirf/greaseweazle). I tried to build one some time ago with a spare [Blue Pill](https://www.electronicshub.org/getting-started-with-stm32f103c8t6-blue-pill/) board I had. Suffice to say, I never got it working for one reason or another and soon lost interest.

I know there was some specific reason for wanting one at the time but can't remember what.
One idea I had at the time was to write copy protected Atari ST and Amiga disks to real floppy disks and attempt to learn some cracking. I also thought it'd be nice to have around in the event that I need to write a floppy disk that can't be done with a regular drive / OS. Also, let's be honest, for a nerd like me, it's another tool to have around for those "just in case" situations. I don't have a specific use in mind right now but I saw one online the other day for a reasonable price and decided to snap it up. It has just arrived so I thought I'd document the learning process now so that when I need to use it, I can just refer back to these notes instead of having to try and piece it together. For all I know, it might be simple enough to not need these notes.... we shall find out.

## What is it?

Taken from the [Greaseweazle Wiki](https://github.com/keirf/greaseweazle/wiki)
> Greaseweazle is a USB device and host tools allowing versatile floppy drive control. By extracting the raw flux transitions from a drive, any disk format can be captured and analysed: PC, Amiga, Amstrad, PDP-11, musical instruments, industrial equipment, and more. Greaseweazle also supports writing to floppy disks, from a range of image file formats including those commonly used for online preservation (ADF, IPF, DSK, IMG, HFE, ...).

I'll translate that to BitMad language...
Greaseweazle allows you to connect any type of floppy drive to a modern PC via USB. Not only that but it then allows the modern PC to read or write disks with perfect accuracy regardless of disk format / bad sectors etc. It achieves this by performing some sort of magic with the magnetic flux on (around?) the disk. I won't pretend to understand it, I just appreciate that someone else does and released this amazing tool.

There are two parts to the project, the hardware interface and the software stack. I'll cover both here.

## Hardware

The hardware element of the Greaseweazle provides a physical connection between the PC and floppy drive. There are several models available, all of which can be viewed on [Greaseweazel Models](https://github.com/keirf/greaseweazle/wiki/Greaseweazle-Models) however at the time of writing, the V4 seems to be the most popular for sale currently and the version I have.

Mine arrived in a case with all the cables required to connect one drive. The greaseweazle does support multiple drives but I only intend to use one. With a drive dug out of the collection, the power and data cables were connected up. I left the USB to PC connection disconnected for the time being while I checked the documentation and looked into the software side of things. I'm also powering the drive directly from the Greaseweazle as I'm using a 3.5" drive. If I were using a 3" or 5.25." drive I would need to power them externally. This is all explained well in the [V4 setup doc](https://github.com/keirf/greaseweazle/wiki/V4-Setup).

## Software

As per the rest of this project, the [Software Installation](https://github.com/keirf/greaseweazle/wiki/Software-Installation) documentation is well written and detailed enough to get you up and running quickly. I'll use my Windows 10 machine to try it out for now and will give it a go on linux another day (not that I expect it to be drastically different). For Windows it's a case of downloading the software zip file and extracting it. That's it, connect the GW to your machine and you're done.

You can check this by opening up command prompt and changing into the directory you extracted the zip file to then run

    gw info

In the image below, you can see the message you see if the device isn't connected, followed by the expected output.

![cmd output](cmdoutput.png)

I ran the " gw update" command which informed me that I am running the latest firmware version which is nice.

That's it, we're up and running. Now let's use the thing!

## Reading a Disk

At this point I went away to read the [Yann Serra Tutorial](https://github.com/keirf/greaseweazle/wiki/Yann-Serra-Tutorial)

Before I went nuts inserting my old original floppy disks into the drive, I threw an old HP driver disk or something similar that I wouldn't mind losing if the drive ate it.

I ran a command prompt and changed into the Greaseweazle directory then ran the following command :-

    gw read --format=ibm.1440 --drive=b test.img

I'm lying. I didn't run that command straight away. I got lots of things wrong several times and didn't get it to work. I went away for a few hours and did something else. When I came back with a fresh head and *actually* read the links I've been pasting throughout this article, I finally saw the error of my ways and adjusted accordingly.

This is where I found out the importance of the two options I specified. You have to tell it the type of disk format that it's reading. I got this wrong initially and saw errors scrolling up the screen. the other issue was because I'd left of the --drive option but because I'm using a cable with no twist, I have to tell the Greaseweazle that I'm using device B.

Anyway, once the process was complete, I was left with this screen :-

![Greasewazle read complete](readcomplete.png)

I quickly extracted the .img file and checked the contents. It worked perfectly. I ought to note here that this is the "simple" method of data reading. There are more advanced methods to read disks but I'll let you read all about that in some of the provided links.

## Writing a Disk

For this test I'm going to try what I wrote at the beginning of the article and see if I can write an original Amiga game to disk, protection included. As before, I referred to the [Yann Serra Tutorial](https://github.com/keirf/greaseweazle/wiki/Yann-Serra-Tutorial) to get started. The first thing I needed to do was obtain a .ipf file. I opted to use an [image](robocop) of RoboCop because well, why not.

I placed the file into my Greaseweasle folder and inserted a new looking 720K disk then ran this command :-

    gw write --format=amiga.amigados --drive=b RoboCop.ipf
    
It failed. Several times. I tried a different game image and got the same errors. That "new looking" floppy disk might not be so new after all. I didn't have any more 720K disks to hand and couldn't be bothered to go back into the loft (after several trips looking for floppy drives and disks) so I went the OG route and stuff some toilet paper into the bottom right hand corner and tried again.

![modded disk](moddedfloppy.png)

This time I also removed the --format option and went with the following command :-

    gw write --drive=b MidnightResistance.ipf

That worked perfectly so I then ran it again with a fresh disk and the original RoboCop image I tried. Success again.

This is where I realised that I hadn't tried the 720K disk without the --format option so gave it another bash. Failed again. This at least confirmed that the disk was some of the blame so I'm ok with that.

Time to test the disks....

A resounding success! Both disks booted however the Midnight Resistance disk needed two attempts to load as the first one failed. The Amiga drive is old and in need of a service so I attributed it to that.

![RoboCop Loaded](robocoploaded.png)
![Midnight Resistance Loaded](mrloaded.png)
Ignore the state of my poor old Amiga. it's filthy and needs a good refurb but that will happen at a later date. Ahe works and that's the main thing.

## Conclusion

I'm in love with this thing! Being able to write obscure images onto disk is a lovely thing. I'm sure software archivists also love this kit because of the level it can read disks at. This device won't be for everyone but for those it is aimed at, I imagine will be invaluable. For those of you wondering why you might want this over something like a Gotek drive, you wouldn't. While both being floppy related projects, they're completely different beasts designed to do different thing. I'm glad I have one in my toolkit and can highly recommend it to anyone who may have been interested but maybe not fully decided. I don't have anything planned immediately that requires the Greaseweazle but as soon as I use it for anything interesting, I'll update this article accordingly.
