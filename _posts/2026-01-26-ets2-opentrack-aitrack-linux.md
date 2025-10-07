---
layout: post
title:  "Head tracking for ETS2 on Linux using Opentrack and AITrack"
date:   2026-01-26 00:00:00 +0200
author: Odysseas
commentsId: 4
---


With the end of support for Windows 10, I had to move all my games to an Ubuntu setup. Running ETS2 using Steam and Proton is very straightforward. However, I wanted to keep the head tracking system I was using on Windows. By running AITrack in the same proton prefix as ETS2 and opentrack, we allow the three programs to communicate with each other.

## 1. Setting up Opentrack
While there seems to be a way to [build opentrack for Linux](https://github.com/opentrack/opentrack/wiki/Building-on-Linux), I prefer to stick to the Windows version through Proton. This was very easy to do using [opentrack-launcher](https://github.com/markx86/opentrack-launcher) which worked out-of-the-box. All it does is start opentrack before launching the actual game.

## 2. Setting up AITrack
Using [protontricks](https://flathub.org/en/apps/com.github.Matoking.protontricks), it is possible to install AITrack to a Proton prefix and run it as a Windows application. The steps I followed were:

1. Download AITrack from the [official repository](https://github.com/AIRLegend/aitrack/tags). Version v0.7.1-alpha worked great for me.
2. Copy the `aitrack` folder into the `C:\` folder of the ETS2 prefix. Note that 227300 is the SteamID of ETS2 and thus the ID of the Proton prefix.
```bash
cp -r $HOME/Downloads/aitrack $HOME/.steam/steam/steamapps/compatdata/227300/pfx/drive_c/
```
3. Open a Windows explorer into the ETS2 prefix.
```bash
protontricks-launch --appid 227300 $HOME/.steam/steam/steamapps/compatdata/227300/pfx/drive_c/
```
4. Navigate to the `aitrack` folder and run `AITrack.exe`

The AITrack window should pop-up. After AITrack has started, you can start ETS2 using the opentrack-launcher through Steam.


