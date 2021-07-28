Based on my plan, I started reading

https://eli.thegreenplace.net/2020/implementing-raft-part-0-introduction/

and the first thing it said was

> I assume you've read the Raft paper at least once; in addition it's highly recommended to spend some time perusing the resources on the Raft website - watch a talk or two by its creators, play with the visualization, skim Ongaro's PhD thesis for more details, etc.

So...I guess it makes sense, because the post is named as "implementation"

So I'm going to read the Raft research paper once at least :)

https://raft.github.io/raft.pdf

Long ago a colleague (https://github.com/dineshba) tried to explain it in a session in two parts. But it was long ago and I don't remember much now. So I guess it's gonna be a fresh start ;)

---

I started reading the first part - the introduction

https://eli.thegreenplace.net/2020/implementing-raft-part-0-introduction/

Was reading a bit of CAP theorem too which I found linked to in the introduction post

https://en.wikipedia.org/wiki/CAP_theorem

Another interesting link that I found on the way in the introduction post

https://eli.thegreenplace.net/2018/go-hits-the-concurrency-nail-right-on-the-head/

I'm reading it now - https://eli.thegreenplace.net/2018/go-hits-the-concurrency-nail-right-on-the-head/

Looks like the author is making a BIG case for Golang by comparing with other languages and from the words of other people. For a moment I was thinking if the author is biased because I found out they are from Google, the company behind Go language . https://github.com/eliben says they are in Google. So yeah, for now I'm just going to assume that they are telling the truth based on their experience and that Go language is pretty suitable. Not to mention even I'm biased to Go language - probably due to the hype and also some experience with it - most of the experience has been good, except for a few annoying Go dependency management, Go modules craziness and stupidity, and also the fact that I write tons of code in Golang, but usually I'm okay with it but people mention how other languages are so concise and have a very rich standard library that provides a lot of things. I guess Go language is simple, and hence provides just what is necessary in terms of power and simplicity, and then leaves the rest to developers I think. Not to mention the cool cross compilation and of course the single static binary with ease, I love it! :)

Moving on, I'm going to read https://eli.thegreenplace.net/2020/implementing-raft-part-1-elections/

So, I have cloned the code

```bash
$ mkdir eliben
$ cd eliben
$ git clone git@github.com:eliben/raft.git
$ cd raft
$ git branch -a
$ git status
$ ls
LICENSE			part1			part3			tools
README.md		part2			raftlog-screenshot.png
```

There's some image and all, hmm. I saw the `raftlog-screenshot.png` and it shows how different servers get started and how the timer times out and how one of the servers become a leader. Interesting ! :) It also shows what's happening at each point like a timeline, hmm

Moving on, I'm going to checkout the code in `part1`

https://github.com/eliben/raft/tree/master/part1

I'm going to use Visual Studio Code (VSCode) for coding this system using Golang extension

```bash
code part1
```

Looks like this is only for leader election and there's no client interactions and hence no inputs / operations / requests from clients and hence nothing to log to the disk for persistence and durability, and since there's no logs, there's nothing to replicate for the leader. So no log replication

I read the whole of part1 checking out the code, it was mostly straight forward and simple - following a lot of things from the Raft paper of course

I also tried running one test by checking the repo README

```bash
$ code .

$ cd part1

$ go test -v -race -run TestElectionFollowerComesBack | tee /tmp/raftlog
=== RUN   TestElectionFollowerComesBack
10:02:26.890095 [0] listening at [::]:49678
10:02:26.890643 [1] listening at [::]:49679
10:02:26.890914 [2] listening at [::]:49680
10:02:26.902823 [2] election timer started (183ms), term=0
10:02:26.902827 [1] election timer started (251ms), term=0
10:02:26.902870 [0] election timer started (176ms), term=0
10:02:27.082983 [0] becomes Candidate (currentTerm=1); log=[]
10:02:27.083210 [0] sending RequestVote to 1: {Term:1 CandidateId:0 LastLogIndex:0 LastLogTerm:0}
10:02:27.083258 [0] election timer started (245ms), term=1
10:02:27.083227 [0] sending RequestVote to 2: {Term:1 CandidateId:0 LastLogIndex:0 LastLogTerm:0}
10:02:27.087799 [2] RequestVote: {Term:1 CandidateId:0 LastLogIndex:0 LastLogTerm:0} [currentTerm=0, votedFor=-1]
10:02:27.087821 [2] ... term out of date in RequestVote
10:02:27.087837 [2] becomes Follower with term=1; log=[]
10:02:27.087931 [2] ... RequestVote reply: &{Term:1 VoteGranted:true}
10:02:27.088010 [2] election timer started (290ms), term=1
10:02:27.088499 [0] received RequestVoteReply {Term:1 VoteGranted:true}
10:02:27.088521 [0] wins election with 2 votes
10:02:27.088537 [0] becomes Leader; term=1, log=[]
10:02:27.088625 [1] RequestVote: {Term:1 CandidateId:0 LastLogIndex:0 LastLogTerm:0} [currentTerm=0, votedFor=-1]
10:02:27.088644 [1] ... term out of date in RequestVote
10:02:27.088664 [1] becomes Follower with term=1; log=[]
10:02:27.088765 [1] ... RequestVote reply: &{Term:1 VoteGranted:true}
10:02:27.088771 [0] sending AppendEntries to 1: ni=0, args={Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.088814 [0] sending AppendEntries to 2: ni=0, args={Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.088894 [1] election timer started (262ms), term=1
10:02:27.089272 [0] received RequestVoteReply {Term:1 VoteGranted:true}
10:02:27.089297 [0] while waiting for reply, state = Leader
10:02:27.093332 [0] in election timer state=Leader, bailing out
10:02:27.093349 [2] AppendEntries: {Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.093356 [1] in election timer term changed from 0 to 1, bailing out
10:02:27.093376 [2] AppendEntries reply: {Term:1 Success:true}
10:02:27.093413 [1] AppendEntries: {Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.093436 [1] AppendEntries reply: {Term:1 Success:true}
10:02:27.093415 [2] in election timer term changed from 0 to 1, bailing out
10:02:27.139625 [0] sending AppendEntries to 1: ni=0, args={Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.139625 [0] sending AppendEntries to 2: ni=0, args={Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.146314 [2] AppendEntries: {Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.146341 [2] AppendEntries reply: {Term:1 Success:true}
10:02:27.146317 [1] AppendEntries: {Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.146436 [1] AppendEntries reply: {Term:1 Success:true}
10:02:27.188894 [0] sending AppendEntries to 1: ni=0, args={Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.188897 [0] sending AppendEntries to 2: ni=0, args={Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.193268 [2] AppendEntries: {Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.193307 [1] AppendEntries: {Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.193339 [1] AppendEntries reply: {Term:1 Success:true}
10:02:27.193309 [2] AppendEntries reply: {Term:1 Success:true}
10:02:27.204521 [TEST] Disconnect 1
10:02:27.238892 [0] sending AppendEntries to 1: ni=0, args={Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.238905 [0] sending AppendEntries to 2: ni=0, args={Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.240463 [2] AppendEntries: {Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.240494 [2] AppendEntries reply: {Term:1 Success:true}
10:02:27.289697 [0] sending AppendEntries to 1: ni=0, args={Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.289707 [0] sending AppendEntries to 2: ni=0, args={Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.293988 [2] AppendEntries: {Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.294013 [2] AppendEntries reply: {Term:1 Success:true}
10:02:27.340210 [0] sending AppendEntries to 1: ni=0, args={Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.340217 [0] sending AppendEntries to 2: ni=0, args={Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.345632 [2] AppendEntries: {Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.345684 [2] AppendEntries reply: {Term:1 Success:true}
10:02:27.389904 [0] sending AppendEntries to 2: ni=0, args={Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.389904 [0] sending AppendEntries to 1: ni=0, args={Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.395596 [2] AppendEntries: {Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.395665 [2] AppendEntries reply: {Term:1 Success:true}
10:02:27.438892 [0] sending AppendEntries to 1: ni=0, args={Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.438902 [0] sending AppendEntries to 2: ni=0, args={Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.441337 [2] AppendEntries: {Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.441362 [2] AppendEntries reply: {Term:1 Success:true}
10:02:27.459451 [1] becomes Candidate (currentTerm=2); log=[]
10:02:27.459818 [1] sending RequestVote to 0: {Term:2 CandidateId:1 LastLogIndex:0 LastLogTerm:0}
10:02:27.459857 [1] sending RequestVote to 2: {Term:2 CandidateId:1 LastLogIndex:0 LastLogTerm:0}
10:02:27.459919 [1] election timer started (226ms), term=2
10:02:27.489000 [0] sending AppendEntries to 2: ni=0, args={Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.489005 [0] sending AppendEntries to 1: ni=0, args={Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.490356 [2] AppendEntries: {Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.490386 [2] AppendEntries reply: {Term:1 Success:true}
10:02:27.538935 [0] sending AppendEntries to 1: ni=0, args={Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.538940 [0] sending AppendEntries to 2: ni=0, args={Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.541633 [2] AppendEntries: {Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.541671 [2] AppendEntries reply: {Term:1 Success:true}
10:02:27.590125 [0] sending AppendEntries to 1: ni=0, args={Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.590174 [0] sending AppendEntries to 2: ni=0, args={Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.594231 [2] AppendEntries: {Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.594267 [2] AppendEntries reply: {Term:1 Success:true}
10:02:27.638912 [0] sending AppendEntries to 1: ni=0, args={Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.638920 [0] sending AppendEntries to 2: ni=0, args={Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.640252 [2] AppendEntries: {Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.640280 [2] AppendEntries reply: {Term:1 Success:true}
10:02:27.690041 [1] becomes Candidate (currentTerm=3); log=[]
10:02:27.690179 [1] sending RequestVote to 0: {Term:3 CandidateId:1 LastLogIndex:0 LastLogTerm:0}
10:02:27.690229 [0] sending AppendEntries to 1: ni=0, args={Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.690232 [0] sending AppendEntries to 2: ni=0, args={Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.690287 [1] sending RequestVote to 2: {Term:3 CandidateId:1 LastLogIndex:0 LastLogTerm:0}
10:02:27.690320 [1] election timer started (174ms), term=3
10:02:27.695021 [2] AppendEntries: {Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.695056 [2] AppendEntries reply: {Term:1 Success:true}
10:02:27.739016 [0] sending AppendEntries to 2: ni=0, args={Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.739021 [0] sending AppendEntries to 1: ni=0, args={Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.745394 [2] AppendEntries: {Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.745431 [2] AppendEntries reply: {Term:1 Success:true}
10:02:27.788970 [0] sending AppendEntries to 1: ni=0, args={Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.788972 [0] sending AppendEntries to 2: ni=0, args={Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.794949 [2] AppendEntries: {Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.794984 [2] AppendEntries reply: {Term:1 Success:true}
10:02:27.839073 [0] sending AppendEntries to 2: ni=0, args={Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.839081 [0] sending AppendEntries to 1: ni=0, args={Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.841805 [2] AppendEntries: {Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.841846 [2] AppendEntries reply: {Term:1 Success:true}
10:02:27.855402 [TEST] Reconnect 1
10:02:27.870710 [1] becomes Candidate (currentTerm=4); log=[]
10:02:27.870881 [1] sending RequestVote to 0: {Term:4 CandidateId:1 LastLogIndex:0 LastLogTerm:0}
10:02:27.870951 [1] sending RequestVote to 2: {Term:4 CandidateId:1 LastLogIndex:0 LastLogTerm:0}
10:02:27.871042 [1] election timer started (187ms), term=4
10:02:27.874226 [0] RequestVote: {Term:4 CandidateId:1 LastLogIndex:0 LastLogTerm:0} [currentTerm=1, votedFor=0]
10:02:27.874228 [2] RequestVote: {Term:4 CandidateId:1 LastLogIndex:0 LastLogTerm:0} [currentTerm=1, votedFor=0]
10:02:27.874254 [0] ... term out of date in RequestVote
10:02:27.874277 [2] ... term out of date in RequestVote
10:02:27.874288 [0] becomes Follower with term=4; log=[]
10:02:27.874331 [2] becomes Follower with term=4; log=[]
10:02:27.874420 [0] ... RequestVote reply: &{Term:4 VoteGranted:true}
10:02:27.874463 [2] ... RequestVote reply: &{Term:4 VoteGranted:true}
10:02:27.874486 [0] election timer started (264ms), term=4
10:02:27.874571 [2] election timer started (238ms), term=4
10:02:27.874921 [1] received RequestVoteReply {Term:4 VoteGranted:true}
10:02:27.874947 [1] wins election with 2 votes
10:02:27.874966 [1] becomes Leader; term=4, log=[]
10:02:27.875145 [1] sending AppendEntries to 0: ni=0, args={Term:4 LeaderId:1 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.875165 [1] sending AppendEntries to 2: ni=0, args={Term:4 LeaderId:1 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.875242 [1] received RequestVoteReply {Term:4 VoteGranted:true}
10:02:27.875267 [1] while waiting for reply, state = Leader
10:02:27.878247 [2] in election timer term changed from 1 to 4, bailing out
10:02:27.878251 [0] AppendEntries: {Term:4 LeaderId:1 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.878327 [0] AppendEntries reply: {Term:4 Success:true}
10:02:27.881210 [1] in election timer state=Leader, bailing out
10:02:27.881219 [2] AppendEntries: {Term:4 LeaderId:1 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.881372 [2] AppendEntries reply: {Term:4 Success:true}
10:02:27.927120 [1] sending AppendEntries to 2: ni=0, args={Term:4 LeaderId:1 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.927121 [1] sending AppendEntries to 0: ni=0, args={Term:4 LeaderId:1 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.931593 [0] AppendEntries: {Term:4 LeaderId:1 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.931646 [0] AppendEntries reply: {Term:4 Success:true}
10:02:27.932596 [2] AppendEntries: {Term:4 LeaderId:1 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.932656 [2] AppendEntries reply: {Term:4 Success:true}
10:02:27.976958 [1] sending AppendEntries to 0: ni=0, args={Term:4 LeaderId:1 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.976979 [1] sending AppendEntries to 2: ni=0, args={Term:4 LeaderId:1 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.978622 [0] AppendEntries: {Term:4 LeaderId:1 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.978660 [0] AppendEntries reply: {Term:4 Success:true}
10:02:27.983368 [2] AppendEntries: {Term:4 LeaderId:1 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.983456 [2] AppendEntries reply: {Term:4 Success:true}
10:02:28.016345 [0] becomes Dead
10:02:28.016442 [1] becomes Dead
10:02:28.016552 [2] becomes Dead
10:02:28.026344 [0] in election timer state=Dead, bailing out
10:02:28.026374 [2] in election timer state=Dead, bailing out
--- PASS: TestElectionFollowerComesBack (1.18s)
PASS
ok  	github.com/eliben/raft	1.646s

$ open /tmp/TestElectionFollowerComesBack.html
The file /tmp/TestElectionFollowerComesBack.html does not exist.

$ ls
dochecks.sh	go.mod		raft.go		server.go
dotest.sh	go.sum		raft_test.go	testharness.go

$ gst
On branch master
Your branch is up to date with 'origin/master'.

nothing to commit, working tree clean

$ cat /tmp/raftlog 
=== RUN   TestElectionFollowerComesBack
10:02:26.890095 [0] listening at [::]:49678
10:02:26.890643 [1] listening at [::]:49679
10:02:26.890914 [2] listening at [::]:49680
10:02:26.902823 [2] election timer started (183ms), term=0
10:02:26.902827 [1] election timer started (251ms), term=0
10:02:26.902870 [0] election timer started (176ms), term=0
10:02:27.082983 [0] becomes Candidate (currentTerm=1); log=[]
10:02:27.083210 [0] sending RequestVote to 1: {Term:1 CandidateId:0 LastLogIndex:0 LastLogTerm:0}
10:02:27.083258 [0] election timer started (245ms), term=1
10:02:27.083227 [0] sending RequestVote to 2: {Term:1 CandidateId:0 LastLogIndex:0 LastLogTerm:0}
10:02:27.087799 [2] RequestVote: {Term:1 CandidateId:0 LastLogIndex:0 LastLogTerm:0} [currentTerm=0, votedFor=-1]
10:02:27.087821 [2] ... term out of date in RequestVote
10:02:27.087837 [2] becomes Follower with term=1; log=[]
10:02:27.087931 [2] ... RequestVote reply: &{Term:1 VoteGranted:true}
10:02:27.088010 [2] election timer started (290ms), term=1
10:02:27.088499 [0] received RequestVoteReply {Term:1 VoteGranted:true}
10:02:27.088521 [0] wins election with 2 votes
10:02:27.088537 [0] becomes Leader; term=1, log=[]
10:02:27.088625 [1] RequestVote: {Term:1 CandidateId:0 LastLogIndex:0 LastLogTerm:0} [currentTerm=0, votedFor=-1]
10:02:27.088644 [1] ... term out of date in RequestVote
10:02:27.088664 [1] becomes Follower with term=1; log=[]
10:02:27.088765 [1] ... RequestVote reply: &{Term:1 VoteGranted:true}
10:02:27.088771 [0] sending AppendEntries to 1: ni=0, args={Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.088814 [0] sending AppendEntries to 2: ni=0, args={Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.088894 [1] election timer started (262ms), term=1
10:02:27.089272 [0] received RequestVoteReply {Term:1 VoteGranted:true}
10:02:27.089297 [0] while waiting for reply, state = Leader
10:02:27.093332 [0] in election timer state=Leader, bailing out
10:02:27.093349 [2] AppendEntries: {Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.093356 [1] in election timer term changed from 0 to 1, bailing out
10:02:27.093376 [2] AppendEntries reply: {Term:1 Success:true}
10:02:27.093413 [1] AppendEntries: {Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.093436 [1] AppendEntries reply: {Term:1 Success:true}
10:02:27.093415 [2] in election timer term changed from 0 to 1, bailing out
10:02:27.139625 [0] sending AppendEntries to 1: ni=0, args={Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.139625 [0] sending AppendEntries to 2: ni=0, args={Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.146314 [2] AppendEntries: {Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.146341 [2] AppendEntries reply: {Term:1 Success:true}
10:02:27.146317 [1] AppendEntries: {Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.146436 [1] AppendEntries reply: {Term:1 Success:true}
10:02:27.188894 [0] sending AppendEntries to 1: ni=0, args={Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.188897 [0] sending AppendEntries to 2: ni=0, args={Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.193268 [2] AppendEntries: {Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.193307 [1] AppendEntries: {Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.193339 [1] AppendEntries reply: {Term:1 Success:true}
10:02:27.193309 [2] AppendEntries reply: {Term:1 Success:true}
10:02:27.204521 [TEST] Disconnect 1
10:02:27.238892 [0] sending AppendEntries to 1: ni=0, args={Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.238905 [0] sending AppendEntries to 2: ni=0, args={Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.240463 [2] AppendEntries: {Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.240494 [2] AppendEntries reply: {Term:1 Success:true}
10:02:27.289697 [0] sending AppendEntries to 1: ni=0, args={Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.289707 [0] sending AppendEntries to 2: ni=0, args={Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.293988 [2] AppendEntries: {Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.294013 [2] AppendEntries reply: {Term:1 Success:true}
10:02:27.340210 [0] sending AppendEntries to 1: ni=0, args={Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.340217 [0] sending AppendEntries to 2: ni=0, args={Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.345632 [2] AppendEntries: {Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.345684 [2] AppendEntries reply: {Term:1 Success:true}
10:02:27.389904 [0] sending AppendEntries to 2: ni=0, args={Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.389904 [0] sending AppendEntries to 1: ni=0, args={Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.395596 [2] AppendEntries: {Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.395665 [2] AppendEntries reply: {Term:1 Success:true}
10:02:27.438892 [0] sending AppendEntries to 1: ni=0, args={Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.438902 [0] sending AppendEntries to 2: ni=0, args={Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.441337 [2] AppendEntries: {Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.441362 [2] AppendEntries reply: {Term:1 Success:true}
10:02:27.459451 [1] becomes Candidate (currentTerm=2); log=[]
10:02:27.459818 [1] sending RequestVote to 0: {Term:2 CandidateId:1 LastLogIndex:0 LastLogTerm:0}
10:02:27.459857 [1] sending RequestVote to 2: {Term:2 CandidateId:1 LastLogIndex:0 LastLogTerm:0}
10:02:27.459919 [1] election timer started (226ms), term=2
10:02:27.489000 [0] sending AppendEntries to 2: ni=0, args={Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.489005 [0] sending AppendEntries to 1: ni=0, args={Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.490356 [2] AppendEntries: {Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.490386 [2] AppendEntries reply: {Term:1 Success:true}
10:02:27.538935 [0] sending AppendEntries to 1: ni=0, args={Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.538940 [0] sending AppendEntries to 2: ni=0, args={Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.541633 [2] AppendEntries: {Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.541671 [2] AppendEntries reply: {Term:1 Success:true}
10:02:27.590125 [0] sending AppendEntries to 1: ni=0, args={Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.590174 [0] sending AppendEntries to 2: ni=0, args={Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.594231 [2] AppendEntries: {Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.594267 [2] AppendEntries reply: {Term:1 Success:true}
10:02:27.638912 [0] sending AppendEntries to 1: ni=0, args={Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.638920 [0] sending AppendEntries to 2: ni=0, args={Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.640252 [2] AppendEntries: {Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.640280 [2] AppendEntries reply: {Term:1 Success:true}
10:02:27.690041 [1] becomes Candidate (currentTerm=3); log=[]
10:02:27.690179 [1] sending RequestVote to 0: {Term:3 CandidateId:1 LastLogIndex:0 LastLogTerm:0}
10:02:27.690229 [0] sending AppendEntries to 1: ni=0, args={Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.690232 [0] sending AppendEntries to 2: ni=0, args={Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.690287 [1] sending RequestVote to 2: {Term:3 CandidateId:1 LastLogIndex:0 LastLogTerm:0}
10:02:27.690320 [1] election timer started (174ms), term=3
10:02:27.695021 [2] AppendEntries: {Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.695056 [2] AppendEntries reply: {Term:1 Success:true}
10:02:27.739016 [0] sending AppendEntries to 2: ni=0, args={Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.739021 [0] sending AppendEntries to 1: ni=0, args={Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.745394 [2] AppendEntries: {Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.745431 [2] AppendEntries reply: {Term:1 Success:true}
10:02:27.788970 [0] sending AppendEntries to 1: ni=0, args={Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.788972 [0] sending AppendEntries to 2: ni=0, args={Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.794949 [2] AppendEntries: {Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.794984 [2] AppendEntries reply: {Term:1 Success:true}
10:02:27.839073 [0] sending AppendEntries to 2: ni=0, args={Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.839081 [0] sending AppendEntries to 1: ni=0, args={Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.841805 [2] AppendEntries: {Term:1 LeaderId:0 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.841846 [2] AppendEntries reply: {Term:1 Success:true}
10:02:27.855402 [TEST] Reconnect 1
10:02:27.870710 [1] becomes Candidate (currentTerm=4); log=[]
10:02:27.870881 [1] sending RequestVote to 0: {Term:4 CandidateId:1 LastLogIndex:0 LastLogTerm:0}
10:02:27.870951 [1] sending RequestVote to 2: {Term:4 CandidateId:1 LastLogIndex:0 LastLogTerm:0}
10:02:27.871042 [1] election timer started (187ms), term=4
10:02:27.874226 [0] RequestVote: {Term:4 CandidateId:1 LastLogIndex:0 LastLogTerm:0} [currentTerm=1, votedFor=0]
10:02:27.874228 [2] RequestVote: {Term:4 CandidateId:1 LastLogIndex:0 LastLogTerm:0} [currentTerm=1, votedFor=0]
10:02:27.874254 [0] ... term out of date in RequestVote
10:02:27.874277 [2] ... term out of date in RequestVote
10:02:27.874288 [0] becomes Follower with term=4; log=[]
10:02:27.874331 [2] becomes Follower with term=4; log=[]
10:02:27.874420 [0] ... RequestVote reply: &{Term:4 VoteGranted:true}
10:02:27.874463 [2] ... RequestVote reply: &{Term:4 VoteGranted:true}
10:02:27.874486 [0] election timer started (264ms), term=4
10:02:27.874571 [2] election timer started (238ms), term=4
10:02:27.874921 [1] received RequestVoteReply {Term:4 VoteGranted:true}
10:02:27.874947 [1] wins election with 2 votes
10:02:27.874966 [1] becomes Leader; term=4, log=[]
10:02:27.875145 [1] sending AppendEntries to 0: ni=0, args={Term:4 LeaderId:1 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.875165 [1] sending AppendEntries to 2: ni=0, args={Term:4 LeaderId:1 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.875242 [1] received RequestVoteReply {Term:4 VoteGranted:true}
10:02:27.875267 [1] while waiting for reply, state = Leader
10:02:27.878247 [2] in election timer term changed from 1 to 4, bailing out
10:02:27.878251 [0] AppendEntries: {Term:4 LeaderId:1 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.878327 [0] AppendEntries reply: {Term:4 Success:true}
10:02:27.881210 [1] in election timer state=Leader, bailing out
10:02:27.881219 [2] AppendEntries: {Term:4 LeaderId:1 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.881372 [2] AppendEntries reply: {Term:4 Success:true}
10:02:27.927120 [1] sending AppendEntries to 2: ni=0, args={Term:4 LeaderId:1 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.927121 [1] sending AppendEntries to 0: ni=0, args={Term:4 LeaderId:1 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.931593 [0] AppendEntries: {Term:4 LeaderId:1 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.931646 [0] AppendEntries reply: {Term:4 Success:true}
10:02:27.932596 [2] AppendEntries: {Term:4 LeaderId:1 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.932656 [2] AppendEntries reply: {Term:4 Success:true}
10:02:27.976958 [1] sending AppendEntries to 0: ni=0, args={Term:4 LeaderId:1 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.976979 [1] sending AppendEntries to 2: ni=0, args={Term:4 LeaderId:1 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.978622 [0] AppendEntries: {Term:4 LeaderId:1 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.978660 [0] AppendEntries reply: {Term:4 Success:true}
10:02:27.983368 [2] AppendEntries: {Term:4 LeaderId:1 PrevLogIndex:0 PrevLogTerm:0 Entries:[] LeaderCommit:0}
10:02:27.983456 [2] AppendEntries reply: {Term:4 Success:true}
10:02:28.016345 [0] becomes Dead
10:02:28.016442 [1] becomes Dead
10:02:28.016552 [2] becomes Dead
10:02:28.026344 [0] in election timer state=Dead, bailing out
10:02:28.026374 [2] in election timer state=Dead, bailing out
--- PASS: TestElectionFollowerComesBack (1.18s)
PASS
ok  	github.com/eliben/raft	1.646s


$ cd ..

$ cat /tmp/raftlog go run tools/raft-testlog-viz/main.go 
raftlog

$ cat /tmp/raftlog | go run tools/raft-testlog-viz/main.go 
PASS TestElectionFollowerComesBack map[0:true 1:true 2:true TEST:true] ; entries: 152
... Emitted file:///tmp/TestElectionFollowerComesBack.html

PASS
```

The cool part is - there's a separate tool to read the test logs and create a visualization that can be viewed in the browser :D :D Wow!


