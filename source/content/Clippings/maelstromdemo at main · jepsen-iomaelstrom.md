---
title: "maelstrom/demo at main · jepsen-io/maelstrom"
source: "https://github.com/jepsen-io/maelstrom/blob/main/resources/protocol-intro.md"
author:
  - "[[GitHub]]"
published:
created: 2025-01-28
description: "A workbench for writing toy implementations of distributed systems. - maelstrom/demo at main · jepsen-io/maelstrom"
tags:
  - "clippings"
---
Maelstrom nodes receive messages on STDIN, send messages on STDOUT, and log debugging output on STDERR. Maelstrom nodes must not print anything that is not a message to STDOUT. Maelstrom will log STDERR output to disk for you.

## Nodes and Networks

A Maelstrom test simulates a distributed system by running many *nodes*, and a network which routes *messages* between them. Each node has a unique string identifier, used to route messages to and from that node.

- Nodes `n1`, `n2`, `n3`, etc. are instances of the binary you pass to Maelstrom. These nodes implement whatever distributed algorithm you're trying to build: for instance, a key-value store. You can think of these as *servers*, in that they accept requests from clients and send back responses.
- Nodes `c1`, `c2`, `c3`, etc. are Maelstrom's internal clients. Clients send requests to servers and expect responses back, via a simple asynchronous [RPC protocol](https://github.com/jepsen-io/maelstrom/blob/main/resources/#message-bodies).