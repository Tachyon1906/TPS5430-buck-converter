# TPS5430 Buck Converter

A configurable step-down converter built around the Texas Instruments **TPS5430** (3 A, 500 kHz, non-synchronous buck). The output voltage is selected with a solder bridge. Designed in **KiCad** as a 2-layer board.
![3D render](Docs/TPS5430_3drender.png)

## Features

- Wide input range: 5.5 V to 36 V
- Selectable output voltage via solder bridge: **1.8 V / 3.3 V / 5 V / 12 V**
- Reverse-polarity protection with an **AO3401A** P-MOSFET
- Input overcurrent protection with a polyfuse (3 A hold / 6 A trip)
- Powered from a standard 2.1 mm / 5.5 mm Arduino-compatible barrel jack
- Status LED
- 2-layer PCB, [W x H mm]
- JLCPCB assembly files (BOM and component placement)

## Specifications

| Parameter | Value |
|---|---|
| Controller | TPS5430 |
| Input voltage | 5.5 V to 36 V (limited per output voltage, see below) |
| Output voltage | 1.8 V / 3.3 V / 5 V / 12 V (solder bridge) |
| Max load current | up to 3 A [confirm against your inductor and thermal limits] |
| Switching frequency | 500 kHz |
| Input protection | AO3401A reverse polarity, 3 A hold / 6 A trip polyfuse |
| PCB | 2-layer, [thickness / copper weight] |
| Tools | KiCad [version], LTspice |

### Input voltage limits per output

The usable input range depends on the output voltage:

- V<sub>in,min</sub> = 1.15 x V<sub>out</sub> (datasheet section 8.2.1.2.8.1)
- V<sub>in,max</sub> = 8.33 x (V<sub>out</sub> + 0.5) (datasheet section 8.2.1.2.8.1)

Both are further limited by the device's 5.5 V to 36 V absolute range.

| V<sub>out</sub> | V<sub>in,min</sub> | V<sub>in,max</sub> |
|---|---|---|
| 1.8 V | 5.5 V | 19.2 V |
| 3.3 V | 5.5 V | 31.7 V |
| 5 V | 5.75 V | 36 V |
| 12 V | 13.8 V | 36 V |

For 1.8 V and 3.3 V, keep the input below the listed maximum. For 12 V, the input must be at least 13.8 V.

## Schematic

Full-resolution PDF: [`Docs/TPS5430_schematic.pdf`](Docs/TPS5430_schematic.pdf)

## PCB

| Top | Bottom |
|---|---|
| ![Top](Docs/TPS5430_top.png) | ![Bottom](Docs/TPS5430_bottom.png) |

Layout notes:
- [Short input-capacitor / IC / catch-diode loop to limit switching noise]
- [Feedback divider routed away from the switch node]
- [Ground pour and thermal vias under the PowerPAD]
