---
title:  "Mounting a Synology NAS on Ununtu Linux via SMB"
date:   2020-01-15 00:00:00
categories: Technology
published: true
tags: [linux, synology]
---
A year or so ago I picked up a [Synology DS918+][ds918] and a couple [WD Reds][wdred] and could not be more happy with the purchase. Despite being experiencienced with Linux server administration, meaning that putting together a FreeNAS box or the like is well within my grasp, my time is precious and this purchase has saved me a *ton* of time. 

Just yesterday my shiny new [System76 Galago Pro 4][galp4] arrived, which runs Pop!_OS, a derivative of Ubuntu, so naturally I needed to mount up my Synology Drive folder so that I could access my personal files. However, most of the guides out there did not meet my requirements. More specifically, I wanted to:
* Mount the drive via a command in the shell, not a GUI.
* Use a method that requires authentication, so that I'm not opening up access to my entire NAS for anyone on my network. For example, a NFS share that does not use Kerberos or similar for authentication is not secure.
* My password must not be stored in plaintext on my client/laptop. For example, auto-mounting a fileshare by putting a plaintext password in `/etc/fstab` is not secure.
* Minimize the change to the Synology server. Going back to the preciousness of my time, I'm looking for the path of least resistance (that still meets my requirements). SSH'ing into the server and installing obscure packages that need to be onerously maintained is to be avoided.

What I landed on ended up being pretty simple:
```bash
sudo apt install cifs-utils
sudo mount -t cifs -o username=SYNOLOGY_USER_NAME,uid=SYNOLOGY_USER_NAME,gid=SYNOLOGY_USER_NAME //SYNOLOGY_SERVER_ADDRESS/homes/SYNOLOGY_USER_NAME/Drive ~/synology/
```

If the mount fails and `dmesg` revealse an error regarding the dialect/version of the server not being supported, try hopping onto your Synology server and going to **File Services -> SMB/AFP/NFS -> SMB -> Advanced Settings** and setting the **Maximum SMB protocol** to **SMB3**.


[ds918]:        https://www.amazon.com/gp/product/B075N1Z9LT/ref=ppx_yo_dt_b_search_asin_title?ie=UTF8&psc=1
[wdred]:        https://www.amazon.com/gp/product/B00EHBERSE/ref=ppx_yo_dt_b_asin_title_o00_s03?ie=UTF8&psc=1
[galp4]:        https://system76.com/laptops/galago

