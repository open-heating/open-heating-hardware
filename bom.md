# Bill of materials

## Base station (once per installation)

| Component | Description | Qty | Price (approx.) | Source |
|---|---|---|---|---|
| ESP32 DevKit V1 | ESP-WROOM-32, USB-C | 1 | €6 | AliExpress, Amazon |
| Raspberry Pi 4 Model B | 2GB+ RAM, for hub (optional) | 1 | €45–70 | BerryBase, Amazon |
| Pi power supply | USB-C 5V/3A | 1 | €10 | BerryBase |
| MicroSD card | 32GB+ for Pi | 1 | €8 | Amazon |
| 5V power supply | For ESP32 + sensors, DIN rail mount | 1 | €8 | Amazon |
| DS18B20 outdoor sensor | Waterproof, 1m+ cable | 1 | €3 | AliExpress, Amazon |
| 4.7kΩ resistor | 1-Wire bus pullup | 1 | €0.10 | Any |
| DIN rail enclosure | For ESP32 + relay modules | 1 | €10–15 | Amazon |
| Wago 221 connectors | Assorted 2/3/5-way | 1 set | €15 | Amazon, Hornbach |

**Base station total: ~€105–130** (with Pi) or **~€45–55** (without Pi)

## Per heating circuit

| Component | Description | Qty | Price (approx.) | Source |
|---|---|---|---|---|
| 2-channel relay module | 5V coil, 230V/10A contacts, optocoupler | 1 | €3 | AliExpress, Amazon |
| ESBE ARA661 | 230V 3-point actuator, 60s, 6Nm | 1 | €80–120 | Heating supplier |
| DS18B20 | Waterproof, pipe-mount or immersion | 1 | €3 | AliExpress, Amazon |
| **OR** PT1000 + MAX31865 | For higher precision circuits | 1+1 | €5 + €8 | AliExpress, Adafruit |

**Per circuit total: ~€86–134** (depending on sensor and actuator sourcing)

## 4-circuit installation total

| | With Pi | Without Pi |
|---|---|---|
| Base station | €130 | €55 |
| 4x circuits (DS18B20) | €344 | €344 |
| **Total** | **~€474** | **~€399** |

*Note: ESBE ARA661 actuator pricing varies significantly. Prices above assume retail; bulk or trade pricing can be considerably lower. The actuator is the most expensive component per circuit.*

## GPIO assignment (4-circuit default)

| GPIO | Function |
|---|---|
| 4 | 1-Wire bus (DS18B20 sensors) |
| 18 | SPI CLK (PT1000 via MAX31865) |
| 19 | SPI MISO |
| 23 | SPI MOSI |
| 5 | SPI CS — PT1000 circuit 0 |
| 15 | SPI CS — PT1000 circuit 1 |
| 25 | Relay OPEN — circuit 0 |
| 26 | Relay CLOSE — circuit 0 |
| 27 | Relay OPEN — circuit 1 |
| 14 | Relay CLOSE — circuit 1 |
| 32 | Relay OPEN — circuit 2 |
| 33 | Relay CLOSE — circuit 2 |
| 12 | Relay OPEN — circuit 3 |
| 13 | Relay CLOSE — circuit 3 |

*Note: GPIOs 34–39 are input-only on ESP32 and cannot drive relays. GPIO 2 is connected to the onboard LED. Avoid GPIO 0, 6–11 (flash SPI).*

## Tools needed

- Soldering iron (for pullup resistor, optional headers)
- Multimeter
- Wire strippers
- Wago connector tool (or screwdriver terminals)
- Qualified electrician for 230V wiring
