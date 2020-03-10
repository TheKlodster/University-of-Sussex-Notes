# Transport Layer

#### Transport Services and Protocols
- Provides logical communication between applications running on different hosts.
- Transport protocols run in **end systems**.
	- *Send Side* : breaks app messages into segments, passes to network layer.
	- *RCV Side* : reassembles segments into messages, passes to application layer.
- More than one transport protocol is available to applications.
	- Internet : TCP & UDP.

**Network Layer** : logical communication between hosts. <br>
**Transport Layer** : logical communication between processes.
	- relies on network layer services.

#### Internet Transport Layer Protocols
- Reliable, in order delivery : **TCP**
	- congestion control.
	- flow control.
	- connection setup.
- Unreliable, unordered delivery : **UDP**
	- no-frills extension of "best-effort" IP.
- Unavailable services :
	- delay guarantees.
	- bandwidth guarantees.

### Multiplexing / Demultiplexing
--------------------------------------------------
**Multiplexing at Sender** : handle data from multiple sockets, add transport header (used for demultiplexing) <br>
**Demultiplexing at Receiver** : use header info to deliver received segments to correct socket.

#### Demultiplexing
- Host receives IP datagrams
	- each has source IP address, destination IP address.
	- each carries one transport-layer segment.
	- each has source, destination port number.
- Host uses IP addresses & port numbers to direct segment to appropiate socket.

#### Connectionless Demultiplexing : UDP
- Check destination port # in segment.
- Direct UDP segment to socket with that port #.

<img src="https://cf2.ppt-online.org/files2/slide/d/dFNZvcijg9rLaJQEwCnT5sz6IqAkftHW4RhUGX/slide-9.jpg">

#### Connection-Orientated Demultiplexing :TCP
- 4-Tuple TCP socket :
	1. *source IP address*.
	1. *source port *.
	1. *destination IP address*.
	1. *destination port #*.
- Receiver uses **ALL 4** values to direct segment to the appropiate socket.

<img src="https://cf2.ppt-online.org/files2/slide/d/dFNZvcijg9rLaJQEwCnT5sz6IqAkftHW4RhUGX/slide-11.jpg">

### UDP : User Datagram Protocol
--------------------------------------------------
- "bare bones" Internet Transport Protocol.
- "best effort" service. UDP segments may be:
	- lost.
	- delivered out-of-order app.
- *connectionless* :
	- no handshaking between UDP sender & receiver.
	- each USP segment is handled independently.

#### UDP Uses
- streaming multimedia apps (loss tolerant, rate sensitive).
- DNS.
- SNMP.

#### Reliable Transfer over UDP
- add reliability ad application layer.
- application-specific error recovery!

<img src="https://cf2.ppt-online.org/files2/slide/d/dFNZvcijg9rLaJQEwCnT5sz6IqAkftHW4RhUGX/slide-15.jpg">


#### UDP Checksum
Goal : detect errors (e.g. flipped bits) in transmitted segment.

**Sender** :
- treat segment contents, including header fields, as sequence of 16-bit integers.
- checksum: addition (one's complement sum) of segment contents.
- sender puts checksum value into UDP checksum field.

**Receiver** :
- compute checksum of received segment.
- check if computed checksum equals checksum field value :
	- **NO** - error detected.
	- **YES** - no error detected.
	- However, **DOUBLE ERROR?** = CORRECT when it isn't.

Example : add two 16-bit integers <br>
<code> 1110011001100110</code> <br>
<code> 1101010101010101</code> <br>

<code>11011101110111011</code> Wraparound  <br>

<code> 1011101110111100</code> Sum<br>
<code> 0100010001000011</code> Checksum <br>

Note : when adding numbers, a carryout from the most significant bit needs to be added to the result.

### Principles of Reliable Data Transfer
--------------------------------------------------
Important in application, transport and link layers! <br>
Characteristics of unreliable channel will determine complexity of reliable data transfer protocol (rdt).

#### rdt2.0 : channel with bit errors
- Underlying channel may flip bits in packet.
	- checksum to detect bit errors.
- The question : how to recover from errors?!
	- **Acknowledgements** : receiver tells sender that packet received OK.
	- **Negative Acknowledgements** : receiver tells sender that packet received had errors.

#### Flaws with rdt2.0
- If it is corrupted, the sender doesn't know what happened at the receiver.
	- can't just retransmit the data : possible duplicate.

But we can handle the duplicates :
- sender retransmits current packet if ACK/NAK corrupted.
- sender adds *sequence number* to each packet.
- receiver discards duplicate packet.

Also known as a **STOP AND WAIT** protocol.
- Sender sends one packet, then waits for receiver response.

#### rdt2.2 a NAK-free protocol.
Same functionaity as rdt2.1, but using ACKs only.
- Instead of NAK, receiver sends ACK for last packet received OK.
	- sending the sequential # of the packet.
- Duplicate ACK at sender results in the same action as a NAK : retransmit current packet.

#### rdt3.0 : channels with errors *and* loss
New Assumption :
- underlying channel can also lose packets (data, ACKs).
	- checksum, seq. #, ACKs, retransmissions - will be of help but not enough.

The Approach :
- sender awaits a "reasonable" amount of time for ACK.
	- retransmits if no ACK received in this time.
	- if packet (or ACK) is delayed :
		- retransmission will be a duplicate, but seq # will handle this.
		- receiver must specify seq # of packet being ACKed.
	- requires countdown timer.


Performance : rdt3.0 is correct, but performance stinks! **STOP AND WAIT** is why it's so slow! When we send a packet, we sit and sleep, doing nothing until we have received the ACK.

### Pipelined Protocols
--------------------------------------------------
#### Pipelining
Sender allows multiple, yet-to-be-acknowlegded packets.
- Range of sequence numbers must be increased.
- Buffering at sender and/or receiver.

Two generic forms of pipelined protocols : **go-Back-N** and **selective repeat**.
