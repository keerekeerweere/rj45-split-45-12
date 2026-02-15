# rj45-split-45-12

Schematic-only KiCad project for combining Ethernet and DSMR P1 over a single cable run.

## Purpose

This project documents a passive wiring method where one physical RJ45 cable carries:

- 10/100 Mbps Ethernet
- DSMR P1 smart meter connection (via RJ12)

The setup uses:

- A standard passive RJ45 splitter at each end
- A custom RJ12 <-> RJ45 adapter at each end (before/after the splitters)

## Scope

- This repository contains a wiring schematic, not a PCB design.
- `rj45-split-45-12.kicad_pcb` is only an empty placeholder file.
- The relevant content is in `rj45-split-45-12.kicad_sch`.

## What Is Custom Here

- The custom part is the RJ12 <-> RJ45 wiring mapping used for the DSMR P1 path.
- The rest of the schematic content is included as reference context.

## Pinout Summary

### 1) Passive RJ45 Splitter (1x RJ45 <-> 2x RJ45)

For 10/100 Ethernet + P1 sharing on one cable:

- Ethernet branch uses pins `1,2,3,6`
- P1 branch uses pins `4,5,7,8`

| Trunk RJ45 Pin | Ethernet RJ45 Branch | P1 RJ45 Branch |
|---|---|---|
| 1 | 1 | - |
| 2 | 2 | - |
| 3 | 3 | - |
| 4 | - | 4 |
| 5 | - | 5 |
| 6 | 6 | - |
| 7 | - | 7 |
| 8 | - | 8 |

### 2) RJ45 Ethernet (TIA-568B, 10/100Base-TX)

| RJ45 Pin | T568B Color | 10/100 Signal |
|---|---|---|
| 1 | White/Orange | TX+ |
| 2 | Orange | TX- |
| 3 | White/Green | RX+ |
| 4 | Blue | Unused in 10/100 |
| 5 | White/Blue | Unused in 10/100 |
| 6 | Green | RX- |
| 7 | White/Brown | Unused in 10/100 |
| 8 | Brown | Unused in 10/100 |

### 3) RJ12 DSMR P1 Port (6P6C)

| RJ12 Pin | P1 Signal |
|---|---|
| 1 | +5V |
| 2 | Data Request |
| 3 | Data GND |
| 4 | NC |
| 5 | Data |
| 6 | Power GND |

### 4) Custom RJ12 <-> RJ45 Adapter (This Project)

This custom mapping is used so P1 can run over the splitter's secondary pair set (`4,5,7,8`):

| RJ12 Pin | P1 Signal | RJ45 Pin (P1 Branch) |
|---|---|---|
| 1 | +5V | 7 |
| 2 | Data Request | 8 |
| 3 | Data GND | 5 |
| 4 | NC | - |
| 5 | Data | 4 |
| 6 | Power GND | 5 (tied with pin 3) |

## Files

- `rj45-split-45-12.kicad_sch`: Main wiring schematic.
- `rj45-split-45-12.kicad_pro`: KiCad project file.
- `rj45-split-45-12.kicad_prl`: Local KiCad preferences/state.
- `rj45-split-45-12-backups/`: KiCad backup archives.

## Open In KiCad

1. Open KiCad 9.
2. Open `rj45-split-45-12.kicad_pro`.
3. Inspect `rj45-split-45-12.kicad_sch`.

## Note

This is a reference wiring project only; no manufacturing outputs are included.
