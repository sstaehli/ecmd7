---
title: "Control Interface"
weight: 40
---

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