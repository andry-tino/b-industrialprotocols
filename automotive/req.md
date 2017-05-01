# Requirements in the Automotive Industry

The requirements to be taken into consideration in automotive systems given the functional domains are:

- [Fault tolerance](req.md#fault-tolerance)
- [Predictability](req.md#predictability)
- [Bandwidth](req.md#bandwidth)
- [Flexibility](req.md#flexibility)
- [Security](req.md#security)

---

## Fault tolerance
Systems can be affected by **faults**.

> A fault is an unexpected condition in which the system does not behave as per specifications.

When a system is robust or tolerant to faults, it means it is capable of properly handle unexpected conditions. Thus keeping on guaranteeing adequate service levels without a brutal interruption (maybe performance decay might be experienced).

In order to be robust to faults, systems today have come up with several strategies:

- Apply redundancy to information in space (use more lines) and time (repeat transmission).
- Check data by using error detection/correction codes.
- Use redundant circuits (backups) in case of failures.
- Use bus guardians to prevent babbling idiots.

## Predictability
Systems that requiremessages to be delivered within certain time (deadlines) need to employ real time systems which can guarantee high levels of predictability. This is done by guaranteeing **determinism** in message transmissions.

> When a system guarantees high levels of timeliness in transmissions, it is predictable.

**Timeliness** is a necessary guarantee for some systems like [Airbag](https://en.wikipedia.org/wiki/Airbag), [ABS](https://en.wikipedia.org/wiki/Anti-lock_braking_system), etc. In fact, these systems need messages to be delivered according to specific deadlines in order to function well, and when they do not function well, high risks will be considered for the safety of the driver and passengers.

**Fault tolerance** Timeliness is connected to fault tolerance. A fault tolerant system makes it more likely to be predictable. For example, **message integrity**: when a message is not properly received it must be retransmitted, thus increasing the delivery time, thus increasing the change of a deadline-miss.

## Bandwidth
Many systems and subsystems employed in cars have high requirements in terms of bandwidth. However the following has to be kept into consideration:

- High bandwidth might result in worse predictability as the probability of error on transmission is higher.
- High bandwidth might result in lower fault tolerance as a consequence of the previous point.

For this reason **low bandwidth is not a bad thing**:

> Low bandwidth guarantees more robust and predictable systems.

Since high bandwidth is also costly, systems tend to find trade-offs to afford good solutions price-wise.

## Flexibility
The ability of a network to cope with the change of different quantities over time:

- Number of messages being exchanged dunring a certain window frame (bandwidth).
- Number of event and time triggered messages.
- Different lengths of frames (different data).
- Scalability (adding/removing devices).

For example, [CAN](../can/intro.md) is more flexible than [Profinet IO](../rte/profinetio.md) when it comes to scalability. When adding or removing devices on the network, CAN can adapt immediately, thanks to [CSMA-CR](../can/phy-collision.md), while Profinet IO uses [TDMA](https://en.wikipedia.org/wiki/Time-division_multiple_access), so the slots have to be redesigned in the cycle, which will cause the IO Controller to take time for that before letting the network be 100% functional. The same goes for [EPL](../rte/epl.md).

## Security
Many systems are accessible from outside of a car (Wireless or Bluetooth communication systems), and others from inside (enterteinment systems). Also it is possible to have direct access to some systems by wire. Manufacturers must protect users' data by implementing all the necessary protection.

---

## Requirements vs systems

An overview of different requirements per system is provided following:

| System | Fault tolerance | Predictability | Bandwidth | Flexibility | Security |
|:-------|:---------------:|:-------------:|:----------:|:-----------:|:--------:|
| Powertrain | Yes | Yes | Yes | No | No |
| Chassis | Yes | Yes | Yes | No | No |
| Body | Some | Some | Some | Yes | Yes |
| Multimedia & enterteinment | No | Some | Yes | Yes | Some |
| X-by-wire | Yes | Yes | Yes | No | No |
| Telematics | No | Some | Some | Yes | Yes |
| Diagnostics | No | Some | No | Yes | Yes |
