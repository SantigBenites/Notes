
# BigFlow: Real-time and reliable anomaly-based intrusion detection for high-speed networks

# Introduction

Most attacks n our days make usage of the quantity of data traversing the internet to hide themselves
Previously, the usage of Hadoop based clusters was approached, but never applied in reality because of efficiency
Current approaches to network traffic and measurement usually use unsupervised ML, however because of the size of the data, supervised ML should be considered
However, considering we are using real time systems, and that ML models cant easily be retrained, these models tend to lose accuracy overtime with the presence of new attacks
In this paper we will analyse the accuracy loss of ML classifiers overtime, in average of 23% over a year
Normally to keep, the model from going out of date, monthly revisions need to be made, with human intervention from the rebuilding of the model
Wit this in mind the authors present BigFlow a system for reliable real-time network traffic classification
It possesses 2 main insights
- Make the administrator aware of possible changes that happened in traffic behaviour, and not just evaluation events as attacks or not, but also realising new traffic behaviour is happening
- Using streaming techniques to allow for near-real-time traffic analysis, and to also allow for systematic updates to the model. Allowing for a better overall performance of the model
In summary BigFlow possesses
- Better deception accuracy with less misclassifications
- Identification of new traffic characteristics
These 2 culminate in better reliability overtime, and less storage space required

Concluding the paper did
- Provide new datasets for intrusion detection engines
- Analyse the performance of traditional ML classifier with the new dataset (and see their downsides)
- Present BigFlow, a reliable streaming learning intrusion detection engine
- Experiment with bigflow and compare it to other engines

# Background

## Stream Processing

BigFlow makes usage of streaming processing platform for dealing with large volumes of data,
These are platforms which receive data from registered sources and compute over said data with usage of processing elements
The near real time processing in such platforms is achieved by keeping each PE as small as possible, and by trying to parallelize PE's as much as possible

## ML for intrusion detection

There exist 2 types of approaches detect intrusions in a network
- signature based
- anomaly based
While the first one requires lots of signature to attacks, that might not even be useful against small variants of the attack
The second one is more used in practise when combined with ML, this leads to 2 branches
- Unsupervised - which is simpler but results in false positives
- Supervised - Requires expensive processes, like the training stage, but it is more accurate
When using ML for intrusion detection, we turn the flow of the traffic into a a set of features, and search for anomalies in those features to detect and attack
Unfortunately, general purpose networks seldom exhibit stable patterns, this combined with the difficulty of using ML models in real time development, leads to these process being unfeasible for most high speed networks
This makes way to stream learning algorithms, that update models with new entries instead of training a whole new model

# MAWIFlow

To benchmark ML-based NIDS, the authors created MAWIFlow, with record collected over a year
The main challenges to build a dataset like this were
- Realism - The dataset needed to be obtained from real sources
- Validity - The network traces used needed to be collected from real network traces, and needed to be sanitised for sensitive data
- Prior Labelling - The events on the dataset needed to be properly identified
- High Variability - Having a long period of recording so that the data could be evaluated with high variability of data types
- Reproducibility and Public Availability - The network traces needed to from from public sources, and the source code needed to be publicly available

## Accuracy degradation of ML classifiers

The main foal if this analysis will be to determine if ML-based approaches can maintain accuracy overtime, with real network traffic
In order to test this the authors used 4 different model to train 8 ML-based approaches, and then decided to retrain 4 of the approaches on a weekly basis with the last week of data, and the other 4 approaches were only trained in the begging of the year once.
The results concluded that the ML-Based NIDS that weer only trained once had significantly worst results that the weekly trained counterparts, leading to conclusion that retraining models periodically is better for accuracy

# Bigflow

To address these shortcoming, the authors present BigFlow a reliable stream learning intrusion detection system, whose goal is to maintain high accuracy overtime, while trying to minimise human intervention and stored data,
It works in 2 phases
- Feature Extraction
- Reliable stream learning
In feature extraction we extract features using traditional stream processing framework
The reliable stream learning stage classifies inputs (feature vectors) as normal or attack

## Feature Extraction

The usage of stream processing allows for monitoring of high-speed evolving networks, without the need to store lots of data.
The feature selection process is done in almost real-time
BigFlow can extract up to 158 features, and considers both flow statistics and host statistics

## Reliable Stream Learning

After network flow computation, it becomes possible to Bigflow to classify vectors as normal or attack.
The classifier must be able to cope with changes to the network content and traffic changes over time.
Moreover, in real systems the model must be updated weekly to counter effect evolving changes

### Setup

Uses a training dataset to start the model
A base classifier is obtained and replicated 
During validation, base rates for attack and not attack are defined to analyse if the model is accurate

### Real time learning

During this process, instances are classified as attack or not attack, with a certain rate of confidence.
If the confidence is above the expected value, this instance is considered in the dataset and used to train the model in real time
If the confidence is below the expected value, the instance is store until it can be proven the value, if proven the model can now use this instance to train
Instances confirmed as attacks are then sent to humans or alternative confirmation methods to be assured and dealt with appropriately
This allows for minimal human intervention, and mitigates false positives and negative alarms
Also minimises cost in model updates, by not training with all instances that are rejected.


# Related Work

## Benchmark dataset for IDS

The creation of MAWIFlow presents an alternative to the flawed datasets used to train common IDSes such as DARPA1998
While some work as been done in improving in this area all attempts lack some crucial points
In general, datasets lack upgradability, wrong assumption of immutable network traffic and believe user behaviour can be modelled

## Flow measurement and classification

To analyse flows some authors used Hadoop-based network traffic monitoring analysis.
Others implemented anomaly detectors into Hadoop architecture for network monitoring, added with hashing to divide network traffic into splits
However all of this work was for nought considering the complex computations used made this system unusable in high speed network monitoring


# Conclusion

Current approaches for network traffic classification aren't effective in real systems because of desired throughout and chaining behaviour
The approach presented bigflow, was able to perform feature extraction and classification and allowed for all of that with simpler computation effort and storage
To maintain reliability against evolving network traffic, bigflow employs a verification system which checks classification outcome.
Finally to provide easier updates to the system, Bigflow makes usage of stream learning algorithms, in combination with expert assistance to label rejected events.
Additionally the paper created MAWIFlow a dataset with real intrusion data, which was used to verify Bigflow's results. 