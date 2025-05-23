# NATS Bugs

This repository mainly exists to document bugs or shortcomings in [NATS](https://nats.io/) that the developers seem to disagree with.

<div style="text-align:center">
<img src="./conat.png"/>
</div>

**May 2025 UPDATE:** I've decided to implement something that works much like NATS, but that is very suitable for building a distributed web application with a large number of users.  This will be called "Conat" (for **Co**Calc **Nat**s, but also suggesting "connate" from biology).   See https://github.com/sagemathinc/cocalc/pull/8346   
Basically NATS has a bunch of excellent API design choices and patterns involving how pub/sub, subject hierarchies, queue groups, etc., all work.  But many of the architectural decisions, e.g., around authentication, scalability of Jetstreams, etc, are extremely bad from my point of view, having really pushed NATS over the last few months.   Also, built with way too much of "Not Invented Here Syndrome", e.g., why spend years building Jetstream as a new database from scratch, rather than using existing mature open source databases (like sqlite)?  Why is the Websocket connectivity with browsers from scratch, rather than being built on mature proven technology like socket.io that solves a wide range of subtle problems involving dropped connections?   


---

## Why does this repo exist?

[NATS](https://nats.io/) is an amazing and very powerful high quality piece of software. I love it. 

**I AM A NATS SUPERFAN.**

Like all software, it has bugs, and there are also many difficult design decisions
the developers have to make, which balance the needs of wide range of users.

I've started using NATS a lot in the development of https://CoCalc.com, and interacting with their GitHub repo,
and noticed a pattern, where I finally find something wrong or missing \(but easy to fix\)
in NATS, and instead of fixing the problem, the developers close the issue or disagree
that it is an issue at all. Sometimes, if I comment on something, they suddenly suggest the feature I'm
using should be removed! It's disconcerting, but of course 100% within their right
as authors of open source software. I've noticed this with other projects as well
\(e.g., [with JuiceFS](https://github.com/sagemathinc/cocalc-compute-docker/tree/main/src/cloud-filesystem/patches/juicefs)
I found a major problem in the JuiceFS inode allocation algorithm
that causes silent filesystem corruption, but they didn't seem
to agree.

With NATS-io it's disconcerting because this has happened so much. I've watched most of the youtube videos they posted to better understand NATS, and it seems like development is done pretty much 100% by employees of the company (which is fine -- my company is the same), which could explain this pattern. Probably there's other channels where real discussion happens, and I'm not part of them so I can't really argue my case. Or it may be that I'm just bad at
communicating. In any case, perhaps this repo will help.  It will definitely help me personally
to keep track of all these edge cases, in case I have to maintain some sort of fork or
patches at some point.

So I'm creating this repo to document this so I can better keep track of it, since the
issues themselves often get closed. Also, in case I have to maintain a fork of NATS to
maintain functionality I rely on, this repo will be a useful resource.


