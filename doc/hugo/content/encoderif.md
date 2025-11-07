---
title: "Encoder Interfaces"
weight: 30
---

The design provides two commonly used sensor interfaces.

- Supports:
  - **ABZ incremental**
  - **BiSS-C**, **SSI**
- 12V/5V/3.3V switchable encoder supply
- Up to 12V tolerant inputs
- differential receivers for ABZ incremental encorer
- RS422 Rx/Tx for BiSS-C
- ESD protection on all inputs

The quadrature encoder interface transforms differential signals to single ended 3.3V signals with a propagation delay of < 50 ns.

The BiSS-C/RS422 interface provides a robust, 12 Mb/s RS422 signaling from and to 3.3V IO on the controller side.

### ABZ Encoder Connector (J5)

A quadrature encoder with differential output can be connected to J5.

| Pin # | Signal |
| --- | ------ |
| 1 | B- |
| 2 | B+ |
| 3 | A+ |
| 4 | Z- |
| 5 | A- |
| 6 | Z+ |
| 7 | GND |
| 8 | V_ABZ* |

*V_ABZ can by set soldering **one** jumper of JP1, JP2 or JP4.

5V is pre-connected on the PCB and has to be cut before one of the other voltages can be applied.
  
| V_ABZ | JP1 | JP2 | JP4 |
| - | - | - | - |
| 3.3V | | | x |
| 5V   | | x | |
| 12V  | x | | |

**WARNING!** Soldering mutiple jumpers shorts supplies and reults in damage of the ECMD PCB.

> **NOTE:** The input circuit can be reconfigured for single ended and/or signals requiring pull-up or pull/down resistors. Consult the schematic for details.

### BiSS-C/RS-422 Connector (J7)

A BiSS-C encoder or RS-422 device can be connected to J5.

| Pin # | Signal |
| --- | ------ |
| 1 | B- |
| 2 | B+ |
| 3 | A+ |
| 4 | Z- |
| 5 | A- |
| 6 | Z+ |
| 7 | GND |
| 8 | V_BISS_C* |

*V_BISS_C can by set soldering **one** jumper of JP1, JP2 or JP4.

5V is pre-connected on the PCB and has to be cut before one of the other voltages can be applied.
  
| V_BISS_C | JP5 | JP6 | JP7 |
| - | - | - | - |
| 3.3V | | | x |
| 5V   | | x | |
| 12V  | x | | |

**WARNING!** Soldering mutiple jumpers shorts supplies and reults in damage of the ECMD PCB.