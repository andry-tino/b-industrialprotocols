# Advantages and disanvantages of CAN

CAN is a very good protocol, but it presents very string points and drawbacks as well.

## Advantages
CAN represented a revolution when first introduced, some of the reasons are the following:

- CAN is simpler and more efficient than a token based access scheme.
- CAN is more flexible than Time Triggered medium access based protocols and promotes composability. Stations can be attached and detached from the channel with no need to reconfigure the network.
- It is distributed, no need of a centralized authority. So it is simpler.
- Less delays due to collisions. CAN handles collisions in a way that we actually have throughput even during collisions thanks to the AND arbitration on the bus and thanks to the _Binary countdown_ frame arbitration scheme.

Among all these things, we need to consider some important aspects of the protocol:

- CAN **is not preemptive**. A lower priority frame can still block a higher priority one if it accessed the bus before. However since the frames are very lightweight (no more than 8 actual byte of payload), the non-preemption does not impact so badly.
- CAN is very responsive thanks to its properties. Tus it is used a lot in real-time contexts even though it offers a low bandwidth.
- Priority assignment via IDs is crucial for real-time requirements to be met in a network.**Most urgent messages should be assigned with lowest identifiers**.

## Disadvantages
CAN also presents some issues:

- Synchronization of stations is crucial because the arbitration technique heavily relies on that.
- Signal propagation must be guaranteed in certain times. Given the arbitration mechanism, signal must be able to propagate from one end of the bus to the opposite and come back before the same node samples the channel to get the acquired value by the bus. **Propagation delay must be kept under control**.

About the propagation delay $$\delta$$, we need to make it clear that this quantity measure the time needed for the signal to traverse the bus from one end to the other.

> The sampling point is located roughly at the center of each bit.

In order for the acquired value on the bus to be properly read by the transmitting node, the signal must have time to propagate to the other end of the bus ($$\delta$$) and come back again (one more $$\delta$$). This time has to be lower than half of the time spanned by one bit $$\tau_b$$:

$$
2 \delta < \frac{\tau_b}{2} \iff \delta < \frac{\tau_b}{4}
$$

> The propagation time must be lower than one quarter of the bit transmission time in order to have effective arbitration.

For this reason, we have that the CAN bus is limited in length by the desired bandwidth as explained in chapter [Bus characterization](phy-bus.md).
