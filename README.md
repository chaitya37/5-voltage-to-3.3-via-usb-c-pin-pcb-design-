# USB-C 5V/3.3V Power Module

A compact power supply board that takes USB-C 5V input and provides regulated 5V (passthrough) and 3.3V outputs, with an onboard LED indicator for the 3.3V rail. Designed in KiCad.

## Specs

| Parameter | Value |
|---|---|
| Input | USB-C, 5V (default profile, no PD/QC negotiation) |
| Output 1 | 5V passthrough, up to ~1A |
| Output 2 | 3.3V regulated (AMS1117-3.3), up to ~500mA |
| PCB | 2-layer |

## Schematic

![Schematic](images/schematic.png)

## PCB Layout

![PCB 3D Render](images/pcb_3d_render.png)

## Design Notes

- **CC1/CC2 (5.1kΩ to GND):** Required per USB Type-C spec so the source negotiates default 5V/900mA-1.5A power, without these the connector won't output any power at all.
- **AMS1117-3.3 regulator:** Chosen for simplicity and wide availability. Input/output capacitors (10µF each) placed close to the IC per datasheet recommendations for stability.
- **LED indicator:** Wired in parallel off the 3.3V rail (not in series with the output header) through a 330Ω resistor, so it only lights when the regulator is actually working correctly — doubles as a quick diagnostic.
- **Shield grounding:** USB-C shield tab tied to GND through a 330Ω resistor for basic ESD/EMI mitigation.
- **Ground plane:** Bottom-layer copper pour tied to all GND pads via 4 vias, reducing return path resistance and simplifying top-layer routing.

## Bill of Materials

| Ref | Component | Value/Part | Footprint |
|---|---|---|---|
| J1 | USB-C Receptacle | HRO TYPE-C-31-M-12 | USB_C_Receptacle_HRO_TYPE-C-31-M-12 |
| J2 | Pin Header | 1x3, 2.54mm | PinHeader_1x03_P2.54mm_Vertical |
| U1 | LDO Regulator | AMS1117-3.3 | SOT-223-3_TabPin2 |
| R1, R2 | Resistor | 5.1kΩ | R_0805_2012Metric |
| R3, R4 | Resistor | 330Ω | R_0805_2012Metric |
| C1, C2 | Capacitor | 10µF | C_1206_3216Metric |
| D1 | LED | Generic | LED_0805_2012Metric |

## Files

- `schematic/` — KiCad schematic source + exported PDF
- `pcb/` — KiCad PCB source
- `gerbers/` — Fabrication-ready Gerber + drill files (JLCPCB/PCBWay compatible)
- `bom.csv` — Full bill of materials

## Status

Designed and DRC-clean (0 violations, 0 unconnected nets). Ordered for fabrication — board photos and test results to be added once assembled.

## License

MIT — feel free to use, modify, or build on this design.
