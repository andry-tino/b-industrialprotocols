# Implementartions of CAN

There are many protocols based on CAN, 2 however are the most used today:

- [BasicCAN](implementations.md#basiccan) by [Philips](https://en.wikipedia.org/wiki/Philips)
- [FullCAN](implementations.md#fullcan) by [Intel](https://en.wikipedia.org/wiki/Intel)
- [Hybrid](implementations.md#hybrid) Both previous implementations are employed.

These two implementations differ by 3 main factors:

- Frame buffering
- Frame filtering
- Remote frame handling (strategies for reacting to remote frames)

---

## BasicCAN
This implementation employs chep controllers, as it moves great part of the logic on the CPU (thus the software on upper layers), and, therefore, requires expensive microprocessors. Hardware-wise, it is distributed as a chip (with the CPU and a basic board) and a controller separately, thus requiring more space.

### Frame buffering
Two buffers are employed: one for receiving and one for transmitting a frame. The _Receive buffer_ though implements a **double buffering** mechanism with **shadow buffering**. Basically, a frame is received straight from the bus and placed in the _Receive buffer_, while the _Shadow receive buffer_ (another one) contains the frame that the controller is currently processing. This pipeline ensures that the controller can keep up with the received frames as it processes each one of them.

Two write a frame on the bus, the controller writes it into the transmission buffer.

### Frame filtering
The controller performs an initial filtering. It is a **preliminary filtering** based on the _Identifier_ of the frames.

1. When a message arrives from the buffer, it is placed into the _Receive buffer_.
2. When the controller is done processing the current frame in the _Shadow receive buffer_, it cleans this buffer and moves the frame from the _Receive buffer_ into it.
3. So now the controller can process the frame. The processing is done by using some bitmasks against the _Identifier_ field.
4. If the check is ok, the frame will proceed to the upper layers. Otherwise it will be discarded.

Further filtering has to be done in upper layers by the CPU. But the application layer needs to implement this logic.

### Remote frame handling
BasicCAN promotes simple controllers, thus it does not support automatic replies to remote frames at controller level. Thus the controller will send the remote frame to the upper layers, where the CPU will process it and handle the sending of the _Data frame_.

## FullCAN
This protocol is more performant than BasicCAN and employs simple CPUs but much more complex controllers. It is sold as a unique component: chip mounted on the controller.

### Frame buffering
The protocol employs a broad collection of buffers called **mailboxes** which are initialized either in _Send_ or _Receive_ mode, each one of them is also assigned with a single frame ID. So after initialization, the controller will have a lot of buffers: a pair for each frame ID. This will allow the protocol to be very efficient when handling frames to receive of send, as each one of them will have its own assigned buffer (depending on the ID).

### Frame filtering
Filtering is performed entirely in the controller. Upon frame reception, all buffers are checked i order to locate the one that frame belongs to (basing on the frame ID). So the frame is stored there if the frame is relevant. In fact no buffer will be allocated to frames which are not relevant to the node, thus the filtering is handled immediately.

Upon transmission, a frame is moved in its assigned buffer. To select which frame to write first on the bus the controller can take advantage of different policies. Typically the frame priority based on the ID is the preferred solution. This makes the protocol more reliable from a real time point of view as the transmission buffer can be implemented as a **priority queue**, differently from BasicCAN which employs a simple FIFO queue.

### Remote frame handling
The controller performs the transmission of _Data frames_ automatically upon reception of _Remote frames_. When a _Remote frame_ arrives, the controller checks the transmission buffers for that specific ID, if it finds the buffer and it contains a frame, it will be sent.

## Hybrid
In modern times, FullCAN and BasicCAN ar destined to disappear in favor of an architecture employing both solutions.
