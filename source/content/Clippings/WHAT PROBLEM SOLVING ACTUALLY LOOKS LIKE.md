---
title: "WHAT PROBLEM SOLVING ACTUALLY LOOKS LIKE"
source: "https://infosecwriteups.com/my-personal-ctf-challenge-4016e9c176b3"
author:
  - "[[Nilesh Kumar]]"
published: 2020-08-22
created: 2025-02-14
description: "posted photos on Instagram wiped from phone retrieved using HAR HTTP Archive file Linux tool jq for extracting image URL automation using bash script"
tags:
  - "clippings"
---
## The proof of concept images for the vending machine hack were lost. How did I get them back?

**August 9, 2020:** I was starting to piece together my last week’s post, when I opened Google Photos for the images to be included as proof-of-concept. Unfortunately, I couldn’t find them anymore. Then I remembered factory resetting my phone two weeks after, so they must have been wiped since I do not remember backing them up. But you saw my last post, and it has those images. How did I get them back?!… Through an **HTTP Archive** file and some amazing Linux tools.

I posted few photos of the hack on Instagram stories some 4000 years ago. Luckily, I added them to the profile highlights as well.

![instagram web stories highlights](https://miro.medium.com/v2/resize:fit:1000/1*B1nvt99ZbLsuqytSbWRjyQ.png)

4000 years ago

Now that they’re stored on Instagram servers, I just need to find a way to get them on my computer since there is no “Save to Device” option in the app menus. I quickly logged in to Instagram web to see if they have the highlights function there and if so, I can get links to those images using ==the most amazing piece of hacking software there is… the Developers Tools==.

![developer tools network tab on instagram web stories](https://miro.medium.com/v2/resize:fit:1000/1*nRGjU7ggaJjjZnTkmj-ynQ.png)

notice the domains and file types

I opened the console to see GET requests with the source image request URLs. Awesome! I can download the images now,… but should I? They were NINE images, NINE links to be clicked and saved manually using more clicks. The math is too much! I decided to look for a more automated solution in case there’s ever a need to scale up. Enter HAR.

![saving HAR file menu](https://miro.medium.com/v2/resize:fit:700/1*Px-71pe7ZVl-SyLi8VsCiQ.png)

never used it for its original purpose but this is a good start

This HTTP Archive file, which can be exported from the Networks tab, is a JSON file containing [detailed performance data](https://confluence.atlassian.com/kb/generating-har-files-and-analyzing-web-requests-720420612.html) of the browser about the webpage it loads. This would include the image requests URLs I’m interested in. I’ve been looking for a way to collect request URLs like this for ever, and I’ve finally found it during this engagement.

![HAR JSON file contents](https://miro.medium.com/v2/resize:fit:700/1*8rPDbsiDkqCSW-SAQCtlpQ.png)

the servers keep changing so this HAR becomes obsolete in a few days

After analyzing the JSON structure, I found which request URL values I need. It’s the one with host as ‘instagram.fdel11–1.fna.fbcdn.net’. I used jq for parsing through this JSON data, all 15,566 lines of it. I thought about using grep or awk or sed but I suppose they would have required a lot more tweaking. Plus I wanted to get better at jq, since I’ve only used it once before.

![jq manuals on GitHub Pages](https://miro.medium.com/v2/resize:fit:700/1*Zz5-ZmcWvfWxaNeUGSvXyg.png)

finding string matching techniques

I spent some time reading up on [how to traverse arrays](https://www.baeldung.com/linux/jq-command-json), creating a regex for [string matching the URL](https://zerokspot.com/weblog/2013/07/18/processing-json-with-jq/), also trying to resolve a recurring “error: test is not defined” . Let me know if you managed to solve this because I couldn’t get it working on my terminal. So I resorted to using their [online playground](https://jqplay.org/) for testing… A ==one-line bash command for extracting direct image URLs from the HAR file==. And another one to download them.

![jq playgorund](https://miro.medium.com/v2/resize:fit:1000/1*rJkG-cblIlvPSzjzXChUYg.png)

18 URLs because profile pictures loaded when I accidentally clicked on chats

At this point I had everything I needed, complete with a bash script to go over the URLs, and download the images using wget. Because everything looks cool in script?! Take a look for your experimental pleasures :p

only it doesn’t work on my machine. yet.

This is an example of how problem solving works in the real world. Taking existing random knowledge bits, sometimes learning new bits as well and connecting them in a clever way to get results. Click below to see my last week’s post where I used these images for proof of concept.