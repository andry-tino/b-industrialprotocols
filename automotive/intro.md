# Network protocols in automotive systems

Starting from 1970 the automotive market has seen an increase in the number of electronic devices being employed in a car replacing mechanical systems. These devices implement functions targeting several aspects of the **driving experience**:

- On board comform handling
- Passengers safety
- Vehicle control
- On board enterteinment
- On board instrumentation control (lights, wipers, doors, windows)

We recognize 2 important concepts here:

- **Function** The purpose or duty of one device or family of devices.
- **Electronic Control Unit (ECU)** A standalone electronic system implementing a function and made of a set of sensors and actuators.

## From point2point to multiplexed communications
Cars are embedded with many different ECUs. They way these components are installed, deployed and interconnected ahs changed in time. Initially ECUs were installed standalone, each one of them serving a specific purpose. Later on these different systems had to interact together, thus the need for a networking protocol inteconnecting them.

Until 1990, connection between ECUs were point-to-point. Thus many different links were interconnecting the different systems. Since every component was connected to the others, networks' topology nearly ended up collapsing into a [full mesh network](https://en.wikipedia.org/wiki/Mesh_networking). In such networks the number of links between nodes is $$N^2$$ ($$N$$ being the number of devices).

Given the many components and the incredibly high cabling effort, these networks ended up adding an iincredible amount of weight on cars. Also the whole infrastructure ended up being very costly. To cope with that communications started evolving into bus-oriented networks (multiplexed communications).

> BMW reported in 1998 that, after a wiring harness effort on their vehicles, the whole weight decreased by 15 kg.

In 1986 [CAN](../can/intro.md) revolutionized the industry as the leading networking technology for interconnecting ECUs in cars.

## Car function domains
In cars, the different functions of the many subsystems can be grouped into categories.

> A _function domain_ is a set of systems designated to the same function.

We recognize 4 very important function domains in cars:

- [Powertrain](intro.md#powertrain) Engine and transmission control.
- [Chassis](intro.md#chassis) Suspension, steering and braking control.

Those 2 categories are real time function domains and need to be served by real time systems. They are in fact concerned with the safety on board and directly affect the control of the vehicle. Other classes are:

- [Body](intro.md#body) Comfort on board.
- [Telematics](intro.md#telematics) Integration with wireless communications, multimedia, interfaces, etc.

### Powertrain
All systems responsible for controlling the engine:

- Fuel injection
- Engine speed
- Valve control
- Gear control

Due to the fact that it is necessary for these systems to keep up with the engine rotation speed, these ECUs are all designed with time constrains in the order of **millisecond**. Controllers are required to be highly performant too. These systems also require a lot of interaction with the other components such as [ESP](https://en.wikipedia.org/wiki/Electronic_stability_control), [ABS](https://en.wikipedia.org/wiki/Anti-lock_braking_system), etc.

Furthermore, ECUs are moving towards a Time Triggered (TT) scheduling approach (like [TDMA](https://en.wikipedia.org/wiki/Time-division_multiple_access)) which guarantees high predictability, high **composability** of different components and high determinism.

#### About composability
With this term, we refer to the ability of interconnecting different components together with ease of deployment. Time triggered scheduling systems facilitate composability, since each ECU can be assigned to a time slot in the transmission cycle. When a system is composable, it reduces the inter-dependence with the other systems.

### Chassis
ECUs related to the chassis cover safety and motion control:

- Safety systems
- Vehicle dynamics control
- Motion control (suspensions, steering and braking)

Among the most important ones, we found:

- [Antilock Braking System (ABS)](https://en.wikipedia.org/wiki/Anti-lock_braking_system): Based on an optical sensor on the wheel which employs a hole-marked disk, this system tries to avoid the slipping phenomenon upon sudden braking by acting on brakes and activating them at high frequency.
- [Electronic Stability Program (ESP)](https://en.wikipedia.org/wiki/Electronic_stability_control): Tries to avoid the swerve phenomenon by acting on each single wheel via incrementing or decrementing its speed to keep the car on track when turning.
- [Adaptive/Automatic Cruise Control (ACC)](https://en.wikipedia.org/wiki/Autonomous_cruise_control_system): Cruise control to keep constant speed on the road.
- Electronic Damper Control (EDC): Primarily employed by [BMW](https://en.wikipedia.org/wiki/BMW), this system enables bump absorption by actively working on suspections. Even if only one wheen is involved in a bump, all the other suspensions help the car keeping a stable level.

Becaue all these systems are directly connected to safety, networks are required to be real time. Thus the same requirements apply in this domain as for [Powertrain](intro.md#powertrain), but considering more time critical constraints.

#### X-by-wire
With this term we refer to mechanical or hydraulic components in cars which get replaced by fully electrical/electronic units. They are based on [feedback control](https://en.wikibooks.org/wiki/Control_Systems/Feedback_Loops) and must be as reliable as their mechanical counterparts. Examples are:

- Steer-by-weire
- Brake-by-wire
- Shift-by-wire

### Body
In this functinoal domain, we find ECUs responsible for comfort management and accessories handling:

- Climate control
- Blinkers
- Windows
- Lights (interior, exterior)
- Parking control
- Car Access Systems (CAS) like smart keys or alarms

All body systems are typically **triggered/activated by the driver** or passengers. Furthermore, they handle the exchange of **small pieces of information** across components.

Given the simplicity (compared to the other domains) of these systems, no hard real time functionality has to be featured, thus networks here tend to be cheaper and simpler like [LIN](lin.md). From a traffic point of view, **low bandwidth** is usually required.

**CAN integration** In this domain we really find a lot of systems. Given this condition and the fact that many different components communicate with each other, a high level of connectivity is required. To avoid increasing the cost, these systems are connected with each other by means of a hierarchical structure whose backbone is supported by [CAN](../can/intro.md). See [LIN](lin.md).

### Telematics
Because of the rapid spread of luxury systems in cars, Wireless and multimedia systems are now fully integrated in such environments.

- [Wireless](https://en.wikipedia.org/wiki/Wireless_network)
- [Bluetooth](https://en.wikipedia.org/wiki/Bluetooth)
- Multimedia systems, TV, radio
- Speech recognition
- Navigation systems
- Smart cars

The characteristics of these domain is to include systems which **exchange an extremely large amount of data** consisting in heavvy information units (image stream, audio. etc.). **High bandwidth** is often required in these cases.

#### On board computers
Since cars are now also equipped with on-board systems, Internet connection is available. It is possible to connect phones and other devices. Also smart cars will enable remote control and road reading systems interfacing with the outside worll. Because of this increasing interfacing with the external world, **security** has become a huge concern. These systems must guarantee a very hogh level of protection of data being exchanged.

#### Diagnostics
Given recent world and European regulations on emissions and pollution, cars are required to be equipped with a whole set of sensors providing statistics on consumes and many other quantities. These components interact with the engine and the fuel injection systems, thus they need reliable transmissions.

Typically we are not talking about high requirements in bandwidth or time, as many of these systems are just for monitoring values like:

- Fuel levels
- Engine temperature
- System overall status
- Central unit status
- Consumptions

They are especially needed when operating maintenance on the vehicle, so it is often required to have a data store unit to save all information into.
