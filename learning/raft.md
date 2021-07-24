# Raft

I think it's good to start off by answering some basic questions like: 
- What is Raft? [Question]
- Why is Raft needed? One of the most important questions [Question]
- What problem does it solve? [Question]
- Are there no other things that solve the same problem? [Question]
- How is it different / novel from other alternatives if there are alternatives? [Question]
- How popular is it? Any reason for it's popularity? [Question]
- How technically sound is it? [Question]

---

I just read the `What is Raft?` , `Hold on—what is consensus?` sections in https://raft.github.io/

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
- is it possible that no leader gets elected in a term? [Question] [Answered]
- is it possible that no leader gets elected ever at some point? [Question] [Answered]
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

[Question-And-Answer]

is it possible that no leader gets elected in a term?

[Answer]

After going through the talk https://www.youtube.com/watch?v=vYp4LYbnnW8, yes, it is possible no leader gets elected in a term. It is possible when there's a "split-vote" situation where the candidates get equal number of votes and not a majority and none of them become a leader. So, in such cases, the servers just wait for their timeouts and since there's no leader, they don't get heartbeats so they will timeout. So, whichever server times out will then again increment it's term and request for votes. Usually only one times out first and will get all the votes before others timeout and it will become the leader

---

[Question-And-Answer]

is it possible that no leader gets elected ever at some point?

[Answer]

After going through the talk https://www.youtube.com/watch?v=vYp4LYbnnW8, no, it's not possible. The Raft algorithm suggests some ways to avoid this, so if that's followed, meaning if Raft algorithm is properly followed, no, it's not possible that no leader gets elected ever at some point. Raft algorithm ensures safety AND liveness

Safety - atmost only one leader gets elected in a single term. "Atmost one" means - 0 or 1. So yeah, there can be no leaders in a term as answered in `is it possible that no leader gets elected in a term?` question, but there cannot be more than 1

Liveness - the cluster progresses - one of the servers get elected as a leader at some point

For a leader to surely get elected, the algorithm suggests to use random timeout times for each of the servers. A random value between the same range for all servers, like [T, 2T], for example [150ms, 300ms], and choose timeouts from this range for all the servers. This way, not all will timeout at the same time, instead some will timeout earlier than the others and mostly one will timeout first - assuming each has a different random timeout - because we don't want servers to timeout at the same time and send requests for votes

Also another thing mentioned in the talk and in the algorithm was how it is important for the broadcast time to be way less than time T - the start of the timeout range for choosing a random value. The reason for this is that - it's expected for a server to timeout first and when it times out, it will try to send request for votes to all the servers using a broadcast and it's expected that the other servers are still waiting for their timeouts while they reply to the voting request and vote for the server that timed out first. This way the server that timed out first will become leader before the other servers even time out

Also, apparently this random time out value method was chosen as an easier and simpler and understandable alternative to some sort of ranking method to rank servers. It seems that was more complex and had many special cases - basically many `if`s and also more state space, and then they stumbled upon the random timeout value idea and felt that it was way simpler and solved problems

---

I had this other question before too but didn't note it down and assumed it might be solved in some way or the other

[Question-And-Answer]

The servers tend to simply vote for whoever sends a voting request to them. I noticed in the visualization that the servers vote for one and then deny votes for the others, how is this happening?

[Answer]

From the talk https://www.youtube.com/watch?v=vYp4LYbnnW8 , it is very important that a follower votes only for one candidate in a given term or else it affects the safety feature of the leader election where atmost only one leader can be elected - and a candidate will assume it's leader when it gets majority of votes. If followers grant vote for multiple candidates in a given term, then it's possible that many candidates think they got majority of votes and will think they have become leader. It's just a problematic thing completely basically. So, to avoid any such problems where a follower grants vote for different candidates in a given term, it's advised that the follower persit their vote so that even if they crash, when they come back, they know they voted in a given term

[Guess] [Question] I'm assuming that the follower server will first persist their vote on disk and then reply to a candidate's request that they grant their vote. This way, there's no possibility of losing the persisted data. I think that if the follower replied to the candidate's request first with their vote and then tried to persist their reply, then it's possible that in some weird case - the follower could crash right after replying but before persisting their reply to the disk. That can be problematic because now follower would have voted but didn't persist it and when it crashes and comes back, the follower will think it didn't vote for the given term because there's no persisted data and will vote for any request vote messages it gets from other candidates and grant them vote, which means multiple votes by a single follower in a given term - that's a problem! So, it's more like -

Assuming the follower hasn't voted yet in the given term, if the algorithm is -

- Receive vote request
- Reply to vote request and grant vote
- Persist the grant vote data to disk

Then the following things can happen, where a crash can happen before or after any step -

Situation 1
- Receive vote request
- Crash

Now, here the crash happened even before replying. It's okay I guess? It's like the server didn't exist before the vote or just during it, doesn't make much of a difference, since it couldn't reply

Situation 2 - a problematic situation
- Receive vote request
- Reply to vote request and grant vote
- Crash

Now, here the crash happened after replying. But it never persisted the grant vote data to the disk. Next time if it comes back alive, since there's no data on disk, according the follower, it never voted in the given term. This is a problematic situation!! As it can affect the safety feature of the Raft's leader election algorithm. In this situation, the follower could grant votes to multiple candidates in the same term because of this crash and no persistence of the grant vote reply. Also, there could also be multiple crashes - a crash after every reply to grant vote without persisting, that can be a lot of votes to a lot of candidates in a given term!

Situation 3
- Receive vote request
- Reply to vote request and grant vote
- Persist the grant vote data to disk
- Crash

This is okay. It crashed after replying and persisting. Since it persisted the data, it doesn't affect safety feature of leader election

Situation 3
- Crash

This is okay too I guess, it doesn't affect safety feature of leader election. The follower crashes before even receiving the vote request

Assuming the follower hasn't voted yet in the given term, I think the following is a better algorithm -

- Receive vote request
- Persist the grant vote data to disk. The data that the follower is going to reply with
- Reply to vote request and grant vote

Then the following things can happen, where a crash can happen before or after any step -

Situation 1
- Receive vote request
- Crash

Now, here the crash happened even before replying. It's okay I guess? It's like the server didn't exist before the vote or just during it, doesn't make much of a difference, since it couldn't reply

Situation 2
- Receive vote request
- Persist the grant vote data to disk. The data that the follower is going to reply with
- Crash

This is okay I guess? I mean, the follower didn't respond to the request and crashed before it could respond. It did persist it though - about what it's going to respond with. Can this be problematic though? Like, if the follower receives any other vote request for the same, after it comes back alive, it will think it replied to the previous request and deny votes. Is that okay? [Question] I guess it's okay? It's almost as if the follower's crash for a small period of time during the leader election affected the election - as if the the follower didn't take part in it at all - since it didn't grant vote to any candidate even if it receives requests - almost as good as follower being in crashed state the whole time and not replying / granting vote to any candidate. Probably if no leader got elected, then in the next term one could get elected. This doesn't affect the safety feature I guess as I don't see the follower voting for multiple candidates in a given term [Question] [Guess]

Situation 3
- Receive vote request
- Persist the grant vote data to disk. The data that the follower is going to reply with
- Reply to vote request and grant vote
- Crash

This is okay too. I mean, the crash happens after persisting and voting for a candidate. So, not a problem. Nothing affecting the safety feature of leader election

Situation 4
- Crash

Again, it's okay - it doesn't affect the safety feature of leader election

---

[Guess] [Question] Also, I'm assuming that the follower simply has to store the following data before replying to the request vote message -

- Term of Vote
- Voted For

[Guess] [Question] Assuming that this entry in the disk simply means they have already voted, so no need for another field like "voted?", and I don't think the follower has to remember the votes it denied or didn't vote. Also, maybe, if the leader for the term is elected, I guess this data for the particular term can be removed from the disk

[Guess] [Question] I'm also assuming that when a follower gets a vote request, it will first check the disk and see if it has voted for the given term and then, if has voted already, deny it, and if it hasn't voted already, persist to disk and then reply to the vote

---

[Question] Is it possible that in a given term a candidate sends multiple vote requests to the same candidate? Or it's only once? If it's multiple, is it okay? Can it happen? Or it should never happen and it's a problem? Also, if multiple vote requests come from the same candidate - is it more of a multiple broadcast and hence multiple vote requests from the same candidate to other servers in a given term? Also, if multiple is possible / is okay, so, servers need to remember who they voted for apart from the term they voted in by persisting it and vote for the same candidate if they send the vote request again for the same term?

---

I'm reading the research paper now. I plan to read each line and understand what it means or ask questions which I can answer later

The paper starts with

```
Raft is a consensus algorithm for managing a replicated log
```

Looks like the main feature of Raft is - a consensus algorithm for managing a replicated log. Note how it talks about the replicated log. I think the leader election and leader concept is just to maintain one perfect log - as the algorithm ensures that the leader's log is perfect - this is from the talk - https://www.youtube.com/watch?v=vYp4LYbnnW8

I was skimming through a bit about consensus algorithm in wikipedia

https://duckduckgo.com/?t=ffab&q=consensus+algorithm&ia=web

https://en.wikipedia.org/wiki/Consensus_(computer_science)

It was a very formal definition and a bit vague too for me. Maybe I'll come back and read again later

Moving on

```
It produces a result equivalent to (multi-)Paxos, and it is as efficient as Paxos, but its structure is different from Paxos; this makes Raft more understandable than Paxos and also provides a better foundation for building practical systems
```

Looks like there's something called as the `multi-Paxos` and Raft's result is equivalent to the result of `multi-Paxos`. What's `multi-Paxos` at a high level and what kind of result does it produce? [Question]

And it's as efficient as Paxos - what does this mean - what kind of efficiency? What kind of performance / efficiency numbers is it talking about over here? [Question]

Raft's structure is different frmo Paxos - hmm. I think this was mentioned in the talk too - how Raft is decomposed into sub problems - https://www.youtube.com/watch?v=vYp4LYbnnW8 - mostly relatively independent sub problems

The structure of Raft `makes Raft more understandable than Paxos` it seems. And it `also provides a better foundation for building practical systems` - why is that, does Paxos not help with building practical systems? And practical systems? What does that mean? Real world systems? [Question] I think I had similar question before too, hmm

```
In order to enhance understandability, Raft separates the key elements of consensus, such as leader election, log replication, and safety, and it enforces a stronger degree of coherency to reduce the number of states that must be considered.
```

Okay, so, we see the key elements of Consensus, or is it key elements of Raft? Is it generic here? or should it be specific and say "key elements of Raft"?

Key elements being - leader election and log replication and also safety. So, that's how the sub problems are divided - the sub problems are all key elements I guess

What happened to log compaction? membership changes? persistence? [Question]

And yeah, to make things easier to understand, there are less states in Raft algorithm. Like, for example in server states - there's only three states - follower, candidate and leader

```
 Results from a user study demonstrate that Raft is easier for students to learn than Paxos.
```

Yup, I noticed this from the talk https://www.youtube.com/watch?v=vYp4LYbnnW8 . I'm yet to see the user study and details around the results. It does sound like an interesting thing. Funny thing is, the Paxos and Raft course - both was taught by John Ousterhout, the co-author of Raft :P In the talk https://www.youtube.com/watch?v=vYp4LYbnnW8 , one of the students asks "Didn't you say you didn't understand Paxos?" :P I think he did understand it a lot / enough, and completely after building Raft, like he mentioned in the talk

```
Raft also includes a new mechanism for changing the cluster membership, which uses overlapping majori- ties to guarantee safety.
```

Why do they refer to it as `a new mechanism` ? [Question]

Also, how do the cluster membership changes happen? A server just goes away? Is it like shutdown server and done? And then like, bring up new servers and start them off. Also, how does it smoothly happen, like no issues, no downtime etc. Also, what are the scenarios when you would need it. I mean, is it more like - some old servers are not there (removed) and/ not functioning will be removed from the cluster membership and list of cluster members? Or is it about servers that do exist and work well but later can become unhealthy and others get to know about this server not working / being unhealthy but it is not removed from the cluster and is shown as part of the members but as an unhealthy member. Is that how it is?

Also, does cluster membership help with maintenance works? Like, some server needs to be taken for maintenance - upgrade OS etc [Question]

And in what cases would new members be added? To replace older members for some reason? To scale? But Raft has bottlenecks with more servers, right? I mean, if there are more servers, all servers must spend more time sending broadcasts and do what not - especially when they are leaders [Question]

And what does `overlapping majorities` mean? How does using `overlapping majorities` `guarantee safety`? 🤔 [Question]

---

I have been reading more of the paper, this time lessening the questions and just trying to read and understand and create an idea of some things in my mind and also try to understand what happens if something happens differently

---

[Question] Let's say if the leader gets a command from a client, and if it appends the command to it's log for durability and then it gives the command to it's state machine as input to produce output and state, but without replicating the log, specifically without replicating the log containing that command. Now, what's the problem in this? Also let's say that the leader has replied to the client that the command was accepted and the execution was successful. Now what? I'm assuming it's a problem because - now, if the leader crashes - losing log information or it's state machine output and state or a combination of these, then things go horribly wrong. Especially when the log is lost - then it's bad - because the log is meant to be the most important thing as it's meant to help with durability. Also, if the log is not replicated to other servers, and if the leader loses network connection or crashes, then when other servers become leaders / if they become leaders, then when the clients interact with them, the clients will assume that it's previous commands were successfully executed - this is based on the client's assumption that it's all a single system and not multiple servers - the distributed system is supposed to act as a single system and coordinate and cooperate and work together as a single unit - at least that's the definition and meaning I remember from college. So, here, the new leaders would not have executed the previous commands of the client, especially the ones whose logs weren't replicated by the previous leader, which is a blunder mistake. So, is this why it's recommended to ensure that a majority of servers have replicated the command log before the leader executes the command in it's state machine? This part of the algorithm was mentioned in the talk https://www.youtube.com/watch?v=vYp4LYbnnW8 If it's present in the majority of the servers then even if the leader crashes, the other servers still have the command in their logs and will eventually process it with their state machine to get series of outputs and states similar to that of the leader. As part of the talk https://www.youtube.com/watch?v=vYp4LYbnnW8 , it was also mentioned that it's a bit of a tricky thing to replicate the leader's log - the command from the client in majority of servers. It wasn't exactly called out as tricky, instead a student asked a question about it and the answer seemed tricky to me. Why is it tricky? Well, when a client sends a command and the leader is busy trying to persist the command to it's log and also replicating the log with the command to a majority of servers and then only applying the command to it's state machine and then finally replying to the client, the client can be waiting for a long time. The response time can be high. Not to mention, if there are more and more servers in the cluster, the majority number is going to be high, which is (N/2) + 1 and hence there will be more majority servers to replicate the log to and hence that could take more time, and only after replication the leader is going to apply the command to the state machine and then reply. So, of course this replication can be tricky and time consuming

One of the things that John Ousterhout mentions in the talk https://www.youtube.com/watch?v=vYp4LYbnnW8 is that - it's better to keep the cluster smaller in size and if more servers are needed, then have a cluster of cluster of servers, something like that. How does that work? I'm not sure [Question]

---

Recently I was reading and sometimes skimming through a lot of the sections of the Raft paper

Now I'm at Section 8 - which I have completed reading

One of the questions I had was - around read-only requests returning stale data - how is this possible? And why is it that we are considering only read-only requests when it comes to stale data? What about write operations going wrong? I'm using the word `requests` and `operations` interchangeably here [Question]

---

I'm currently at section 9. Apparently the researchers have implemented Raft with C++ for their service and it's freely available!! :D

LogCabin source code - https://github.com/logcabin/logcabin

And of course there are many other implementations mentioned in https://raft.github.io/ , previously http://raftconsensus.github.io

So, in this section we are looking at implementation and evaluation as the name of the section suggests. There are criterias for evaluation, interesting

For some weird reason the user study materials weren't available in the link provided in the paper -

http://ramcloud.stanford.edu/~ongaro/userstudy/

But I got it here

https://ongardie.net/static/raft/userstudy/ through https://duckduckgo.com/?t=ffab&q=raft+user+study&ia=web

I might take the quizzes at some point ;) After checking out the videos :D At least the Raft one, if not Paxos one

https://ongardie.net/static/raft/userstudy/quizzes.html

There's also this answers / guide to check the answers -

https://ongardie.net/static/raft/userstudy/rubric.pdf

https://ongardie.net/

Next there's mention of Correctness and Proof

It talks about TLA+ which I haven't used but I have kind of heard of it before I think. A system to prove stuff or something like that

https://duckduckgo.com/?t=ffab&q=TLA+specification&ia=web

https://www.learntla.com/introduction/ , https://www.learntla.com/book/

https://en.wikipedia.org/wiki/TLA%2B

Okay, so it's a formal specification language. The full form is "Temporal Logic of Actions", nice name!

Apparently there's the TLA+ code, not sure where, I couldn't exactly find it in the dissertation

"ONGARO, D. Consensus: Bridging Theory and Practice. PhD thesis, Stanford University, 2014"

https://github.com/ongardie/dissertation

I'm moving on to Performance for now

Wow, there was a lot of information in Performance section but I couldn't grasp it well. The explanation and especially the graph was hard to make sense. I think I'll have to spend more time later on this and read this again in a second parse later



---

Resources:
- https://www.youtube.com/results?search_query=Raft+distributed+systems


