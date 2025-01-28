---
title: "How to Search Instagram caption text?"
source: "https://stackoverflow.com/questions/27042672/how-to-search-instagram-caption-text"
author:
  - "[[Stack Overflow]]"
published: 2014-11-20
created: 2025-01-28
description: "Is it possible to search Instagram photo stream posts ( captions ) instead of searching hashtags for certain area . Many people are posting without defining hashtags , and some disable their locati..."
tags:
  - "clippings"
---
Is it possible to search Instagram photo stream posts ( captions ) instead of searching hashtags for certain area . Many people are posting without defining hashtags , and some disable their location , So how to search Media ' captions ' in the public stream or area stream !

[https://api.instagram.com/v1/media/search](https://api.instagram.com/v1/media/search)

has no search query .

[https://api.instagram.com/v1/tags/tag/media/recent](https://api.instagram.com/v1/tags/tag/media/recent)

just look for hashtags not the caption text !

[

![VLAZ's user avatar](https://i.sstatic.net/hy0Bnl.png?s=64)

](https://stackoverflow.com/users/3689450/vlaz)

[VLAZ](https://stackoverflow.com/users/3689450/vlaz)

29k9 gold badges62 silver badges82 bronze badges

asked Nov 20, 2014 at 14:59

[

![Hamza's user avatar](https://www.gravatar.com/avatar/ec3292466c215a2700318e062ca63109?s=64&d=identicon&r=PG)

](https://stackoverflow.com/users/143703/hamza)

4

You can try google search:

"site:instagram.com/p sunset"

answered Jun 12, 2020 at 1:28

[

![kdqed's user avatar](https://lh6.googleusercontent.com/-xDSJSy_xPPc/AAAAAAAAAAI/AAAAAAAAA6U/U3HIVga7ZGI/photo.jpg?sz=64)

](https://stackoverflow.com/users/9975991/kdqed)

[kdqed](https://stackoverflow.com/users/9975991/kdqed)kdqed

665 bronze badges

Using GraphQL APIs. Take a look at getAllUserJsonData() function of the IGPF project [here](https://github.com/LucaBarile/InstagramPostFinder).

answered Mar 24, 2023 at 16:09

[

![John Deere's user avatar](https://www.gravatar.com/avatar/29cd50e9154edd277cc0fd4e073791e3?s=64&d=identicon&r=PG&f=y&so-version=2)

](https://stackoverflow.com/users/21476876/john-deere)