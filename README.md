<img width="1919" height="955" alt="image" src="https://github.com/user-attachments/assets/4505499e-cf53-400a-89c7-3c39a21ca27a" /># Battery Energy Storage System with Grid Integration

## Brief Overview

This project focuses on the design and simulation of a Battery Energy Storage System integrated with a grid-connected inverter. The system includes a PV array, boost converter, battery storage, DC-link, three-phase inverter, and grid connection.

The battery is tested under three operating conditions: charging, discharging, and standby mode. For each condition, the grid-side voltage and current, boost converter output, battery SOC, battery voltage, and battery current are observed.

During simulation, it was found that the inverter-side currents and grid-side currents were not synchronized in open-loop operation. Therefore, PLL-based dq control is required to synchronize the inverter output with the grid voltage and ensure stable power transfer.

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

## AC Side Results

The AC side of the system consists of the three-phase inverter, grid-side filter, and three-phase grid. The inverter converts the regulated DC-link voltage into three-phase AC voltage and supplies it to the grid through the filter.

The combined AC-side result shown below includes the important parameters observed during simulation, such as inverter-side voltage, inverter-side current, grid-side voltage, and grid-side current.

![AC Side Results](https://github.com/shanks005/Design-of-a-BESS-with-grid-integration/blob/main/ac_side_closed_loop.png)

From the AC-side simulation results, it was observed that the inverter-side current and grid-side current were not properly synchronized. The phase currents were not in synchronism with the corresponding grid voltages. This indicates that open-loop inverter operation is not sufficient for proper grid integration.

The lack of synchronization may occur due to:

- Absence of PLL-based grid angle detection
- Incorrect phase angle used for PWM generation
- Improper current feedback control
- Incorrect phase sequence
- Improper PI controller tuning
- Lack of dq-axis current control

Therefore, PLL-based dq control is required to synchronize the inverter output current with the grid voltage and ensure stable active and reactive power exchange.

---

### AC Side Observation

From the AC-side simulation results, it was observed that the inverter-side current and grid-side current were not properly synchronized. The phase currents were not in synchronism with the corresponding grid voltages. This indicates that open-loop inverter operation is not sufficient for grid integration.

The lack of synchronization may occur due to:

- Absence of PLL-based grid angle detection
- Incorrect phase angle used for PWM generation
- Improper current feedback control
- Incorrect phase sequence
- Improper PI controller tuning
- Lack of dq-axis current control

Therefore, PLL-based dq control is required to synchronize the inverter output current with the grid voltage and ensure stable active and reactive power exchange.

---

## Need for dq Control

For grid-connected operation, the inverter current must be synchronized with the grid voltage. This can be achieved using synchronous reference frame control, also called dq control.

In dq control, the three-phase grid voltages and currents are converted into the rotating dq reference frame using the grid angle obtained from a Phase-Locked Loop.

The dq transformation allows the AC quantities to be controlled as DC quantities using PI controllers.

The active and reactive power expressions are:

```math
P = \frac{3}{2} V_d i_d
