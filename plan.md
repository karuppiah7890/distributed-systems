# Plan

Following https://medium.com/@polyglot_factotum/how-i-am-learning-distributed-systems-7eb69b4b51bd

Start with the series of blog posts about Raft

https://eli.thegreenplace.net/2020/implementing-raft-part-0-introduction/

Try the code at https://github.com/eliben/raft and learn by
- Running it
- Changing the code
- Running the tests
- Adding new tests / modifying existing tests and running them to see how things work and answer questions I have

Come up with a set of questions that I have while learning

Next Steps? 🤔

---

Currently I'm looking at other various ways to learn too. Raft implementation has been on hold a bit.

Other ways - reading articles, but that's just theoretical, yeah. Totally these are the ways -

- Reading articles - theoretical and sometimes practical too if there's code or mention about real life experiences
- Reading blogs and blog posts - theoretical and sometimes practical too if there's code or mention about real life experiences
- Contributing to Open Source projects or even closed source projects - very practical and some theory too that will be needed to do things so I'll learn it on the way
- Reading books / ebooks - theoretical and sometimes practical too if there's code or mention about real life experiences
- Reading research papers - theoretical and sometimes practical too if there's code or mention about real life experiences
- Trying out YouTube and other videos and video series - theoretical and sometimes practical too if there's code or mention about real life experiences
- Trying out Online Courses - video and non-video, for example Coursera courses, college online courses - theoretical and sometimes practical too if there's code or mention about real life experiences
- Listening to podcasts - theoretical and sometimes practical too if there's mention about code in audio, but it's probably very very rare, or there couldn be mention about real life experiences which is very practical knowledge
- Attending meetups - online and offline - theoretical and sometimes practical too if there's code or mention about real life experiences

Three broad mediums for learning
- Audio
- Video
- Text

There's also interaction / collaboration with people as part of the mediums. Interactions - discussions, question and answer forums etc. Collaboration - working together and collaborating on some project

---

About Contributing to Open Source projects, I could checkout open source projects which have distributed systems at their core - just applications that are based on distributed systems concepts, for example Kubernetes platform is a distributed system with many components working together. But come to think of it...I don't think any of them have state or is aware of one another. All the state is in etcd or similar backend databases, and I believe almost all components are stateless and depend on the API server for data or sometimes have some cache which is kind of like a state. And all things happens through the API server instead of having direct communication with other components. Gotta check if Kubernetes really fits the distributed system definition

And then there's distributed databases - I could contribute to open source distributed databases like CockroachDB among many others. And I could also check the operators for managing distributed databases or just databases, for automatic management - because some databases are not distributed or may need manual management for some actions and hence need some controller / operator / manager for automated actions. And such operators and managers kind of system are usually distributed
