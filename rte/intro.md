# Real Time Ethernet

At the end of 90s the world of Industrial Automation started considering the possibility of using [Ethernet](https://en.wikipedia.org/wiki/Ethernet) in time critical environments.
The technology was introduced by [Xerox-PARC](https://en.wikipedia.org/wiki/PARC_(company) around 1970, and sice that time has been undergoing constant revising and performance improvements.

Even though Ethernet on its own was not designed for time critical applications, well designed modifications could adapt the different protocols to be aligned with the different sets of requirements typical of automation contexts. 

## Why
The main reasons which motivated the community to push for Ethernet were:

- [TCP/IP](https://en.wikipedia.org/wiki/Internet_protocol_suite) protocol suite naturally stacks up on Ethernet. This opened up to the possibility of online/remote factory management.
- Low cost (theoretically). The hardware for supporting Ethernet is not as expensive as that we can find in protocols fully supporting real time systems. However the limitations and unpredictability introduced by TCP/IP or other protocols such as [CSMA/CD](https://en.wikipedia.org/wiki/Carrier-sense_multiple_access_with_collision_detection) have to be considered, thus adding costs to the original infrastructure in order to have a minimal time critical coverage.
- Good and high bandwidth. Ethernet was initially designed to operate on 10 mbit/s, a limit which was quite rapidly overtaken by the next generation of protocols which could support up to 100 Mbit/s thanks to [FastEthernet](https://en.wikipedia.org/wiki/Fast_Ethernet). In 1990, [Gigabit Ethernet](https://en.wikipedia.org/wiki/Gigabit_Ethernet) pushed the limit to 1000 Mbit/s as it was standardized as _IEEE 802.3z_.

## Adaptations
Ethernet cannot be used _AS-IS_ as it lacks support for time criticalities. For this reason, factory protocols based on Ethernet, more specifically today on IEEE 802.3, do apply some changes to the protocol to make it align to real time requirements where possible.

### Ethernet requirements in Automation
Every networking technology in automation contexts relying on Ethernet must meet the following requirements:

- **Deterministic medium access** It must guarantee a deterministic communication. Access to the medium must be provided with precise control.
- **Network simultaneity** It must be able to handle the many different simultaneous events occurring on the network.
- **Small data** It must efficiently support the exchange of small data frames over the network as such is the type of messaging in Automation.
