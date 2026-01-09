---
title: "Circuit Description"
weight: 10
---

## Overview And PMOD Control Interface

The design mechanically fits the Digilent Arty A7 or Zybo Z7 development board.

- **PMOD-compatible** I/O headers (3.3V)
- FPGA interfaces:
  - PWM (3+3 driver signals)
  - SPI (TMC6200, encoders)
  - Encoder signals (ABZ, BiSS-C)
  - Compatible with:
    - **Arty A7**
    - **Zybo Z7**

### PMOD SPI & Encoder (J1)

| Pin # | Signal | I/O | PMOD JB (A7)*, PMOD JC (Z7)** | A7 FPGA Pin #* | Z7 SoC Pin #** | Description |
| - | - | - | - | - | - | - |
| 1 | 3.3V | In | 6 | - | - | I/O supply from FPGA board |
| 2 | 3.3V | In | 12 | - | - | I/O supply from FPGA board |
| 3 | GND | In | 5 | - | - | Signal GND |
| 4 | GND | In | 11 | - | - | Signal GND |
| 5 | ENC_B | Out | 4 | C15 | T10 | Quadrature encoder B signal |
| 6 | ENC_A | Out | 10 | J15 | U12 | Quadrature encoder A signal |
| 7 | CS1 | In | 3 | D15 | T11 | SPI Chip delect 1 for 2-to-4-line decoder |
| 8 | ENC_Z | Out | 9 | K15 | T12 | Quadrature encoder Z (Ref) signal |
| 9 | SPI_SCK | In | 2 | E16 | W15 | SPI Clock |
| 10 | CS0 | In | 8 | J18 | Y14 | SPI Chip delect 0 for 2-to-4-line decoder |
| 11 | SPI_SDI | In | 1 | E15 | V15 | SPI serial data in (from Controller) |
| 12 | SPI_SDO | Out/HiZ | 7 | J17 | W14 | SPI serial data out (to controller) |

### PMOD ADC & BiSS-C/RS422 Rx/Tx (J2)

| Pin # | Signal | I/O | PMOD JC (A7)*, PMOD JD (Z7)** | A7 FPGA Pin #* | Z7 SoC Pin #** | Description |
| - | - | - | - | - | - | - |
| 1 | 3.3V | In | 6 | - | - | I/O supply from FPGA board |
| 2 | 3.3V | In | 12 | - | - | I/O supply from FPGA board |
| 3 | GND | In | 5 | - | - | Signal GND |
| 4 | GND | In | 11 | - | - | Signal GND |
| 5 | RS422_RX | Out | 4 | V11 | R14 | RS422 receive signal (to controller) |
| 6 | RS422_TX | In | 10 | U13 | V18 | RS422 transmit signal (from controller) |
| 7 | AD_SDO_IW | Out | 3 | V10 | P14 | SPI serial data output from W-Phase current ADC |
| 8 | AD_SDO_VBUS | Out | 9 | T13 | V17 | SPI serial data output from bus voltage ADC |
| 9 | AD_SDO_IU | Out | 2 | V12 | T15 | SPI serial data output from U-Phase current ADC |
| 10 | AD_SDO_IV | Out | 8 | V14 | U15 | SPI serial data output from V-Phase current ADC |
| 11 | /CS_AD | In | 1 | U12 | T14 | SPI /CS line. Rising edge starts conversion, low level enables data output on AD_SCK rising edges |
| 12 | AD_SCK | In | 7 | U14 | W14 | SPI clock signal |

### PMOD Drive Control (J3)

| Pin # | Signal | I/O | PMOD JD (A7)*, PMOD JE (Z7)** | A7 FPGA Pin #* | Z7 SoC Pin #** | Description |
| - | - | - | - | - | - | - |
| 1 | 3.3V | In | 6 | - | - | I/O supply from FPGA board |
| 2 | 3.3V | In | 12 | - | - | I/O supply from FPGA board |
| 3 | GND | In | 5 | - | - | Signal GND |
| 4 | GND | In | 11 | - | - | Signal GND |
| 5 | DRV_EN | Out | 4 | F3 | H15 | Gate driver enable signal, active high |
| 6 | FAULT | In | 10 | G2 | Y17 | Gate driver fault signal, active high |
| 7 | WL | Out | 3 | F4 | J15 | Phase W low side switch control |
| 8 | WH | Out | 9 | H2 | T17 | Phase W high side switch control |
| 9 | VL | Out | 2 | D3 | W16 | Phase V low side switch control |
| 10 | VH | Out | 8 | D2 | U17 | Phase V high side switch control |
| 11 | UL | Out | 1 | D4 | V12 | Phase U low side switch control |
| 12 | UH | Out | 7 | E2 | V13 | Phase U high side switch control |

#### References

> *[Digilent Arty A7 Reference Manual](https://digilent.com/reference/programmable-logic/arty-a7/reference-manual)

> **[Digilent Zybo Z7 Reference Manual](https://digilent.com/reference/programmable-logic/zybo-z7/reference-manual)

---
## Power Stage

The design is dimensioned for high currents to continuously deliver up to 500W from 12V up to 60V. PWM frequencies are supported from 4 kHz up to 25kHz. 4 quadrant operation is possible with battery. There is no brake chopper.

- **Input Voltage**: 12V–48V (up to 60V abs max)
- **Output**: 35A RMS, 50A peak
- **60V/40A, low RDSOn MOSFETs** (N-channel, low R_DS(on))
- Mechanical reverse polarity protection
- Overvoltage protection

### Battery (J4) and Motor Phase Connections (U, V, W)

- A 12-48 Battery or 4-Qudrant Power Supply can be connected to the **XT60 connector J4** or the mounting holes **PGND** and **VMot**
- The Motor terminals can be connected to **M3 mounting holes U, V and W**

### Gate Driver (U1)

The [TCM6200](../files/datasheet/TMC6200_datasheet_rev1.08.pdf) matches or exceeds the requiremnts for controlling the power stage and provides support for current sensing.

- 3-phase gate driver with:
  - 3x or 6x PWM support
  - SPI config & diagnostics
  - Shoot-through & UV/OV protection
  - Charge pump for 100% duty cycle
- Interfaces directly with external MOSFETs
- Supports external current sensing

---
## ADC

The design supports PWM synchronous sampling of all three phase currents and the DC bus voltage.

- **Current**: 3-phase sensing (inline or low-side), routed to FPGA
- **Voltage**: Phase voltages + DC bus
- **Temperature**: digital sensor input for MOSFET temp

The ADC are of type [MCP3315141](../files/datasheet/MCP3315141-Data-Sheet-DS20006220.pdf)

---
## Sensors

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

There is also a temperature sensor of type [TMP122](../files/datasheet/tmp122.pdf).

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

---
## Memory + CS Decoder

The board features an [MB85RS512](../files/MB85RS512T-DS501-00029-0v01-E.pdf) FRAM memory (U16). The memory can be used to store any kind of data, e. g. configuration or calibation. When JP10 is shorted, /WP = 1, (No write protection)
When JP12 is shorted, /WP = 0, (Write protection)

A 2-to-4 line decoder is provided to control 4 chip selects for SPI peripherals.

| CS1 | CS0 | /CS | Device |
| --- | --- | --- | ------ |
| 0 | 0 | - | 
| 0 | 1 | 1 | Drive Controller U1 |
| 1 | 0 | 2 | FRAM U16 |
| 1 | 1 | 3 | Temperature Sensor U17 |

**WARNING!** Soldering both jumpers shorts the +3.3V rail and results in damage of the ECMD PCB.

---

## Power Supply

The power supplies are designed to provide sufficient power to supply also the controller board.
12V and 5V supplies are designed around a [LM5118](../files/datasheet/lm5118.pdf) IC, U13 and U14 respectively. The circuits were dimensioned with TI Vebbench.

- [12V Calculation](../files/datasheet/LM5118-12V-3A.pdf)
- [5V Calculation](../files/datasheet/LM5118-5V-2A.pdf)

The 3V supply is designed around a [LT1616](../files/datasheet/lt1616.pdf). The 3V supply can be enabled externally trough 3.3V IO (JP3 shorted, JP8 and JP5 open) or internally from 12V with 3.3V and 3.3V IO shorted.

### 12V Connector (J6)

Max. 3A

**NOTE:** This connector can be used to supply 12V to an Arty A7 on its connector J7, pins 7 (GND) and 8 (+)

### 5V Connector (J8)

Max. 2A

**NOTE:** This connector can be used to supply 5V to a Zybo Z7 on its connector its JP6, pin 2 (+) and J16.

