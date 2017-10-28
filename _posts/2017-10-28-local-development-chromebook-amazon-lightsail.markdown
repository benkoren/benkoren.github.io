---
title:  "Rails and PHP Development on a Chromebook"
date:   2017-10-28 04:00:00
categories: Engineering
published: false
tags: Rails, PHP
---
Today we'll explore how I use a [$170 Chromebook][chromebook], [vim][vim], tmux and [Amazon Lightsail][lightsail] to do PHP and Ruby on Rails development.


## Background

I purchased a Chromebook about a year ago for our family's casual computing needs such as web browsing and Google Docs from the comfort of our couch _without_ the sweaty lap that comes from the use of a traditional laptop (or the pricetag!), while still having a standard-sized keyboard. Most importantly, it required absolutely minimal technical effort on my part, even if one of our kids tosses it into the bathtub; we could simply have another unit shipped for a reasonable price, log in, and pick up right where we had left off (after dealing with the bathtub incident, of course). 

Then I decided I'd like this same level of convenience for my work life as a software engineer: I wanted to web development from my Chromebook, but with the following requirements:

1. *Language-agnostic*: I need a reasonable setup for developing PHP and Ruby on Rails in the immediate term. The solution cannot be language-specific, though I have no immediate interest in the Microsoft languages.
2. *Bathtub Test*: if the device is destroyed, I need to be able to pick up where I had left off with minimal effort.
3. *Debugging*: I need to be able to debug code, and none of this `var_dump()` nonsense. We're professionals, not savages.
4. *Pricetag*: The solution needs to be reasonably priced, if not free. I'd prefer to spend some time upfront tinkering and working out a clever setup than to shell out money for a sub-optimal pre-packaged setup, but I need to spend a little cash then so be it.
5. *Comfy Factor*: No list of requirements is complete without a subjective, immeasurable requirement: this needs to _feel_ like a comfy development environment. Yes, I'll only have a single screen that has comparatively low resolution to my dedicated office complete with a mouse, external monitors, and a sound system.
6. *Chair Hopping*: This is a soft requirement, but I'd like to be able to shift between my work machine in the office and the Chromebook, picking up right where I had left off - even in the middle of an active debugging session.

Our final solution meets all of these requirements.


## The Solution

My immediate inclination was to use a Cloud-based IDE, such as CodeEnvy or Cloud9, but after trying each for a week or so they failed my _Comfy Factor_ and _Debugging_ requirements. Another option I explored was local development, but this failed _Bathtub Test_, _Comfy Factor_, and _Chair Hopping_.

Finally though, I've landed on a combination that meets all of my requirements, using Amazon Lightsail, Vim, and Tmux. I know what you're thinking: "_Vim?  VIM?!?  Do you live under a rock? The mouse was invented decades ago! Next thing I know you'll be telling me to use the [Dvorak][dvorak] keyboard layout because QWERTY was specifically designed to be anti-ergonomic._" And to that I say: don't be silly. If you switch to Dvorak then you'll have a hard time helping your Grandma remove malware from her decade-old PC because it uses the same keyboard layout as everyone else.

Now, as for that Vim thing, it actually makes a lot of sense on paper: it's language-agnostic, highly-customizable, and significantly more comfy on a Chromebook than a mouse-oriented GUI because you won't be using the trackpad. Furthermore, it supports all of the features I expect from a modern IDE, such as auto-completion, auto-indentation, fuzzy file search, fuzzy text search, git integration, code linting, spell-checking, syntax highlighting, copy/paste, code-completion, code snippets, and all of the language-specific integrations you'd expect.

(TODO: INSERT ANIMATED GIF OR ASCIINEMA SHOWING OFF VIM)

Plus, vim is everywhere. I can't tell you how many times I've watched a developer SSH into a client's web server and struggle with even the lightests of tasks because they can't cope without their shiny GUIs. Don't get me wrong: there is a moderate learning curve and Vim pretty much _requires_ that you have a deep appreciation for minimalism. The most difficult part of this whole solution is learning Vim, but it's worth the investment.

I've already gotten too far into the weeds; let's pull back out and get into setting up this beast.


### Setting up Lightsail

[Amazon Lightsail][lightsail] is essentially Amazon's answer to DigitalOcean: they provide a virtual private server (VPS) that's very affordable (starts at $5/mo) and sports an easy-to-use interface. Despite being very familiar with many of Amazon AWS offerings and being no stranger to bare-bones systems administration, sometimes it's nice to just click a button and have an environment.

Lightsail provides a number of "blueprints" (preconfigured server images for specific use cases) for common software stacks such as LAMP and MEAN, application platforms such as Drupal and Magento, and barebone OSs such as Debian and Amazon Linux. Since this instance will serve as a general PHP and Rails development environment we'll go with a barebones Ubuntu blueprint.

(TODO: INSERT SCREENSHOT)

Once you've set up your server, download the corresponding SSH Keypair from the [account page][lightsail-account]. It'll be named something like `LightsailDefaultPrivateKey-us-east-2.pem`. Also, find the IP address of your Lightsail instance and make note of it. You'll need these soon.


### Setting up the Chromebook

On your Chromebook, install the [Secure Shell][secureshell] extension. This is highly-preferred over the built-in SSH client in Chrome because of the _Comfy Factor_ requirement.

Speaking of comfy, let's configure Secure Shell by clicking on the Options button and updating a few things:
* Set `font-size` to `15`.
* Select `copy-on-select`.
* Select `mouse-right-click-paste`
* Select `ctrl-c-copy`
* Select `ctrl-v-paste`

Before we can use Secure Shell to connect to our Lightsail instance, we need turn our `.pem` file into something more digestible. To do this, press `Ctrl-Alt-T` to open up a terminal tab


### Getting cozy with Vim

tutorial

key bindings

color scheme

### Tmux: 





## 





## Downsides

Bonus points go to a solution that works offline and that does not degrade as network latency increases. 

Debugging

Trackpad

Sound.

Ergonomics of key bindings.


## Further Reading

https://vimawesome.com/

https://asciinema.org/

Spacemacs




[chromebook]: http://a.co/8zhnwZW
[vim]: https://github.com/vim/vim
[lightsail]: https://amazonlightsail.com/
[lightsail-account]: https://lightsail.aws.amazon.com/ls/webapp/account/keys
[dvorak]: https://en.wikipedia.org/wiki/Dvorak_Simplified_Keyboard
[tmux]: https://github.com/tmux/tmux
[secureshell]: https://chrome.google.com/webstore/detail/secure-shell/pnhechapfaindjhompbnflcldabbghjo?hl=en
