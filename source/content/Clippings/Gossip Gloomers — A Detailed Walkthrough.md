---
title: "Gossip Gloomers — A Detailed Walkthrough"
source: "https://medium.com/@burnerlee/gossip-gloomers-a-detailed-walkthrough-2b65844ab45b"
author:
  - "[[Aviral Jain]]"
published: 2024-07-19
created: 2025-01-28
description: "I recently stumbled upon these awesome distributed system challenges by fly.io. I was pleasantly surprised because I’ve always been on the lookout for interesting dev-related challenges. You know…"
tags:
  - "clippings"
---
I recently stumbled upon these awesome distributed system challenges by fly.io. I was pleasantly surprised because I’ve always been on the lookout for interesting dev-related challenges. You know, besides the usual competitive programming stuff, which I don’t really consider all that dev-focused.

I think every backend engineer **must** give these challenges a shot. They’re not just educational but also a lot of fun. Plus, they really propel you forward in your developer journey.

Before diving into these challenges, I had some experience with Golang, but my knowledge of distributed systems was pretty basic. I knew about the CAP Theorem, but if you asked me what each letter stood for, I might have guessed “C” for consistency, “A” for availability, and “P” for… maybe permanence? 😄

So, if you’re a beginner too, don’t get intimidated by the challenges. This is going to be a fun and detailed walkthrough of all the challenges, approaches I took to solve them including the local setup and documentation navigation.

> Note: If you are familiar with the problems, and looking for solutions, you can skip this article and head to the solutions directly:
> 
> [Challenge 2](https://medium.com/@burnerlee/gossip-gloomers-a-detailed-walkthrough-challenge-2-fe1dc7a63496)  
> [Challenge 3a](https://medium.com/@burnerlee/gossip-gloomers-a-detailed-walkthrough-challenge-3a-132b12a13122) | [Challenge 3b&3c](https://medium.com/@burnerlee/gossip-gloomers-a-detailed-walkthrough-challenge-3b-and-3c-c4a22a8c6e32) | [Challenge 3d](https://medium.com/@burnerlee/gossip-gloomers-a-detailed-walkthrough-challenge-3d-342f6fbf621e) | [Challenge 3e](https://medium.com/@burnerlee/gossip-gloomers-a-detailed-walkthrough-challenge-3e-b6a939983d34)  
> [Challenge 4](https://medium.com/@burnerlee/gossip-gloomers-a-detailed-walkthrough-challenge-4-caf49b1d69b2)

## Understanding the architecture

Before we dive into setting up our system, let’s understand how do you solve the challenges and evaluate your solutions. Since, it is completely different from cp challenges, it is critical to understand the tools provided by fly.io team to test our distributed systems.

![](https://miro.medium.com/v2/resize:fit:700/1*anaZgDJdP511evyNxmA0Xg.png)

Your code is compiled to a binary

![](https://miro.medium.com/v2/resize:fit:700/1*3HQfF4hxFQO4cTBCzPbJzA.png)

Maelstrom binary deploys a distributed system using your compiled binary and a set of clients

The above diagrams is pretty self-explanatory. We download the `Maelstrom Binary` (a tool) from their website which deploys our code as a server node in the distributed system.

Hence, we need to implement the node servers with the following assumptions of a generic distributed system:

1. Clients might make concurrent calls on a single node, i.e. a node might be handling multiple clients at the same time in as many go-routines.
2. Concurrent calls might be distributed among the node servers.
3. There is no client-server mapping, any client’s request might be served by any server-node.
4. More about communication between nodes later.

## Setting up the playground

## 1\. Download the Maelstrom Binary

a. Install Deps:

Maelstrom is built in [Clojure](https://clojure.org/) so you’ll need to install [OpenJDK](https://openjdk.org/). It also provides some plotting and graphing utilities which rely on [Graphviz](https://graphviz.org/) & [gnuplot](http://www.gnuplot.info/). If you’re using Homebrew, you can install these with this command:

```
brew install openjdk graphviz gnuplot
```

You can find more details on the [Prerequisites](https://github.com/jepsen-io/maelstrom/blob/main/doc/01-getting-ready/index.md#prerequisites) section on the Maelstrom docs.

b. Install the binary:

You can find the binary here: [Maelstrom 0.2.3](https://github.com/jepsen-io/maelstrom/releases/tag/v0.2.3)

## 2\. Setting up your local code

```
mkdir gossip-gloomers
cd gossip-gloomers
mkdir maelstrom-echo
cd maelstrom-echo
touch main.go
go mod init maelstrom-echo
go mod tidy
```

Now you can start coding in `main.go`

The first challenge of maelstrom is a walkthrough challenge in itself to explain the setup. We will follow the same procedure

So you can follow the instructions below:

Copy the following file in `main.go`

```
package mainimport (
 "encoding/json"
 "log"
 "os" maelstrom "github.com/jepsen-io/maelstrom/demo/go"
)func main() {
 n := maelstrom.NewNode() 
 n.Handle("echo", func(msg maelstrom.Message) error {
  
  var body map[string]any
  if err := json.Unmarshal(msg.Body, &body); err != nil {
   return err
  }  
  body["type"] = "echo_ok"  
  return n.Reply(msg, body)
 }) 
 if err := n.Run(); err != nil {
  log.Printf("ERROR: %s", err)
  os.Exit(1)
 }
}
```

Now run the following commands:

```
# make sure GOPATH is set and added to your PATH env
go mod tidy && go mod vendor
go install .# you should be able to access this cmd
maelstrom-echo
```

Using `go install .` , you compiled your `main.go` to a binary. Then you can use the `maelstrom` binary (downloaded in Step 1), to test your compiled binary.

```
/path/to/downloaded/maelstrom/binary test -w echo --bin /path/to/compiled/maelstrom-echo --node-count 1 --time-limit 10
```

Breaking down the command:

1. `/path/to/downloaded/maelstrom/binary` — The path to the maelstrom binary you downloaded
2. `test` — the testing command name
3. `-w echo` — the workload argument. This tells the binary, which workload (challenge) you are testing for
4. `--bin /path/to/compiled/maelstrom-echo` — the path to your compiled binary. This is the code (binary) to be tested
5. `--node-count=1` — The number of nodes (server) to be deployed in the distributed system to be tested.
6. `--time-limit` — The time for which the system is tested

There are more available arguments, but we would get to know them later. For now make sure you get an idea of what we’re trying to do.

Now that you have a little understanding, let’s go through the code in `main.go`

```
import maelstrom "github.com/jepsen-io/maelstrom/demo/go"
```

We import the maelstrom golang library which helps us define the node, and define the handlers for handling requests from the clients. We can think of these handlers as normal http requests.

```
n := maelstrom.NewNode()
```

Here, we define `n` as the node. Now we can define the handlers on this node object using `n.Handle()`

```
 n.Handle("echo", func(msg maelstrom.Message) error {
  
  var body map[string]any
  if err := json.Unmarshal(msg.Body, &body); err != nil {
   return err
  }  
  body["type"] = "echo_ok"  
  return n.Reply(msg, body)
 })
```

`n.Handle()` takes in the first parameter as a string. This is what maelstrom calls `RPC` . In simpler terms, you can think of this as a the router value (like `/ping`)in a http call. This is the identifier to map a function to the request type.

The second parameter is the handler function. It provides the request message by the object `msg` of the type `maelstrom.Message` . This object generally looks like:

```
{
  "src": "c1",
  "dest": "n1",
  "body": {
    "type": "echo",
    "msg_id": 1,
    "echo": "Please echo 35"
  }
}
```

`src` : `c1`refers to client with id `c1`

`dest` : `n1` refers to node with id `n1`

The body contains other information (like POST data). It will always contain the field `type` which is equal to the `RPC` value.

We unmarshal `msg.Body` into `map[string]any` . The problem (Challenge 1) states that the node only needs to return `echo_ok` as the response to the request. So we change `body[type]="echo_ok"` and send a message back to the client using `n.Reply()`

> You can send message to any nodes/clients in the cluster using `n.Send` , `n.RPC` or `n.SyncRPC` by specifying the address. You don’t need to specify address when using `n.Reply` since it sends back the response to the requester.

```
 if err := n.Run(); err != nil {
  log.Printf("ERROR: %s", err)
  os.Exit(1)
 }
```

And finally we run the node service using n.Run() at the end of the main function. This is similar to running a http server. This is a blocking command and runs until a fatal error.

**You can view the entire source code** [**here**](https://github.com/burnerlee/gossip-gloomers/blob/c7b392156849c36105ddb61aaa74f35fd4bebd25/maelstrom-echo/main.go)

The objective of this article was to make you comfortable with the stack. We haven’t even started solving the challenges yet. We will cover each challenge in a separate article, so that I can cover each of them in detail.

Hope you guys found it interesting. I would really recommend you to create a new directory `gossip-gloomers/maelstrom-unique-ids` and try to solve [Challenge 2](https://fly.io/dist-sys/2/).

The real fun is in trying yourself and scratching your heads all over it. Then feel free to jump on to the next article if you are stuck for a while (atleast a day or 2), or even if you solved it (just in case).

Hope this was worth your time :)

**Here is the link to the detailed walkthrough of** [**Challenge2**](https://medium.com/@burnerlee/gossip-gloomers-a-detailed-walkthrough-challenge-2-fe1dc7a63496)