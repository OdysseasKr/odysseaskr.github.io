---
layout: post
title:  "Working with legacy Pinnacle MovieBox USB"
date:   2023-09-29 00:00:00 +0200
author: Odysseas
commentsId: 1
---


I recently got my hands on a Pinnacle MovieBox USB. It's a capture card with Composite and S-Video input from the mid-2000. It looked very sturdy as a device and would have been handy in a few art projects. If I could get it to work that is.

Here are some resources I could find on the internet.

Manual: https://manualmachine.com/pinnacle/movieboxusb/10304172-manual/

A Youtube video that shows it in use in a Windows 10 setup: https://www.youtube.com/watch?v=UGfLlNgKug8

So far I have not been able to get it to work on any of my machines. I am documenting my attempts here with the hope that someone else can do better.


### Windows Drivers

I came across this official Pinnacle page with a bunch of legacy drivers. As far as I can see there are only drivers for 32-bit setups up-until Windows 7.

https://cdn.pinnaclesys.com/SupportFiles/Hardware_Installer/readmeHW10.htm 

I could not get these drivers to work in Windows 10. This [forum post](https://forums.tomshardware.com/threads/pinnacle-moviebox-usb-b-driver-for-windows-10.3681379/) also seems to confirm that they wouldn't work.

My second attempt was to setup a Windows XP machine in virtual box. That didn't seem to detect the MovieBox at all.

Third attempt was to install Windows XP on an old laptop I had lying around. After installing the drivers, my MovieBox actually came to life and the fan starting spinning! Good sign! However, I could not get any input from the device. Most software would just crash or show a black image as input.

### Linux Drivers

Found a Linux driver in [Sourceforge](https://sourceforge.net/projects/pinnaclembusb/). Need to build it yourself though and it seems quite out-of-date.

If you are comfortable with C and willing to fiddle with old Linux kernel versions, this is probably your best bet.

### Accompanying software

Archive.org has a ISO of the "studio" software that you can use to capture and edit: https://archive.org/details/pinnaclestudio8

It requires a 10-digit activation code and I was able to brute-force it in just three tries. Didn't write down the code unfortunately.