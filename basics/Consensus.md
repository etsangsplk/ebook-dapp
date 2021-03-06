# Consensus in P2P

One of the biggest problem in any distributed system is how to reach consensus: agreement on what the current state is. As anyone, who ever tried to organize a dinner with a few friends, can tell you, coming to an agreement in a distributed or even asynchronous fashion is really hard. And it often comes down to one person making a decision that other accepts.

In our classic web model, this is what the central server is doing. More than just a place of communication to channel through, it provides a convenient way of central authority about a state: if the server says that is latest post, then it doesn't matter if any client contests that, it is what we consider the truth of the current state. Of course, in many systems in production this state is actually handled in complex databases, but they still act as a central authority in most things. And that is a very handle model. If the king is the law, then all you need to know the law, is ask the king.

## The king is dead

But in a true peer-to-peer-network, you don't have a king - intentionally - so how do you come to a decision? Well, how do we decide things in the free world? We ask the public, hold referendums and elections, and let the majority decide in a one-party-one-vote-system. Elections mainly consists of two parts: reduction of the electorate, and electing the winner. 

We've generally agreed to reduce the number of options, either through a formality process or some other form of qualification scheme - in many democracies you need to demonstrate that you have enough supporters through signatures for example - because if we'd have to elect from the entire population we'd never reach a majority. Once we've selected the subset of options, we ask everyone to cast their vote normally within a certain time frame, then count the votes and based on the will of the majority select the winner (this is of course a highly simplified view of things).

### Reduced Electors

But this process is tedious, takes a lot of time and is very expensive. One very common way, to speed up an election process is to reduce the number of parties that can actually participate in the election. This is why most western democracies have parliaments or senats: to reduce the amount of people, who are part of the actual election process of laws to a number that allows us to find consensus faster than if we had to ask the population every time. However, this comes with a loss of control of course.

These expenses of elections are still true in computer science, which is why a lot of distributed agreement systems (like Paxos) are similarly only used to select the next leader ("master") in a network (and all others become "minions") but not for every decision that needs to be taken. Having elected leaders of the entire network isn't much of an option in distributed peer-2-peer-network of untrusted nodes however, as we have very few (read "none") other checks and balances on that node and they could easily be compromised. Therefore, most decentralized protocols require the consensus process to take place on every change made. The bigger the network, the harder that gets of course. Thus, protocols need to be designed to speed up that process.


## Bitcoin and blockchains

Bitcoin, for example has a two part reduction system: first it doesn't agree on _every transaction_ but puts them into a block of transactions and then creates a really hard and expensive to calculate mathematical puzzle on it. By cracking that puzzle you earn new Bitcoins, thus there is an incentive to do that. However as a block is only valid once the puzzle has been cracked, there is always only a limited number of possible valid next blocks - a reduction of the electorate. By then following a predefined process of always continuing with the longest block they know of, the voters elect the winning branch of the blockchain.

However, consensus is only reached once there is no competing fork before that block anymore and even just cracking that puzzle takes ten minutes on average (now). So, while Bitcoin provides a protocol to reach consensus in a large scale distributed network, it is still quite slow - too slow for general purpose apps. Just consider you'd have to wait for 10 minutes for the confirmation before your picture has been uploaded. That's unacceptably slow.
 

