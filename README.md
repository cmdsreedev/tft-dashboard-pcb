# ESP32 TFT Dashboard PCB

A compact two-layer carrier board for building a small ESP32-based dashboard. It connects a 30-pin ESP32 development board to an SPI TFT display and a five-pin rotary encoder, with four M2 mounting holes for mechanical assembly.

> **Project status:** Hardware design / first-revision prototype. Review the connector orientation and module pinouts against your exact ESP32 and TFT modules before fabrication or assembly.

## Features

- Socketed 30-pin ESP32 development board
- 11-pin SPI TFT display connection
- Five-pin JST-XH rotary encoder connection
- Bottom-layer ground plane
- Four non-plated 2.2 mm mounting holes for M2 hardware
- Through-hole construction for straightforward hand assembly
- KiCad source files and FreeCAD mechanical models

## Board specification

| Property | Value |
| --- | --- |
| Board size | 79.2 × 54.46 mm |
| Layers | 2 |
| Substrate | FR-4 |
| Thickness | 1.6 mm |
| Copper weight | 1 oz / 35 µm |
| Signal trace width | 0.25 mm |
| Power trace width | 0.56 mm |
| Mounting holes | 4 × 2.2 mm NPTH |

## Interfaces

### TFT display

The display header carries 3V3, GND, backlight, clock, serial data, data/command, reset, and chip-select signals. The PCB silkscreen identifies pin 1 and the power connections.

### Rotary encoder

The JST-XH connector carries `ENC_CLK`, `ENC_DT`, `ENC_SW`, `3V3`, and `GND`.

## Repository contents

- `tft-design.kicad_pro` — main KiCad project
- `tft-design.kicad_sch` — schematic
- `tft-design.kicad_pcb` — PCB layout
- `tft-design.FCStd` — FreeCAD mechanical model
- `tft-design_resized.FCStd` — alternate/resized mechanical model
- `1.kicad_pro` and `1.kicad_pcb` — additional KiCad design files retained with the project

Fabrication outputs are intentionally not tracked. Generate fresh Gerber and drill files from the current PCB revision before ordering.

## Fabrication export

1. Open `tft-design.kicad_pro` in KiCad 10 or a compatible newer release.
2. Open PCB Editor, refill copper zones, and run the Design Rules Checker.
3. Plot `F.Cu`, `B.Cu`, `F.Mask`, `B.Mask`, `F.SilkS`, `B.SilkS`, and `Edge.Cuts` as Gerbers.
4. Generate both PTH and NPTH Excellon drill files.
5. Load every Gerber and both drill files in Gerber Viewer.
6. Confirm the outline, plated connector holes, non-plated mounting holes, copper, and silkscreen before creating the fabrication ZIP.

## Assembly checks

Before powering the board:

- Confirm the ESP32 header orientation and pin-1 positions.
- Confirm the TFT module uses the expected 11-pin ordering.
- Verify that the TFT module includes suitable backlight current limiting, or add an appropriate external driver/current-limiting solution.
- Check for shorts between `3V3` and `GND`.
- Power the board with a current-limited supply for initial bring-up.

## Software

Firmware is not included in this repository. The chosen display driver and GPIO definitions must match the fitted TFT module and the PCB net assignments.
