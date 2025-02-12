---
title: "I have a few qualms with this app: 1. For a Linux user, you can already build su... | Hacker News"
source: "https://news.ycombinator.com/item?id=9224"
author:
published:
created: 2025-02-10
description:
tags:
  - "clippings"
---
I have a few qualms with this app:

1. For a Linux user, you can already build such a system yourself quite trivially by getting an FTP account, mounting it locally with curlftpfs, and then using SVN or CVS on the mounted filesystem. From Windows or Mac, this FTP account could be accessed through built-in software.

2. It doesn't actually replace a USB drive. Most people I know e-mail files to themselves or host them somewhere online to be able to perform presentations, but they still carry a USB drive in case there are connectivity problems. This does not solve the connectivity issue.

3. It does not seem very "viral" or income-generating. I know this is premature at this point, but without charging users for the service, is it reasonable to expect to make money off of this?

1\. re: the first part, many people want something plug and play. and even if they were plug and play, the problem is that the user experience (on windows at least) with online drives generally sucks, and you don't have disconnected access.

windows for sure doesn't hide latency well (CIFS is bad, webdav etc. are worse), and most apps are written as if the disk was local, and assume, for example, accessing a file only takes a few ms. if the server is 80ms away, and you do 100 accesses (e.g. the open file common dialog listing a directory and poking files for various attributes or icons) serially, suddenly your UI locks up for \_seconds\_ (joel spolsky summarizes this well in his article on leaky abstractions.) ditto saving any file; you change one character in your 20mb word file and hit save, and your upstream-capped 40k/sec comcast connection is hosed for 8 minutes. sure for docs of a few hundred k it's fine, but doing work on large docs on an online drive feels like walking around with cinder blocks tied to your feet. anyway, the point of that rant was that dropbox uses a \_local\_ folder with efficient sync in the background, which is an important difference :)

2\. true, if you're both not at your computer and on another computer without net access, this won't replace a usb drive :) but the case i'm worried about is being, for example, on a plane, and dropbox will let you get to the most recent version of your docs at the time you were last connected, and will sync everything up when you get back online (without you having to copy anything or really do anything.)

3\. there are some unannounced viral parts i didn't get to show in there :) it'll be a freemium model. up to x gb free, tiered plans above that.