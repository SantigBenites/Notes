# What is the difference between intrusion tolerance and intrusion prevention? Give an example of a mechanism for each

Intrusion prevention is when we try to remove of put systems in place to prevent intrusions in our system, take for example firewalls or removing vulnerabilities from the code before they are explored
Intrusion tolerance is when we put systems in place to make sure the system can tolerate the consequences of an intrusion and doesn't "crash" or malfunction when the system is intruded on, take for example replication and redundancy.

# Define the “integrity” property. Name and describe a method based on intrusion tolerance for enforcing it in a replicated system

Integrity is a property of systems that consists on a systems information not being corrupted/modified by outside forces when an intrusion happens,
A way of implementing this property in a replicated system, with an implementation based on intrusion tolerance can be the use of a replica to maintain a copy of the data in use, this would allow the system to make sure that the integrity of the data it was providing wasn't violated when it was provided too the user, it would also provide some tolerance to intrusion considering it would minimise the consequences of that intrusion given that the altered data wouldn't be passed on to the user.

# Describe the main differences between “Behaviour-based (or anomaly detection) systems” and “Knowledge-based (or misuse detection) systems”.

The main difference between "Behaviour-based systems" and "Knowledge-based systems", stems from the way they detect intrusions on the system.
On one hand,  "Behaviour-based systems" try to detect intrusions by comparing the behaviour of the current system against the normal behaviour of the system, and if they are different the system concludes that an intrusion is taking place.
On the other hand, "Knowledge-based systems" try to detect intrusions by comparing the operations of the system to known attack patterns stored in a database, if any pattern is detected then the system knows an attack is occurring.

This lead to several characteristics on each type of IDS
Regarding type of attacks that can be detected
- Behaviour based - Can detect 0-day attacks in some situations (usually use ML, and ML models cant detect what they aren't trained on), can detect novel attacks that change system status, can detect variations of known attacks
- Knowledge based - Only detects attacks present in the database
Regarding false positives
- Behaviour based - Leads to some false positives in situation where the behaviour might be abnormal, but not caused by intrusion
- Knowledge based - Doesn't have false positives

# Write a script (in high level - just describe the overall idea) that receive the network flows collected in the last week and detect if there are beaconing and raiding behaviours in the network.

## Beaconing

Beaconing attacks are situation where a host sends messages to the target in semi-synchronous patterns, to try to keep a connection alive and waste resources
```
for each connection
	x = check each host for number of messages sent
	y = check the connection time for the host
	if x/y < some value:
		then the conncetion too a long time and it was very spaced out
		if !connectionIsKeepAlive(host,target)
			possible attack

```

## Raiding

Raiding attacks happen when a host tries to get information/files and copy the to an outside resource, characteristically these attacks have short duration and big load size
```
for each connection
	x = check the connection duration
	y = check the connection load size
	if x < someDuration && y > someSize:
		the connection can be a raiding attack 

```


# Why anomaly detection is rarely used in practice? How machine learning algorithms can still be effectively employed for detecting threats against an infrastructure?

Machine learning algorithms are rarely used in practise for several reasons amongst them are
- The need to retrain them after certain periods of time so that they don't lose accuracy
- The slowness of training algorithm and the need to have a lot of data regrading the system to train them
- The marginal increase they provide against signature detection methods(i say marginal but depends on situation)
- The several problem of using ML, like dimensionality, Big data, feature selection, among others

One of the possible changes to do to optimise such algorithms can stem from using semi-supervised models, better pre-processing, better datasets, among others.
Lastly systems like Bigflow present a new way of doing anomaly detection which implements some of the optimisations previously referenced, with promising results.

# Consider the implementation of a standard Byzantine State Machine Replication (SMR) system, which requires $n=3f+1$ nodes to work, for f faults.  


## It is well known that to do a voting in the presence of f faulty processes, $2f+1$ nodes would suffice. What is the reason for the requiring $3f+1$ for BFT SMR

The fact that we need $2f+1$ nodes to propose the same vote for BFT is dependant on the existence of $3f+1$ nodes in the system.
This because in a system with $3f+1$ nodes, $2f+1$ represents a quorum meaning a majority of the system.
The reason we use $2f+1$ is because in a system with $3f+1$ nodes there cant be 2 quorum of $2f+1$ which leads to only one value being possibly agreed on by the entire network, and not allowing violating the validity property of BFT. 