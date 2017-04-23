# Ethernet PowerLink

[EPL](http://www.ethernet-powerlink.org/) is a protocol defined by [Bernecker & Rainer (B&R)](https://www.br-automation.com). Now the protocol is also part of a standardization group.

## Nertwork structure
EPL defines the following pillars in its architecture:

- **Master/slave scheduling** One single node called _Managing Node_ or MN schedule all transmissions and is the only active station which can autonomously decide to initiate a communication on the channel.
- **Time-slotted scheduling** Time is divided into time slots, thus a [TDMA](https://en.wikipedia.org/wiki/Time-division_multiple_access) is deployed.
- **Shared Ethernet segment** All stations are connected to a shared bus link managed by the MN. Also, all communications are acked (since Ethernet is used).

This communication system is called: _Slot Communication Network Management_.

## Transmission scheduling
The MN acts like a bus arbitrator. All other stations on the shared segment are called _Controlled Nodes_ (or CN) and they can only initiate a transmission upon request by the MN.

Since we have TDMA, synchronization of clocks is necessary in this CP. So all stations are clock-synchronized. The MN signals all CNs the beginning of new communication cycle by broadcasting a _Start-Of-Cycle_ (or SoC) frame.

**Real-time vs non-real-time traffic** The MN ensures that real-time traffic is scheduled in a cyclic phase where it polls every station for transmission and, if one was requested, grants it; on the other hand, non-real-time traffic is handled afterwards in later time slots reserved for non-real-time data.

### Scheduling cycles
Every communication cycle, referred to as: _Isochronous EPL Cycle_, is divided into 4 different periods:

- **Start period** Lasts the time needed to convey the SoC frame (sent in broadcast) to all stations in the shared segment. This period duration should not vary, its duration is extremely connected to the SoC frame which, therefore, has very strict requirements in terms of delivery time and jitter.
- **Isochronous period** Here the MN sends unicast poll request frames to every CN in their respective time slots (defined and handled by the MN itself). Real time traffic is scheduled here.
- **Asynchronous period** Non-cyclic data transmissions are allowed, always supervised by the MN. Here non-real-time trafic is scheduled.
- **Additional idle period** An idle time frame necessary to guarantee synchronization before starting an new cycle.

**MN polling** In the isochronous period, the MN sends (unicast) a _Poll-Request_ (or PReq) frame to every CN. If the polled CN has something to send, it will send a broacast _Poll-Response_ (or PRes) frame on the shared segment. Real time data can flow from one CN to other stations in this way.

**Multiplexed devices** During the isoschronous period, also multiplexed devices are polled. Multiplexed devices are devices which are not polled during every cycle as they share the same time slot with some other device.

#### Acyclic traffic
The asynchronous period is used to transmit non-real-time traffic. To signal all CNs that this period has started, a _Start-Of-Asynchronous_ (or SoA) message is sent broadcast by the MN.

Here, time is still slotted and the MN grants access to the shared segment to one single CN or to itself in order to transmit one single asynchronous message only.

How does the MN know which CN has acyclic data to transmit? Duering the isoschronous period, that CN was supposed to send that information in its PRes after being polled by the MN. 

**Important** EPL prefers using UDP/IP for asynchronous messages. 

## Network design
EPL allows the possibility to connect to the network EPL and non-EPL devices. Of course, non-EPL nodes will use TCP/IP and Ethernet. However this possibility comes with a limitation: 

> It is not possible to have EPL nodes and non-EPL nodes cohexist on the same shared segment.

The limitation comes from the fact that non-EPL nodes, which do not use the EPL upper protocols, will currupt the bus arbitration performed by the MN! Since these nodes have no knowledge of EPL, they will not observe the time slotting performed by the MN.

> However, EPL nodes can perfectly operate as normal Ethernet devices.

In order to overcome this issue, we must avoid mixing EPL and non-EPL devices on the same shared segment. Thus the network is split into more segments by a [router](https://en.wikipedia.org/wiki/Router_(computing\)) or a [bridge](https://en.wikipedia.org/wiki/Bridging_(networking\)), thus making the EPL segment a protected Ethernet.
