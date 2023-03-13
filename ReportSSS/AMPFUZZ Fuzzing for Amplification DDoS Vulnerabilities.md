# Introduction

AmpFuzz is a fuzzing application dedicated to fuzzing for amplification DDOS vulnerabilities in networks, it focuses on a systemic way of finding of finding these types of vulnerabilities in UDP services in a prognostic way, ideally it will find the application vector for said vulnerability.
We will assume everyone knows what a fuzzer is, considering it was the topic of a T class, and what a DDOS class, considering it should be common knowledge for security students,

# Amplification Attacks
Therefore we will begin be explaining what and amplification attack is.
Amplification attacks are a type DDOS attack, DDOS attacks are characterised by overwhelming the attacked party with an immense amount of packages leading to losses in service and performance. This being said, in a Amplification DDOS we use services using protocols with looser headers,specifically protocols where the header isn't verified for authentication, and without handshake, take for example UDP protocol, to send immense amounts of packages to a certain victim.
Moreover, the services provided by these types protocols usually have an amplification factor associated with them, this meaning that instead of responding with 1 package to a 1 package request, they can send a plethora of packages in response to a request, making it that much easier for the attacker to overwhelm the victim.

## "Advantages" of this type of attack

Large Amplification potential - For example NTP (Network Time Protocol) had up to 5500x amplification rate
New vulnerabilities discovered regularly

# AmpFuzz

Therefore it was the goal of the researchers to have a systematic way of finding these types of vulnerabilities in protocol a priori and without having to wait for them to be exploited.
They therefore sough out to adapt fuzzing techniques to solve this type of problem. The researchers found 3 main problems:

## How to sincronize Requests and Responses

The first problem is that servers don't have endless up time and we have specific intervals in which we can communicate with them.
In these cases, if the message is sent too soon, the socket wont be open and therefore wont be able to receive the message, if the message is sent too late, we are wasting too much time and therefore our fuzzing becomes ineffective.
Therefore, we must try to send the message as soon as the socket is ready, this is something we can do by making sure that the server notifies the fuzzer as soon as it is ready to receive the packet.
For this purpose the researchers decided to add to the code a function that would be called to signal the fuzzer when the socket was available.

## How to Use Fuzzing Without Crashes
Another problem, was that normal fuzzer work by waiting for crashes from the program and therefore are difficult to apply when the program not only works on an infinite loop, nor does it crash.
For this purpose, researchers tried to find a way to turn a server that does not terminate into a one shot program, this was done by separating the functions called by the server into 3 types:
- Sources - functions that receive a packet
- Sinks - functions that send out a packet
- Blocking - functions that can block execution while waiting for a packet
After this, they analysed the flow of the program and searched for links in which a source cannot reach a sink without passing through another source, and defined this links as end points of the program.
One could ask if there would be certain intervals of time where using a timeout would be more efficient that this this complicated process: 

*Show time graphs for using and not using UDP-Aware Fuzzing*

## How to analyse how big the Request/Response ratio is

The last problem, is that normal fuzzers work, by given a certain program, "throwing" inputs at it and awaiting a possible crash. 
This being said, in the case of Amplification attacks, we aren't searching for crashes. Considering that the metric we want to evaluate is bandwidth amplification ratio, how bigger the message we received is compared to the message we sent.
In order to analyse this, we must take into consideration 2 alterations we must make when compared to normal fuzzer.
Firstly, we must be aware that some of the protocols in question reply with zero length packages and and send additional headers in different protocol layers, therefore we must also consider this size when trying to calculate the ratio for a certain interaction. This leads us to an alteration of the normal bandwidth amplification ratio formula.
*add new bandwidth amplification formula*
Secondly, we must diverge from the approach used by normal fuzzers, as we learned when a fuzzer discover a input that leads to a crash, it cuts all links that derive from that input. 
This because it knows that inputs deriving from a crash will also lead to a crash.
In the case of AmpFuzz, our objective is not only trying to find inputs that lead to responses, but also to find inputs that lead to responses with bigger numbers of packets, this being said we cant just remove all links from a response because unlike a normal fuzzer, the links can have bigger amplification ratios that the original response. 
More over, in another trick used by the researchers to improve the amplification ratio, is also to try to remove insignificant parts of the packet in order to be able to diminish its size, and therefore get equal sized reposes with smaller requests.

# Results

In terms of results, when researchers run AmpFuzz over 28 target programs using a multitude of protocols such as UDP,DNS,SSDP... , they found that 13 of the targets had amplification vulnerabilities, and that of these 13 9 of the vulnerabilities where unknown. 
In these vulnerabilities, multiple not only had one amplification vector but some had up to 200 with ratios of up to 32x amplification.
In terms of shortcomings, AmpFuzz as some caveats these being:
- Services can be fuzzed only if they can be compiled using an LLVM-based toolchain.
- Services must use UDP sockets for communication between the fuzzer and the server.
- Depending on service, take for example DNS, there might be need for expert knowledge when using domain names.
- Considering UDP-Awareness needs some level of insight, AmpFuzz cant operate over entirely closed services