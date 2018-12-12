---
title:  "Setting up the Raspberry Pi Zero W"
date:   2018-12-11 15:04:23
categories: [raspberrypi]
published: false
tags: [raspberrypi]
---
I recently picked up a Raspberry Pi Zero W, which is an inexpensive and lightweight version of the Raspberry Pi (yet it still has
built-in Wifi). I've long-considered buying one of these for general tinkering, but had a hard time settling on which version and
set of peripherals to get. So I decided to just pick a project - any project, really - just to have an excuse to get started: a
programmable camera for our chicken coop. Or for our driveway. Or for a robot. Or a motion-tracking human-sensing auto-aiming
nerf gun. Hey look, a butterfly!

All I really know is that I bought a Pi and I've started playing with it, but I am somewhat concerned that one of my kids (or more
realistically, me) will drop it in the dog's water dish and my progress will be wiped away, so I figure this post is as good of a 
place as any to chronicle the efforts as a backup.

## Parts Manifest

TODO


## Preparing the Storage and Operating System

First, we need to install NOOBS, the de facto Raspberry Pi OS installer, onto the SD card. This is pretty straightforward:
 # Download the latest NOOBS [here](https://www.raspberrypi.org/downloads/noobs/)
 # Use OS X's Disk Utility to reformat the card as FAT32
 # Copy the contents of the NOOBS archive into the freshly-formated disk volume

Plug that sucker in the Pi and power it on. Follow the steps to install Raspbian; this is very straightforward.


## Fixing Vim

The default key bindings in vim on the Pi are wonky. Apparently they use a lightweight version of Vim that's optimized to ensure
I can't modify the simplest of config files without wanting to pull out the little remaining hair I have. Let's fix that by
installing full-on vim: `sudo apt-get install vim`


## Opening up Shell Access

The Pi should be accessible from anywhere on the network without having to plug it into a monitor, so the next course of action
is to get SSH up and running (even through restarts):
```
sudo service ssh start
sudo update-rc.d ssh enable
```


