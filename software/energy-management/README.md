# AeroHelio Energy Management and Control System

**Subsystem Lead:** Khoa Duong  
**Project:** AeroHelio | UC Riverside Senior Design 2026–2027  
**Status:** Control architecture designed; software implementation and hardware validation in progress.

## Overview

The AeroHelio Energy Management System (EMS) is designed to coordinate renewable power generation, battery backup, and device charging through the ESP32-S3 microcontroller.

The controller will monitor electrical measurements and determine how the system should operate based on available renewable power, battery conditions, device demand, and potential faults.

The goal is to prioritize renewable energy while maintaining reliable power delivery and protecting system components.

## System Architecture

The proposed control system receives information from three principal measurement points:

- **Solar generation:** Voltage and current measurements from the solar power subsystem.
- **Battery storage:** Battery voltage and signed current measurements to distinguish charging from discharging.
- **Device output:** Output voltage and current measurements to monitor the power delivered to the connected device.

The system is designed around INA226 voltage and current sensors, an ESP32-S3 controller, battery-charging hardware, and regulated power-delivery circuitry.

## Operating Modes

The EMS is designed around three operating modes.

| Mode | Condition | Intended Operation |
|---|---|---|
| Normal | A device is connected and renewable generation can support its demand | Prioritize renewable power delivery |
| Backup | A device is connected but renewable generation is insufficient | Use available battery power to support the load |
| Idle | No device is connected | Allow renewable energy to recharge the battery when conditions permit |

The ESP32-S3 will evaluate sensor measurements and system conditions to determine the appropriate operating mode.

### Operating-Mode Selection

The proposed control sequence is:

1. Acquire voltage, current, charger status, and device-connection information.
2. Validate the measurements before using them for control decisions.
3. Calculate electrical power using `P = V × I`.
4. Check for faults and unsafe operating conditions.
5. Determine whether renewable generation can support the connected device.
6. Select Normal, Backup, or Idle operation.
7. Issue supported hardware control commands.
8. Report system measurements and operating status.

## Fault Detection and Protection

Fault handling takes priority over normal power-management decisions.

The proposed controller will monitor for:

- Battery undervoltage
- Excessive current
- Temperature outside permitted operating limits
- Missing or outdated sensor measurements
- Unsuccessful power-source transitions

When a fault is identified, the controller is intended to restrict the affected operation when supported by the hardware and report the event through the monitoring interface.

**Hardware protection remains independent of the ESP32-S3.** Fuses, reverse-current protection, charger limits, and the battery's internal protection circuitry must provide their intended safeguards even if the microcontroller stops functioning.

## Battery Management and Charging Supervision

The selected 3S lithium-ion battery includes built-in battery protection.

AeroHelio's EMS is not intended to replace that protection system. Instead, the ESP32-S3 will provide system-level supervision by monitoring external battery measurements and coordinating supported charging and backup operations.

Proposed functions include:

- Monitoring battery voltage and charging/discharging current
- Supervising battery charging based on operating conditions
- Coordinating renewable input and battery backup
- Reporting battery and charging information
- Responding to detected system faults

The precise charger-control interface and available commands will be finalized after the hardware configuration is confirmed.

## Energy Tracking

An additional planned feature is monitoring the amount of electrical energy generated, stored, and delivered over time.

Using measured power and elapsed time, the controller could estimate energy transfer in watt-hours:

`Energy (Wh) += Power (W) × elapsed time (s) / 3600`

Potential tracked measurements include renewable generation, battery charging/discharging energy, output energy, and time spent in each operating mode.

This information could also support backup-runtime estimation and system performance analysis.

## Development Status

| Feature | Status |
|---|---|
| Normal, Backup, and Idle mode definitions | Designed |
| Operating-mode selection logic | Designed |
| Fault priorities and response rules | Designed |
| Sensor acquisition and validation | In development |
| Charging-control integration | In development |
| Automated power-source selection | Planned for validation |
| Energy tracking | Proposed |
| Backup-runtime estimation | Proposed |
| Complete hardware-integrated testing | Pending |

The operating-mode architecture has been documented, but successful operation of the full controller has not yet been experimentally established.

## Planned Testing

- Validate INA226 voltage and current measurements.
- Test operating-mode decisions using controlled inputs.
- Verify correct transitions between Normal, Backup, and Idle.
- Evaluate responses to missing or invalid sensor readings.
- Test charging-control commands against the selected hardware.
- Verify fault handling and safe recovery conditions.
- Integrate control logic with solar, wind, battery, and device-output subsystems.

## Team Contributions

**Khoa Duong — Energy Management and Control Lead**  
Responsible for the proposed EMS architecture, sensor acquisition, operating-mode logic, charging supervision, and fault-handling design.

**Peter Hsia — Device Communication and Monitoring**  
Developing iPhone battery-information collection, ESP32-S3 communication, the monitoring interface, and charging-time estimation.

**Matthew Hacker — Solar and Battery Hardware**  
Developing solar generation, battery-charging circuitry, voltage regulation, and protection hardware.

**Anthony Ocampo — Wind Generation**  
Developing turbine mechanics, generator integration, rectification, and wind-power conditioning.

The four members collaborate on system integration, component selection, and overall testing.

## Future Development

As the system progresses, this directory will be updated with controller source code, operating-mode diagrams, test results, and documentation of validated hardware behavior.
