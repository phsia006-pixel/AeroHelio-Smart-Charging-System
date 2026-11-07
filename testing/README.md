
# AeroHelio Testing and Validation

This directory documents completed subsystem tests and planned system validation.

## Test 1: ESP32-S3 and iPhone Communication

**Status: Successfully tested**

### Objective
Establish wireless communication between an ESP32-S3 and an iPhone without requiring an external router.

### Implementation
- Configured the ESP32-S3 as a local Wi-Fi access point.
- Created an iOS Shortcut to retrieve the iPhone battery percentage.
- Implemented an HTTP endpoint to receive battery measurements.
- Implemented a second endpoint to retrieve the latest stored measurement.
- Configured an iOS automation triggered by joining the AeroHelio Wi-Fi network.

### Endpoints

`POST /battery` - Receives an updated battery percentage.

`GET /latest` - Returns the most recently received battery reading.

### Results

Successfully transmitted iPhone battery-percentage measurements to the ESP32-S3 and retrieved the stored values.

Verified repeated data updates through the HTTP interface.

### Limitations

This test validates wireless communication and data transfer. It does not establish the accuracy of charging-time predictions or validate the complete charging hardware.

## Future Tests

- INA226 voltage and current measurements
- Battery charging and discharging behavior
- Solar and wind input characterization
- Regulated 5 V output
- Charging-time prediction accuracy
- Full system integration
