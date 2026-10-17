---
title: Power Budget
---

# Power Budget

**Team 102 – Project Aurora** · Taylor Callo · Member C: Reminder & Alerts (Hub)

This page checks that my wall adapter and voltage regulators can power everything on my hub board at the same time, with a 25% safety margin on top. It follows the course power budget template: each part that uses power is put on one power rail, each rail's total is multiplied by 1.25, and then I check that the regulators and wall adapter still have current left over. All currents are the maximum values from each part's datasheet unless I say it is an estimate.

## +5V Power Rail

| +5V Power Rail | Component Name | Part Number | Supply Voltage Range | Qty. | Absolute Maximum Current (mA) | Total Current (mA) | Unit |
|---|---|---|---|:-:|:-:|:-:|:-:|
| | Audio Amplifier | LM386N-1/NOPB | 4 V – 12 V | 1 | 258 | 258 | mA |
| | Alert LED | WP7113SEC/J3 | 5 V rail (150 Ω resistor) | 1 | 20 | 20 | mA |
| | Curiosity Nano (powers the +3.3V rail) | DM164150 | 5 V (VBUS) | 1 | 130.4 | 130.4 | mA |
| | | | | | **Subtotal** | **408.4** | **mA** |
| | | | | | **Safety Margin** | **25%** | |
| | | | | | **Total Current Required on +5V Rail** | **510.5** | **mA** |
| **Regulator** | +5V Linear Regulator | L7805CV | 7 V – 35 V | 1 | 1500 | 1500 | mA |
| | | | | | **Total Remaining Current Available on +5V Rail** | **989.5** | **mA** |

- **LM386:** uses up to 8 mA just being on, plus up to 250 mA at the loudest point of the beep going to the 8 Ω speaker.
- **Curiosity Nano:** its built-in 3.3 V regulator gets its power from this 5 V rail, so it pulls the same current as everything on the +3.3V rail below.
- **Not listed** (per the assignment): the AO3400A switch (it turns the LED on and off but uses almost no power itself), the speaker (its current is already counted in the LM386 line), and resistors and capacitors.

## +3.3V Power Rail

| +3.3V Power Rail | Component Name | Part Number | Supply Voltage Range | Qty. | Absolute Maximum Current (mA) | Total Current (mA) | Unit |
|---|---|---|---|:-:|:-:|:-:|:-:|
| | Microcontroller + debugger | PIC18F57Q43 Curiosity Nano | 1.8 V – 5.5 V | 1 | 100 | 100 | mA |
| | Real-Time Clock | MCP7940N-I/P | 1.8 V – 5.5 V | 1 | 0.4 | 0.4 | mA |
| | Status LEDs | Standard indicator LEDs | 3.3 V rail | 3 | 10 | 30 | mA |
| | | | | | **Subtotal** | **130.4** | **mA** |
| | | | | | **Safety Margin** | **25%** | |
| | | | | | **Total Current Required on +3.3V Rail** | **163.0** | **mA** |
| **Regulator** | +3.3V Regulator (built into the Nano) | MIC5353 | 2.6 V – 6 V | 1 | 500 | 500 | mA |
| | | | | | **Total Remaining Current Available on +3.3V Rail** | **337.0** | **mA** |

- **Microcontroller:** 100 mA is my estimate for the PIC running at full speed plus the Nano's built-in programmer/debugger. The Curiosity Nano guide doesn't give one single maximum number.
- **Clock:** uses at most 0.4 mA while talking to the PIC, and only 1.2 µA the rest of the time.
- **Status LEDs:** these are regular LEDs. I listed them anyway because together they add 30 mA, which isn't tiny.
- **Ribbon-cable signals** going to the other boards use less than 0.1 mA total, so they are not listed.

## External Power Source

| External Power Source 1 | Component Name | Part Number | Supply Voltage Range | Output Voltage | Absolute Maximum Current (mA) | Total Current (mA) | Unit |
|---|---|---|---|:-:|:-:|:-:|:-:|
| **Power Source 1 Selection** | Plug-in Wall Supply | Triad Magnetics WSU090-2000 | 100 – 240 VAC | +9 V | 2000 | 2000 | mA |
| **Power Rails Connected to External Power Source 1** | +5V Regulator | L7805CV | 7 V – 35 V | +5 V | 1500 | 1500 | mA |
| | | | | | **Total Remaining Current Available on External Power Source 1** | **500** | **mA** |

- Even if the 5 V regulator used its full 1.5 A, the adapter would still have 500 mA left over, so the remaining current is positive and the adapter is big enough.
- The +3.3V regulator doesn't connect to the adapter directly. It gets its power from the +5V rail, so its current is already counted there.
- The adapter's plug is 5.5 × 2.1 mm with positive in the center, which fits the board's Same Sky PJ-102AH barrel jack. Don't order the "WSU090-2000-R" version, because its polarity is flipped.

## Regulator Choices

| Rail | Choice | Also considered | Why |
|---|---|---|---|
| +5V | L7805CV (linear, 1.5 A) | LM2940CT-5.0 (linear); R-78E5.0-1.0 (switching) | It follows the course rule of using a linear regulator, gives about 3× the current I need, works with cheap capacitors, and is the cheapest. The full comparison is on my [Component Selection](../02-Component-Selection/Component-Selection.md) page. |
| +3.3V | MIC5353 (built into the Nano, 500 mA) | MCP1700-3302E/TO (250 mA) | It already comes on the Curiosity Nano at no extra cost, and 500 mA is about 3× the 163 mA I need. Adding a separate regulator would only add parts and take up board space. |

### Heat check (L7805CV)

| Check | Result |
|---|---|
| Heat made: (9 V − 5 V) × 0.51 A + regulator's own use | about 2.1 W |
| Without a heatsink (50 °C/W) | about 130 °C, **too hot** (limit 125 °C) |
| With a TO-220 heatsink (25 °C/W or better) | about 89 °C, **safe** |

A linear regulator gets rid of the extra 4 V (9 V in, 5 V out) by turning it into heat. Without a heatsink it would get too hot at the worst case, so I will add a clip-on TO-220 heatsink. In normal use the speaker and alert LED are only on during a reminder, so most of the time it will run much cooler than this worst case.

## Calculated Battery Life

My hub board runs from the wall adapter, so it doesn't have a main battery. The only battery is the small coin cell that keeps the clock running when the adapter is unplugged.

| Calculated Battery Life | Component Name | Part Number | Supply Voltage Range | | Capacity (mAh) | Required By RTC (mA) | Unit |
|---|---|---|---|---|:-:|:-:|:-:|
| | RTC Backup Battery | Panasonic CR2032 | +3 V | | 225 | 0.0012 | mA |
| | | | | | **Battery Life** | **187,500** | **hours** |

187,500 hours is about 21 years. That is longer than the battery's shelf life of about 10 years, so the backup battery should last as long as the product does.

## Notes

- The 9 V input is above the 7 V the L7805CV needs to work (5 V out + 2 V it needs as extra).
- The hub is one single board, so one power budget covers everything.
