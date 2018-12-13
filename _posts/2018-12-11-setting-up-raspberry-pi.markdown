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

All I really know is that I bought a Pi and I've started playing with it, but I am somewhat concerned that one of my kids (or more realistically, me) will drop it in the dog's water dish and my progress will be wiped away, so I figure this post is as good of a 
place as any to chronicle the efforts as a backup.

## Parts Manifest

TODO


## Preparing the Hardware

This mostly consists plugging the male parts into matching female parts. Since I opted for a Pi Zero W though, this did make for
some soldering of the header pins to the main PCB: TODO_INSERT_PHOTO


## Preparing the Storage and Operating System

First, we need to install NOOBS, the de facto Raspberry Pi OS installer, onto the SD card. This is pretty straightforward:
1. Download the latest NOOBS [here](https://www.raspberrypi.org/downloads/noobs/)
2. Use OS X's Disk Utility to reformat the card as FAT32
3. Copy the contents of the NOOBS archive into the freshly-formated disk volume

Plug that sucker in the Pi and power it on. Follow the wizards to install and configure Raspbian; this is all very
straightforward.


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


## Configuring Wifi

As a part of the Raspbian setup wizard, the wifi should already be configured. However, we'll be running the Pi in runlevel 3,
which means that the window system will not fire up, which means we'll need to do some more fiddling to get the wifi to
automatically connect. Modify `/etc/wpa_supplicant/wpa_supplicant.conf` to consist of the following:
```
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1
country=US

network={
        ssid="YOUR_SSID"
        psk="YOUR_PLAINTEXT_WIFI_PASSWORD"
        scan_ssid=1
        proto=WPA RSN
        key_mgmt=WPA-PSK
        pairwise=CCMP TKIP
        group=CCMP TKIP
}
```

Why, you might ask? The Internet told me to do this and it worked.


## Change the default runlevel

We won't be using the GUI on the Pi, and it eats up resources so we may as well disable it: `sudo systemctl set-default multi-user.target`. This is also a good time to `sudo reboot` to make sure we didn't screw up anything too badly.


## Firewall

I don't know what services this thing is running, nor what it'll be running by the time I'm done cobbling together some
monstrosity, but now's the time to get a whitelist-based firewall configuration rolling:

```
sudo apt-get install iptables-persistent

sudo iptables -A INPUT -i lo -j ACCEPT
sudo iptables -A INPUT -p tcp -m tcp --dport 22 -j ACCEPT
sudo iptables -A OUTPUT -o lo -j ACCEPT
sudo iptables -A OUTPUT -p tcp --sport 22 -m state --state ESTABLISHED -j ACCEPT
sudo iptables -P INPUT DROP
sudo iptables -P OUTPUT DROP
sudo iptables -P FORWARD DROP

sudo netfilter-persistent save
```







