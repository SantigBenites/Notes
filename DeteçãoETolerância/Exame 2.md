
# Consider the Bitcoin consensus protocol (also called Proof-of-Work consensus).

## What is a proof-of-work? Explain the PoW cryptopuzzle used in bitcoin.

Proof of work or POW is the way bitcoin guarantees integrity in the blocks, this is done by inputting into the block the solution to a cryptografic puzzle this puzzle.
The puzzle in question used in bitcoin is the hash of the prevoius block which has been altered until N number of 0's are at the begginign of the hash.
This type of hash normally takes the netowkr about 10 minutes to solve, so we can see that it is very costly from a computacional standpoint.
This is used to garantee that a certain block is the following link of the chain from the prevois block, and its complixty allows for only the chain to fabricate these block considering the compuational power required to refrabicate a single block is immense, and consideirn they are chained toghether in order to change a single block in the chain we would need to recaulcate all seqsequent blocks.

## Why it is said that the PoW consensus is secure as long as the adversary control less than 50% of the network CPU power? In which situations the network speed can modify this bound?

POW consensus is secure as long as the adversary has control of less that 50 perecent of the nework CPU power, this is beacuse if the attacker has more than 50 percent it has the ability to input transactions into the blockchain uncontested
This happens beacuse the blockchain requires consensus, an attacker with 51% of the network can finnalize blocks by itself wihtout rquirin the rest of the network.
This being said, we can change the speed of the network to make sure that even though an attacker has a majgority of the network it is not able distribute the blocks accross the network fast enough to outpace normal users, making it so that even though the attacker has a bigger part of the network's compuational power, it cant use it to control the blockchain uncostentested.

## Why it is recommended to wait for several blocks to be inserted in the blockchain after the block containing a transaction t before considering t to be “committed”?

The reason it is recommended to wait for several blocks to be inserted into the chain before commiting a certain block is beacuse in some sitations it can be advantageus to revert some operations executed in a block to this effect insted of commiting blocks instantly to the chain, which is very costly, we just prepare them to be added and only commit them after we are sure that the probability of them being reverted is low.

# Explain how the GHOST protocol (used in Ethereum) improves the performance of PoW consensus.

In GHOST, unlike in normal POW consensus, to decide on which fork of the chain should be added to view the number of attestant which attest for a certain chain fork.
This allows the effiency of this algorythm to be much faster than the one used in POW consussu in which we choose the longest chain.
This is faster considering we dont need to evaluate all possible chains which can come from a single node with tree algorythms but only see how many attestats are associated with a single node.

# Consider the implementation of a standard Byzantine State Machine Replication (SMR) system, which requires n=3f+1 nodes to work, for f faults

## It is well known that to do a voting in the presence of f faulty processes, 2f+1 nodes would suffice. What is the reason for the requiring 3f+1 for BFT SMR?



## Why the USIG service implemented by the TPM chip enables the implementation of BFT state machine replication using only 2f+1 replicas?

The usage of the USIG service with a TPM chiip allows for a smaller quorrum of only 2f+1, this is because by using TPM we can have UI (Unique Identifier) for each node.
This not only allows us to know who sent each message but also have a universal order to the messages.
All these factors in conjunction allow the quorum size of this type of approach to go from 3f+1 to 2f+1.

## Is the MinPBFT (the BFT state machine replication protocol that uses USIG) vulnerable to the performance degradation attacks that affect PBFT?

All BFT protocols are vulnerabable to DDOS attacks which are a type of performance degradation.

This being said there are 2 attacks more prevalent in BFT systems
- View change from slow client
- Slow primary delaying the view


The second one can be classified as performance degradation, this attack revolves around the usage of a malicious primary which sends the order messages at the last second with the intent of given it just enought time to execute and not change view. Its goal is to waist as much time as possible, wihtout leading to a view change and removing him from primary.

This being said a solution to this attack is to switch primaries in each view, consideirng this is done by MinPBFT, we can conclude that this protocol is not sujectible to this type of attack.