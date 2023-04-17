# Wireless sensor networks

3 types 
- WPAN - Wireless Personal Area Network -> used in Bluetooth
- WLAN - Wireless Local Area Network -> used in WiFi
- WMAN - Wireless Metropolitan Area Network

in WSN, we have a wireless network where the nodes are sensors which monitor specific environment conditions.
Unlike the other network types, these don't have a specific topology

The nodes are composed of 3 components
- Low cost computer
- Controllers for environment conditions
- Radio to transmit data to the outside

# WSN Characteristics

These network are usually small size, low cost and with a big number of nodes
Have constraints in energy, computation and communication

## Nodes

This implies that our nodes will have low power CPU, and a radio with low bandwidth and range
The ad-hoc deployment implies that there is no maintenance or battery replacement

This makes it so that our network be composed of a large number of self-organising nodes, that are randomly deployed.
They must work to communicate in a nearest neighbour communication
And must take into consideration the fragility and fallibleness of wireless networks

## Ad-Hoc

While these networks have a lot of similarities with ad-hoc networks, considering the nodes organise into a infrastructure-less network.

The main differences come from
- Sensing and data processing are crucial
- More node density
- Cheap Hardware
- Energy constraints
- Static nodes
- Many-to-one communication rather than peer-to-peer

## Lifetime

Nodes are battery powered, are not meant to last forever
The nodes must be as power efficient as possible
The nodes lifetime is crucial


## Scalability and Reliability

For a WSN to be scalable and reliable it should
- Self-Configure - Accepts topology changes
- Maintain configurability - Base station has connection with all nodes
- Ensure coverage - All relevant phenomena are observed

## Data Collection

3 main types of data collection
- Centralised - Puts extra burden of nodes close to the centre
- Clustering - Data from groups is fuzzed
- Often - Getting data from nodes which haven't changed, is less important

Leads to some security problems

## Power supply

AAA or AA batteries usually (Duracell)
Rechargeable would work but who does the recharging
Solar cells depend on application

# Design Challenges

## Heterogeneity
There can various types of device deployed in the network

## Distributed processing
The algorithms might be centralised, but the processing needs to be distributed

## Low Bandwidth
There should be efficient communication between nodes

## Large Scale Communication
The sensors need to communicate with each other

## Utilisation of Sensors
Sensors should try to maximise performance while minimising energy usage

## Real-time Communication
The computation should be done in real-time, or as quick as possible