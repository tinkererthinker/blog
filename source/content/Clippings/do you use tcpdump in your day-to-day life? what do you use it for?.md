---
title: "Thread by @b0rk"
source: "https://x.com/b0rk/status/585234410980712448"
author:
  - "[[@b0rk]]"
published: 2015-04-07
created: 2025-02-22
description: "do you use tcpdump in your day-to-day life? what do you use it for?"
tags:
  - "clippings"
---
**Julia Evans** @b0rk [2015-04-07](https://x.com/b0rk/status/585234410980712448)

do you use tcpdump in your day-to-day life? what do you use it for?

---

**Julia Evans** @b0rk [2015-04-07](https://x.com/b0rk/status/585266745012805632)

@sdstrowes out of curiosity -- what kinds of failures? why do you need to look at DNS responses?

---

**Kenny Hoxworth** @hoxworth [2015-04-07](https://x.com/hoxworth/status/585268470113144832)

@b0rk another use is guaranteeing proper character encoding on the wire to determine where encoding bugs occur (client or server).

---

**Julia Evans** @b0rk [2015-04-07](https://x.com/b0rk/status/585269944515952640)

@hoxworth oooo character encoding oooooooo

---

**Charity Majors** @mipsytipsy [2015-04-07](https://x.com/mipsytipsy/status/585301316718563329)

@b0rk "why is cassandra exploding? ohhhh, developers generating high cardinality columns !@#!" still haven't found a better way to debug

---

**silentbicycle** @silentbicycle [2015-04-07](https://x.com/silentbicycle/status/585242031171227648)

@b0rk Yes, though I tend to use wireshark more for actually interpreting the data (whether live or tcpdump-captured). Debugging networks.

---

**Jen Andre (funcuddles@infosec.exchange)** @fun\_cuddles [2015-04-07](https://x.com/fun_cuddles/status/585400195866828801)

@b0rk used it recently to aid in reverse engineering some proprietary database protocol

---

**Fran García @frangdlt@mstdn.social** @frangdlt [2015-04-07](https://x.com/frangdlt/status/585241881212223488)

@b0rk to diagnose a Cisco router bug that cause 'ACK' packet loss and +30sec delays in a trading environment ;-) #thankgoditsover

---

**Chetan Ahuja** @IAmChetanAhuja [2015-04-08](https://x.com/IAmChetanAhuja/status/585720440959668227)

@b0rk tcpdump and Wireshark are like bread and butter for @packetzoom ( for obvious reasons). Great page on unix tools btw ;-)

---

**Jerry Chen** @jcsalterego [2015-04-07](https://x.com/jcsalterego/status/585234552915755010)

@b0rk ngrep is much more useful, IME

---

**Julia Evans** @b0rk [2015-04-07](https://x.com/b0rk/status/585234679743258624)

@jcsalterego what do you use ngrep for?
- viewing or debugging a handful of JSON REST APIs we have, or looking at MySQL traffic even. or seeing if things are routing correctly

---

**Michael Hicks** @numillustration [2015-04-07](https://x.com/numillustration/status/585261116336386049)

@b0rk although I'm using snoop more lately

---

**Michael Hicks** @numillustration [2015-04-07](https://x.com/numillustration/status/585248790136791040)

@b0rk used extensively to troubleshoot NAT, VPNs, fancy routing, firewall issues,

and SDN successes and failures.

---

**Sean Cassidy** @sean\_a\_cassidy [2015-04-07](https://x.com/sean_a_cassidy/status/585237995793571841)

@b0rk debugging VPC networking issues, verifying programs are actually sending data, etc. it's the ground truth

---

**Wally Quevedo** @wallyqs [2015-04-07](https://x.com/wallyqs/status/585276871064989696)

@b0rk I think it is great for quickly debugging plain text protocols, even more so when no other kind of logging is available

---

**Will Thames** @willthames [2015-04-07](https://x.com/willthames/status/585242400177594369)

@b0rk fairly regularly for debugging connectivity/authentication problems. Just discovered tcpflow for being able to see tcp streams

---

**Robin Smidsrød** @robinsmidsrod [2015-04-07](https://x.com/robinsmidsrod/status/585325119301672960)

@mjdominus @b0rk I've always found iptraf more useful for that use-case, running it directly on the router.

---

**Robin Smidsrød** @robinsmidsrod [2015-04-08](https://x.com/robinsmidsrod/status/585688236128915456)

@mjdominus @b0rk It will pick up all the same packets as tcpdump/wireshark. I just find the UI easier for that use-case.

---

**shale** @logicregressor [2015-04-07](https://x.com/logicregressor/status/585320831036825600)

@b0rk cs458 had us write an ids using tcpdump. Explanation inside:

https://crysp.uwaterloo.ca/courses/cs458/W15-material/a2.pdf…

---

**Natalie** @Lesbiologist [2015-04-07](https://x.com/Lesbiologist/status/585234989760978946)

@b0rk pooping through the network

---

**Jay Parlar** @parlar [2015-04-07](https://x.com/parlar/status/585236418169020416)

@b0rk I used to use it extensively in an old job. Mostly debugging SNMP packets, if memory serves

---

**依云** @lilydjwg [2016-01-16](https://x.com/lilydjwg/status/688327094221209601)

@b0rk not everyday but every time the network goes wrong or I want to peek processes talking MySQL, Redis, TLS or the like.

---

**依云** @lilydjwg [2016-01-16](https://x.com/lilydjwg/status/688327509448851456)

@b0rk I use Wireshark more, and I pipe data from tcpdump on servers or Androids to local Wireshark for easy viewing.

---

**Matthew Curry** @mattjcurry [2015-04-07](https://x.com/mattjcurry/status/585267157866545152)

@b0rk troubleshooting openvswitch and NSX.

---

**Bea Hughes** @beajammingh [2015-04-07](https://x.com/beajammingh/status/585235925111705600)

@b0rk most days. Well, most good or bad days.

---

**Lawrence Teo** @lteo [2015-04-07](https://x.com/lteo/status/585252442184495104)

@b0rk troubleshooting network issues

---

**dmiller@recurse.social** @jazzdan [2015-04-07](https://x.com/jazzdan/status/585271394302328833)

@b0rk “What is this memcached client I wrote \*actually\* sending memcached because clearly I messed something up here”

---

**Hsing-Hui Hsu** @SoManyHs [2015-04-07](https://x.com/SoManyHs/status/585241488079978497)

@b0rk @drbrain does. He even wrote one.

---

**Klerisson Paixao** @klerissonpaixao [2015-04-07](https://x.com/klerissonpaixao/status/585236173334904832)

@b0rk I seldom use it for debug apps.

---

**imre Fitos** @imreFitos [2015-04-07](https://x.com/imreFitos/status/585243616102100992)

@b0rk tcpdump tells the truth when I work with APIs. Documentation is usually not enough.

---

**Julia Evans** @b0rk [2015-04-07](https://x.com/b0rk/status/585237738984710145)

@d6 i'm trying to write a blog post explaining why you'd want to use tcpdump and I think 'reverse engineering' is what I'll go with :)

---

**Julia Evans** @b0rk [2015-04-07](https://x.com/b0rk/status/585250236043501568)

@nelhage how do you find out about latency? just by looking at how long it takes for packets to come back?