# Realizations of RTE

There are 3 typical possible architectures which can be used in order to target different requirements. Typically we have a differentiation by delivery time, but other PIs can be associated to each of the recomended architectural approaches.

- [On Top of TCP\IP](top-tcp-ip.md): Both real-time and non-real-time traffic flows pass through TCP/IP or UDP/IP.
- [On Top of Ethernet](top-ethernet.md): Non-real-time traffic passes through TCP/IP or UDP/IP protocols, while real-time traffic will bypass higher layer protocols and go straight to Ethernet.
- [Modified Ethernet](top-tcp-ip.md): Non-real-time traffic can be fed to TCP/IP or UDP/IP, while real-time traffic will always go straight to the Ethernet layer which is a modified one.

## Realizations vs PIs
Each architecture is implemented by a CP and fulfills certain requirements. In the case of delivery time, a typical association is:

| Class | Name | Realization |
|:-----:|:----:|:-----------:|
| [Class 1](pi.md#low-speed-class) | Low speed | [On Top of TCP/IP](top-tcp-ip.md) |
| [Class 2](pi.md#process-control-class) | Process control | [On Top of Ethernet](top-ethernet.md) |
| [Class 3](pi.md#motion-control-class) | Motion control | [Modified Ethernet](mod-ether.md) |