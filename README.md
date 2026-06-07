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
