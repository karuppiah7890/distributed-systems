# Raft

I think it's good to start off by answering some basic questions like:
- What is Raft?
- Why is it needed? One of the most important questions
- What problem does it solve?
- Are there no other things that solve the same problem?
- How is it different / novel from other alternatives if there are alternatives?
- How popular is it? Any reason for it's popularity?
- How technically sound is it?

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

