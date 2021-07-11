# Raft

I think it's good to start off by answering some basic questions like: 
- What is Raft? [Question]
- Why is it needed? One of the most important questions [Question]
- What problem does it solve? [Question]
- Are there no other things that solve the same problem? [Question]
- How is it different / novel from other alternatives if there are alternatives? [Question]
- How popular is it? Any reason for it's popularity? [Question]
- How technically sound is it? [Question]

---

I just read the `What is Raft?` , `Hold on—what is consensus?` in https://raft.github.io/

I also tried out the `Raft Visualization` in https://raft.github.io/ It was interesting to note that there are a lot of interactive elements!! I had used it for moment or so long ago and forgot that some things can be interacted with.

I was able to interact with the servers themselves - I could click on the server and stop it. I noticed other commands on the server like - resume, restart, timeout and request. I'm yet to try those out. I tried only one thing - stopping a server

I also noticed that the timeline is super cool - I could pause and play. I was able to hover over it to understand what it is with the tool tip text. I also noticed that the visualization remembers when I stopped a server. So if I go back in time, it shows that the server is up and running and then when I go forward passing the time when I stopped it, it shows the server is stopped. I could time travel ! :D I could also see the elements of the visualization going backwards / opposite direction in movement when going back in time and proper direction when going forward in time

I also noticed that the Simulation speed is very very cool!! :D I realized that the speed was based on some timing. I'm guessing 1x or 1/1x as it shows means that - in real time if 1 second has passed, even in the simulation 1 second has passed. But if I choose 1/1000x then I guess it means that if 1 second has passed in real time, then only 0.001 second has passed in simulation, as we have decreased the speed of the simulation to 1/1000th of the real time. Also, everything is functioning and running only when the timeline is on play and not on pause. I also noticed that I could change the simulation speed even if the timeline is on play and it was interesting to change the value all in real time without having to pause and stuff

The craziest thing I noticed was - I could click on the data sent between the servers. The RequestVote request and reply packet, AppendEntries request packet. Also, I just noticed that I could drop the packet / data to simulate packet drops. Wow. Just wow!

I noticed that I can't interact with the packets if the simulation is playing - even if it's too slow. Only after pausing I was able to interact with it

I enjoyed trying out the simulation trying to figure out what's going and guess based on some previous little knowledge to make sense of the simulation

Something I quickly realized was how I can't truly or entirely trust visualizations including this one - because it's still a copy or implementation of the Raft consensus algorithm defined in the research paper. It's possible that the visualization has bugs and hence shows buggy things at times in some cases - edge cases etc, and if I trust it and try to make sense of it - that's just crazy - because then I would be believing even the errors in the visualization and thinking what's going on and trying to make sense of how Raft works entirely based on that, which doesn't seem logical

The website also mentions that the visualization is not perfect by saying

> This visualization (RaftScope) is still pretty rough around the edges; pull requests would be very welcome. 

So yeah, I guess the research paper is a better way to learn and start from instead of me decrypting the visualization 😅 🙈

Also, there are more visualizations which I can use to play with later after reading the research paper. For example the site mentions another one here -

http://thesecretlivesofdata.com/raft/

The research paper link - https://raft.github.io/raft.pdf

So, the research paper is published by two people - Diego Ongaro and John Ousterhout

I see that there are many talks also by the two creators in `Talks` section

Also, there seems to be many related research papers in the `Publications` section

I can also see a reference to something called as the dissertation. It's mentioned as `Diego Ongaro's Ph.D. dissertation` - https://github.com/ongardie/dissertation#readme

I can also see many references to courses that teach Raft and also have assignments for Raft in `Courses teaching Raft` section! Cool stuff!

There's also a common Raft Google Group! https://groups.google.com/g/raft-dev

Apparently there are some implementation specific forums too that I can find only in those specific projects, makes sense

And then finally I see a lot of Raft implementations that people have published here - https://raft.github.io/#implementations . Who knows, there might be more but not updated in this list. Anyways, this is still a lot and a good list! :D

As part of the implementations I also see what features the implementations have. Hmm

- Leader Election + Log Replication
- Persistence
- Membership Changes
- Log Compaction

I'm wondering what each means. [Question] I can guess what it might be basically. For example -

Leader Election is about electing a leader among the nodes? [Question]

Log replication is the replication of logs? [Question] Logs which contains a sequence of commands which are inputs to the state machine as mentioned previously in the website

Persistence is about persisting state on disk? [Question] State of state machine? 🤔 [Question]

Membership Changes is about membership changing? [Question] New members coming up, existing members going away? [Question]

Log Compaction is about compacting logs? Compacting as in? [Question] Compressing like zip, tar etc? Or taking all the commands and compacting intelligently? Like, if the logs say initially the value of X is 5, then it's 10, then it's 20, and finally it's 30, if the Log has all the values, and if it's passed to the state machine - I guess finally however the state machine is going to have the value of X as 20. So, one could compact all those logs of multiple values of X into one log? One log which contains X is 20? I don't know, just guessing as of now [Question]

Also, I'm wondering why Leader Election + Log Replication are put together in the same column, hmm [Question]

I guess these are good questions to ask. I'll probably revisit these when I'm done reading the research paper and understanding some of these or all of these :D

I also realized I actually have more questions now, which need answering. For example, the "What is Raft?" para says this -

```
Raft is a consensus algorithm that is designed to be easy to understand. It's equivalent to Paxos in fault-tolerance and performance. The difference is that it's decomposed into relatively independent subproblems, and it cleanly addresses all major pieces needed for practical systems. We hope Raft will make consensus available to a wider audience, and that this wider audience will be able to develop a variety of higher quality consensus-based systems than are available today. 
```

I'm going to tag my questions with `[Question]` so that I can search later. I could use `?` to search too, still, because I used `?` too much in other places too and also, sometimes I don't use `?` but just say I'm guessing or I'm wondering, where it's actually a question. So, to revisit, I think both `?` and `[Question]` will help :)

Some more questions from the above para about what's Raft -

- `Raft is a consensus algorithm`, is there a formal definition for what's a consensus algorithm? Like, what's the problem statement and what's expected of the solution? Considering Raft is a particular solution / implementation [Question]

- `that is designed to be easy to understand` - How did they come to the conclusion that it's easy to understand? Given easy and hard are subjective. Also, how do they know that the design is easy to understand, how did they even approach the problem with design, specifically easy to understand design as the main goal? Like, are there some designs that are easy to understand? Did they just go ahead and use that, like, use some existing approach? How did the authors think about the solution? 🤔 [Question] [Answered]

- `It's equivalent to Paxos in fault-tolerance and performance.` - How do they say this statement? Are there some sort of numbers to prove this? Numbers that denote fault-tolerance and performance for both Paxos and Raft and show that they are the same? Does the Raft paper prove this? Or this is just a general statement? Also, if there are numbers, what exactly do they denote under fault-tolerance and performance? As those are very generic, for example performance can mean "very fast" but uses more resources, or "very fast" but uses less resources comparatively, "uses less disk space" etc. Also, what do they mean by fault-tolerance? Like, what kind of faults / issues can it tolerate? Nodes going down? Network issues? [Question]

- What is Paxos? I have heard it's also a consensus algorithm and that it's hard to understand. But, what is it? Like, under the hood what does it do? When did it come out (paper publish date)? What systems use it today? [Question]

- How are Paxos and Raft different? Does it make sense to compare them like apples to apples comparison? Assuming they are both in the consensus algorithms domain and can be compared, or they both have different goals, different ideologies, designed with different things in mind etc and it doesn't make sense to compare them? [Question]

- Are there other consensus algorithms other than Paxos and Raft? [Question] Algorithms that came way before or algorithms that are recent, that came after Paxos and Raft. [Question]

- `The difference is that it's decomposed into relatively independent subproblems, and it cleanly addresses all major pieces needed for practical systems.` - How is Raft decomposed into relatively independent subproblems compared to Paxos? Does this mean that Paxos was more of a monolith or very tightly coupled with different subsystems solving different subproblems and was more dependent on each other? How does Raft address `major pieces`? What are these `major pieces`? And why are they `major`? Are there other `minor` pieces? or trivial pieces? And it says `for practical systems` - what does that mean? `practical`? Does Raft paper mention anything about it? [Question]

I also had questions about the "Hold on - what is consensus?" para, it says

```
Consensus is a fundamental problem in fault-tolerant distributed systems. Consensus involves multiple servers agreeing on values. Once they reach a decision on a value, that decision is final. Typical consensus algorithms make progress when any majority of their servers is available; for example, a cluster of 5 servers can continue to operate even if 2 servers fail. If more servers fail, they stop making progress (but will never return an incorrect result).

Consensus typically arises in the context of replicated state machines, a general approach to building fault-tolerant systems. Each server has a state machine and a log. The state machine is the component that we want to make fault-tolerant, such as a hash table. It will appear to clients that they are interacting with a single, reliable state machine, even if a minority of the servers in the cluster fail. Each state machine takes as input commands from its log. In our hash table example, the log would include commands like set x to 3. A consensus algorithm is used to agree on the commands in the servers' logs. The consensus algorithm must ensure that if any state machine applies set x to 3 as the nth command, no other state machine will ever apply a different nth command. As a result, each state machine processes the same series of commands and thus produces the same series of results and arrives at the same series of states. 
```

- `fault-tolerant distributed systems` - what kind of faults does it refer to and tolerate? I had asked a similar question before too. So, is it like nodes going down? Network issues (delay, connectivity issues etc)? [Question]

- `Consensus involves multiple servers agreeing on values` - what values are these? I mean, does Raft define what kind of value this is? Is this value used by the system that uses Raft? For example, if etcd uses Raft, then there does it refer to a key-value pair? Or just a value maybe? Are there any constraints from Raft about what this value must be or what kind of characteristics or attributes it must have? [Question]

- `Once they reach a decision on a value, that decision is final` - Reach a decision as in reach a consensus? And how does it ensure the part about `decision is final` and what does that mean? [Question]

- `Typical consensus algorithms make progress when any majority of their servers is available; for example, a cluster of 5 servers can continue to operate even if 2 servers fail. If more servers fail, they stop making progress (but will never return an incorrect result).` - So, the majority is calculated by (N/2) + 1 ? Where N is the number of servers and (N/2) is an integer and not a floating point (with decimal points and values after decimal point other than 0) number? Also, it says if more servers fail - that is, when majority is not available, they stop making progress but that they will never return an incorrect result - does this mean that Raft values correctness over making progress and being available? More like consistency and correctness over availability, is it? Thinking about CAP theorem that is, which I don't know too much about though [Question]

- `Consensus typically arises in the context of replicated state machines, a general approach to building fault-tolerant systems` - what are replicated state machines? and are there other approaches to build fault-tolerant systems? And why and how does consensus typically arise in the context of replicated state machines? [Question]

- `Each server has a state machine and a log` - state machine meaning? Something that has a state and can have different states / change states? Log? Is it a WAL - Write Ahead Log? Does Raft define how should a state machine be? Or should a log be? Like, any constraints or characteristics or attributes around them? [Question]

- `The state machine is the component that we want to make fault-tolerant, such as a hash table` - what does making the state machine fault tolerant mean? [Question]

- `It will appear to clients that they are interacting with a single, reliable state machine, even if a minority of the servers in the cluster fail` - so, the cluster of servers appear as a single system for the client? How? Does the client know how to connect to just one host and assume there's just one server / system? It says `reliable` - how reliable? And it says `even if a minority of the servers in the cluster fail` - so, does it mean that it's fault tolerant because it is able to tolerate the failure / fault of a minority of servers? [Question]

- `Each state machine takes as input commands from its log. In our hash table example, the log would include commands like set x to 3`. Is it like, state machine takes input / input commands from it's log and then moves to a new state as output? 🤔 And the state machine and log can depend on the system using Raft? Like, it can state machine can do any kind of thing? Same for log - it can store any kind of thing? Depending on the system using Raft? So, in this case / example, a hash table, so log includes hash table related commands? Like get, set etc? And state machine would be the hash table itself? As mentioned in `The state machine is the component that we want to make fault-tolerant, such as a hash table`

- `A consensus algorithm is used to agree on the commands in the servers' logs`. Okay, so, in the example of a hash table log, every server has to agree to a log like `set x to 3` ?

- `The consensus algorithm must ensure that if any state machine applies set x to 3 as the nth command, no other state machine will ever apply a different nth command` - So, when does the applying of commands from logs happen? Do different state machines apply the log at different times / can apply at different times? Assuming that it's already decided (decision) based on consensus what the nth command in the log will be

- Is the consensus a blocking operation? Like, when a client tries to set a value to V, then, does Raft mention to append to the log this operation? And then tries to have a consensus among the servers? And when does state machine / raft, reply / respond to the client? It's the state machine that replies, right? Since Raft is only for consensus, and state machine is doing the job that the client wants. Does the state machine reply after consensus on the log, and applying the log to the state machine and changing the state? What about waiting for other state machines to apply the log? Hmm, maybe it's not needed? Also, considering all this, something to think about it, how is the performance of the state machine in case of too many servers being involved - to come to consensus and also how state machine performs in a write heavy client compared to a read heavy client, or let's say lot of requests - since all requests / commands become logs, right? But, does read and write require consensus? Also, what happens if the command / request / operation requested by the client is an invalid one? Does it still go to the log and state machine processes the command from the log and replies to the client that it's wrong? Hmm. And does the log with invalid command get replicated to all state machines? Hmm [Question]

`As a result, each state machine processes the same series of commands and thus produces the same series of results and arrives at the same series of states.` - Makes sense! I guess, this is assuming that the cluster of state machines are the same program - like, same version of the program, which behave the same way given an input and produce the same output. Also, I'm assuming this is more like a pure function - given an input, it always returns the same output, regardless of what time etc and is not affected by any other external thing, and just works on the input

---

I'm wondering if I should see some videos / talks from the web page before reading the paper, hmm. Like, if it will be a good introduction instead of jumping into the research paper directly, hmm

Like, some talk from the creators themselves?

---

Also, some extra questions that I had in mind based on the visualizations

Questions
- how does leader election work? [Question]
- if there are five nodes and one node is dead, and two nodes are candidates in an election in a term. If other two nodes vote for the same one node, will that node become leader? Given the 3 votes - from itself, from other two nodes [Question]
- is it possible that no leader gets elected in a term? [Question]
- is it possible that no leader gets elected ever at some point? [Question]
- when can leader election always fail for sure? Like, a leader is never elected at all, any time. Is that possible? [Question]

---

I'm watching this talk now - https://www.youtube.com/watch?v=vYp4LYbnnW8 It's just wow! It shows a bit about the history of how Raft came to be, and what was in the minds of the creators while designing Raft. It also kind of answers some of the questions I had. For example, to answer the question of - easy to understand

---

[Question-And-Answer]

`that is designed to be easy to understand` - How did they come to the conclusion that it's easy to understand? Given easy and hard are subjective. Also, how do they know that the design is easy to understand, how did they even approach the problem with design, specifically easy to understand design as the main goal? Like, are there some designs that are easy to understand? Did they just go ahead and use that, like, use some existing approach? How did the authors think about the solution? 🤔

[Answer]

The creators did a user study it seems. I'm yet to watch the section in this video https://www.youtube.com/watch?v=vYp4LYbnnW8 . I did notice two user studies here - 

Paxos Lecture (Raft user study) - https://www.youtube.com/watch?v=JEpsBg0AO6o

Raft Lecture (Raft user study) - https://www.youtube.com/watch?v=YbZ3zDzDnrw

I have to check those and check what they exactly did. From the initial parts of https://www.youtube.com/watch?v=vYp4LYbnnW8 - it was mentioned that the user study confirmed that Raft was easier to understand than Paxos

Apart from this, the author Professor John Ousterhout also talks about other things that they did to ensure that Raft is easy to understand - for example, things like minimal state space - he mentioned it's like less if statements in a program

`minimal state space` - does it mean less number of possible states in a state machine? [Question]

The whole design started with the main goal of understandability, as Paxos was hard to understand and Professor John Ousterhout had a hard time wrapping his head around it. It seems he understood it really well only after designing Raft. So, he had to build a whole new consensus algorithm to understand it. He also mentioned how he believed Paxos after reading the proof of correctness and understood that it works but couldn't understand how it works and also couldn't get an intuitive idea of how it works

Raft is also easy to understand because it tries to use lesser things to solve more. For example, a single mechanism to solve multiple problems. How does this show up in the Raft design? For example, the AppendEntries Remote Procedure Call (RPC) is used by the leader to append log entries in other machines to replicate logs AND it is also used by the leader to send heart beats to other machines by using the same AppendEntries RPC but with no log in it, so, more like an empty message / empty thing, for using it as a heart beat. See? AppendEntries is a mechanism that solves two problems - log replication AND heartbeat :)

Raft is also designed in such a way that there are no special cases. Common cases should take care of stuff - all stuff. Interesting thing!

There's also a mention about maximizing coherence and minimizing non-determinism. This is something I need to read about. The talk mentions that it's not possible to completely eliminate non-determinism, why? [Question]

Also, there are less things for people to understand I guess. In terms of Server states - there's only 3 of them - follower, candidate and leader

There are only two RPCs in Raft - RequestVote and AppendEntries, that's all. And like simple procedures / functions which have input and output, or like HTTP with request and response, in RPCs there's request and response (or reply) and both of the RequestVote and AppendEntries RPCs have those

---

The talk "Designing for Understandability: The Raft Consensus Algorithm" by John Ousterhout https://www.youtube.com/watch?v=vYp4LYbnnW8 was part of the " CS @ ILLINOIS Distinguished Lecture Series" - https://cs.illinois.edu/news/distinguished-lecture-series-dr-john-ousterhout

https://cs.illinois.edu/news/featured-lectures#dls

https://web.stanford.edu/~ouster/

RaftScope - https://raft.github.io/raftscope/index.html

PDF for the talk - https://raft.github.io/slides/uiuc2016.pdf

---

Resources:
- https://www.youtube.com/results?search_query=Raft+distributed+systems


