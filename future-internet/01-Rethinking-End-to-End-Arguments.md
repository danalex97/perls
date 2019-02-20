# [Rethinking the Design of the Internet](http://nms.lcs.mit.edu/6829-papers/bravenewworld.pdf)

### Paper summary

The authors wonder around the issues of the actuality[in 2001] of the end-to-end design principles["only if sufficient", "only if necessary", "only if useful"] in the context of changes of the internet landscape regarding matters such as end-user trust, demanding applications(e.g. streaming), increasing importance of certain stakeholders(ISPs, governments) and 3rd parties(e.g. certificate authorities, firewalls).

The benefits of the end-to-end argument lie in flexibility, generalizability and openness. However, the paper argues that changes need to be made within the network. A list of possible technical responses includes firewalls and traffic filters(providing better trust), traffic labeling schemata(as a compromise for ISPs in internet neutrality issues) and 3rd party certification(for security and accountability).

### Key insight(s)
- Changes of the internet landscape from 2001 are described.

- Current and future technical solutions are provided for raising issues.

- The importance of law in shaping the internet is discussed.

- Examples of widely used techniques that violate the end to end principles are given(e.g. caching).

- Are noted changes in stakeholders(ISPs and governments), user trust and internet availability.

### What could be improved?

The paper very interestingly notes issues that are still actual such as the lack of trust or internet neutrality.

It is very interesting to note a large list of precursors of current technologies or research directions showing in the paper. We list a few with their today equivalent:
- encryption and integrity - IPSec
- middle actors that mask traffic - Tor
- caching content - CDNs
- discussions whether ISPs should filter or prioritize traffic - net neutrality related problems
- NATs for companies - IPv6
- demanding streaming applications - CDNs
- overlays on top of Internet - IPFS, distributed ledgers

Another interesting fact to notice is the importance of trust which can be highlighted by the large interest in trustworthy computation and storage introduced by technologies such as distributed ledgers.

Personally, I think that the end-to-end principle is still actual, but compromise is acceptable until a better system design that can guarantee flexibility and openness appears.

### Other reviews:
 - https://sites.google.com/site/franciscabarle/home/cs-255/reviewofrethinkingthedesignoftheinternettheendtoendargumentsvsthebravenewworld

 - https://medium.com/@bennegeek/notes-on-rethinking-the-design-of-the-internet-the-end-to-end-arguments-vs-the-brave-new-world-b6fbd79d2682
