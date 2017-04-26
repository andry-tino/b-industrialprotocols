# Network structure

CAN presents some interesting networking characteristics. We will analyze the structure of the network and the protocol.

## Protocol stack
CAN, differently from other standards, does not present an application layer as part of the standard. The layers covered by that are (from bottom to top):

1. The physical layer, consisting in a shared bus. The standard covers the bus technology and the CAN tranceivers and connectors.
2. The Data Link Layer (DLL) also regarded to as: _CAN controller_. It has a sublayer division:
    - MAC sublayer, responsible for arbitrating the access to bus.
    - LLC (Logical Link Control), responsible for providing the services to upper layers.

### Topology
The only topology supported by the protocol is the shared bus. All nodes are connected to the same wired segment and the controller in each device will handle the bus arbitration.

One very important thing to notice in CAN is the absence of a centralized arbitrator. Other standards usually employ one special device (e.g. [Profinet](../ert/profinetio.md) and [EPL](../ert/epl.md)) which acts like a coordinator, granting access to the links to each controlled device. This does not happen in CAN which takes advantage of a **distributed control** strategy.
