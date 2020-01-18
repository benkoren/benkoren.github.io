---
title:  "Hopping on the 3d Printer Bandwagon with Prusa and PETG"
date:   2020-01-18 00:00:00
categories: Technology
published: true
tags: [3dprinting]
---
I started playing Minecraft about 4 years after it wasn't new and cool any more, so my timing with the 3d printer seems about right.

At the end of 2019, I purchased a [Prusa i3 MK3s](https://www.prusa3d.com/original-prusa-i3-mk3/) 3D printer. I had previously regarded them as somewhat of a gimmick, at least for the consumer-grade versions, whose primary purpose was to pump out flimsy plastic trickets that would quickly make their way into a landfil. However, I've changed my tune for two reasons: working with electronics is far more fun when we can design the things they mount to, and the strength of the plastics able to be printed is impressive.

3d printing is a great way to satisfy my itch for mechanical engineering, electrical engineering, and general tinkering. Wood and metalworking will always have a place for me, but the speed at which I can fabricate inexpensive yet strong parts on the 3d printer is what sets it apart. The technology is far from turn-key, so hopefully I can shed some light on things that took a good deal of time for me to get right. 

## Why a Prusa?

Prusa printers are relatively expensive for a non-commercial application, but they're of a very high quality for the price. More than that though, the company is one I feel I can get behind: they have very humble beginnings as a passion project for a young Josef Prusa, and from what I can tell they have been building an honest business, creating many jobs for their local citizens. [This video](https://www.youtube.com/watch?v=xX3pDDi9PeU) showcases their history. They also do their fair share of supporting the maker community.

I purchased the kit version of the i3 MK3s and took a half day to assemble it, which I do recommend over purchasing the pre-assembled version; the process got me acquainted with the construction (and maintenance) of the printer. 


## Why PETG?

When it comes time to choose a filament, PETG is objectively the best filament type. 

Alright, not really. But I do love it for engineering prints, which is mainly what I make.

[Here](https://www.prusa3d.com/material-guides/) is a decent article on the high-level difference between filament types. I do highly recommend [PETG](https://www.matterhackers.com/store/c/mh-build-series-petg), which deserves its reputation as being almost as easy to print as PLA and almost as strong as ABS - the best of both worlds.

Regardless of your choice, **pick a filament type & vendor and stick with them**, at least until we're getting good, consistent results across a variety of prints. When I first started printing I was a bit overwhelmed with all the different filament types and ordered up 4 different types. However, this greatly slowed me down because I didn't get the hang of one type before I switched to another. 


## Printer Calibration

After powering on a printer for the first time, it can be tempting to jump right into printing elaborate, eye-pleasing models. However, a lot of time and heartache will be saved by first properly calibrating the printer. There are many variables, but the most important ones are bed adhesion, first layer height, bed temperature, nozzle temperature, ambient temperature, and print speeds. It's also tempting to indefinitely optimize, but based on the diminishing returns invovled in optimization,
we'll aim to strike a happy medium that takes the minimum amount of time to produce prints of acceptable quality.


### Bed Adhesion

The Prusa uses a heated PEI print surface, which plastic loves to stick to, so really all we need to do is keep it clean. There is a lot of information out there about using a glue stick, blue painter's tape, PVA glue, and others, but none of these are necessary with Prusa's print sheets. I've tried the Prusa's [Textured Sheet](https://shop.prusa3d.com/en/mk3mk3s/214-powder-coated-spring-steel-sheet.html), but could not get PETG to adhere well to it. I get much better adhesion on the [Smooth Sheet](https://shop.prusa3d.com/en/mk3mk3s/216-spring-steel-sheet-smooth-pei.html).


### First Layer Height

The first layer of a print is extremely important; if it doesn't go down well, the print should be cancelled and it should be addressed. The goal of the first layer is to _squish_ the extrusion just enough that neighboring lines meld into each other, but not so much that it flakes up from the bed, or gums the sides of the nozzle. The latter is especially an issue with PETG, which is more sticky than other filaments.

However, the first layer calibration built into the Prusa isn't very helpful, as consists primarily of a thin line, which does little to help us gauge how the extrusion is bonding to itself. Use it once as a very rough starting point, but no more. Use an opaque filament for this; a transparent filament is more difficult to see whether the extrusion is properly bonding to the bed and itself.

For fine tuning of the first layer height, take a look at Bob George's page [here](http://projects.ttlexceeded.com/3dprinting_live_z_calibration.html) for an excellent explanation of using the "Life Adjust" method of calibration.


### Temperatures

Temperatures greatly affect how a print will come out. The nozzle and bed temperatures must be precisely configured, but ambient temperature plays a big role as well. If a printer is in a drafty area, or the room temperature is cold (say 60 degrees F, as in my house), then the ambient temperature should be controlled by building an enclosure for the printer. Just be sure not to build it too airtight, because when electronics such as your power supply go above 50 degrees Celsius, permanent
damage may be caused. 

PETG is attracted to very hot surfaces, so under the right conditions we can actually see it curl from the nozzle right back around on itself, causing a buildup on the nozzle. Some folks advise dealing with this by cranking up the nozzle temperature and down the bed temperature for the first layer, but in my experience that caused more problems than it solved.

Every manufacturer's filament is different, so always use the temperature ranges recommended by them as a starting point, and if you find yourself tempted to go outside those ranges to address some issue, there is probably something amiss elsewhere in your configuration.


### Print Speeds

PETG is a hot, sticky mess. If the print speed is set too high, the first layer will curl right up off the bed. So slow the speeds down. Way down. 


## Slicer Profiles

The slicer is the software that takes a model and produces gcodes that define the exact actions the printer needs to take to produce a physical rendition; every little movement, every little tweak. Managing all the settings for printing can be daunting, but making use of slicer profiles eases this drastically. In practice I only use one profile for a given filament and make temporary changes specific to a given print. If the settings changed for that print are something I think would work
well for all prints of that filament type, I'll overwrite the profile and save them; if the print was a failure, I'll simply revert them.


## Modeling Software

There are many options here, but Autodesk Fusion 360 and FreeCAD are the two that stood out to me. 

[Fusion 360](http://autodesk.com/products/fusion-360/overview) is a high-end piece of software with a _ton_ of functionality, used by many professions, and yet it is made freely available for hobbyist and educational use. Gone are the days of needing to fork out thousands of dollars for good, commercial-grade CAD software. I love this model in principle. It gets Autodesk's foot in the door with people that are just starting out and do not want to invest a great deal of funds into their software, if any. It is only once someone starts making
money using the software that they start to charge. This greatly increases the availability of quality tools to everyone, regardless of wealth. It would be all to generous to say that this is do to Autodesk's charity, however. As with many industries, the availability of free alternatives puts a very real pressure on the big companies, which brings me to FreeCAD.

I have not yet used [FreeCAD](https://www.freecadweb.org/), but it's what I'll be learning soon. While I've been very happy with the performance of Fusion 360, I do not like how much of my creations are in the hands of a company; it is a cloud-based product. FreeCAD is an open source parametric modeler.


## Further Reading

I've long maintained that one of the most valuable skills a person can have is that of how to learn. Get used to using a search engine to diagnose issues that will inevitably arise with 3d printing; we are almost never the first to encounter any given problem.

To help accelerate this process, here are some resources that greatly helped me along the way:
* [Bob George (Muppet Labs)](http://projects.ttlexceeded.com/3d_printing.html)
* [Maker's Muse](https://www.youtube.com/user/TheMakersMuse)
* [PrusaPrinters.org Forum](https://forum.prusaprinters.org/)

