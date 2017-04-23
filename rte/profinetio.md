# Profinet IO

The [Profinet IO](http://www.profibus.org) protocol appears in CPs 3/4, 3/5 and 3/6 in the the CPF-3 definet in IEC 61784-2. It is vastly used by many manufacturers (including [Siemens](https://www.siemens.com)) and supports highly time-critical applications with strict constraints on delivery time and jitter.

**Class** Profinet IO fulfills the requirements for [Class 3](pi.md#motion-control-class) in IEC 61784.

## Network structure
Profinet IO defines two categories of devices:

- **IO controllers** An Ethernet subnet is controlled by one special device which orchestrates transmissions.
- **IO devices** Devices which might have real-time traffic to send.

All nodes can be arranged into different topologies, though daisy-chain and ring are preferred. It is not necessary to specify which topology one network is using as IO controllers are equipped with [LLDP](https://en.wikipedia.org/wiki/Link_Layer_Discovery_Protocol) which detects the topology automatically.

## Communications
The IO controller defines one communication cycle called: _Sendclock cycle_ into which all transmissions are scheduled.