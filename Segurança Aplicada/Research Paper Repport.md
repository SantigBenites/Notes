# Catching Transparent Phish: Analyzing and Detecting MITM Phishing Toolkits



Phishing toolkits have been aiding attackers in automating and streamlining their phishing campaigns for more than a decade. 
These toolkits have transformed the process of creating phishing websites by automating the retrieval of static copies of web pages from targeted websites. They serve these copies to unsuspecting victims while employing cloaking mechanisms to evade detection. 

However the continuous adoption of better security methods, such as 2 factor authentication, has forced the evolution of these methods.
This led to the emergence of Man-in-the-Middle (MITM) phishing toolkits, these toolkits function as malicious reverse proxy servers, imitating legitimate online services to users while intercepting credentials and session cookies. 

This paper presents am analysis regrading the usage of these MITM phishing toolkits in the wild, then proceeds with developing a ML classified which is able to detect these models with astonishing accuracy, they named this model PHOCA.

In sequence with these developments, the authors utilized PHOCA to conduct a search for MITM phishing toolkits in real-world environments, with the goal of uncovering usage patterns. This investigation enabled them to reveal the source and destination of phishing campaigns. 

Over the course of a year 1,220 MITM phishing websites were analised revealing that these toolkits often evade existing phishing blocklists, leaving users susceptible to attacks. 

These websites were hosted on dedicated malicious servers and were largely absent from widely used URL blocklists. 

This new method differiates from previous attemps at this type of approach considering PHOCA showed resilience to cloaking mechanisms employed by the toolkits and offers methods for online services to fingerprint and prevent phishing attempts in real-time.

In conclusion this paper, has shed light on the significant impact MITM Phishing Toolkits have in the current panorama of attacks in the Internet. Moreover this research has demonstrated the feasibility of identifying and classifying these toolkits with high accuracy.

Future work regarding this subject is mentioned in the paper but there are 2 main areas of importance:

- Improvement of the dataset used to train the classifier so it can be more effective against possible edge cases.
- Implement a similar process to detect normal phishing attacks, a feature that PHOCA doesn't have .