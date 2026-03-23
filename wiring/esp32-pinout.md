# ESP32 pinout — 4-circuit configuration

## Wiring overview

```
                    ┌──────────────────┐
                    │   ESP32 DevKit   │
                    │                  │
    1-Wire bus ◄────┤ GPIO 4           │
                    │                  │
   SPI CLK    ◄────┤ GPIO 18          │
   SPI MISO   ◄────┤ GPIO 19          │
   SPI MOSI   ◄────┤ GPIO 23          │
   PT1000 CS0 ◄────┤ GPIO 5           │
   PT1000 CS1 ◄────┤ GPIO 15          │
                    │                  │
   Relay K0 OPEN ◄─┤ GPIO 25          │
   Relay K0 CLOSE◄─┤ GPIO 26          │
   Relay K1 OPEN ◄─┤ GPIO 27          │
   Relay K1 CLOSE◄─┤ GPIO 14          │
   Relay K2 OPEN ◄─┤ GPIO 32          │
   Relay K2 CLOSE◄─┤ GPIO 33          │
   Relay K3 OPEN ◄─┤ GPIO 12          │
   Relay K3 CLOSE◄─┤ GPIO 13          │
                    │                  │
                    │      3V3  ──────►│── 3.3V to sensors
                    │      GND  ──────►│── Common ground
                    │      VIN  ◄──────│── 5V input
                    └──────────────────┘
```

## 1-Wire bus (DS18B20 sensors)

All DS18B20 sensors share a single bus on GPIO 4. Each sensor has a unique 64-bit address and is individually addressable.

```
GPIO 4 ──┬──── DS18B20 (outdoor)
         │        │
    4.7kΩ├──3V3   ├── DS18B20 (circuit 0)
         │        │
         │        ├── DS18B20 (circuit 2)
         │        │
         │        └── DS18B20 (circuit 3)
         │
        GND
```

**Important:** One 4.7kΩ pullup resistor between GPIO 4 and 3V3 is required for the entire bus. Do not use individual pullups per sensor.

**Cable length:** DS18B20 works reliably up to ~20m with Cat5 cable. For longer runs, use a stronger pullup (2.2kΩ) or an active pullup circuit.

## SPI bus (PT1000 via MAX31865)

PT1000 sensors connect via MAX31865 breakout boards on the shared SPI bus. Each MAX31865 gets its own chip-select (CS) pin.

```
GPIO 18 (CLK)  ──┬── MAX31865 #0 (circuit 0)
GPIO 19 (MISO) ──┤       CS ◄── GPIO 5
GPIO 23 (MOSI) ──┤
                  │
                  └── MAX31865 #1 (circuit 1)
                          CS ◄── GPIO 15
```

## Relay modules

Each circuit uses a 2-channel relay module. The relay coils are driven at 5V via optocouplers; the ESP32 GPIO (3.3V) triggers the optocoupler input (active LOW on most modules).

```
GPIO 25 ── Relay K0 CH1 (OPEN)  ── ARA661 circuit 0 (brown/CW)
GPIO 26 ── Relay K0 CH2 (CLOSE) ── ARA661 circuit 0 (black/CCW)

GPIO 27 ── Relay K1 CH1 (OPEN)  ── ARA661 circuit 1 (brown/CW)
GPIO 14 ── Relay K1 CH2 (CLOSE) ── ARA661 circuit 1 (black/CCW)

GPIO 32 ── Relay K2 CH1 (OPEN)  ── ARA661 circuit 2 (brown/CW)
GPIO 33 ── Relay K2 CH2 (CLOSE) ── ARA661 circuit 2 (black/CCW)

GPIO 12 ── Relay K3 CH1 (OPEN)  ── ARA661 circuit 3 (brown/CW)
GPIO 13 ── Relay K3 CH2 (CLOSE) ── ARA661 circuit 3 (black/CCW)
```

**ARA661 cable colors:**
- Blue = COM (common/neutral)
- Brown = CW (clockwise / open)
- Black = CCW (counter-clockwise / close)

⚠️ The relay contacts switch **230V AC**. Use properly rated relay modules (≥10A/250VAC) and ensure all 230V wiring is done by a qualified electrician.
