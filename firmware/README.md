# AeroHelio ESP32-S3 Firmware

**Primary Contributor:** Peter Hsia  
**Status:** Wi-Fi communication tested; full energy-management integration ongoing.

## Overview

This subsystem provides communication between the ESP32-S3 microcontroller and an iPhone. It allows the ESP32 to receive device battery-percentage measurements, which will later support charging-time estimation and system monitoring.

## Implemented Features

- Configured the ESP32-S3 as a local Wi-Fi access point named `AeroHelio`.
- Implemented an HTTP interface for receiving battery-percentage data.
- Connected an iOS Shortcut that reads the iPhone's battery percentage and transmits it to the ESP32.
- Implemented an endpoint for retrieving the latest received battery measurement.
- Tested automatic transmission triggered by connecting to the AeroHelio Wi-Fi network.
- Verified repeated updates and retrieval of battery data.

## Communication Interface

| Endpoint | Function |
|---|---|
| `POST /battery` | Receives battery-percentage measurements from the iPhone |
| `GET /latest` | Returns the latest stored battery reading |

The ESP32-S3 operates locally without requiring an external Wi-Fi router or internet connection.

## Testing

Wireless communication was tested by sending battery-percentage measurements from an iPhone and verifying the stored readings through the ESP32's HTTP interface.

This established the device-data communication required for the future charging-time estimation subsystem.

## Planned Integration

Future development includes connecting the communication interface to INA226 sensor measurements, system-status monitoring, and the charging-time estimation algorithm.

The full charging-control and monitoring system remains under development.

## Source Code

The ESP32-S3 firmware will be added to this directory along with configuration instructions and supporting test documentation.
