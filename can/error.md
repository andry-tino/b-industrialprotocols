# Error management

CAN is known for its robustness. Given the protocol specification, it is very unlikely for an error not be detected, thus making the network robust and highly reliable. Here we resume and detail the most important error management features of the protocol. 4 features are used by nodes fro detecting errors on transmssions:

- [Error detection and Acking](error.md#error-detection-and-acking)
- [Wrong frame format](error.md#wrong-frame-format)
- [Bit monitoring](error.md#bit-monitoring)
- [Bit stuffing](error.md#bit-stuffing)

### Error detection and Acking
Frames have a 15 bit field which is a [CRC](https://en.wikipedia.org/wiki/Cyclic_redundancy_check) of the frame from SOC until _Data_ (basically all the frame up until the CRC field, which is not included fo course). This enables detection of errors in transmission. 

1. The transmitter sends a frame with the CRC computed by it: $$C_{\text{TX}}$$.
2. So does the receiver when receiving the _CRC Delimiter_, so $$C_{\text{RX}}$$ is computed.
3. The receiver then computes both of them and checks they are the same: $$C_{\text{RX}} = C_{\text{TX}}$$?
4. If yes, no problem. If the equality is negative, then the receiver will not override then _ACK Slot_ bit with a dominant value (`0`), thus notifying the transmitter that the frame was not successfully sent.

### Wrong frame format
The frame has some key control bits. The reserved bits and the delimiters are an example. When they do not have the expected recessive (`1`) level, the receiver will generate an error.

### Bit monitoring
When a transmitter sends a frame, it always monitors the value on the bus:

- **Binary countdown** When sending the _Arbitration_ field, the transmitter checks that the value corresponds on the bus. If that does not happen, the transmitter knows that he lost the contention and stops the transmission.
- **Acking** When sending the _ACK slot_ field, the transmitter checks the value on the bus to become dominant (`0`). In case it does not happen, he knows its frame was not properly received and he will need to send it again.
- **Bitstream validity check** For the remaining fields of the frame, the transmitter will check that the value on the bus is the same as the value he transmitted. If that does not happen, an error is generated.

### Bit stuffing
[Bit stuffing](phy-enc-sync.md#bit-stuffing) is performed on all fields of the frame until CRC. This ensures that the bus is consistent. Every node reads the bitstream on the bus from SOC to CRC and if it encounters a sequence of 6 or more consecutive dominant or recessive frames, it generates an error.

## Error frames
Nodes, when generating errors, will send error frames. However 2 strategies are considered:

- **Delayed** When an error is computed on the CRC, the station will wait for the _ACK delimiter_, then it will start sending the error frame. This is done in order to allow a data frame to be successfully transmitted.
- **Immediate** For every other type of error, the error frame is sent immediately. If it is an _Active Error Flag_, this will cause all nodes to transmit the same and the bus will enter an error state, thus whatever transmission was going on is drastically interrupted.

**Important** Remember that the ACK field is used only for errors on the CRC field.

---

CAN, with all its transmission checks, is one of the most robust protocols in industrial networks. 

> It has been calculated that the probability of an unmanaged error on the CAN bus is extremely low.

## Bubble idiot
Even though a lot is done to avoid unexpected conditions on the bus, there is a possible occurrance from which the protocol does not implement any protection shielding.

It can happen, because of a whatever error condition on the node, that it starts emitting a continuos infinite dominant stream on the bus. This condition is known as _Bubble idiot_ and CAN cannot do anything about it. That is why an external component is employed: the **bus guardian**. 

Bus guardians are separate units which can be connected with nodes and separate them from the bus. The bit stream sent by the node is always inspected by the guardian, so if the guardian detects something is wrong on the stream sent by the station, it will disconnect it and save the bus. Bus guardians are deployed per node, one each!

## Fault confinement
Thanks to the way CAN handles errors, every station operates in 3 states: _Error-Active_, _Error-Passive_ and _Bus-Off_ which we have already described. This mechanism is able to protect the bus from nodes which are not behaving fine. If a node eventually enters the _Bus-Off_ state, it will be forcibly disconnected from the bus in order to avoid doing any harm.

This fault confinement handling mechanism is implemented in the MAC sublayer into a unit called **Fault Confinement Unit** (FCU). It is into this unit that the [REC and TEC counters](frame-error.md#error-states) are saved.
