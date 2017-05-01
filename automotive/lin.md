# LIN

[Local Interconnected Network (LIN)](https://en.wikipedia.org/wiki/Local_Interconnect_Network) is a protocol created by a consortium comprising [BMW](https://en.wikipedia.org/wiki/BMW), [Volvo](https://en.wikipedia.org/wiki/Volvo) and [Volkswagen](https://en.wikipedia.org/wiki/Volkswagen) in 1998 targeting the interconnection of units in the **Body** function domain.

LIN was designed to be used in automotive systems, however it was introduced as an alternative to CAN by providing device connectivity services at a lower cost. As a result, LIN is mainly adopted today in **non-safety related systems** as it employs real time handling of messages but with loose time constrains.

## Protocol details
LIN employs a bus topology with the following characteristics:

- Bandwidth up to 20 Kbit/s.
- Payload (data) up to 8 byte.
- Identifiers on 6 bits (up to $$2^6 = 64$$ variables).
- Content based addressing like CAN. 
- Producer/consumer data exchange model (consequence of the previous point).

**Bus arbitration** Differently from CAN, LIN uses a [TDMA](https://en.wikipedia.org/wiki/Time-division_multiple_access) strategy to grant the bus to devices. One special device, the master, is the only active device on the network.

**Frame structure** Frames consist of:

- A header, containing the ID of the variable. Always sent by the master.
- A response part, contaiing the variable length data field.

**Data exchange** The master, by following an offline scheduling table, initiates transmissions:

1. The master sends a frame in broadcast specifying the variable ID whose value is required in the header.
2. The slave producing that variable will reply by filling the response with the variable's value.

**Synchronization** The master synchronizes slaves on his clock by sending the clock itself in the header of every frame.

## LIN/CAN
In order to achieve good levels of interoperability between systems and keep good levels of robustness, different LIN subsystems are often interconnected together using CAN serving as a backbone infrastructure. LIN masters typically have the ability to act like **CAN gateways** so that they can interface with CAN.

In automotive, espacially in the **Body** function domain, CAN/LIN is a common combination. Furthermore, since different LIN subsystems can have different requirements in terms of predictability, CAN is a good choice for interconnecting them as a protocol able to guarantee a robust and reliable transmission of frames gateway-to-gateway between different LIN networks.

## Extra functionalities
LIN offers services to put nodes to sleep and to wake them up. This functionality is extremely important from the **energy consumption** point of view especially in those conditions were the engine is off.
