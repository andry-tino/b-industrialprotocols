# Priority management & addressing

We now describe a very important aspect of the CAN protocol with regards to bus arbitration.

It is very common, especially in [Fieldbus](../rte/iec.md#iec-61784), to find arbitration mechanisms based either on priorities being assigned to stations, or on bus access granting strategies relying on a central coordinating node. 

CAN does not apply any of these policies in order to grant permission on the bus. By employing [CSMA-CR](phy-collision.md#) by means of [AND arbitration](phy-collision#contention-management), CAN is simultaneously capable of:

- Arbitrating the bus.
- Assigning priorities for transmissions.
- Avoiding data loss and latency on collision, thus improving throughput.

## Addressing
In CAN, there are no addresses and there is no addressing. Nodes basically write content by producing it and they also consume content. CAN is all based on this **producer/consumer** mechanism where everything is **data centric**.

Then how can messages reach the proper destination? Remember that CAN is a bus, so every frame sent on it is basically a broadcast message which is receiveable by all other nodes on the medium. The basic flow is the following:

1. One station is either typically responsible for a certain quantity or needs to consume values in order to perform a controlling task.
2. Nodes which can send values of variables are producers. Nodes which only read variables are consumers. It is also possible to have nodes being both producers and consumers.
3. When a quantity is updated, the producer will need to send on the bus, thus it sends the message with the updated value of that variable. The message will have an **identifier** which uniquely identifies that variable.
4. Once on the bus, all nodes will read the variable ID. All consumers which are interested in that variable will consume the value, otherwise the message will be discarded.

So, by using IDs on every message identifying variables being produced, CAN can avoid using addresses. All messages are always sent broadcast.

## Priority handling and bus arbitration
CAN's revolution resides in the fact that:

> When 2 frames are sent at the same time, a collision will happen, but a transmission will still occur. 

We have learnt that CAN performs an [AND arbitration](phy-collision.md#contention-management) on the bus by giving priority to dominand (D) values. Now let us consider two different frames and let us imagine that they are both sent, at the same time, from 2 different nodes on the bus. Always remember that:

> Transmissions occur bit by bit and stations are synchronized to receive 1 bit while being sent by different stations (stations can collide, but one value will be written on the bus).

As the 2 stations send, at the same time, the frames, collisions might occur:

- Best case scenario, both frames have the same value, so the bus will have the value of both frames being transmitted and everything is ok. 
- As soon as the $$k$$th bit is read, the 2 nodes will write different values on the bus (this must happen as the frames are supposed to be different by hypothesis). So the dominant value will win.

At this point, when the $$k$$th frame is being transmitted, the stations will actually know that a collision has occurred as **stations always read the bus after transmitting something**.

### Transmission protocol
When we reach the condition of detecting a collision we must remember that this detection occurs only on the station who lost the contention! The station which won the contention on the $$k$$th bit, will not feel anything as it read the same value being written.

> When a station detects a collision it knows it lost the contention on the bit for the frame it is transmitting. Thus it stops its transmission, letting the other station continue with its own.

### Content-based priority
Thanks to this mechanism, priority is basically given to the station sending the frame with a higher number of dominant bits in the initial part of the frame (from head to tail). Which rephrased is:

> CAN assigns priority to frames. The more dominant bits a frame has, from its head to its tail, the higher its priority will be.

The priority can be calculated by converting the bitstream of a frame (on the bus) into a number. Remember that CAN inverts the bittream since dominant values are codified as low levels on the bus. Thus, the frame whose numeric conversion is lower gets higher priority.

This process is called: _frame contention mechanism_ as it considers the whole frame, not to be confused with the contention on each single bit.

### An example
Consider 2 frames:

```
A = DRRDDRDR => 01100101
B = DRRRDRRR => 01110111
```

We are showing the bitstream before and after transmission on the bus. Let's consider they are sent at the same time:

1. $$k=1$$: `A[k] = 0` and `B[k] = 0`. They are the same value on the bus, no collision.
2. $$k=2$$: `A[k] = 1` and `B[k] = 1`. They are the same value on the bus, no collision.
2. $$k=3$$: `A[k] = 1` and `B[k] = 1`. They are the same value on the bus, no collision.
2. $$k=4$$: `A[k] = 0` and `B[k] = 1`. `A` wins as the AND resurns `0`, the station feels nothing. `B` reads `0` on the bus when it was sending `1` so it understands that another station won the contention. `B` stops the transmission and waits for the current frame being transmitted to be done.

If we convert the 2 frames into decimal numbers by considering the leftmost bit the MSB (Most Significant Bit):

$$
A = 1 \cdot 2^0 + 0 \cdot 2^1 + 1 \cdot 2^2 + 0 \cdot 2^3 + 0 \cdot 2^4 + 1 \cdot 2^5 + 1 \cdot 2^6 + 0 \cdot 2^7 = 101
$$
$$
B = 1 \cdot 2^0 + 1 \cdot 2^1 + 1 \cdot 2^2 + 0 \cdot 2^3 + 1 \cdot 2^4 + 1 \cdot 2^5 + 1 \cdot 2^6 + 0 \cdot 2^7 = 119
$$

We can see that `A` has a higher priority because $$A < B$$!

## The role of the _Identifier_ field
Every frame in CAN starts with a field called _Identifier_ which is the identifier of the variable whose value is being transmitted (or, to be more precise, whose value is matter of interest of the frame). 

The frame contention (not the bit contention) occurs only on this field. Typically, different frames have different identifiers as they represent different variables. So as the concurrent transmission goes on, the collision detection will occur not after the last bit of the identifier field is sent. This mechanism is called: _Binary countdown_.

### Priority and producer/consumer
As a note, it can happen that 2 frames with the same identifier are sent, so they will represent the same variable, however we will see in later chapters that a bit flag later in the frame indicates if the frame contains the value of the variable or is just a request for that variable. Of course the protocol will set the flag to `0` in the former case so that producing is prioritezed on consuming.
