---
title: "Gossip Glomers"
source: "https://fly.io/blog/gossip-glomers/"
author:
  - "[[Fly]]"
published:
created: 2025-02-09
description: "Fly.io Distributed Systems Challenges"
tags:
  - "clippings"
---
Author

![Ben Johnson](https://fly.io/static/images/ben.webp)

Name

Ben Johnson

@benbjohnson

[@benbjohnson](https://twitter.com/benbjohnson)

![Hooking into NATS to centralize logs](https://fly.io/blog/gossip-glomers/assets/gossip-glomers.webp)

Image by [Annie Ruygt](https://annieruygtillustration.com/)

We’re Fly.io. We run apps for our users on hardware we host around the world. This post isn’t about our platform. Rather, it’s an elaborate plot to get you to write some code just for the hell of it.

In the field of computer science, the industry is represented by two separate yet equally important groups: the software developers who build Rails applications and mobile games, and the academics who write theory papers about why the problems those apps try to solve are NP-hard. This is a story about both.

Distributed systems span the practical-academic divide. Reading a stack of MIT PhD dissertations may be a good Friday night, but it won’t equip you for debugging a multi-service outage at 2am. That requires real-world experience.

Likewise, building a fleet of microservices won’t give you the conceptual tools to gracefully & safely handle failure. Many failure scenarios are rare. They don’t show up in unit tests. But they’re devastating when they do show up. Nailing down the theory gives you a fighting chance at designing a correct system in the first place.

The practical and academic tracks seldom converge. To fix this, we teamed up with [Kyle Kingsbury](https://aphyr.com/about), author of [Jepsen](https://jepsen.io/), to develop a series of distributed systems challenges that combine real code with the academic rigor of Jepsen’s verification system.

We call these challenges the [Gossip Glomers](https://fly.io/dist-sys).

**What the f$#\* is a Glomer?**  
It’s an elaborate pun about the CAP theorem.

## How it works

You know Kyle Kingsbury from his “[Call Me Maybe](https://jepsen.io/analyses)” blog posts that eviscerate distributed databases. You may also have known about [Jepsen](https://github.com/jepsen-io/jepsen), the Clojure-based open-source tooling Kyle uses to conduct these analyses. Well, Kyle also wrote another tool on top of Jepsen called [Maelstrom](https://github.com/jepsen-io/maelstrom).

Maelstrom runs toy distributed systems on a simulated network. It easily runs on a laptop. Kyle uses it to teach distributed systems. We all thought it’d be neat to build a series of challenges that would teach people around the Internet Maelstrom, and, in turn, some distributed systems theory.

Each challenge is composed of several parts:

- The *workload* acts as a set of clients to your distributed systems. These clients send different types of messages as defined by the challenge and expect certain constraints to be met. These workloads can vary between a simple distributed counter all the way to multi-operation, transactional database systems.
- The *simulated network* injects network partitions or slows messages between nodes.
- The *verification system* uses Jepsen to check consistency and availability constraints required by the challenge.
- And finally, the binary for the *node* which is written by you!

## Pathway to distributed systems enlightenment

Our challenges start off easy and get more difficult as you move along. They’re organized into six high-level challenges with many of those having several smaller challenges within them.

First, you’ll start with the Echo challenge. This is the “hello world” of distributed systems challenges. It gets you up and running and helps you understand how these challenges work.

Next, you’ll build a totally-available, distributed unique ID generator. In this challenge, nodes will need to be coordination-free and independently generate a unique identifier for any number of clients.

After that, the difficulty starts to ramp up with the broadcast challenge. In this challenge, you’ll need to propagate messages out to all the nodes in the cluster. You’ll need to ensure fault tolerance in the face of network partitions and then work to optimize your message delivery to minimize the number of messages sent within your system.

Once you’ve made it past broadcast, you’ll implement a grow-only counter, or g-counter. The tricky part with this challenge is that you’ll need to build on top of Maelstrom’s [sequentially](https://jepsen.io/consistency/models/sequential) consistent key/value store.

Then you’ll dive into the world of replicated logs by building a Kafka-like system. This challenge will build on the [linearizable](https://jepsen.io/consistency/models/linearizable) key/value store provided by Maelstrom but you’ll need to figure out how to not only make it correct but also efficient.

Finally, you’ll wrap up with the totally-available transactions challenge where you’ll build a transactional database on various consistency levels.

## A bit of history

Over the past year, we’ve been growing like gangbusters. That’s great. But it also means we’ve been hiring, and hiring is hard.

We hire [resume-blind, based on work-sample tests](https://fly.io/docs/hiring/): we have people write code and design systems, and then score those submissions based on a rubric. We’ve got criteria set up for [early-career, mid-level, and team-lead developers](https://fly.io/docs/hiring/levels/). But we didn’t have strong criteria for hiring staff engineers.

So we began tossing around ideas. In a previous life, some of us had success with a series of cryptography challenges called [Cryptopals](https://cryptopals.com/), so we figured we’d try something similar, but with a distributed systems flavor.

That sounded great but how do you actually test distributed systems to know if someone passed or failed? For weeks, we wrote up one iteration after another but none of them felt right.

Finally, we had a brilliant idea. Let’s find someone who lives and breathes distributed system validation! That someone is Kyle Kingsbury.

After working on these challenges with Kyle, we realized that they are too much fun to keep to ourselves as an internal evaluation tool. So we’re releasing them for anyone to play with.

## But wait… there’s more!

If you scoff in the face of cascading failures, if you bend consistency levels to your will, and if you read [k8s.af](https://k8s.af/) post-mortems as bedtime stories to your kids, you may be interested in trying our hardest challenge.

We reserved this last challenge for evaluating our staff engineers at Fly.io. So if you think you’d be up to the challenge, [we’d love to talk to you](https://fly.io/jobs/).

Next post ↑

[Fly.io ❤️ JS](https://fly.io/blog/flydotio-heart-js/)

Previous post ↓

[Shipping Logs](https://fly.io/blog/shipping-logs/)