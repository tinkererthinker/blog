---
title: "Distributed Systems: Challenges, Experiences and Tips"
source: "https://dev.to/sirneij/distributed-systems-challenges-experiences-and-tips-eik"
author:
  - "[[John Owolabi Idogun]]"
published: 2023-12-30
created: 2025-02-09
description: "Motivation   About 4 months ago (approximately the last time I wrote something here), I... Tagged with distributedsystems, cpp, systems."
tags:
  - "clippings"
---
## Motivation

About 4 months ago (approximately the last time I wrote something here), I opted to embark on a graduate school journey at Stony Brook University, Computer Science (if you have a remote position — Technical Writer and/or Software Engineer position — at any company, don't hesitate to [reach out](https://gmail.com/)). Was it the best decision to make considering more theoretical undertakings, assumptions, and a new culture and environment? I can't tell sincerely. I, however, genuinely want to garner enough knowledge to do real research and this is the best time for me to do so. That's enough motivation. I have also met cool and loving individuals. Besides, I had a thorough challenge posed by one of the courses I took in the 2023 fall semester: [Distributed Systems](http://mpaxos.com/teaching/ds/23fa/). It had some labs — 4 normal labs with a bonus, the skeletal files for each lab can be seen [here](https://github.com/stonysystems/dslabs-cpp). The labs culminated in building a sharded and replicated fault-tolerant key-value store with transaction support based on the [Raft Consensus Algorithm](https://raft.github.io/) using [Optimistic Concurrency Control](https://en.wikipedia.org/wiki/Optimistic_concurrency_control)(OCC) and subsequently, [two-phase locking (2PL)](https://en.wikipedia.org/wiki/Two-phase_locking). All the implementation was in the difficult low-level programming language, [C++](https://cplusplus.com/). Though some untoward stuff happened at the tail end (I may get to write about it later), my goal was eventually achieved. I learned quite a bit:

- I got familiar with various distributed systems algorithms, patterns, design decisions, trade-offs, and new kids.
- Debugged and battled the not-so-interesting segmentation faults and core dumps prevalent in C++ programs.
- Serialized data in a rather low-level manner so they can safely be sent via [RPC](https://www.ibm.com/docs/en/aix/7.3?topic=concepts-remote-procedure-call)s.
- Struggled to properly use [lock](https://cplusplus.com/reference/mutex/lock/) primitives while also building a simple locking system from scratch to ensure proper concurrency control and prevent uncontrolled access to application state (data).
- Implemented a batching system to group RPCs and potentially reduce the total number sent. And so much more.

The biggest challenge was knowing how to do some stuff based on the environmental restrictions of the labs. The skeletal code was void of documentation, the straw that broke the Carmel's back!

**NOTE: This article is NOT to implement the labs and my implementation CAN'T be made available. It however summarizes my experiences, challenges and tips on how I succeeded in getting the labs done. Everything written here is solely based on my current understanding of things.**

I hope you find it resourceful.

## Lab experiences and challenges

### [Lab 1](http://mpaxos.com/teaching/ds/23fa/labs/lab1.html): [The Raft Consensus Algorithm](https://raft.github.io/)

For a system to be distributed, several "separate" computation nodes in the same and/or different geographical locations are working to achieve a common, shared goal. Such a system is expected to tolerate failures (crashes and network partitions) and ensure data availability even during such failures. Another requirement can be that the data the system sends to the client MUST be the latest! These requirements can concisely be expressed as Data Consistency (C), Data Availability (A), and Partition tolerance (P). The birth of CAP and its famous theorem, [CAP theorem](https://en.wikipedia.org/wiki/CAP_theorem). Some questions that beg to be answered are:

1. How can a system with many nodes situated in a different location(s) be implemented and expertly connected (mostly via a network which, inherently, may fail) to provide (the correct) data as fast as possible even when the connecting links between the nodes fail?
2. Since any of these nodes may be provided with data, how can the other nodes be aware of such data and reach a "truce" to either accept or reject the data provided by the client?

To answer most of these questions, the raft algorithm was invented by Diego Ongaro and John Ousterhout in the [raft paper](https://raft.github.io/raft.pdf). Raft isn't the first consensus algorithm. It first appeared less than a decade ago (May 20, 2014)! Before it was the notoriously difficult-to-implement [Paxos](http://lamport.azurewebsites.net/pubs/paxos-simple.pdf) by [Leslie Lamport](https://en.wikipedia.org/wiki/Leslie_Lamport), as well as Viewstamped Replication among others. Raft is, however, simpler to reason about than Paxos. Implementing it isn't a trivia undertaking notwithstanding.

To address the second question, Raft has a strong leader duly elected by the participating nodes during the raft's electoral process (via `RequestVote` RPC). Does this mean there can only be one leader in a raft system? Under normal conditions, yes! However, during extreme cases of network partitions, a previously elected leader may be partitioned or the partitioned servers may "elect" a new leader if they make a quorum — to tolerate $$
f
$$ failures in non-Byzantine fault-tolerant systems, there must be a total of $$
2f + 1
$$ ( $$
3f +1
$$ for Byzantine systems) servers with about $$
f + 1
$$ ( $$
2f + 1
$$ for Byzantine systems) quorum size. Raft, however, has a nifty way of ensuring only a leader successfully takes the mantle of ensuring consistent logs. Hence, the raft election system is one of the safety nets of the protocol as any supposed leaders whose logs and terms are "stale", will eventually be turned into followers!

As soon as a leader is elected, he takes total control of accepting data from the client(s) and propagating such data to the other nodes (followers). This is done via the `AppendEntries` RPC. The first question gets some attention here. To understand raft, kindly read the [paper](https://raft.github.io/raft.pdf). I also recommend the visualization on the protocol's website as well as this [interesting visualization](http://thesecretlivesofdata.com/raft/).

To implement raft in Go, this [series of articles](https://eli.thegreenplace.net/2020/implementing-raft-part-0-introduction/) is recommended. If you want to take up the challenge of implementing the protocol via the repository previously shared, these tips might be helpful:

- Most of the labs are equivalent to MIT's [Distributed systems labs](https://pdos.csail.mit.edu/6.824/index.html) from 2 to 4 with some differences.
- Sending an RPC is via the repo's event system. For instance, assuming I want to send an `AppendEntries` RPC to the system's followers, I could have something like:  

```cpp
...
auto event = commo()->SendAppendEntriesRPC(partition_id,id_of_the_follower,...); // You can pass as many arguments as you want based on your implementation
event->Wait(1000000); // How long do you want the request to wait before timing out (in microseconds, )?
...
```

If the `event` variable is of type `std::shared_ptr<rrr::IntEvent>`, it has a member variable called `status_` that tells you what the current status of the RPC is and it's one of:  

```cpp
...
INIT = 0, 
WAIT = 1, 
READY = 2,
DONE = 3, 
TIMEOUT = 4, 
DEBUG
...
```

It should be noted that sending a custom `struct` through the RPC framework might not work. You should consider breaking the `struct` into primitives such as `bool`, `int`, `string` or `vector<...>`. For instance, in Figure 4 of the [raft paper](https://raft.github.io/raft.pdf), an `AppendEntries` RPC should have `int term`, `int leaderId`, `int prevLogIndex`, `int prevLogTerm`, `vector<Log> entries`, and `int leaderCommit` as arguments while `int term`, `bool success` are what each follower should return. `vector<Log> entries` might be very problematic to send and the annoying thing is you might be getting some errors in your tests without an informational log to point you in the right direction. Assuming the `Log` struct is:  

```cpp
struct Log
{
    int index;
    int term;                  
    shared_ptr<Marshallable> command;
};
```

If you have a system-wide variable to hold all the logs, say `vector<Log> logs`, you'd split the `logs` variable into three vectors:  

```cpp
...
vector<int> indexes;
vector<int> terms;
vector<shared_ptr<Marshallable>> commands;
...
```

And then send individual vectors over the network. Then, at the receiving end (the follower's end), merge them to become one vector of `Log` again. If you have got a struct like this instead:  

```cpp
struct Log
{
    int term;                  
    shared_ptr<Marshallable> command;
};
```

Then, the split can be:  

```cpp
vector<int> terms;
vector<shared_ptr<Marshallable>> commands;
```

A caveat is that the RPC framework available in the repo cannot "serialize" `shared_ptr<Marshallable>` nor a `vector<shared_ptr<Marshallable>>`. You need to convert it to `MarshallDeputy` or `vector<MarshallDeputy>`. You can retrieve `shared_ptr<Marshallable>` from `MarshallDeputy` by just doing `MarshallDeputy.sp_data_`.
- The high overview of the raft system is:  

```shell
client -> server -> commo -> services
```

When a client wants to make a request, it should call the `Start` method in the code's `server.cc`. This method "magically" initiates the process of starting the raft's server, which in turn starts the leader election process and the subsequent leader heartbeating (broadcasting messages to its followers at intervals — 150 milliseconds to 300 milliseconds in the raft paper. However, the lab's recommends higher intervals for some reasons). The `commo` system is used to request votes and subsequent communications (like the `AppendEntries` RPC). It utilizes the codes you write in `commo.cc` to asynchronously call those you also write in `services.cc`. `services.cc` should be written to handle the follower side of the process based on the raft protocol. There is a file called `raft_rpc.rpc` which should be modified based on the arguments and return values of the RPCs you define there. It auto-generates some C++ codes if you properly modify the file and `services.h/cc`.
- Since the sources of error could be very difficult to pinpoint, it's recommended to use some debugger and/or the logging framework built into the repo. Among other things, you need to keep track of the application states such as `int currentTerm`, `int votedFor`, `vector<Log> logs`, `int commitIndex`, `int lastApplied`, `vector<int> nextIndex` or `map<int, int> nextIndex`, and `vector<int> matchIndex` or `map<int, int> matchIndex`. You can write some helper methods to help stringify the complex types and use the framework's logging system to output the states at every stage of running the tests. There are about 4 levels:  

```cpp
#define Log_debug(msg, ...) ...
#define Log_info(msg, ...) ...
#define Log_warn(msg, ...) ...
#define Log_error(msg, ...) ...
#define Log_fatal(msg, ...) ...
```

`Log_info` prints logs to the console effortlessly. You need to be careful though. Excessive printing of logs can lead to some sort of errors as well. An example of how to log is:  

```cpp
Log_info("election timer started at term: %d", currentTerm)
```

Those are the basic high-level overview of the raft implementation for lab 1. Note that there are a lot of things to do to get it to work. You've got to debug and debug and debug. As a brand new person to systems programming, it took me weeks (2 weeks and 5 days) to complete with brutal trial and error. It took some less and others more time. The experience was a mixed one, like how you feel when your code doesn't work and then works. That implementation series I shared greatly helped. Also, ensure that your implementation is efficient and performant. Other labs need those to pass.

### [Lab 2](http://mpaxos.com/teaching/ds/23fa/labs/lab2.html): A replicated (or fault-tolerant) key-value store

The raft implementation above is pretty low-level and by itself, isn't particularly useful. It needs to be used by a bigger system which directly benefits the users. An example of such a system is a key-value store like [Redis](https://redis.io/). This lab expects you to utilize the raft previously implemented to build a fault-tolerant key-value database. Your implementation should support `Put(key, value)`, `Append(key, value)`, and `Get(key)`. Of course, you can support `Delete(key)` too to have a full [CRUD](https://en.wikipedia.org/wiki/Create,_read,_update_and_delete) functionality. It's relatively simpler compared to the previous lab though it has its nuances:

- Depending on your implementation, you need to wait for the participating raft servers to reach a consensus before responding to the client's requests. For instance, if the client sends a `Get("John")`, you shouldn't immediately respond with either its value or `NOT FOUND` error. You should wait via the `OnNextCommand` method for the agreement of the servers. Only after that should you respond to the client. If you don't, some of the tests will not pass. The waiting mechanism could be event-based (like the event system introduced above) or just some timing mechanism that retries until a timing upper bound is reached. You should avoid a busy wait though by sleeping for some microseconds before retrying.
- Locking is extremely important since you are working with a concurrent system. A recursive locking primitive was built into the framework. Judiciously use it because with locking comes deadlock. You can't afford to write a system that's susceptible to deadlocks.

This lab was a lot easier than Lab 1. It took a few days for me to implement having had some rusty experience writing and debugging C++-based systems programming.

### [Lab 3](http://mpaxos.com/teaching/ds/23fa/labs/lab3): Sharded key-value store

This is another intense lab. In lab 1, we built a barebone raft implementation whose non-volatile states (`currentTerm`, `votedFor`, `logs`) were not made to be as such. Currently, if the raft server crashes, those states are gone. This defeats the purpose of the raft algorithm. A crashed server needs to "recover" with its previous states intact! That's what the first part of this lab aims to achieve — to persist those important server states. It has some caveats though:

- The [raft paper](https://raft.github.io/raft.pdf) considers `commitIndex` and `lastApplied` volatile states on all servers. However, to scale through the tests, they need to be persisted as well. If not, the last committed log will likely get recommitted again which will fail the test.
- The persistent methods should be carefully sprinkled over places where they are needed to avoid performance bottlenecks. Starting the server should read from the persisted states in case such states exist.

The next part of the lab is implementing a checkpointing mechanism called `Snapshotting`. This is needed to prevent an infinitely long `vector<Log>` which is not practical since computer memories ain't infinite! Snapshotting allows `log[]` to be truncated at a particular index. **I skipped this part when it was taking a lot of my time without a headway**.

The next part was building a sharded key-value store. The store is equivalent to the one built in lab 2 aside from the sharding feature. Sharding is a nifty way of splitting datasets into partitions or shards. It aims to utilize parallel processing capabilities to process smaller datasets across shards thereby making the overall system more performant. It is used extensively in systems such as [DynamoDB](https://aws.amazon.com/pm/dynamodb/?gclid=Cj0KCQiA7aSsBhCiARIsALFvovxgmzVvBfQFtlAimxe570_DuF1ImZYKqq0qkgoG2A-MixQqPq21wxYaArKQEALw_wcB&trk=94bf4df1-96e1-4046-a020-b07a2be0d712&sc_channel=ps&ef_id=Cj0KCQiA7aSsBhCiARIsALFvovxgmzVvBfQFtlAimxe570_DuF1ImZYKqq0qkgoG2A-MixQqPq21wxYaArKQEALw_wcB:G:s&s_kwcid=AL!4422!3!610000101513!e!!g!!dynamodb!11205224796!115505094368) which uses a **0-hop Distributed Hash Table (DHT)** as its sharding mechanism to reduce latency and increase efficiency. There is also **X-hop DHT** which is utilized in systems such as [BitTorrent](https://www.bittorrent.com/). They have their use cases. In the lab, however, a traditional sharding mechanism where data are sharded by their "unhashed" keys was used. For it to work, you need to handle scenarios where nodes `Join` or `Leave` a shard. You also handle situations where nodes are `Move`d from one shard to the other. As in lab 2, these processes should pass through raft and until the servers are aware and have agreed on any of the operations, you should keep retrying. The tips for this part are:

- Your raft implementation must be aware that the systems are now partitioned and when asking for votes or agreement, the RPCs should only be sent to the servers in a partition.
- The client of `shardkv` must be implemented in such a way as to only send the request on a key to the leader of the servers in the shard it belongs. You can get the servers in a shard by using the `Query` endpoint of the shardmaster you have implemented.
- Rebalancing of shards must be efficiently done so that shards are evenly divided and "should move as few shards as possible to achieve that goal". Therefore, after every successful `Join` and `Leave` operation, you need the rebalancing logic to evenly distribute servers into shards in an optimal way.
- The `sharkv` server itself is identical to what was done in lab 2.

Implementing this last part gives you an idea of how Google's BigTable & Spanner and Apache's HBase were implemented. It was thrilling for me to get them working.

### [Lab 4](http://mpaxos.com/teaching/ds/23fa/labs/lab4): Distributed transactions

Now to the meat of it! Till now, we have not had a truly distributed database system that supports transactions. In the database world, it is the dream of database systems to be [ACID](https://www.mongodb.com/basics/acid-transactions)\-compliant. This means that concurrent transactions are expected to be **A**tomic, **C**onsistent, run in **I**solation, and **D**urable.

**NOTE**: The **Concurrency** in [ACID](https://www.mongodb.com/basics/acid-transactions) isn't the same as Distributed Concurrency. Distributed Concurrency is more related to **Isolation**. It entails having a consistent state of data as against having data that obey constraints (integrity, referential and other constraints) stated by an application or Software Engineer utilizing a Database Management System. This means that a consistent distributed system should always respond with the latest written data of a particular key. This however depends on the consistency and isolation level the system adopts. Google [Spanner](https://static.googleusercontent.com/media/research.google.com/en//archive/spanner-osdi2012.pdf), for example, is [linearizable](https://jepsen.io/consistency/models/linearizable) and [serializable](https://jepsen.io/consistency/models/serializable) having used [Paxos](http://lamport.azurewebsites.net/pubs/paxos-simple.pdf) for replication, [2PL](https://en.wikipedia.org/wiki/Two-phase_locking) and [Two-phase commit](https://en.wikipedia.org/wiki/Two-phase_commit_protocol)(2PC) for transaction execution and commit. Though performance is always an issue and to mitigate that, Spanner adopted a relaxed isolation level for read operations. The isolation level used is called `Snapshot Isolation`. For details about all the isolation levels and what they mean, I suggest you check out this [paper](https://www.microsoft.com/en-us/research/wp-content/uploads/2016/02/tr-95-51.pdf).

In lab 4, you will spend time mostly on the client side (because the client is the coordinator) implementing a concurrency control protocol called [OCC](https://en.wikipedia.org/wiki/Optimistic_concurrency_control). Some tips:

- Build a locking system from scratch. You don't need to use C++'s locking primitive. You may have a store for keeping locks and ensure that once a transaction has acquired a lock, no other transaction is allowed.
- Two phases need to be handled: Prepare and Commit. In the "prepare" phase, locks of all the transactions (reads and writes) are acquired (abort if not successful). Then, for reads, check the versions of the keys there with the ones directly from the server. Any disparity should abort such a process. If the prepare phase succeeds, proceed to commit the writes by simply sending `Put` requests to the server. If the commit isn't successful, you should abort and release the locks. Otherwise, release the locks and return a nod to the requesting client.

The implementation is a bit involved but almost of the same intensity as Lab 2.

## Conclusion

That summarized my experience in Distributed Systems so far. It was challenging stuff for me as I had no prior familiarity with systems programming. What I learnt, however, was worth the stress.

A very interesting thing is my Professor, [Yanhong Annie Liu](https://en.wikipedia.org/wiki/Yanhong_Annie_Liu), created a language for distributed algorithms, [DistAlgo](https://github.com/yanhongliu/distalgo). The implementation of Raft and other distributed algorithms in the language is pretty solid. I shall be writing about the language as soon as I get comfortable with it. Kindly be on the lookout.

In the meantime, compliments of the season. It's good to write again after a while off! See ya!

## Outro

Enjoyed this article? I'm a Software Engineer and Technical Writer actively seeking new opportunities, particularly in areas related to web security, finance, health care, and education. If you think my expertise aligns with your team's needs, let's chat! You can find me on LinkedIn: [LinkedIn](https://www.linkedin.com/in/idogun-john-nelson/) and Twitter: [Twitter](https://twitter.com/Sirneij).

If you found this article valuable, consider sharing it with your network to help spread the knowledge!

## Attribution

Cover image: [Designed by fullvector / Freepik](http://www.freepik.com/).