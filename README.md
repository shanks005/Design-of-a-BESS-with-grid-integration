<img width="1919" height="955" alt="image" src="https://github.com/user-attachments/assets/4505499e-cf53-400a-89c7-3c39a21ca27a" /># Battery Energy Storage System with Grid Integration

## Project Overview

This project presents the design and simulation of a Battery Energy Storage System (BESS) integrated with a grid-connected inverter. The system is designed to support energy exchange between a photovoltaic source, battery storage, DC-link, inverter, and grid.

The main objective of this project is to analyze the operation of the battery energy storage system under different operating states such as charging, discharging, and standby condition. The simulation also studies grid-side voltage and current behavior, boost converter output, battery state of charge, battery voltage, and battery current.

A key observation from the simulation is that the inverter-side current and grid-side current are not properly synchronized in open-loop operation. Therefore, PLL-based dq control is required for proper grid synchronization and stable power transfer.

---

## System Architecture

The overall system consists of:

- PV array
- Boost converter
- Battery energy storage system
- Bidirectional DC-DC converter
- DC-link capacitor
- Three-phase inverter
- Grid-side filter
- Three-phase grid
- Measurement and control blocks

---

## System Block Diagram

![BESS Grid Integration System](https://github.com/shanks005/Design-of-a-BESS-with-grid-integration/blob/main/closed_loop_system.png)

---

## Operating States

The BESS is analyzed under three major operating states.

### State 1: Battery Charging Mode

In this mode, excess power from the PV array or grid is used to charge the battery. The battery current becomes negative depending on the sign convention used in the simulation, and the battery state of charge increases gradually.

The boost converter maintains the DC-link voltage required for grid-side inverter operation.

![Battery Charging Mode](https://github.com/shanks005/Design-of-a-BESS-with-grid-integration/blob/main/battery_during_charging.pdf)

---

### State 2: Battery Discharging Mode

In this mode, the battery supplies power to the DC-link through the DC-DC converter. The inverter converts the DC-link voltage into three-phase AC power and supplies it to the grid or connected load.

The battery current becomes positive depending on the sign convention, and the state of charge decreases.

![Battery Discharging Mode](https://github.com/shanks005/Design-of-a-BESS-with-grid-integration/blob/main/battery_during_discharging.png)

---

### State 3: Battery Standby Mode

In standby mode, the battery neither charges nor discharges significantly. The battery current remains approximately zero and the state of charge remains nearly constant.

This state is useful when the PV array or grid is able to maintain the DC-link without requiring battery support.

![Battery Standby Mode](https://github.com/shanks005/Design-of-a-BESS-with-grid-integration/blob/main/battery_standstill.png)

---

## PV Array

The photovoltaic array acts as the renewable energy source of the system. It converts solar irradiance into DC electrical power. The PV output voltage and current depend mainly on irradiance and temperature.

The PV output power is given by:

```math
P_{PV} = V_{PV} I_{PV}
