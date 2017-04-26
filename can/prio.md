# Priority management & addressing

We now describe a very important aspect of the CAN protocol with regards to bus arbitration.

It is very common, especially in [Fieldbus](../rte/iec.md#iec-61784), to find arbitration mechanisms based either on priorities being assigned to stations, or on bus access granting strategies relying on a central coordinating node. 

CAN does not apply any of these policies in order to grant permission on the bus. By employing [CSMA-CR](phy-collision.md#) by means of [AND arbitration](phy-collision#contention-management), CAN is simultaneously able to:

- Arbitrating the bus.
- Assigning priorities for transmissions.

## Addressing
TODO

## Priority handling and bus arbitration
TODO