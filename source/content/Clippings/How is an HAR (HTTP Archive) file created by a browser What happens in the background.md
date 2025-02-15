---
title: "How is an HAR (HTTP Archive) file created by a browser? What happens in the background?"
source: "https://www.reddit.com/r/learnprogramming/comments/hb7s4s/how_is_an_har_http_archive_file_created_by_a/"
author:
  - "[[quittersflora]]"
published: 2020-06-18
created: 2025-02-14
description: "Any help greatly appreciated!"
tags:
  - "clippings"
---
[MarketAntique4382](https://www.reddit.com/user/MarketAntique4382/)

• [5y ago](https://www.reddit.com/r/learnprogramming/comments/hb7s4s/comment/g2s2iw0/) • Edited 4y ago

when you go over to the network tab on developers tools, you'll see all the requests and responses between the browser and the webpage it loads, HTTP performance data, the tracked webpages, response times about the whole transaction. [more details what it stores](https://fileinfo.com/extension/har)

HAR file format is storing exactly that information in a JSON format for debugging performance and page rendering issues in an offline environment. [HOW?](https://confluence.atlassian.com/kb/generating-har-files-and-analyzing-web-requests-720420612.html)

when you click to export it, the browser bundles all this into a JSON format with .har extension. since all of this data is already being captured by the browser.

hope this answers your question! there is an article about how a HAR file can be used for automating requests. [if you're interested](https://medium.com/@nileshkg/my-personal-ctf-challenge-4016e9c176b3?source=friends_link&sk=c124cc0a4b72ec72a9a43f8ca289b778)
- [[WHAT PROBLEM SOLVING ACTUALLY LOOKS LIKE]]
	- instagram har file