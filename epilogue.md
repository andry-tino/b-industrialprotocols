# Summary of protocols

We have examined some protocols, following is a summary of the most important characteristics about them:

| Protocol | Access method | Synchronization | Comm. model | Topology |
|:---------|:-------------:|:---------------:|:-----------:|:--------:|
| [Modbus](rte/top-tcp-ip.md) | [CSMA-CD](https://en.wikipedia.org/wiki/Carrier-sense_multiple_access) | N/A | [P2P](https://en.wikipedia.org/wiki/Peer-to-peer) | Any |
| [Ethernet PowerLink](rte/epl.md) | [TDMA](https://en.wikipedia.org/wiki/Time-division_multiple_access) | Clock, Master polling | Master/slave | [Bus](https://en.wikipedia.org/wiki/Bus_network) |
| [Profinet IO](rte/profinetio.md) | TT-Switch, [TDMA](https://en.wikipedia.org/wiki/Time-division_multiple_access) | Modiefied [IEEE 1588](https://en.wikipedia.org/wiki/Precision_Time_Protocol) | Master/slave | Daisy-chain, ring |
| [CAN](can/intro.md) | Binary countdown | Clock | [P2P](https://en.wikipedia.org/wiki/Peer-to-peer) | [Bus](https://en.wikipedia.org/wiki/Bus_network) |
| [LIN](automotive/lin.md) | [TDMA](https://en.wikipedia.org/wiki/Time-division_multiple_access) | Clock | Master/slave | [Bus](https://en.wikipedia.org/wiki/Bus_network) |
| [FlexRay](automotive/flexray.md) | FTDMA | Clock | Master/slave | [Bus](https://en.wikipedia.org/wiki/Bus_network) |
