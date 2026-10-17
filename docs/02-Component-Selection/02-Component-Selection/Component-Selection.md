---
title: Component Selection
---

# Component Selection

**Team 102 – Project Aurora** · Taylor Callo · Member C: Reminder & Alerts (Hub)

This page compares at least three real options for every major component on my Reminder & Alerts hub board and explains which one I chose and why. The hub keeps the dose schedule with a real-time clock, alerts the user with a speaker and a bright LED, and is powered from a 9 V wall adapter through a 5 V linear regulator. The microcontroller (PIC18F57Q43 Curiosity Nano) was selected for us, and passives, push buttons, and ordinary indicator LEDs are not included, per the assignment.

Prices are for quantity 1 in USD, checked on 10/14/2026. The board is milled at the Peralta lab and hand-soldered, so through-hole or easy-to-solder packages are preferred.

## Summary of Selections

| Major component | Subsystem | Selected part | Unit cost |
|---|---|---|---|
| Audio amplifier | **Reminder & Alerts (Hub)** | Texas Instruments LM386N-1/NOPB | $1.18 |
| Speaker | **Reminder & Alerts (Hub)** | Same Sky CMS-40558N-L152 | $5.88 |
| Real-time clock | **Reminder & Alerts (Hub)** | Microchip MCP7940N-I/P | $0.92 |
| RTC backup battery | **Reminder & Alerts (Hub)** | Panasonic CR2032 + Keystone 1066 holder | $0.36 + $1.12 |
| Alert LED switch | **Reminder & Alerts (Hub)** | Alpha & Omega AO3400A | $0.52 |
| High-brightness alert LED | **Reminder & Alerts (Hub)** | Kingbright WP7113SEC/J3 | $0.76 |
| 5 V voltage regulator | **Power (Hub board)** | STMicroelectronics L7805CV | $0.50 |
| External power supply | **Power (Hub board)** | Triad Magnetics WSU090-2000 | $12.43 |

---

## 1. Audio Amplifier — **Reminder & Alerts (Hub)**

Amplifies the PWM tone from microcontroller pin RC2 so it can drive an 8 Ω speaker from the 5 V rail.

| Solution | Pros | Cons |
|---|---|---|
| <img src="https://mm.digikey.com/Volume0/opasdata/d220001/medias/images/6222/296%7E4040082%7EP%7E8.jpg" width="200"><br>**Option 1.** Texas Instruments LM386N-1/NOPB, 8-PDIP<br>$1.18/each<br>[LM386N-1 at DigiKey](https://www.digikey.com/en/products/detail/texas-instruments/LM386N-1-NOPB/6284) | • Through-hole DIP-8, easy to hand-solder on the milled board<br>• Runs from 4–12 V, so it works directly on the 5 V rail<br>• Gain is fixed at 20 internally, so only a few external parts are needed<br>• Very well documented with many example circuits | • Single-ended output needs a large (~250 µF) output coupling capacitor<br>• Only about 0.25 W into 8 Ω at 5 V, which is enough for a reminder tone but not very loud<br>• 4–8 mA quiescent current even when silent |
| <img src="https://mm.digikey.com/Volume0/opasdata/d220001/medias/images/376/8-DIP.jpg" width="200"><br>**Option 2.** Nisshinbo NJM2113D, DIP-8<br>$0.96/each<br>[NJM2113D at DigiKey](https://www.digikey.com/en/products/detail/nisshinbo-micro-devices-inc/NJM2113D/805551) | • Through-hole DIP-8 and the cheapest of the three<br>• Bridged (BTL) output, so no large output capacitor is needed<br>• Has a mute/power-down pin that a 3.3 V GPIO can drive, cutting current to 72 µA between alerts | • Datasheet gives no output power rating into 8 Ω (rated for 32 Ω loads)<br>• Neither speaker lead can be grounded because of the BTL output<br>• Much less example material than the LM386 |
| <img src="https://mm.digikey.com/Volume0/opasdata/d220001/medias/images/5734/31%7E8SOP-3.9%7EE%2CS%7E8.jpg" width="200"><br>**Option 3.** Diodes Inc. PAM8302AADCR, SOIC-8 (class-D)<br>$0.67/each<br>[PAM8302AADCR at DigiKey](https://www.digikey.com/en/products/detail/diodes-incorporated/PAM8302AADCR/4033280) | • Class-D, up to 88% efficient, so it barely heats up<br>• Up to 2.5 W into 4 Ω from 5 V, by far the loudest option<br>• Built-in shutdown pin plus short-circuit and thermal protection | • Surface-mount only (SOIC-8), harder to solder on a milled board<br>• Switching output can add electrical noise near the analog signals from the sensing boards<br>• BTL output, so neither speaker lead can go to ground |

**Choice:** Option 1, Texas Instruments LM386N-1/NOPB

**Rationale:** The LM386N-1 is a through-hole part that works directly from the 5 V rail with only a few external parts, which keeps the milled board simple. About 0.25 W is enough for an audible reminder tone in a home, and the part is in stock with a large amount of reference material for debugging. The PAM8302A is louder and more efficient, but it is surface-mount only and its switching output is not needed for a short alert tone. The NJM2113D was close, but it has no 8 Ω power rating, so I could not confirm it would drive my speaker.

---

## 2. Speaker — **Reminder & Alerts (Hub)**

Produces the audible dose reminder. Needs to be 8 Ω and rated for at least the ~0.25 W the LM386 can deliver.

| Solution | Pros | Cons |
|---|---|---|
| <img src="https://mm.digikey.com/Volume0/opasdata/d220001/medias/images/2109/CMS-40558N-L152.jpg" width="200"><br>**Option 1.** Same Sky CMS-40558N-L152, 40 mm, 8 Ω<br>$5.88/each<br>[CMS-40558N-L152 at DigiKey](https://www.digikey.com/en/products/detail/same-sky-formerly-cui-devices/CMS-40558N-L152/6137744) | • 8 Ω, 0.5 W rated (1 W max), safely above the LM386's output<br>• 90 dB sensitivity, so it is loud even at low power<br>• Comes with wire leads, so it connects to a header without extra soldering<br>• Thin (5.5 mm) and in stock at DigiKey | • 40 mm diameter is the largest of the three<br>• Weak bass below about 500 Hz, so the tone must be set in its range |
| <img src="https://mm.digikey.com/Volume0/opasdata/d220001/medias/images/17/MFG_AS02808MR-LW152-R.JPG" width="200"><br>**Option 2.** PUI Audio AS02808MR-LW152-R, 28 mm, 8 Ω<br>$4.82/each (Mouser)<br>[AS02808MR-LW152-R at DigiKey](https://www.digikey.com/en/products/detail/pui-audio-inc/AS02808MR-LW152-R/4835129) | • Small 28 mm size fits more easily in the medication holder<br>• 8 Ω, 1 W rated with 95 dB sensitivity<br>• Has wire leads | • DigiKey stock could not be confirmed, so it may need to be ordered from Mouser<br>• Smaller cone gives a thinner sound |
| <img src="https://mm.digikey.com/Volume0/opasdata/d220001/medias/images/327/K-28-WPC-BL---8-OHM-VIEW-A.jpg" width="200"><br>**Option 3.** Visaton K 28 WPC BL, 28 mm, 8 Ω<br>$7.24/each<br>[K 28 WPC BL at DigiKey](https://www.digikey.com/en/products/detail/visaton-gmbh-co-kg/K-28-WPC-BL-8-OHM/9842354) | • 1 W rated (2 W max), the most power headroom<br>• Mounting ears make it easy to screw to the enclosure<br>• High-quality brand with wide frequency range (300 Hz–20 kHz) | • Most expensive option<br>• Solder lugs instead of leads, so wires must be added by hand |

**Choice:** Option 1, Same Sky CMS-40558N-L152

**Rationale:** It has the right impedance (8 Ω), a power rating double what the LM386 can deliver, and high sensitivity, so the reminder is loud without stressing the amplifier. The pre-attached leads plug straight into a 2-pin header on my board, and it is in stock at DigiKey with the rest of my parts. Its 40 mm size still fits in the hub enclosure.

---

## 3. Real-Time Clock — **Reminder & Alerts (Hub)**

Keeps the time of day for the dose schedule, even when the board loses power, and raises an alarm interrupt on RB2. Talks to the microcontroller over I²C (RC3/RC4).

| Solution | Pros | Cons |
|---|---|---|
| <img src="https://mm.digikey.com/Volume0/opasdata/d220001/medias/images/8882/MFG_150%7EC04-018%7EP%2CPA%7E8.jpg" width="200"><br>**Option 1.** Microchip MCP7940N-I/P, 8-PDIP<br>$0.92/each<br>[MCP7940N-I/P at DigiKey](https://www.digikey.com/en/products/detail/microchip-technology/MCP7940N-I-P/3872279) | • Runs from 1.8–5.5 V, so it works natively with 3.3 V logic<br>• Through-hole DIP-8<br>• Two alarms plus an MFP interrupt pin for dose alerts<br>• Cheapest option, and only 1.2 µA from the backup battery | • Needs an external 32.768 kHz crystal and two load capacitors<br>• Accuracy depends on the crystal (about ±20 ppm untrimmed, ~1 min/month)<br>• Firmware must start the oscillator and enable battery backup |
| <img src="https://mm.digikey.com/Volume0/opasdata/d220001/medias/images/6285/175%7E21-0043%7EN%2CPA%7E8.jpg" width="200"><br>**Option 2.** Analog Devices DS1307+, 8-PDIP<br>$6.94/each (Mouser)<br>[DS1307+ at DigiKey](https://www.digikey.com/en/products/detail/analog-devices-inc-maxim-integrated/DS1307/956883) | • Through-hole and extremely well known, with many libraries<br>• Very low battery draw (300–500 nA) | • 5 V-only supply, so the I²C pull-ups must stay at 3.3 V to protect the PIC<br>• No alarm outputs, so the MCU would have to poll the time<br>• Slow 100 kHz I²C, also needs an external crystal, and costs over 7× more |
| <img src="https://mm.digikey.com/Volume0/opasdata/d220001/medias/images/7348/MFG_175%7E21-0042%7EWE%7E16.jpg" width="200"><br>**Option 3.** Analog Devices DS3231SN#, 16-SOIC<br>$19.05/each<br>[DS3231SN# at DigiKey](https://www.digikey.com/en/products/detail/analog-devices-inc-maxim-integrated/DS3231SN/1197576) | • Built-in temperature-compensated crystal, ±2 ppm (about 1 min/year)<br>• No crystal layout to get wrong<br>• Two alarms, runs at 3.3 V | • About 20× the cost of the MCP7940N<br>• Surface-mount only (wide SOIC-16)<br>• Accuracy is more than a daily medication reminder needs |

**Choice:** Option 1, Microchip MCP7940N-I/P

**Rationale:** The MCP7940N is the only option that is through-hole, runs natively at 3.3 V, and has alarm outputs, so it can wake the hub on its MFP pin when a dose is due. It is also the cheapest and comes from the same manufacturer as our microcontroller. The extra 32.768 kHz crystal is a small cost, and its built-in digital trim can correct the crystal error. The DS3231 is more accurate, but a medication reminder only needs to be correct to about a minute, which does not justify 20× the price and an SMD package.

---

## 4. RTC Backup Battery — **Reminder & Alerts (Hub)**

Keeps the real-time clock running when the 9 V adapter is unplugged, so the dose schedule is not lost.

| Solution | Pros | Cons |
|---|---|---|
| <img src="https://mm.digikey.com/Volume0/opasdata/d220001/medias/images/4849/11_CR2032.jpg" width="200"><br>**Option 1.** Panasonic CR2032, 3 V, 225 mAh<br>$0.36/each (+ Keystone 1066 through-hole holder, $1.12)<br>[CR2032 at DigiKey](https://www.digikey.com/en/products/detail/panasonic-energy/CR2032/31939) · [Keystone 1066 holder](https://www.digikey.com/en/products/detail/keystone-electronics/1066/303562) | • 225 mAh gives decades of RTC backup at 1.2 µA<br>• Cheapest cell, huge stock, sold everywhere so the user can replace it<br>• Through-hole holder available | • Holder is 20 mm wide and takes board space<br>• Not rechargeable |
| <img src="https://www.mouser.com/images/renata/images/CR_2032_prv_SPL.jpg" width="200"><br>**Option 2.** Renata CR2032 MFR.IB, 3 V, 225 mAh<br>$0.44/each (Mouser)<br>[Renata CR2032 at Mouser](https://www.mouser.com/ProductDetail/614-CR2032-200) | • Same size and capacity as Option 1<br>• Very low self-discharge (under 1% per year)<br>• Swiss-made with detailed documentation | • Slightly more expensive<br>• Only confirmed at Mouser, not DigiKey |
| <img src="https://www.mouser.com/images/panasonic/images/CR1220_SPL.jpg" width="200"><br>**Option 3.** Panasonic CR1220, 3 V, 35 mAh<br>$1.02/each (Mouser) (+ Keystone 500 holder, $1.22)<br>[CR1220 at Mouser](https://www.mouser.com/ProductDetail/658-CR1220) | • Small 12 mm cell and holder save board space<br>• 35 mAh still lasts years at 1.2 µA | • Only about 1/6 the capacity of a CR2032<br>• About 3× the price<br>• Harder for a user to find a replacement |

**Choice:** Option 1, Panasonic CR2032 in a Keystone 1066 holder

**Rationale:** At the MCP7940N's 1.2 µA backup current, a 225 mAh CR2032 would last far longer than the cell's ~10-year shelf life, so the clock will not need attention during the product's life. It is the cheapest option, uses a through-hole holder that fits the milled board, and is the most common coin cell, so a caregiver can easily replace it.

---

## 5. Alert LED Switch (N-channel MOSFET) — **Reminder & Alerts (Hub)**

Lets microcontroller pin RC5 (3.3 V logic) switch the high-brightness alert LED from the 5 V rail, so the LED current does not flow through the PIC.

| Solution | Pros | Cons |
|---|---|---|
| <img src="https://mm.digikey.com/Volume0/opasdata/d220001/medias/images/6348/785%7EPO-00001%7E%7E3.jpg" width="200"><br>**Option 1.** Alpha & Omega AO3400A, SOT-23<br>$0.52/each<br>[AO3400A at DigiKey](https://www.digikey.com/en/products/detail/alpha-omega-semiconductor-inc/AO3400A/1855772) | • On-resistance is guaranteed at a 2.5 V gate (48 mΩ max), so it turns fully on from a 3.3 V pin<br>• 5.7 A rating leaves room to upgrade to a much brighter LED later<br>• Cheapest option | • Small SOT-23 package needs care to hand-solder<br>• Clone parts with the same name exist, so it must be ordered from an authorized distributor |
| <img src="https://mm.digikey.com/Volume0/opasdata/d220001/medias/images/6157/488%7EMKT-ZA03D%7E%7E3.jpg" width="200"><br>**Option 2.** onsemi 2N7000, TO-92<br>$1.23/each (Mouser)<br>[2N7000 at DigiKey](https://www.digikey.com/en/products/detail/onsemi/2N7000/244278) | • Through-hole TO-92, easiest to solder<br>• Very common and well documented | • Gate threshold can be as high as 3.0 V, so it may barely turn on from 3.3 V<br>• Up to 6 Ω on-resistance and only 200 mA continuous<br>• No room to upgrade the LED |
| <img src="https://mm.digikey.com/Volume0/opasdata/d220001/medias/images/7182/TO-220AB%2CTO-220-3%2CHEXFET%C2%AE.jpg" width="200"><br>**Option 3.** Infineon IRLZ44NPBF, TO-220<br>$1.80/each (Mouser)<br>[IRLZ44NPBF at DigiKey](https://www.digikey.com/en/products/detail/infineon-technologies/IRLZ44NPBF/811808) | • Through-hole TO-220, easy to solder<br>• Logic-level threshold (1–2 V) and very low on-resistance | • On-resistance is only guaranteed from 4 V up, not at 3.3 V<br>• Large package for a small LED load<br>• Most expensive of the three |

**Choice:** Option 1, Alpha & Omega AO3400A

**Rationale:** The AO3400A is the only option whose on-resistance is guaranteed below 3.3 V, so the alert LED is reliably fully on when RC5 goes high. Its 0.95 mm pin pitch meets the Peralta mill's 0.8 mm minimum and can be hand-soldered with care. I considered a through-hole part, but the 2N7000 may not turn on from 3.3 V, and the IRLZ44N is not specified at 3.3 V and is much larger than needed.

---

## 6. High-Brightness Alert LED — **Reminder & Alerts (Hub)**

The visual reminder that a dose is due. It needs to be bright enough to notice across a room, and is driven through the AO3400A from the 5 V rail. (The three small Ready/Taken/Error status LEDs are ordinary LEDs and are not listed here.)

| Solution | Pros | Cons |
|---|---|---|
| <img src="https://mm.digikey.com/Volume0/opasdata/d220001/medias/images/637/WP7113SEC%5EJ3.JPG" width="200"><br>**Option 1.** Kingbright WP7113SEC/J3, 5 mm hyper red<br>$0.76/each (Mouser)<br>[WP7113SEC/J3 at DigiKey](https://www.digikey.com/en/products/detail/kingbright/WP7113SEC-J3/2075399) | • Very bright: 15,000 mcd typical at 20 mA<br>• Red reads clearly as an alert<br>• Through-hole and runs from 5 V with one resistor (~150 Ω)<br>• Low current (20 mA) keeps the power budget small | • Narrow 20° beam, best seen from the front<br>• Only 30 mA max, so brightness cannot be increased much |
| <img src="https://mm.digikey.com/Volume0/opasdata/d220001/medias/images/534/C512A-WNN-CZ0B0151.JPG" width="200"><br>**Option 2.** Cree C503B-WAN-CBBDB231, 5 mm cool white<br>$0.28/each (Mouser)<br>[C503B-WAN at Mouser](https://www.mouser.com/ProductDetail/941-C503BWANCBBDB231) | • Brightest 5 mm option: 20,000–34,000 mcd at 20 mA<br>• Cheapest option<br>• Through-hole | • Very narrow 15° beam, hard to see from the side<br>• White does not signal "alert" as clearly as red<br>• 25 mA max continuous |
| <img src="https://mm.digikey.com/Volume0/opasdata/d220001/medias/images/3964/MFG_XPGDRY-L1-0000-00601-SB01.jpg" width="200"><br>**Option 3.** Cree XLamp XP-G3 white on star board (XPGDWT-01-0000-00LE1-SB01)<br>$11.40/each (Mouser)<br>[XP-G3 star LED at Mouser](https://www.mouser.com/ProductDetail/416-XPGDWT01LE1B1) | • Extremely bright (~165 lm) with a wide 125° beam<br>• Visible from anywhere in the room | • Needs 350 mA, which adds about 1.75 W to the 5 V rail and the regulator<br>• Star board must be wired by hand and needs heat-sinking<br>• About 15× the cost of a 5 mm LED |

**Choice:** Option 1, Kingbright WP7113SEC/J3

**Rationale:** The WP7113SEC/J3 is bright enough to notice across a room, and its red color clearly signals that a dose is due. At only 20 mA it keeps the 5 V regulator cool, and it is a cheap through-hole part. The XP-G3 star is far brighter, but its 350 mA draw would push the linear regulator's heat well past a safe level. Because the LED is switched by the AO3400A, it can be swapped for the star LED later without changing the board.

---

## 7. 5 V Voltage Regulator — **Power (Hub board)**

Converts the 9 V adapter input to the 5 V rail that powers the Curiosity Nano, the LM386, and the alert LED. The course requires a linear regulator.

| Solution | Pros | Cons |
|---|---|---|
| <img src="https://mm.digikey.com/Volume0/opasdata/d220001/medias/images/2660/497%7ETO220-3TO220AB%7E%7E3.JPG" width="200"><br>**Option 1.** STMicroelectronics L7805CV, TO-220<br>$0.50/each<br>[L7805CV at DigiKey](https://www.digikey.com/en/products/detail/stmicroelectronics/L7805CV/585964) | • Linear, meets the course requirement<br>• Up to 1.5 A output, about 3× my worst-case load<br>• Stable with small ceramic capacitors (0.33 µF in, 0.1 µF out)<br>• Cheapest option, with thermal and short-circuit protection | • 2 V dropout, so it needs at least 7 V in (9 V adapter is fine)<br>• Drops (9 − 5) V × load current as heat, so a TO-220 heatsink is needed at full load |
| <img src="https://mm.digikey.com/Volume0/opasdata/d220001/medias/images/3642/296%7ET03B%7ENDE%7E3.JPG" width="200"><br>**Option 2.** Texas Instruments LM2940CT-5.0/NOPB, TO-220 LDO<br>$1.94/each<br>[LM2940CT-5.0 at DigiKey](https://www.digikey.com/en/products/detail/texas-instruments/LM2940CT-5-0-NOPB/32575) | • Low dropout (0.5 V typical), so it keeps working if the adapter sags<br>• Reverse-battery and transient protection<br>• Linear, meets the course requirement | • Needs a ≥22 µF output capacitor with ESR between 0.1–1 Ω, or it can oscillate<br>• Same heat as the 7805, since heat depends on 9 V − 5 V<br>• Higher quiescent current and about 4× the price |
| <img src="https://mm.digikey.com/Volume0/opasdata/d220001/medias/images/2584/MFG_R-78-e%20series.jpg" width="200"><br>**Option 3.** RECOM R-78E5.0-1.0, SIP-3 switching regulator<br>$3.97/each<br>[R-78E5.0-1.0 at DigiKey](https://www.digikey.com/en/products/detail/recom-power/R-78E5-0-1-0/4930585) | • About 92% efficient, so almost no heat and no heatsink<br>• Same pinout as a 7805, so it is a drop-in swap | • Switching, not linear, so it does not meet the course requirement<br>• Output ripple (120 mV) could add noise to analog readings<br>• About 8× the price |

**Choice:** Option 1, STMicroelectronics L7805CV (with a clip-on TO-220 heatsink)

**Rationale:** The L7805CV is a linear regulator that meets the course requirement, supplies 1.5 A against my ~0.5 A worst case, and is stable with small, cheap capacitors. The LM2940's low dropout is not needed with a 9 V input, and it needs a carefully chosen output capacitor. Both linear regulators produce the same heat, so I will add a clip-on TO-220 heatsink, sized in my Power Budget. The switching R-78E would remove the heat but is not allowed by the course rules.

---

## 8. External Power Supply — **Power (Hub board)**

Plugs into the wall and feeds 9 V DC to the Same Sky PJ-102AH barrel jack. It needs a 5.5 × 2.1 mm center-positive plug and at least the ~0.5 A worst-case board current.

| Solution | Pros | Cons |
|---|---|---|
| <img src="https://mm.digikey.com/Volume0/opasdata/d220001/medias/images/1875/MFG_WSU-Series.jpg" width="200"><br>**Option 1.** Triad Magnetics WSU090-2000, 9 V 2 A wall adapter<br>$12.43/each (Mouser)<br>[WSU090-2000 at Mouser](https://www.mouser.com/ProductDetail/553-WSU090-2000) | • 2 A output, about 4× my worst-case need<br>• Regulated switching adapter, plugs directly into the wall<br>• 5.5 × 2.1 mm center-positive plug matches the barrel jack<br>• Cheapest of the three | • Limited stock (76 units) with a long factory lead time<br>• The similar "-R" version is center-negative and must not be ordered |
| <img src="https://mm.digikey.com/Volume0/opasdata/d220001/medias/images/2158/MFG_GST18A.jpg" width="200"><br>**Option 2.** MEAN WELL GST18A09-P1J, 9 V 2 A desktop adapter<br>$14.10/each (Mouser)<br>[GST18A09-P1J at Mouser](https://www.mouser.com/ProductDetail/709-GST18A09-P1J) | • Industrial-quality brand, 2 A output<br>• Correct 5.5 × 2.1 mm center-positive plug | • Desktop "brick", not a wall plug, so it needs a separate AC cord<br>• Low stock at both Mouser and DigiKey |
| <img src="https://www.mouser.com/images/cuiinc/images/swi12-12-n-p6_SPL.jpg" width="200"><br>**Option 3.** CUI SWI12-9-N-P5, 9 V 1.2 A wall adapter<br>$17.59/each (Mouser)<br>[SWI12-9-N-P5 at Mouser](https://www.mouser.com/ProductDetail/490-SWI12-9-N-P5) | • Good stock (800+ units)<br>• Wall plug with correct center-positive 5.5 × 2.1 mm plug | • Most expensive<br>• Only 1.2 A, the least headroom of the three |

**Choice:** Option 1, Triad Magnetics WSU090-2000

**Rationale:** It is the cheapest option, plugs directly into the wall, and supplies 2 A, which leaves plenty of margin over my worst-case 0.52 A (with 25% safety margin). It has the correct center-positive 5.5 × 2.1 mm plug for the PJ-102AH jack. I will order the WSU090-2000 and not the "-R" version, which is center-negative and would apply reverse polarity to the board. If stock runs out, the CUI SWI12-9-N-P5 is the backup.

---

## Microcontroller Pin Table — **Reminder & Alerts (Hub)**

PIC18F57Q43 Curiosity Nano pins used on my hub board, matching my [Block Diagram](../01-Block-Diagram/Block-Diagram.md).

| PIC pin | Peripheral | Direction | Connects to | Signal |
|---|---|---|---|---|
| RB0 | Digital input | In | Take Dose / Acknowledge button | Digital (3.3 V, 1 pin) |
| RB1 | Digital input | In | Set / Mode button | Digital (3.3 V, 1 pin) |
| RB2 | Digital input (interrupt) | In | MCP7940N alarm (MFP) | Digital (3.3 V, 1 pin) |
| RC3 | I²C SCL | Out | MCP7940N real-time clock | Digital - Serial (I²C, 2 pins) |
| RC4 | I²C SDA | In/Out | MCP7940N real-time clock | Digital - Serial (I²C, 2 pins) |
| RA3, RA4, RA5 | Digital outputs | Out | Ready / Taken / Error status LEDs | Digital (3.3 V, 3 pins) |
| RC5 | Digital output | Out | AO3400A gate → WP7113SEC/J3 alert LED | Digital (3.3 V, 1 pin) |
| RC2 | PWM (CCP1) | Out | LM386N-1 input → CMS-40558N speaker | Analog (0–3.3 V PWM, 1 pin) |
| RD0 | Digital output | Out | J1 pin 1 → Weight board (DOSE_READY) | Digital (3.3 V, 1 pin) |
| RD1 | Digital input | In | J1 pin 2 ← Weight board (DOSE_REMOVED) | Digital (3.3 V, 1 pin) |
| RD2 | Digital input | In | J1 pin 3 ← Weight board (WEIGHT_FAULT) | Digital (3.3 V, 1 pin) |
| RD3 | Digital output | Out | J1 pin 4 → Weight board (TARE_REQ) | Digital (3.3 V, 1 pin) |
| RD4 | Digital input | In | J1 pin 5 ← Weight board (HEARTBEAT_A) | Digital (3.3 V, 1 pin) |
| RA0 | ADC | In | J1 pin 6 ← Weight board (WEIGHT_LEVEL) | Analog (0–3.3 V, 1 pin) |
| RD5 | Digital output | Out | J2 pin 1 → Cap board (DOSE_READY) | Digital (3.3 V, 1 pin) |
| RD6 | Digital input | In | J2 pin 2 ← Cap board (LID_OPEN) | Digital (3.3 V, 1 pin) |
| RD7 | Digital input | In | J2 pin 3 ← Cap board (LID_FAULT) | Digital (3.3 V, 1 pin) |
| RE0 | Digital input | In | J2 pin 5 ← Cap board (HEARTBEAT_B) | Digital (3.3 V, 1 pin) |
| RE1 | Digital input | In | J3 pin 2 ← Environment board (TEMP_ALERT) | Digital (3.3 V, 1 pin) |
| RE2 | Digital input | In | J3 pin 3 ← Environment board (LIGHT_ALERT) | Digital (3.3 V, 1 pin) |
| RF2 | Digital input | In | J3 pin 5 ← Environment board (HEARTBEAT_D) | Digital (3.3 V, 1 pin) |
| RA1 | ADC | In | J3 pin 6 ← Environment board (TEMP_LEVEL) | Analog (0–3.3 V, 1 pin) |
| VBUS (5 V) | Power in | In | L7805CV 5 V output | Power |
| GND | Ground | — | Board ground, J1–J3 pin 8 | Ground |

Reserved and not used: RB4 (on-board SW0), RB6/RB7 (programming), RE3 (MCLR), RF0/RF1 (debug UART), RF3 (on-board LED0).
