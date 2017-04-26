# Bus characterization

The CAN bus, by specification, is required to be the closest possible to a single line in order to make it faster (short transmission time and, therefore, high bandwidth).

## Physical mean
In order to guarantee certain bandwidth levels, the bus has to offer a total impedence of about 120 $$\Omega$$.

**Terminators** must also be applied at the extremes of the line in order to avoid signal reflection. **Stubs** are also allowed, but their length must be kept under control. Considering that CAN allows a max bandwidth of 1 Mbit/s, in order to keep that rate stubs must be shorter than 30 cm.

## Technology
The bus can be technologically deployed in 3 possible ways:

- **2-wire bus** Twisted pair for highly reliable communications. The twisting allows the medium to be shielded from electromagnetical interferences, plus an additional shielding layer guarantees better protection.
- **Single wire bus** Simpler technology and cheaper. Provides not good immunity against interferences. Main application in automotive.
- **Optical fiber** Immune to all interferences and is suitable in hazardous environments. If the network is very large, this is a recommended solution for keeping a very high bandwidth by having exceptionally long cabling.

### Bandwidth
CAN supports up to 1 Mbit/s. Other bandwidths are possible, however each bit-rate $$B$$  comes with limitations on the length $$l$$ of the bus. Approximately, the product $$B \cdot l$$ should be constant:

$$
B \cdot l \approx C = 50 \frac{\text{Mbit} \cdot \text{m}}{\text{s}}
$$

The following table shows some of the supported configurations:

| Bus length | Max bandwidth |
|:----------:|:-------------:|
| $$40 \text{m}$$ | $$1 \frac{\text{Mbit}}{\text{s}}$$ |
| $$100 \text{m}$$ | $$500 \frac{\text{Kbit}}{\text{s}}$$ |
| $$200 \text{m}$$ | $$250 \frac{\text{Kbit}}{\text{s}}$$ |
| $$500 \text{m}$$ | $$125 \frac{\text{Kbit}}{\text{s}}$$ |
| $$6 \text{m}$$ | $$10 \frac{\text{Kbit}}{\text{s}}$$ |

## Additional bus features
CAN approves the utilization of repeaters: PHY devices which mirror the eletrical signal from one port onto the other in order to fight back signal attenuation and phase shifting (the signal can, therefore, reach distant stations). However the number of these devices has to be kept in control as they introduce delayes on the bus.

## Limitations
Some Fieldbus networks are able to have buses operating both for power and data transmission. CAN unfortunately does not allow this to happen.
