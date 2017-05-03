# FlexRay

In 1998 an analysis driven by BMW over the many protocols employed in automotive showed that current networking technologies were not enough to serve future generations of cars, especially when considering X-by-wire.

In order to cope with more demands for automotive, the [FlexRay Consortium](https://en.wikipedia.org/wiki/FlexRay) was created and the FlexRay protocol was created a few years later targeting the following requirments:

- Deterministic media access scheme
- Scalability
- Performance
- Bandwidth
- High redundancy for better error handling
- High reliable fault management with reporting to application

## Network structure
FlexRay operates with the following basic characteristics:

- Bandwidth up to 10 Mbit/s.
- Payload data up to 256 bytes.
- Modified [TDMA](https://en.wikipedia.org/wiki/Time-division_multiple_access) channel access arbitration mechanism.

The protocol targets the **Powertrain** and **Chassis** function domains and is going to become the de-facto standard in many automotive systems effectively replacing [CAN](../can/intro.md).

Its first adoption was in 2008 when BMW employed the protocol in one of his models using a bus network.

### Network design
The protocol provides ECUs that can be interconnected on a wired network which can be shaped into **many different supported topologies**, the most common being the bus. 

![FlexRay network structure](../assets/flexray-net.png)

All ECUs include:

- An interface with the upper layers (the host).
- An integrated Communication Controller (CC) providing communication services and connected to the physical layer through many ports (via different BDs).
- A Bus Guardian (BG) can be integrated into BDs.
- One or more Bus Drivers (BD) providing access to different channels on the physical layers (one driver per channel).

The host can access communication services via the CC. This component employs ports to connect to the physical layer; actually each port from the CC is connected to a BD which regulates the access to one single channel. It means that transmissions can be sent to different channels.

![FlexRay controller structure](../assets/flexray.png)

### Redundancy handling
FlexRay makes redundancy a core feature and allows different configurations:

- **Single channel** CCs are all connected to the single channel via one single port.
- **More channels** CCs are connected to many channels via one port per each. CCs choose on which channel routing the frame. Since more channels can be used to transmit different frames at the same time, the total bandwidth can be increased depending on the number of independent channels $$n$$: $$B = n \cdot b$$ (where $$b$$ is the bandwidth of each channel).
- **More redundant channels** CCs may use 2 channels to send the same frame at the same time. This is a **space redundancy** allowing the protocol to be robust in case the transmission on one channel fails.
- **Time redundant channels** CCs can decide to send the same frame on the same channels (at the same time) twice after a certain delay.  The employment of **time redundancy** or **time/space redundancy** is an option to guarantee that a frame arrives at destination with extremely low fault probability.

## Medium access
A modified TDMA is employed and it is called: _Flexible Time Division Multiple Access_ (FTDMA), also known as _Minislotting_. As every TT-based approach,  a transmission cycle controlled by the master, called _Communication Cycle_ is to be considered and in the context of that cyckle, all frame exchanges are orchestrated by the master itself.
