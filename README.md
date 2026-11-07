# AeroHelio: Smart Solar and Wind Charging System

**University of California, Riverside | EE 175 Senior Design | 2026–2027**

**Project Status:** In Development

## Project Overview

AeroHelio is a portable renewable-energy charging system designed to combine solar and wind generation with rechargeable battery storage and regulated power delivery.

The system is intended to provide USB-C charging for portable devices while using an ESP32-S3 microcontroller to monitor electrical conditions, manage charging operations, and estimate the remaining time required to charge a connected device.

A central engineering challenge is coordinating power from sources whose outputs change with environmental conditions while maintaining reliable and regulated power for the load.

## Project Team

AeroHelio is being developed by a four-member electrical engineering senior design team at the University of California, Riverside.

| Team Member | Primary Responsibilities |
|---|---|
| Peter Hsia | ESP32-S3 and iPhone communication, monitoring interface, battery-percentage collection, Energy-management software and charging-time estimation algorithm |
| Khoa Duong | Energy-management software, sensor integration, operating modes, charging supervision, and fault handling |
| Matthew Hacker | Solar generation, battery charging and protection, voltage regulation, and power distribution |
| Anthony Ocampo | Wind turbine CAD and mechanical design, generator selection, rectification, and turbine integration |

All four members collaborate on overall system architecture, component selection, hardware integration, and testing.


## System Architecture

The proposed system consists of several interconnected subsystems.

### Solar Power Generation
- ECO-WORTHY 25 W solar panel
- Ideal-diode protection to prevent reverse current
- INA226 monitoring for voltage and current measurements
- BQ24650-based charging circuit for power regulation and battery charging

### Wind Power Generation
- Custom 3D-printed wind turbine
- Motor used as an electrical generator
- Bridge rectification and voltage conditioning
- Integration with the shared power system

The wind generation and regulation circuitry are under development.

### Battery Storage and Power Delivery
- 3S lithium-ion battery pack with battery-management protection
- Regulated power distribution between renewable sources, battery storage, and output load
- Fuse and reverse-current protection
- 5 V buck conversion for USB-powered devices

The battery integration, power-routing behavior, and complete charging hardware require further implementation and validation.

### Embedded Monitoring and Control
- ESP32-S3 microcontroller
- INA226 voltage, current, and power measurements through I2C
- Monitoring of renewable generation, battery conditions, and load demand
- Control interfaces for charging and power-management circuitry
- Local Wi-Fi communication with an iPhone

The ESP32-S3 communication prototype has been tested. Full sensor integration and hardware control are ongoing.

## ESP32-S3 and iPhone Communication

One completed milestone is establishing wireless communication between an iPhone and the ESP32-S3 without requiring an external router.

The ESP32-S3 creates a local Wi-Fi network named `AeroHelio`. An iOS Shortcut obtains the iPhone's battery percentage and sends it to the ESP32 through an HTTP request.

**Communication sequence:**

1. The iPhone connects to the AeroHelio Wi-Fi network.
2. An iOS Shortcut retrieves the current iPhone battery percentage.
3. The Shortcut sends the percentage to the ESP32-S3 using `POST /battery`.
4. The ESP32 stores the latest received reading.
5. The stored information can be retrieved using `GET /latest`.

### Verified Testing

- Successfully configured the ESP32-S3 as a Wi-Fi access point.
- Confirmed HTTP communication between the iPhone and ESP32-S3.
- Successfully transmitted and retrieved battery-percentage measurements.
- Tested an iOS automation triggered by joining the AeroHelio Wi-Fi network.
- Verified repeated battery-percentage updates during a periodic transmission test.

These tests validate the wireless data-communication subsystem, not the complete renewable charging system.

## Adaptive Charging-Time Estimation

An ongoing part of AeroHelio is developing an algorithm that estimates how much time remains before a connected device reaches its target battery level.

Unlike a constant-rate calculation, the proposed approach accounts for changes in available charging power and battery-charging behavior.

### Proposed Inputs
- Current device battery percentage
- Measured output voltage and current
- Available charging power
- Previous battery-percentage measurements and timestamps
- Changes in renewable-energy input

### Proposed Method

The algorithm will estimate the effective charging rate from measured data and use it to predict the remaining charging time. As new sensor measurements and battery-percentage updates become available, the prediction will be recalculated.

The intended goal is to produce estimates that respond to changing operating conditions rather than assuming charging power remains constant.

### Planned Validation

The algorithm will be evaluated by comparing predicted charging times against actual charging progress under different input-power and battery conditions.

Prediction error, update behavior, and sensitivity to changing power availability will be considered.

**Status:** Algorithm development and experimental validation are ongoing. Prediction accuracy has not yet been established.

## My Contributions

My work on AeroHelio focuses on embedded communication, system integration, electrical architecture, and charging-time estimation.

Contributions include:

- Implementing and testing ESP32-S3 wireless communication with an iPhone using HTTP and iOS Shortcuts.
- Developing the battery-percentage reporting and retrieval interface.
- Contributing to system architecture and power-path planning, including voltage regulation, switching, and reverse-current protection.
- Developing the charging-time estimation approach and identifying the measurements required for its implementation.
- Participating in system integration, troubleshooting, and validation planning.

AeroHelio is a collaborative senior design project, with other team members contributing to solar generation, wind generation, battery integration, and additional electrical and mechanical subsystems.

## Current Progress

| Subsystem | Status |
|---|---|
| Overall system architecture | Design documented; revisions ongoing |
| ESP32-S3 local Wi-Fi network | Tested |
| iPhone battery-percentage transmission | Tested |
| Automated wireless updates | Tested |
| INA226 sensor integration | In development |
| Solar charging and regulation | In development |
| Wind turbine and rectification | In development |
| Battery and regulated USB-C charging | In development |
| Adaptive charging-time algorithm | In development |
| Full system integration | Planned |
| Charging-time accuracy validation | Planned |

## Next Steps

The next development phase focuses on integrating the electrical subsystems with the ESP32-S3, verifying sensor measurements, validating source and battery power flow, and implementing the charging-time prediction algorithm.

Further documentation and experimental results will be added as the project progresses.

## Project Documentation

The repository will include design diagrams, firmware, testing records, and algorithm documentation as development continues.

The system block diagram represents the proposed design and may change as components are tested and revised.
