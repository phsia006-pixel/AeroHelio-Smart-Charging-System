# AeroHelio Solar Power and Battery Charging Subsystem

**Subsystem Lead:** Matthew Hacker  
**Project:** AeroHelio | UC Riverside Senior Design 2026–2027  
**Status:** Design and component selection completed; hardware testing and integration ongoing.

## Overview

The solar subsystem is designed to collect renewable energy from a photovoltaic panel and supply regulated power to AeroHelio's shared energy-storage and distribution system.

A major design consideration is balancing power generation, panel weight, size, efficiency, and cost while ensuring that the battery and connected devices receive appropriate electrical protection.

## Proposed System Architecture

The solar power path follows this general arrangement:

**Solar Panel → Reverse-Current Protection → INA226 Sensor → Solar Charge Controller → Shared Power System**

The shared system connects to the lithium-ion battery and regulated device-output circuitry.

### Main Components

| Component | Function |
|---|---|
| ECO-WORTHY 25 W Solar Panel | Generates electrical power from sunlight |
| INA226 Power Monitor | Measures panel voltage and current |
| BQ24650 Solar Charge Controller | Proposed regulation of charging voltage and current |
| Reverse-Current Protection | Prevents unwanted current flow into the solar panel |
| Fuse | Provides appropriate wiring and circuit protection |
| 3S Lithium-Ion Battery | Stores energy for use when renewable generation is insufficient |
| ESP32-S3 | Receives measurements and provides supervisory control |

The battery is rated at approximately 11.1 V nominal and 12.6 V fully charged, with a listed capacity of 4.5 Ah.

Component ratings and charger compatibility must be verified before final electrical integration.

## Engineering Design Considerations

### 1. Solar Panel Selection

The solar panel was selected with consideration for:

- Available power under different sunlight conditions
- Panel voltage and current ratings
- Weight and physical dimensions
- Electrical compatibility with the battery-charging system
- Cost and portability

An earlier 30 W panel was evaluated before the project moved toward the ECO-WORTHY 25 W option.

### 2. Battery Charging

The proposed charging architecture uses a BQ24650-based solar charger to regulate energy delivered from the panel.

The charging circuit must maintain appropriate voltage and current limits for the 3S lithium-ion battery.

The battery's existing protection circuitry and the external charger serve different purposes. The charger regulates charging, while the battery protection circuit provides additional safeguards.

### 3. Monitoring and Protection

INA226 measurements will allow the ESP32-S3 to monitor electrical conditions.

The proposed protection design includes reverse-current prevention, appropriate fusing, and battery-management protection.

The final choice between diode-based and ideal-diode protection, along with fuse sizing, will depend on component specifications and measurements.

### 4. System Integration

The solar subsystem will interact with the other AeroHelio subsystems to support renewable generation, battery charging, and regulated device output.

Its performance will be evaluated alongside the wind turbine and energy-management system.

## Development Progress

### Completed Design Work

- Researched solar panels and evaluated power, size, weight, and cost constraints.
- Selected the ECO-WORTHY 25 W solar panel in the revised design.
- Identified INA226 sensors for voltage and current monitoring.
- Investigated compatible charging and protection components.
- Contributed to the system architecture and bill of materials.
- Ordered initial components for testing.

### In Development

- Solar panel electrical characterization
- Charger and protection-circuit verification
- INA226 sensor integration
- Battery-charging hardware integration
- Power distribution and system-level control

Initial solar-panel testing was delayed by weather conditions. Validated panel performance measurements have not yet been documented here.

## Planned Testing and Validation

1. Measure solar-panel voltage and current under different sunlight conditions.
2. Evaluate available electrical power under a controlled load.
3. Verify charger input requirements and battery-charging limits.
4. Test reverse-current protection and voltage losses.
5. Validate INA226 measurements against reference instruments.
6. Verify battery-charging behavior with appropriate protection.
7. Evaluate solar generation during integrated system operation.

Final electrical performance will be reported after testing.

## Team Contributions and Collaboration

**Matthew Hacker — Solar Subsystem Lead**

Responsible for solar-panel research and selection, battery-charging hardware, protection design, component compatibility, and solar subsystem development.

**Khoa Duong — Energy Management and Control**

Developing sensor acquisition, operating-mode selection, charge supervision, and fault-handling logic that will interface with the solar hardware.

**Peter Hsia — Monitoring and Charging-Time Estimation**

Developing device communication, battery-percentage collection, monitoring interfaces, and charging-time estimation using measurements from the integrated system.

**Anthony Ocampo — Wind Generation**

Developing the turbine and generator subsystem, which will contribute renewable power alongside the solar branch.

The team collaborates on overall system architecture, component selection, hardware integration, and testing.

## Documentation

Additional circuit diagrams, experimental results, component specifications, and implementation updates will be added as the subsystem develops.

This README describes the design and development plan. Components and circuit arrangements may change following testing.
