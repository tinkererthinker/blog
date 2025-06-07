---
title: "Install help for Ubuntu 20.04 on a Lenovo Thinkcentre M81"
source: "https://www.reddit.com/r/linux4noobs/comments/hq5bzy/comment/lw2hxst/?context=3"
author:
  - "[[doughboyfreshcak]]"
published: 2020-07-13
created: 2025-06-06
description:
tags:
  - "clippings"
---
So my issue is when I install Ubuntu 20.04, it all goes without a hitch and I restart, take the usb out and it boots up to not finding a bootable device.

I have tried Ubuntu 20.04, 18.04, 12.04, then the latest Mint. They all do the same thing. Edit: I have messed with boot order as well, no luck.

---

Ubuntu 24.04.1

i. No secure boot? M81 Lenovo being a d1ck? After 5,989,321 attempts, here's what worked for me;

1. Set startup to LEGACY in BIOS
2. Hit F12 until it feels weird during post, making computer beep a lot.
3. CHOOSE LEGACY BOOT option in USB. You will install Ubuntu in this mode. Should boot in classic purple ncurses screen with ncurses "Ubuntu 24.04 . . ." text.
4. When prompted, CHOOSE MANUAL INSTALL.
5. REMOVE all hard drive partitions. Create ONE partition. Select "/" as mount point. It will automatically create a 1Mb partition as well. Don't worry about it. I did not create swap, I got 22Gb RAM, up to you.

BE SURE THE DRIVE IS SELECTED FOR GRUB INSTALL. (See bottom of partition page, left).

ii. Install bla bla bla....reboot,

