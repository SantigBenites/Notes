
# BigFlow: Real-time and reliable anomaly-based intrusion detection for high-speed networks

# Introduction

Most attacks n our days make usage of the quantity of data tranversing the intenet to hide themselfs
Prevosly, the usage of hadoop based clusters was aproached, but never applied in reality beacuse of effiency
Current approaches to netowkr traffic and measurement usualy use unsupervised ML, however beacuse of the size of the data, supervised ML should be considered
However, considering we are using realtime systems, and that ML models cant easily be retrained, these models tend to lose accuracy overtime with the presensce of new attacks
In this paper we will analyse the accuracy loss of ML classifiers overtime, in average of 23% over a year
Noramly to keep, the model from going out of date, mothly revisions need to be made, with human internvetion from the rebuklding of the model
Wit htis in mind the authors present BigFlow a system for realiable real-time network traffic classification
It posseses 2 main insights
- Make the administrator aware of possible changes that happened in traffic beahaboviour, and not just evalution events as attacks or not, but also realizing new traffic beahvour is happening
- Using streaming tecniques to allow for near-real-time traffic analysis, and to also allow for sistematic updates to the model. Allowing for a better overall performance of the model
In usmmary BigFlow posesses
- Better decetion accuracy with less miscalcifications
- Idenfitcation of new traffic characteristiscs
These 2 culminate in better reliability overitme, and less storage space required

Concluding the paper did
- Provide new dataset for intrusion decteion engines
- ANaluze the performace of traditional ML classificer with the new dataset (and see thir downsides)
- Present Bigflow, a reliable streaming learning instrusion detection engine
- Experiment with bigflow and compare it to other engines

# Background

## Stream Processing

BigFlow makes usage of streaming processing platform for dealing with large volumes of data,
These are platforms which reeive data from registered sources and compute over said data with usage of processing elemtents
The near realtime processing in such platforms is achieved by keeping each PE as small as possible, and by trying to paralelizae PE's as much as possible

## ML for intrusion detection

There exist 2 types of appraoches detect intrusions in a netowrk
- sginature based
- anomlay based
While the first one requires lots of sginutres to attacks, that might not even be useufell agsasint small variants of the attack
The second one is more used in prtacite when combined with ML, this leads to 2 branches
- Unsuppervied - which is simpler but reutls in false positives
- Suppervised - Requreirs expensive procesees, like the traiining stage, but it is more accurate
When using ML ofr intrusion detection, we turn the flow of the traffic into a aseta of features, and serach for anomalies in those feautres to detect and attack
Unfortinately, general purpose networks seldom exibit stable patterns, this combined with the dificulty of using ML models in realtime development, leads to thies process being uneasible for most high speed netowkrs
This makes way to stream lernaing algotyhms, that update models with new entries insted of training a whole new model

# MAWIFlow

To benchmark ML-based NIDS, the authores created MAWIFlow, with record collected over a year
The main chalenges to build a dataset like this were
- Realism - The dataset needed to be obtained from real sources
- Validity - The netowkr traces used neeed to be collected  from real netowkr traces, and needed to be sanitized for sensitive data
- Prior Labelling - The events on the dataset needed to be properly identified
- High Variability - Having a long period of recording so that the data could be evaluted with high varaiblioty of data types
- Reproducibilty and Public Avalilabiluty - The netowkr traces neeed to from from public sources, and the source code needed to be publiccaly avialable

## Accuracy degradation of ML classifiers

The main foal if this analysis will be to determine if ML-based approaches can maintina accuracy overitme, with real netok traffic
In order to test this the authors used 4 diferent model to train 8 ML-based apraoches, and then decied to retrain 4 of the apporaches on a weekly basis with the last week of data, and the other 4 approaches were only trained in the begging of the year once.
The reults conclueded that the ML-Based NIDS that weer onyl trained once had significantly worst results that the weekly trained counterparts, leading to conclusion that retraining models periodically is better for acuracy

# Bigflow

To adress these shortcoming, the authors present BigFlow a reliable stream learning intrusion detection system, whose goal is to maintain high accuracy overtime, while trying to minimize human intervention and stored data,
It works in 2 phases
- Feature Extraction
- Reliable stream learning
In feature extraction we extract features using tradional stream processing framwrok
The reliable stream leraning stage classifies inputs (feature vectors) as normal or attack

## Feature Extraction

The usage of sream processing allows for monitoring of high-speed evolving netowrks, whithou the need to store lots of data.
The feature selection process is done in almost real-time
BigFlow can extract up to 158 features, and considers both flow statistics and host statictics

## Reliable Stream Learning

After network flow computation, it becames possible to Bigflow to classify vectors as normal or attack.
The classifier must be able to cope with changes to the netowkr content and traffic changes over time.
Morevoer, in real systems the model must be updated weekly to cooe with evolving changes

### Setup

Uses a training dataset to start the model
A base classifer is obtained and replicated 
During validation, base rates for attack and not attack are defined to analyse if the model is accurate

### Real time learning

During this process, instances are classified as attack or not attack, with a certain rate of confidence.
If the confidence is above the expected value, this instance is considered in the dataset and used to train the model in realtime
If the confidence is below the expected value, the instance is store until it can be proven the value, if proven the model can now use this isntance to train
Insntaces confimed as attacks are then sent to humans or altenaitve confimation methods to be assured and dealt with apropriatly
This alows for miniaml hiiman intervention, and mitigates false positves and negative alarms
Also minimizes cost in model updates, by not training with all intaces that are rejected.


# Related Work

## Benchmark dataset for IDS

The creation of MAWIFlow presents an alternative to the flawed datasets used to train common IDSes such as DARPA1998
While some work as been done in improving in this area all attempts lack some crucial points
In general, datasets lack upgradability, wrong assumption of immutable network traffic and believe user behaviour can be modeled

## Flow measurement and classification

To anaylise flows some authors used haddop-based network traffic monitoring analysis.
Others implemted anomaly detectors into hadoop atchitectore for netowk monitoring, added with hashing to divide network traffic into splits
However all of this work was for nough considering the complex computations used made this system unusable in high speed network monitoring


# Conclusion

Current aproaches for netowkr traffic classficaiton arent effective in real systems beacuse of desied tjroughput and chaining behaviour
The approach preseted bigflow, was able to perform feature extration and classifcationm and allowed for all of that with simpler computation effort and storage
To maintian reliability against evolving network traffic, bigflow emplys a verification system which checks classifcation outcome.
Finnaly to provide easier updates to the system, Bigflow makes usage of stream learning algoryhtms, in combniation with expert assustance to label rejected events.
Addiotnaly the paper created MAWIFlow a dataset with real intrusion data, which was used to verify Bigflow's results. 