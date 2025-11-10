---
title: "Overview"
---

This is the ECMD7 reference manual. The ECMD7 - Electronically Controlled Motor Driver - is a 500W, three-phase bridge for supply voltages from 10 to 60V.

![ECMD7 PCB](files/3d.png)

The drive card provides a power stage with high qualitiy features to drive a 3-phase motor from typical car lead or RC style lithium batteries for educational and development purposes. The PCB provides the required frontend to an external controller at a common logic level.
The design is cost optimized where possible without compromising functionality under lab conditions. It can directly interface  with Digilent Arty A7 and Digilent Zybo Z7. Due to 2.54 pin headers it is easily adaptible to interface with other boards. The PCB can provide sufficent power supply to the connected controller for standalone, mobile operation.

- Drive **500W** PMSM and other synchronous **motors** from 12V–48V (lead-acid or lithium)
- Based on **TMC6200 gate driver**
- All phase current & bus voltage **sensing** in high resolution (14-Bit, $f_s>=2f_{PWM}$)
- Multiple **encoder** support (ABZ, BISS-C/SSI)
- Interfaces with **Arty A7**, **Zybo Z7**

### Additional Features

- **Onboard 12V/3A supply** for connected controller boards
- **Onboard 5V/2.5A supply** for connecting controller boards
- Dedicated **SPI diagnostic bus** with 2-to-4-line decoded chip select for:
    - TMC6200 gate driver
    - MB85RS* FRAM with at least 64kByte
    - TPM122 temperature sensor close to gate driver and power stage
- **Onboard LED** for supply rails
- **Onboard LED** for drive control and state signals
- **Probe test points** for measurments
- **Assembly options** for single ended or open collector encoder inputs to acommodate single ended encoders or hall switches
- **Selectable sensor supply**
- **Selectable 3.3V I/O voltage** internal or external

![ECMD7 PCB](files/2d.png)