# Bill of Materials

**Team 102 – Project Aurora** · Taylor Callo · Member C: Reminder & Alerts (Hub)

This is the full bill of materials (BOM) for my hub board. It was exported from my KiCad schematic (Tools → Generate BOM, grouped by value) and then filled in with the manufacturer, part number and price for each part. Parts are through-hole wherever possible so the board can be milled at Peralta and hand-soldered. My main subsystem is the **LM386 audio amplifier and speaker** (items 1–2). The real-time clock (items 3–6) is a stretch goal.

Prices are approximate DigiKey prices in US dollars for buying the quantity shown (1-piece pricing). Part-number links open a DigiKey search for that part.

## BOM Table

| Item | Reference(s) | Qty | Description | Manufacturer | Part Number | Package | Unit Price (USD) | Total (USD) |
|:-:|---|:-:|---|---|---|---|:-:|:-:|
| 1 | U3 | 1 | Audio amplifier, gain 20 (main subsystem) | Texas Instruments | [LM386N-1/NOPB](https://www.digikey.com/en/products/result?keywords=LM386N-1/NOPB) | DIP-8 THT | 1.18 | 1.18 |
| 2 | J8 / off-board | 1 | Speaker, 8 Ω (plugs into J8) | Same Sky | [CMS-40558N-L152](https://www.digikey.com/en/products/result?keywords=CMS-40558N-L152) | Off-board | 5.88 | 5.88 |
| 3 | U4 | 1 | Real-time clock, I²C (stretch goal) | Microchip | [MCP7940N-I/P](https://www.digikey.com/en/products/result?keywords=MCP7940N-I/P) | DIP-8 THT | 0.92 | 0.92 |
| 4 | Y1 | 1 | Crystal, 32.768 kHz, 12.5 pF | Abracon | [AB26TRB-32.768KHZ-T](https://www.digikey.com/en/products/result?keywords=AB26TRB-32.768KHZ-T) | Cylinder 2x6 mm THT | 0.35 | 0.35 |
| 5 | BT1 | 1 | Coin cell battery, CR2032, 3 V | Panasonic | [CR2032](https://www.digikey.com/en/products/result?keywords=CR2032) | Coin cell | 0.36 | 0.36 |
| 6 | BT1 | 1 | CR2032 battery holder | Keystone | [1066](https://www.digikey.com/en/products/result?keywords=1066) | THT | 1.12 | 1.12 |
| 7 | Q1 | 1 | N-channel MOSFET (alert LED switch) | Alpha & Omega | [AO3400A](https://www.digikey.com/en/products/result?keywords=AO3400A) | SOT-23 | 0.52 | 0.52 |
| 8 | D7 | 1 | LED, red, high-brightness, 5 mm | Kingbright | [WP7113SEC/J3](https://www.digikey.com/en/products/result?keywords=WP7113SEC/J3) | 5 mm THT | 0.76 | 0.76 |
| 9 | U1 | 1 | 5 V linear regulator, 1.5 A | STMicroelectronics | [L7805CV](https://www.digikey.com/en/products/result?keywords=L7805CV) | TO-220 THT | 0.50 | 0.50 |
| 10 | HS1 | 1 | TO-220 clip-on heatsink | Aavid (Boyd) | [577202B00000G](https://www.digikey.com/en/products/result?keywords=577202B00000G) | TO-220 | 0.70 | 0.70 |
| 11 | J4 | 1 | DC barrel jack, 2.1 mm | Same Sky | [PJ-102AH](https://www.digikey.com/en/products/result?keywords=PJ-102AH) | THT | 0.70 | 0.70 |
| 12 | F1 | 1 | Fuse, 1 A, 250 V, slow-blow, 5x20 mm | Bel Fuse | [5ST 1-R](https://www.digikey.com/en/products/result?keywords=5ST%201-R) | 5x20 mm | 0.40 | 0.40 |
| 13 | F1 | 2 | Fuse clip, 5x20 mm (holder) | Keystone | [3517](https://www.digikey.com/en/products/result?keywords=3517) | THT | 0.30 | 0.60 |
| 14 | D1, D2, D8, D9 | 4 | Schottky diode, 40 V, 1 A | onsemi | [1N5819RLG](https://www.digikey.com/en/products/result?keywords=1N5819RLG) | DO-41 THT | 0.40 | 1.60 |
| 15 | U2 | 1 | PIC18F57Q43 Curiosity Nano dev board (not counted in total) | Microchip | [DM164150](https://www.digikey.com/en/products/result?keywords=DM164150) | Dev board | see note | — |
| 16 | C1 | 1 | Capacitor, 0.33 µF, 50 V, X7R | KEMET | [C330C334K5R5TA](https://www.digikey.com/en/products/result?keywords=C330C334K5R5TA) | Radial THT | 0.60 | 0.60 |
| 17 | C2, C3, C4, C8, C13, C20, C21 | 7 | Capacitor, 0.1 µF, 50 V, X7R | KEMET | [C320C104K5R5TA](https://www.digikey.com/en/products/result?keywords=C320C104K5R5TA) | Radial THT | 0.30 | 2.10 |
| 18 | C5, C6, C7 | 3 | Capacitor, 1 µF, 50 V, X7R (≥ 16 V needed) | KEMET | [C330C105K5R5TA](https://www.digikey.com/en/products/result?keywords=C330C105K5R5TA) | Radial THT | 0.55 | 1.65 |
| 19 | C9 | 1 | Capacitor, 100 µF, 16 V, electrolytic | Nichicon | [UVR1C101MED](https://www.digikey.com/en/products/result?keywords=UVR1C101MED) | Radial THT | 0.27 | 0.27 |
| 20 | C10 | 1 | Capacitor, 10 µF, 16 V, electrolytic | Nichicon | [UVR1C100MDD](https://www.digikey.com/en/products/result?keywords=UVR1C100MDD) | Radial THT | 0.20 | 0.20 |
| 21 | C11 | 1 | Capacitor, 0.047 µF, 50 V, X7R | KEMET | [C320C473K5R5TA](https://www.digikey.com/en/products/result?keywords=C320C473K5R5TA) | Radial THT | 0.35 | 0.35 |
| 22 | C12 | 1 | Capacitor, 220 µF, 16 V, electrolytic | Nichicon | [UVR1C221MED](https://www.digikey.com/en/products/result?keywords=UVR1C221MED) | Radial THT | 0.35 | 0.35 |
| 23 | C14, C15 | 2 | Capacitor, 22 pF, 50 V, C0G | KEMET | [C315C220J5G5TA](https://www.digikey.com/en/products/result?keywords=C315C220J5G5TA) | Radial THT | 0.30 | 0.60 |
| 24 | R1, R3, R5, R11, R19 | 5 | Resistor, 10 kΩ, 1/4 W | Stackpole | [CF14JT10K0](https://www.digikey.com/en/products/result?keywords=CF14JT10K0) | Axial THT | 0.10 | 0.50 |
| 25 | R2, R4, R6, R12, R20, R21 | 6 | Resistor, 1 kΩ, 1/4 W | Stackpole | [CF14JT1K00](https://www.digikey.com/en/products/result?keywords=CF14JT1K00) | Axial THT | 0.10 | 0.60 |
| 26 | R7, R8, R9, R10 | 4 | Resistor, 330 Ω, 1/4 W | Stackpole | [CF14JT330R](https://www.digikey.com/en/products/result?keywords=CF14JT330R) | Axial THT | 0.10 | 0.40 |
| 27 | R13 | 1 | Resistor, 10 Ω, 1/4 W | Stackpole | [CF14JT10R0](https://www.digikey.com/en/products/result?keywords=CF14JT10R0) | Axial THT | 0.10 | 0.10 |
| 28 | R14 | 1 | Resistor, 100 Ω, 1/4 W | Stackpole | [CF14JT100R](https://www.digikey.com/en/products/result?keywords=CF14JT100R) | Axial THT | 0.10 | 0.10 |
| 29 | R15 | 1 | Resistor, 100 kΩ, 1/4 W | Stackpole | [CF14JT100K](https://www.digikey.com/en/products/result?keywords=CF14JT100K) | Axial THT | 0.10 | 0.10 |
| 30 | R16 | 1 | Resistor, 150 Ω, 1/4 W | Stackpole | [CF14JT150R](https://www.digikey.com/en/products/result?keywords=CF14JT150R) | Axial THT | 0.10 | 0.10 |
| 31 | R17, R18 | 2 | Resistor, 4.7 kΩ, 1/4 W | Stackpole | [CF14JT4K70](https://www.digikey.com/en/products/result?keywords=CF14JT4K70) | Axial THT | 0.10 | 0.20 |
| 32 | D3 | 1 | LED, green, 5 mm (Ready) | Kingbright | [WP7113GD](https://www.digikey.com/en/products/result?keywords=WP7113GD) | 5 mm THT | 0.30 | 0.30 |
| 33 | D4 | 1 | LED, blue, 5 mm (Taken) | Kingbright | [WP7113QBC/D](https://www.digikey.com/en/products/result?keywords=WP7113QBC/D) | 5 mm THT | 0.45 | 0.45 |
| 34 | D5, D6 | 2 | LED, red, 5 mm (Error, Debug) | Kingbright | [WP7113ID](https://www.digikey.com/en/products/result?keywords=WP7113ID) | 5 mm THT | 0.30 | 0.60 |
| 35 | SW1, SW2, SW3 | 3 | Tactile push button, 6 mm (Take Dose, Set/Mode, Debug) | TE Connectivity | [1825910-6](https://www.digikey.com/en/products/result?keywords=1825910-6) | THT | 0.15 | 0.45 |
| 36 | J1, J2, J3 | 3 | Shrouded box header, 2x4, 2.54 mm (ribbon cables) | Würth Elektronik | [61200821621](https://www.digikey.com/en/products/result?keywords=61200821621) | THT | 0.70 | 2.10 |
| 37 | J5, J6, J8, JP1 | 4 | Pin header, 1x2, 2.54 mm | Sullins | [PRPC002SAAN-RC](https://www.digikey.com/en/products/result?keywords=PRPC002SAAN-RC) | THT | 0.10 | 0.40 |
| 38 | JP1 | 1 | Jumper shunt, 2.54 mm | Sullins | [QPC02SXGN-RC](https://www.digikey.com/en/products/result?keywords=QPC02SXGN-RC) | — | 0.10 | 0.10 |
| 39 | J7 | 1 | Pin header, 1x14, 2.54 mm (expansion) | Sullins | [PRPC014SAAN-RC](https://www.digikey.com/en/products/result?keywords=PRPC014SAAN-RC) | THT | 0.45 | 0.45 |
| 40 | TP1–TP6 | 6 | Test points (bare PCB pads, no part to buy) | — | — | PCB pad | 0.00 | 0.00 |
| 41 | Off-board | 1 | Wall adapter, 9 V, 2 A, 5.5x2.1 mm plug | Triad Magnetics | [WSU090-2000](https://www.digikey.com/en/products/result?keywords=WSU090-2000) | Off-board | 12.43 | 12.43 |
| | | **80** | | | | | **Total** | **41.09** |

## Summary

| | |
|---|---|
| Unique line items | 41 |
| Total parts | 80 (including 6 test-point pads that need no part) |
| Total cost (one board) | **41.09 USD**, not counting the Curiosity Nano |
| Main subsystem (amplifier + speaker + support parts) | about 9.63 USD |
| Most expensive item | Wall adapter (12.43 USD), then the speaker (5.88 USD) |

## Notes

- The **speaker** and **wall adapter** are off-board parts. The speaker plugs into J8 and the adapter plugs into J4.
- **C5–C7** need at least 16 V. I chose 50 V parts because they cost about the same and are easier to find.
- **TP1–TP6** are bare copper pads on the PCB, so there is nothing to buy.
- The **Curiosity Nano** (U2) is a development board that plugs into headers, so it is listed but not counted in the board's part total.
- The KiCad BOM export is saved in this folder as a spreadsheet: [TC_Hub_BOM.csv](TC_Hub_BOM.csv).
