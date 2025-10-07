---
layout: post
title:  "Working with legacy Pinnacle MovieBox USB"
date:   2023-09-29 00:00:00 +0200
author: Odysseas
commentsId: 2
---


I recently got my hands on a Pinnacle MovieBox USB. It's a capture card with Composite and S-Video input from the mid-2000. It looked very sturdy as a device and would have been handy in a few art projects. If I could get it to work that is.

![picture of moviebox](https://external-content.duckduckgo.com/iu/?u=http%3A%2F%2Fwww.hwp.ru%2FMultimedia%2FPinnaclemoviebox.usb%2FPinnaclemoviebox5.jpg&f=1&nofb=1&ipt=a48a898b6d77e21ff0b1bec896dae32a10dde35d1709693f2db5dd8459c14c5e&ipo=images)

Here are some resources I could find on the internet.

Manual: [https://manualmachine.com/pinnacle/movieboxusb/10304172-manual/](https://manualmachine.com/pinnacle/movieboxusb/10304172-manual/)

There is a [Youtube video](https://www.youtube.com/watch?v=UGfLlNgKug8) that shows it in use in a Windows 10 machine.

So far I have not been able to get it to work on any of my machines. I am documenting my attempts here with the hope that someone else can do better.


### Windows Drivers

I came across this official Pinnacle page with a bunch of legacy drivers. As far as I can see there are only drivers for 32-bit setups, up until Windows 7.

[https://cdn.pinnaclesys.com/SupportFiles/Hardware_Installer/readmeHW10.htm ](https://cdn.pinnaclesys.com/SupportFiles/Hardware_Installer/readmeHW10.htm)

I could not get these drivers to work in Windows 10. This [forum post](https://forums.tomshardware.com/threads/pinnacle-moviebox-usb-b-driver-for-windows-10.3681379/) seems to confirm that they would not work.

My second attempt was to setup a Windows XP machine in virtual box. That didn't seem to detect the MovieBox at all.

Third attempt was to install Windows XP on an old laptop I had lying around. After installing the drivers, my MovieBox actually came to life and the fan starting spinning! Good sign! However, I could not get any input from the device. Most software would just crash or show a black image as input.

### Linux Drivers

Found a Linux driver in [Sourceforge](https://sourceforge.net/projects/pinnaclembusb/). Need to build it yourself though and it seems quite out-of-date. If you are comfortable with C and willing to fiddle with old Linux kernel versions, this is probably your best bet.

### Accompanying software

Archive.org has a ISO of the "studio" software that you can use to capture and edit: [https://archive.org/details/pinnaclestudio8](https://archive.org/details/pinnaclestudio8). It requires a 10-digit activation code. I typed three random codes and one of them was accepted. I didn't write down the code unfortunately.
