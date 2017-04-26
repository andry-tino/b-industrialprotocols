# Physical layer

CAN was one of the first protocols to be extremely robust and reliable in the world of Industrial Automation. It was the first protocol to employ a distributed coordination on a bus with extremely high levels of fault tolerance and error handling. What makes it special is the technology behind the transmissions on the bus.

## Collision handling
The way CAN handles collisions is unique. Let's take for example the collision management in IEEE 802.3: [CSMA/CD](https://en.wikipedia.org/wiki/Carrier-sense_multiple_access_with_collision_detection). This protocol allows stations to listen on the bus, if free, stations will start transmitting. Collisions can be sensed, when a station senses a collision, it stops and then retries later with a certain probability, stations compute random values of waiting intervals before retrying to transmit in order not to collide again. What's wrong with this model?

1. **Data loss** Data is lost. Both frames, after collision, are lost and could not be read as transmissions occur directly on the Ethernet link.
2. **Latency** Because of data loss, it is necessary to re-transmit, this makes the frame delivery time longer.

CAN is able to tackle both problems by employing a collision handling which is **Non destructive**. Arbitration is performed on each single bit of the frame. The bus is AND arbitrated, it means that if two stations simultaneously send two values, a collision will not happen, but the logic AND will be computed between them. 

> Given the collision handling mechanism of CAN, an electric collision will never happen on a CAN bus. However, to indicate that different bits were transmitted and only one survived, we will use the term _collision_ to indicate a collision on data.

So if the stations send the same value, no collision will occur, however if two different values are sent, the station who sent the low level wins.

> CAN associates a higher priority to low-level electrical signals.

### Contention management
How can a collision be handled? Every station which transmits a value on the bus will also simultaneously read the value on the bus. If a different value compared to the one being sent is read, then the node knows a collision occurred. Actually, stations sensing a collision on the bus are those who lost the transmission contension.

Let's make an example. One station transmit a high value, and another one a low value. Since the bus is AND arbitrated, the one who sent the low signal will read low on the bus so it will not detect a collision. But the other station will as it sent a high level and sensed a low level on the bus.

> Given the AND arbitration on bus, CAN is able to handle and solve collisions without data loss and latency. Other protocols typically try to avoid collisions!

### Bus arbitration protocol
The protocol we have just described, implemented by the MAC layer of CAN, is a modification of [CSMA](https://en.wikipedia.org/wiki/Carrier-sense_multiple_access) called: _CSMA-BA_ (Bit-by-bit Arbitration) or also _CSMA-CR_ (Collision Resolution).

With this mechanism also note that CAN ensures a distributed collision handling. There is no need to employ a bus arbitrator for accessing the bus and this is a feature which is actually intrinsic in CSMA!

## Standardization
CAN has been standardized into [ISO 11898](https://www.iso.org/standard/63648.html). 

- Section ISO 11898-1 of the document covers the features of the physical layer.
- Sections ISO 11898-2 and ISO 11898-3 cover the specifications of transceivers for high and low speed communications.

## Bus characterization
TODO

## Bit encoding and synchronization
TODO
