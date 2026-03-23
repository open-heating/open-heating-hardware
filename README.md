# open-heating/hardware

Hardware designs, wiring diagrams, and bill of materials for open-heating controllers.

## Overview

This repository contains everything needed to build the physical hardware for an open-heating installation:

- **Wiring diagrams** for connecting ESP32 to sensors, relays, and actuators
- **KiCad schematics** for a custom PCB (optional — perfboard works fine)
- **Bill of materials** with sourcing links
- **Enclosure designs** for 3D printing or DIN rail mounting

## Safety warning

⚠️ **This project involves 230V mains voltage.** Wiring of relay modules to ESBE ARA661 actuators must be performed by a qualified electrician in accordance with local electrical codes. The ESP32 and sensor side operates at safe 3.3V/5V levels, but the relay outputs switch 230V AC.

## Bill of materials

See [bom.md](bom.md) for the complete parts list with approximate pricing.

## Wiring

See [wiring/](wiring/) for connection diagrams:

- `esp32-pinout.md` — GPIO assignments for 4-circuit configuration
- `relay-actuator.md` — 230V relay to ESBE ARA661 wiring
- `sensor-bus.md` — DS18B20 1-Wire bus and PT1000 SPI connections

## PCB (optional)

The `kicad/` directory contains a KiCad 8 project for a custom carrier board. This is optional — the system works perfectly with off-the-shelf modules on a perfboard or in a Wago-based terminal box.

## License

Apache License 2.0
