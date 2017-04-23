# Realization on Top of TCP/IP

This is the simplest realization to implement for CPs as it does not imply any modification at any level of the protocol stack.

![Visualization of realization On Top of TCP/IP](../assets/on-top-of-tcpip.png)

As it is possible to see, both real-time and non-real-time traffic will follow the same flow and interact through DLL protocols in order to transmit data. The protocol stack has no modification.

**Pros**

- It is possible to have almost every device in the network remotely available if needed.
- Full remote control of the factory.
- The network can extend and scale easily to all parts of the world if necessary.
- Easy to deploy.
- It is possible to use all Internet based features distributed by 3rd-party manufacturers with affordable solutions.

**Cons**

- Traffic handling is not deterministic at all.
- Efficient handling of traffic from timing point of view requires a lot of resources and memory.
- Can support very loose time requirements.

## Case study: Modbus TCP
[Modbus TCP](https://en.wikipedia.org/wiki/Modbus) corresponds to CP 15/1 and 15/2. 

Profile 15/1 was initially defined by [Schneider Electric](http://www.schneider-electric.com/) and is one of the most widely used On Top of TCP/IP realizations in industrial applications today.

**Class** Modbus fulfills the requirements for [Class 1](pi.md#low-speed-class) in IEC 61784.

### Capabilities
Modbus 15/1 iis very simple client/server protocol and implements services for reading and writing data objects. The end user must extend the services with its own specific readers and writers. The DLL protocol being used is TCP/IP.

### Profile 15/2
Later, the same manufacturer extended the protocol and profile 15/2 was introduced. This profile adds support for real-time traffic handling by using the [Real Time Publisher Subscriber (RTPS) protocol](https://en.wikipedia.org/wiki/Data_Distribution_Service) providing 2 main communication models over UDP/IP:

- **Publish-Subscribe** Tgis protocol transfers data from publishers to subscribers. The protocol allows subscribers to define parameters like _Max reception rate_, _Data persistence_ (time validity) and _Data strength_ (priority).
- **Composite State Transfer (CST)** This protocol transfers state information from a writer to a reader.
