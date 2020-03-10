# Introduction : Lecture 1

Coursework
--------------------------------------------------
- **Assignment 1** : Week 7 - programming transport layer.
- **Assignment 2** : Week 11 - socket programming.
-------------------------------------------------

**Internet** - several WANs connected together to form a large connection.<br>
**Protocols** - define *format*, *order* of *messages sent & received* among network entities, and *actions taken* on message transmission and receipt.
- Components of the internet:
	- Hosts
	- Communicaiton Links
	- Packet Switches
	- Interconnected ISPs
	- **Protocols** control sending & receiving of messages: *TCP*, *IP*, *HTTP*...
	- Internet Standards.

Loss & Delay
--------------------------------------------------
Packets *queue* in router buffers:
- packet arrival rate to link temporarily exceeds output link capacity.
- packets queue, wait for turn.

#### Four sources of Pack Delay
1. **Processing Delay** - the time it takes for the packet to decide which queue to join.
1. **Queueing Delay** - the time it waits in the queue for the transmission.
1. **Transmission Delay** - the length of the packet/link bandwidth. 
1. **Propagation Delay** - the distance between the link: i.e. the time it takes to cross that distance.

The **Nodal** delay d<sub>nodal</sub>  is the total sum of time of the delay of:

```
d<sub>nodal</sub> =  d<sub>process</sub> + d<sub>queue</sub> + d<sub>transmission</sub> + d<sub>propagation</sub>
```

#### Packet Loss
- Queue has finite capacity.
- Packet arrives to a full queue - aka it is lost.
- Lost packet may be *retransmitted* by:
	- previous node,
	- source end system,
	- not at all.

Throughput
--------------------------------------------------
**Throughput** : rate (bis/time unit) at which bits transferred between send/receiver.
- **instantaneous** : rate at given point in time.
- **average** : rate over longer period of time.

*Bottleneck Link* - link on end-to-end path that constraints end-to-end throughput.
