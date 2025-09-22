# ECMD7

3-Phase Power Converter Hardware for Motor Drive Experiments

## User Requirements

### 1. Overview
- Drive 500W PMSM motors from 12V–48V (lead-acid or lithium)
- Based on **TMC6200 gate driver**
- Full current & voltage sensing
- Absolute encoder support (BiSS-C, SSI, ABZ)
- Interfaces with **Arty A7**, **Zybo Z7**, or optionally **Vidor 4000**

---

### 2. Power Stage
- **Input Voltage**: 12V–48V (up to 60V abs max)
- **Output**: 35A RMS, 50A peak
- **External MOSFETs** (N-channel, low R_DS(on))
- **Bulk capacitors** for ripple suppression
- Reverse polarity & overvoltage protection

---

### 3. Gate Driver: TMC6200
- 3-phase gate driver with:
  - 3x or 6x PWM support
  - SPI config & diagnostics
  - Shoot-through & UV/OV protection
  - Charge pump for 100% duty cycle
- Interfaces directly with external MOSFETs
- Supports external current sensing

---

### 4. Sensing
- **Current**: 3-phase sensing (inline or low-side), routed to FPGA
- **Voltage**: Phase voltages + DC bus, scaled to 3.3V
- **Temperature**: NTC input for MOSFET temp

---

### 5. Encoder Interface
- Supports:
  - **BiSS-C**, **SSI**
  - **ABZ incremental**
  - **SPI encoders** (e.g., AS5047)
- 5V/3.3V switchable encoder supply
- ESD protection & differential receivers

---

### 6. FPGA / Logic Interface
- **PMOD-compatible** I/O headers (3.3V)
- FPGA interfaces:
  - PWM (3 or 6)
  - SPI (TMC6200, encoders)
  - Encoder signals (ABZ, BiSS-C, etc.)
- Compatible with:
  - **Arty A7**
  - **Zybo Z7**
  - **Intel Vidor 4000** (via adapter)

---

### 7. Mechanical
- PCB Size: ≤ 100mm x 80mm
- Mounting holes for heatsink/enclosure
- Connectors:
  - XT60 or screw terminals (power)
  - Phoenix for motor phases
  - JST/Molex for logic & encoders

---

### 8. Protection
- Hardware:
  - Fuses, TVS diodes, inrush limiter
- TMC6200 protections:
  - OV/UV, shoot-through, overtemp, short-circuit

---

### 9. Optional Features
- Onboard **MCU (STM32/RP2040)** for SPI/telemetry
- USB-C port for debug/config
- BLE/WiFi via ESP32 module

---

### 10. Deliverables
- KiCad schematic + PCB layout
- BOM

---

### Mermaid Diagram: System Overview

```mermaid
graph TD
    Power[Battery Input<br>12V–48V] --> PowerStage
    PowerStage[TMC6200 + MOSFETs<br>3-Phase Inverter] --> Motor[PMSM Motor]
    
    PowerStage -->|Phase Currents| CurrentSense[Current Sensors<br>(INA240 / shunt)]
    PowerStage -->|Phase Voltages| VoltageSense[Voltage Dividers]

    Encoder[Absolute Encoder<br>(BiSS-C / ABZ / SPI)] --> EncoderIF[Encoder Interface]
    EncoderIF --> FPGA[FPGA Board<br>(Arty A7 / Zybo Z7)]

    CurrentSense --> FPGA
    VoltageSense --> FPGA

    FPGA -->|PWM / SPI| TMC6200[TMC6200 Gate Driver]
    FPGA -->|PMOD / GPIO| Connector[PMOD / Logic I/O]

    subgraph Optional
        MCU[Optional MCU (STM32/RP2040)] --> FPGA
        USB[USB-C for Debug] --> MCU
        BLE[Optional BLE/WiFi (ESP32)] --> MCU
    end

