# The CAN protocol

[CAN (Controller Area Network)](https://en.wikipedia.org/wiki/CAN_bus) is a serial bus industrial networking technology designed for real time applications in automotive and soon extended to other industries and areas.

## Brief story
CAN was developed by [Robert Bosch](https://en.wikipedia.org/wiki/Robert_Bosch_GmbH) in 1986 upon request from [Mercedes](https://en.wikipedia.org/wiki/Mercedes-Benz) in order to target connectivity of devices inside cars. Since that moment, CAN has grown in time:

1. **1986** Can is developed.
2. **90s** CAN boards are manufatured and distributed by [Philips](https://en.wikipedia.org/wiki/Philips) and [Intel](https://en.wikipedia.org/wiki/Intel) however with a few implementation differences.
    - **FullCAN** Designed by Intel following specifications from Bosch, required less CPU power since much of the traffic management functionalities (like message filtering) were moved onto the network controller.
    - **BasicCAN** Designed by Philips following specifications from Bosch, was architecturally simpler, though requiring more powerful CPUs (message filtering handled by software). 
3. **Around 1995** The market positively accepts CAN. Car manufacturers like Mercedes, [Volvo](https://en.wikipedia.org/wiki/Volvo), [BMW](https://en.wikipedia.org/wiki/BMW) and [FIAT](https://en.wikipedia.org/wiki/Fiat_Automobiles) acquire CAN.
4. **End of 1995** Standardization efforts of CAN, starting in 1990, begin to produce results. Can 2.0 (the original version designed by Bosch) is standardizaed into [ISO 11898](https://www.iso.org/standard/63648.html). In the same year, CAN 2.0 is extended, thus from original version CAN 2.0A, CAN 2.0B is created (escpecially used in the US market). Standardization documents only covered PHY and DLL layers, though this made CAN flexible, it opened up to many proprietary implementation of the protocol.

### Different versions of CAN
As mentioned, CAN was standardized only for PHY and DLL layers. Many different manufacturers took advantage of the flexibility offered by CAN in order to produce different monolithic, ad-hoc, properietary versions of the protocol. The result is that, today, we find many different implementations of CAN for different application areas.

#### CiA and CAL
Group [CAN in Automation (CiA)](https://en.wikipedia.org/wiki/CAN_in_Automation) was founded in 1992 with the purpose of creating a standard application layer for CAN. A general purpose specification was released: _CAN Application Layer_ (CAL), however the effort ended in a failure since CAL was again designed to be application independent, manufacturers had to develop their own application-specifc layer on top of CAL instead of on top of DLL and PHY layers.

#### CANopen
Even though a failure, some solutions were actually developed from CAL. Bosch himself, in the context of European Project [ASPIC Esprit](http://www.archive.org/details/aspic), lead a group which designed and marketed a CAN solution based on CAL with some modifications, giving birth to [CANopen](https://en.wikipedia.org/wiki/CANopen) which became an European Standard in 1995.

#### DeviceNet and SDS
On a separate track, starting from 1992, CAN was adopted by 2 major manufacturers: [Allen-Bradley](https://en.wikipedia.org/wiki/Allen-Bradley) and [Honeywell](https://en.wikipedia.org/wiki/Honeywell). They both designed and developed a distributed control system based on CAN, the project was discarded a few years later, though carried on by both of them separately.

Allen-Bradley developed [DeviceNet](https://en.wikipedia.org/wiki/DeviceNet) while Honeywell developed [Smart Distributed Systems (SDS)](https://en.wikipedia.org/wiki/SDS_Protocol). The former had more success and is still used today.

---

## Main usages
CAN is mainly used in automotive systems inside cars in order to connect the different electronic devices or also for controlling the engine. 

However other applications started employing CAN since its introduction (given its high robustness), so we find, among the most important:

- Agricultural machinery
- Nautical electronics
- Elevetors control
- Printers
- Medical industry (Image Diagnostics)
- Robotics
