# Realizartion on Top of Ethernet

This realization creates a separation between the real-time and the non-real-time traffic, enabling the former to bypass the DLL and reach Ethernet, thus prioritizing real-time traffic.

![Visualization of realization On Top of Ethernet](../assets/on-top-of-ethernet.png)

The most important thing we must notice is the absence of any alteration of the Ethernet hardware. However this architecture requires some changes to be performed at Application and DLL levels.

**Pros**

- No hardware modification.
- Modifications in the protocol stack are not massive.
- Better time-critial traffic handling.

**Cons**

- Due to requirements on delivery time, it is necessary to apply a dimensioning effort in order to calculate the number of switches in the network.

## Ethernet encapsulation
In order to avoid altering the hardware of devices, the use of Ethernet with a different stacked protocol on top of it is possible by means of the [EtherType](https://en.wikipedia.org/wiki/EtherType) field in the Ethernet frame.

**Important** Remember that in case of non-real-time traffic the Ethernet layer will encapsulate a TCP/IP or UDP/IP packet. In case of real-time traffic though, the encapsulated packet will belong to a different protocol.

The _EtherType_ field helps us in making sure two different higher protocols can be used for transmissions.

### Field definition
This 2-byte field is defined in [Ethernet II](https://en.wikipedia.org/wiki/Ethernet_frame#Ethernet_II) frames (the most commonly used today) and is used to specify which upper-layer protocol