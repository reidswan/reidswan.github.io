---
layout: post
title:  "Grokking Raft; or, Yet Another Raft Breakdown, Part 1"
date:   2023-05-23 00:06:45 +0200
categories: projects learning raft
---

Following on from [part 1][grokking-raft-1], in which we learned about Raft's leader election mechanism, we continue our journey into the [Raft paper][raft-paper]. In this installment, we're learning about Raft's approach to log replication.

## Log replication

In an ideal situation, absent of faults, dropped packets and server crashed, log replication is incredibly simpel: a leader receives a request from a client; they apply the request to their own state machine; tell instruct each of their followers to apply it to the follower's own state machine; end of story. 

Unfortunately, faults do happen, and if we followed this naive approach, we'd end up with followers' state machines diverging from each other, and from the leader's. Imagine a state machine with states `A`, `B` and `C` with operations `X`, `Y` and `Z` as follows:

![State machine diagram](/images/raft-simple-state-diagram.png)

If this machine is subject to the transitions  `X, X, Y`, they should end up in state `C` (`A --[X]--> B --[X]--> A --[Y]--> C`); but if one of the `X` operations is dropped, for example because a follower crashed during a log replication call, their state machine will end up in state `B` instead. This state machine divergence is unacceptable: the goal of a replicated state machine is to get every participant to agree on state machine state.

To remedy this, we'll make the leader keep track of which logs it has sent to each of its followers to replicate. The leader will send the log to a follower repeatedly until the follower indicates that the log has been successfully replicated. There's a chance now that a log will be applied twice to a follower, so to be extra-safe, we'll give the log an integer index; followers can use these as identifiers, and prevent themselves from applying the same log twice. 

This is good! We can't lose a single state machine operation now, and get into an inconsistent state! If a server crashes, or packets are dropped, the follower will simply re-receive the logs at a later point, when the network stabilizes or when the server reboots! Leader and follower agree on state `C`!

But alas, 

[grokking-raft-1]: /grokking-raft/
[raft-paper]:  https://raft.github.io/raft.pdf
