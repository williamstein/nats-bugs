# NATS Bugs

This repository mainly exists to document bugs or shortcomings in [NATS](https://nats.io/) that the developers seem to disagree with.

## Why?

[NATS](https://nats.io/) is an amazing and very powerful high quality piece of software. I love it.

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
communicating. In any case, perhaps this repo will help.

So I'm creating this repo to document this so I can better keep track of it, since the
issues themselves often get closed. Also, in case I have to maintain a fork of NATS to
maintain functionality I rely on, this repo will be a useful resource.

## Issues

- [Upload of large object fails with nats: error: nats: stalled with too many outstanding async published messages](https://github.com/nats-io/natscli/issues/993) - I didn't open this issue, but I hit it within seconds of trying nats large object functionality, and without a workaround, it seems like a huge blocker to using that functionality at all. I was able to give a reproducible test case, after it sat there with no test case (repoted by somebody else) for a year. As a result they closed this issue because, saying fixing it requires adding functionality to nats-server, without a link to a relevant nats server issue. But it's still an issue, so I don't understand why it is closed.

- [Support setting headers for kv put](https://github.com/nats-io/nats.js/issues/217) In my own work, I've found setting headers to be an extremely elegant way to solve numerous problems when using NATS kv functionality. With nats messages and streams it's easy to set headers. But for no evident reason except "currently our specification doesn't support user-specified headers on KV" and "If you want to store arbitrary sized data, object store is the correct API." [note that object store has issues -- see above], they closed this issue. It is a 1-line change to the client to add support for headers, which I've made in my copy of the client code.

- [Auth callout - Better doc/guidance to integrate with an OAuth2/OIDC provider](https://github.com/nats-io/nats-server/issues/5692). This is still opened, but since I worked through understanding it myself by reading source code, and "reverse engineering", I made [some comments](https://github.com/nats-io/nats-server/issues/5692#issuecomment-2729488148) about how it could be addressed based on my experience writing a Typescript client. The [first developer response](https://github.com/nats-io/nats-server/issues/5692#issuecomment-2730428296) to my comment is honest, but also kind of scary/threatening: "I believe that all callout services should be written in Go.". It also gives me deja vu regarding Kubernetes storage.
