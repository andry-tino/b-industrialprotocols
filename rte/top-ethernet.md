# Realizartion on Top of Ethernet

This realization creates a separation between the real-time and the non-real-time traffic, enabling the former to bypass the DLL and reach Ethernet, thus prioritizing real-time traffic.

![Visualization of realization On Top of Ethernet](../assets/on-top-of-ethernet.png)

The most important thing we must notice is the absence of any alteration of the Ethernet hardware. However this architecture requires some changes to be performed at Application and DLL levels.

**Pros**

- No hardware modification.
- Modifications in the protocol stack are not massive.
- Better time-critial traffic handling.

**Cons**

- Due to requirements on delivery time, it is necessary to apply a dimensioning effort in order to calculate the number of switches in the network.

## Encapsulation
This realization takes advantage of [Ethernet encapsulation](ethernet-enc.md).

## Case study
One of the most common CP implementing this realization is [Ethernet PowerLink](epl.md).