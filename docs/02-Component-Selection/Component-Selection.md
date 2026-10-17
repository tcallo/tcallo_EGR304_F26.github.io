---
title: Component Selection
---

# Component Selection

**Team 102 – Project Aurora** · Taylor Callo · Member C: Reminder & Alerts (Hub)

This page compares three real options for every major part on my Reminder & Alerts hub board, and explains which one I picked and why. My hub board keeps track of when each dose is due using a clock chip, warns the user with a speaker and a bright LED when it is time, and gets its power from a 9 V wall adapter that goes through a 5 V regulator. The assignment says not to include the microcontroller (it was picked for us), resistors, capacitors, buttons, or plain LEDs, so those are left out.

All prices are for buying 1 part, in US dollars, checked on 10/14/2026. My board will be cut on the Peralta lab's PCB mill and soldered by hand, so I picked parts with pins that go through the board (through-hole) or parts that are still easy to solder by hand.

## Summary

| Part | Subsystem | Choice | Cost |
|---|---|---|---|
| Audio amplifier | **Reminder & Alerts (Hub)** | TI LM386N-1/NOPB | $1.18 |
| Speaker | **Reminder & Alerts (Hub)** | Same Sky CMS-40558N-L152 | $5.88 |
| Real-time clock | **Reminder & Alerts (Hub)** | Microchip MCP7940N-I/P | $0.92 |
| RTC backup battery | **Reminder & Alerts (Hub)** | Panasonic CR2032 + Keystone 1066 holder | $1.48 |
| Alert LED switch | **Reminder & Alerts (Hub)** | Alpha & Omega AO3400A | $0.52 |
| Alert LED | **Reminder & Alerts (Hub)** | Kingbright WP7113SEC/J3 | $0.76 |
| 5 V regulator | **Power (Hub board)** | STMicroelectronics L7805CV | $0.50 |
| Wall adapter | **Power (Hub board)** | Triad Magnetics WSU090-2000 | $12.43 |

---

## 1. Audio Amplifier — **Reminder & Alerts (Hub)**

The PIC sends a beeping signal (PWM) out of pin RC2, but that signal is too weak to play through a speaker by itself. The amplifier makes the signal stronger so it can drive the 8 Ω speaker, using power from the 5 V rail.

| Solution | Pros | Cons |
|---|---|---|
| <img src="https://mm.digikey.com/Volume0/opasdata/d220001/medias/images/6222/296%7E4040082%7EP%7E8.jpg" width="200"><br>**Option 1.** Texas Instruments LM386N-1/NOPB (DIP-8)<br>$1.18/each<br>[LM386N-1 at DigiKey](https://www.digikey.com/en/products/detail/texas-instruments/LM386N-1-NOPB/6284) | • Its pins go through the board (DIP-8), so it is easy to solder by hand on the milled board<br>• Works on anything from 4 V to 12 V, so it can plug right into my 5 V rail<br>• The gain (how much it boosts the signal) is already set to 20 inside the chip, so I only need a few extra parts<br>• It is a very popular chip, so there are lots of example circuits and help online | • Needs a big (about 250 µF) capacitor between the chip and the speaker, which takes up board space<br>• Only puts out about 0.25 W at 5 V, which is loud enough for a reminder beep but not very loud<br>• Uses 4–8 mA of power even when it is not making any sound |
| <img src="https://mm.digikey.com/Volume0/opasdata/d220001/medias/images/376/8-DIP.jpg" width="200"><br>**Option 2.** Nisshinbo NJM2113D (DIP-8)<br>$0.96/each<br>[NJM2113D at DigiKey](https://www.digikey.com/en/products/detail/nisshinbo-micro-devices-inc/NJM2113D/805551) | • Its pins go through the board and it is the cheapest of the three<br>• Drives the speaker from both sides, so it does not need the big output capacitor<br>• Has a mute pin the PIC can use to turn it almost fully off between alerts, saving power | • The datasheet does not say how much power it can give an 8 Ω speaker (it is rated for 32 Ω), so I can't be sure it will be loud enough<br>• Neither speaker wire can go to ground, because of the way it drives the speaker<br>• There are far fewer examples online than for the LM386 |
| <img src="https://mm.digikey.com/Volume0/opasdata/d220001/medias/images/5734/31%7E8SOP-3.9%7EE%2CS%7E8.jpg" width="200"><br>**Option 3.** Diodes Inc. PAM8302AADCR (SOIC-8, class-D)<br>$0.67/each<br>[PAM8302AADCR at DigiKey](https://www.digikey.com/en/products/detail/diodes-incorporated/PAM8302AADCR/4033280) | • By far the loudest option, up to 2.5 W from 5 V<br>• Very efficient (up to 88%), so it barely gets warm<br>• Has a built-in off switch plus protection if the speaker wires short or it gets too hot | • Surface-mount only (the chip sits on top of the board), which is harder to solder on a milled board<br>• The way it switches on and off very fast can add electrical noise near the sensor signals coming from the other boards<br>• Neither speaker wire can go to ground |

**Choice:** Option 1, Texas Instruments LM386N-1/NOPB

**Rationale:** I picked the LM386N-1 because it is a through-hole chip that runs right off my 5 V rail and only needs a few extra parts, which keeps my milled board simple. About 0.25 W is loud enough to hear a reminder beep inside a home, and the chip is in stock with tons of help online if I run into problems. The PAM8302A is louder and more efficient, but it is surface-mount only and I don't need that much volume for a short beep. The NJM2113D was close, but its datasheet doesn't say how it works with an 8 Ω speaker, so I couldn't be sure it would drive mine.

---

## 2. Speaker — **Reminder & Alerts (Hub)**

Plays the beep that tells the user it is time to take a dose. It needs to be 8 Ω and able to handle at least the 0.25 W the LM386 can send it.

| Solution | Pros | Cons |
|---|---|---|
| <img src="https://mm.digikey.com/Volume0/opasdata/d220001/medias/images/2109/CMS-40558N-L152.jpg" width="200"><br>**Option 1.** Same Sky CMS-40558N-L152 (40 mm, 8 Ω)<br>$5.88/each<br>[CMS-40558N-L152 at DigiKey](https://www.digikey.com/en/products/detail/same-sky-formerly-cui-devices/CMS-40558N-L152/6137744) | • Rated for 0.5 W (1 W max), which is double what the amplifier can send, so it won't get damaged<br>• Very loud for its size (90 dB), so the beep is easy to hear even at low power<br>• Comes with wires already attached, so it can plug into a header on my board<br>• Thin (5.5 mm) and in stock at DigiKey | • At 40 mm across, it is the biggest of the three options<br>• Not good at low sounds (below about 500 Hz), so the beep needs to be a higher pitch |
| <img src="https://mm.digikey.com/Volume0/opasdata/d220001/medias/images/17/MFG_AS02808MR-LW152-R.JPG" width="200"><br>**Option 2.** PUI Audio AS02808MR-LW152-R (28 mm, 8 Ω)<br>$4.82/each (Mouser)<br>[AS02808MR-LW152-R at DigiKey](https://www.digikey.com/en/products/detail/pui-audio-inc/AS02808MR-LW152-R/4835129) | • Smaller (28 mm), so it is easier to fit inside the medication holder<br>• Rated for 1 W and very loud (95 dB)<br>• Comes with wires already attached | • I couldn't confirm DigiKey has it in stock, so I might have to order it from Mouser separately<br>• A smaller speaker sounds thinner and less full |
| <img src="https://mm.digikey.com/Volume0/opasdata/d220001/medias/images/327/K-28-WPC-BL---8-OHM-VIEW-A.jpg" width="200"><br>**Option 3.** Visaton K 28 WPC BL (28 mm, 8 Ω)<br>$7.24/each<br>[K 28 WPC BL at DigiKey](https://www.digikey.com/en/products/detail/visaton-gmbh-co-kg/K-28-WPC-BL-8-OHM/9842354) | • Handles the most power (1 W rated, 2 W max), so there is lots of room for error<br>• Has mounting tabs, so it is easy to screw into the enclosure<br>• Good-quality brand that plays a wide range of sounds (300 Hz–20 kHz) | • The most expensive of the three<br>• Only has solder tabs, so I would have to solder wires onto it myself |

**Choice:** Option 1, Same Sky CMS-40558N-L152

**Rationale:** I picked this speaker because it is the right resistance (8 Ω), it can handle twice the power my amplifier puts out, and it is loud, so the reminder beep will be easy to hear without pushing the amplifier hard. The wires that come attached plug straight into a 2-pin header on my board, and it is in stock at DigiKey with my other parts. Its 40 mm size still fits inside the hub's case.

---

## 3. Real-Time Clock — **Reminder & Alerts (Hub)**

Keeps track of the time and date so the hub knows when each dose is due, even if the board loses power. It can also set an alarm that tells the PIC "it's time" on pin RB2. It talks to the PIC using I²C on pins RC3 and RC4.

| Solution | Pros | Cons |
|---|---|---|
| <img src="https://mm.digikey.com/Volume0/opasdata/d220001/medias/images/8882/MFG_150%7EC04-018%7EP%2CPA%7E8.jpg" width="200"><br>**Option 1.** Microchip MCP7940N-I/P (DIP-8)<br>$0.92/each<br>[MCP7940N-I/P at DigiKey](https://www.digikey.com/en/products/detail/microchip-technology/MCP7940N-I-P/3872279) | • Works on 1.8–5.5 V, so it runs fine on the PIC's 3.3 V<br>• Its pins go through the board, so it is easy to solder<br>• Has two built-in alarms and an alarm pin to tell the PIC when a dose is due<br>• Cheapest option, and only uses 1.2 µA from the backup battery | • Needs a separate 32.768 kHz crystal and two small capacitors to keep time<br>• Only as accurate as the crystal (can drift about 1 minute per month unless adjusted)<br>• The code has to turn on its clock and its battery backup at startup |
| <img src="https://mm.digikey.com/Volume0/opasdata/d220001/medias/images/6285/175%7E21-0043%7EN%2CPA%7E8.jpg" width="200"><br>**Option 2.** Analog Devices DS1307+ (DIP-8)<br>$6.94/each (Mouser)<br>[DS1307+ at DigiKey](https://www.digikey.com/en/products/detail/analog-devices-inc-maxim-integrated/DS1307/956883) | • Its pins go through the board<br>• Very well known, with lots of example code<br>• Uses very little power from the backup battery | • Only runs on 5 V, so I would have to be careful connecting it to the 3.3 V PIC<br>• Has no alarms, so the PIC would have to keep checking the time over and over<br>• Slower communication, also needs a crystal, and costs about 7× more |
| <img src="https://mm.digikey.com/Volume0/opasdata/d220001/medias/images/7348/MFG_175%7E21-0042%7EWE%7E16.jpg" width="200"><br>**Option 3.** Analog Devices DS3231SN# (SOIC-16)<br>$19.05/each<br>[DS3231SN# at DigiKey](https://www.digikey.com/en/products/detail/analog-devices-inc-maxim-integrated/DS3231SN/1197576) | • Extremely accurate (drifts about 1 minute per year)<br>• Crystal is built in, so there is nothing extra to wire up<br>• Has two alarms and works at 3.3 V | • Costs about 20× more than the MCP7940N<br>• Surface-mount only<br>• Much more accurate than a pill reminder needs |

**Choice:** Option 1, Microchip MCP7940N-I/P

**Rationale:** I picked the MCP7940N because it is the only option that has through-hole pins, works at 3.3 V, and has alarms, so it can wake up the hub when a dose is due without the PIC constantly checking. It is also the cheapest and is made by Microchip, the same company as our microcontroller. Adding a small crystal is a small extra step, and the chip can be adjusted in code to fix the crystal's drift. The DS3231 is more accurate, but a pill reminder only needs to be right within about a minute, which isn't worth 20× the price and a harder-to-solder chip.

---

## 4. RTC Backup Battery — **Reminder & Alerts (Hub)**

A small coin battery that keeps the clock running when the wall adapter is unplugged, so the dose schedule isn't lost.

| Solution | Pros | Cons |
|---|---|---|
| <img src="https://mm.digikey.com/Volume0/opasdata/d220001/medias/images/4849/11_CR2032.jpg" width="200"><br>**Option 1.** Panasonic CR2032 (3 V, 225 mAh)<br>$0.36/each + $1.12 holder<br>[CR2032 at DigiKey](https://www.digikey.com/en/products/detail/panasonic-energy/CR2032/31939) · [Keystone 1066 holder](https://www.digikey.com/en/products/detail/keystone-electronics/1066/303562) | • 225 mAh lasts for decades at the clock's tiny 1.2 µA draw<br>• Cheapest, and sold almost everywhere, so a user can easily replace it<br>• Has a through-hole holder that fits my milled board | • The 20 mm holder takes up some board space<br>• Not rechargeable |
| <img src="https://www.mouser.com/images/renata/images/CR_2032_prv_SPL.jpg" width="200"><br>**Option 2.** Renata CR2032 MFR.IB (3 V, 225 mAh)<br>$0.44/each (Mouser)<br>[Renata CR2032 at Mouser](https://www.mouser.com/ProductDetail/614-CR2032-200) | • Same size and capacity as Option 1<br>• Loses less than 1% of its charge per year while sitting<br>• Well-documented Swiss brand | • Costs a little more<br>• I could only confirm it at Mouser, not DigiKey |
| <img src="https://www.mouser.com/images/panasonic/images/CR1220_SPL.jpg" width="200"><br>**Option 3.** Panasonic CR1220 (3 V, 35 mAh)<br>$1.02/each (Mouser) + $1.22 holder<br>[CR1220 at Mouser](https://www.mouser.com/ProductDetail/658-CR1220) | • Small (12 mm), so the battery and holder save board space<br>• 35 mAh still lasts years at 1.2 µA | • Only about 1/6 the capacity of a CR2032<br>• Costs about 3× more<br>• Harder for a user to find a replacement |

**Choice:** Option 1, Panasonic CR2032 in a Keystone 1066 holder

**Rationale:** At the clock's tiny 1.2 µA draw, a 225 mAh CR2032 would last longer than its own ~10-year shelf life, so the user should never need to think about it. It is the cheapest option, fits in a through-hole holder on my board, and is the most common coin battery, so it is easy to replace if ever needed.

---

## 5. Alert LED Switch (MOSFET) — **Reminder & Alerts (Hub)**

Works like an electronic switch. It lets PIC pin RC5 (3.3 V) turn the bright alert LED on and off using power from the 5 V rail, so the LED's current doesn't flow through the PIC itself.

| Solution | Pros | Cons |
|---|---|---|
| <img src="https://mm.digikey.com/Volume0/opasdata/d220001/medias/images/6348/785%7EPO-00001%7E%7E3.jpg" width="200"><br>**Option 1.** Alpha & Omega AO3400A (SOT-23)<br>$0.52/each<br>[AO3400A at DigiKey](https://www.digikey.com/en/products/detail/alpha-omega-semiconductor-inc/AO3400A/1855772) | • The datasheet guarantees it turns fully on with only 2.5 V, so the PIC's 3.3 V is plenty<br>• Can handle up to 5.7 A, so I could switch to a much brighter LED later<br>• The cheapest of the three | • The small 3-pin package takes some care to solder by hand<br>• Fake copies with the same name exist, so I need to buy it from DigiKey |
| <img src="https://mm.digikey.com/Volume0/opasdata/d220001/medias/images/6157/488%7EMKT-ZA03D%7E%7E3.jpg" width="200"><br>**Option 2.** onsemi 2N7000 (TO-92)<br>$1.23/each (Mouser)<br>[2N7000 at DigiKey](https://www.digikey.com/en/products/detail/onsemi/2N7000/244278) | • Its pins go through the board, so it is the easiest to solder<br>• Very common and well-known part | • Might need up to 3 V just to start turning on, so it may barely work from the PIC's 3.3 V<br>• Can only handle 200 mA<br>• Leaves no room to upgrade to a brighter LED |
| <img src="https://mm.digikey.com/Volume0/opasdata/d220001/medias/images/7182/TO-220AB%2CTO-220-3%2CHEXFET%C2%AE.jpg" width="200"><br>**Option 3.** Infineon IRLZ44NPBF (TO-220)<br>$1.80/each (Mouser)<br>[IRLZ44NPBF at DigiKey](https://www.digikey.com/en/products/detail/infineon-technologies/IRLZ44NPBF/811808) | • Its pins go through the board, so it is easy to solder<br>• Turns on at a low voltage (1–2 V) and wastes very little power when on | • The datasheet only guarantees full performance at 4 V or more, not at 3.3 V<br>• Big package for such a small LED<br>• The most expensive of the three |

**Choice:** Option 1, Alpha & Omega AO3400A

**Rationale:** I picked the AO3400A because it is the only option the datasheet guarantees will fully turn on from a 3.3 V pin, so the alert LED will always turn on all the way when the PIC tells it to. Its pins are 0.95 mm apart, which is wider than the Peralta mill's 0.8 mm minimum, so I can still solder it by hand with care. I looked at through-hole parts, but the 2N7000 might not turn on from 3.3 V, and the IRLZ44N isn't guaranteed at 3.3 V and is much bigger than I need.

---

## 6. High-Brightness Alert LED — **Reminder & Alerts (Hub)**

The light that tells the user a dose is due. It needs to be bright enough to notice from across a room. It is turned on and off by the AO3400A using power from the 5 V rail. (The three small Ready/Taken/Error status LEDs are regular LEDs, so they are not listed here.)

| Solution | Pros | Cons |
|---|---|---|
| <img src="https://mm.digikey.com/Volume0/opasdata/d220001/medias/images/637/WP7113SEC%5EJ3.JPG" width="200"><br>**Option 1.** Kingbright WP7113SEC/J3 (5 mm red)<br>$0.76/each (Mouser)<br>[WP7113SEC/J3 at DigiKey](https://www.digikey.com/en/products/detail/kingbright/WP7113SEC-J3/2075399) | • Very bright: 15,000 mcd at 20 mA<br>• Red clearly means "pay attention"<br>• Its pins go through the board and it only needs one resistor (about 150 Ω) to run on 5 V<br>• Only uses 20 mA, which keeps the power budget small | • The light shines in a narrow 20° beam, so it is easiest to see from the front<br>• Can't be made much brighter (30 mA max) |
| <img src="https://mm.digikey.com/Volume0/opasdata/d220001/medias/images/534/C512A-WNN-CZ0B0151.JPG" width="200"><br>**Option 2.** Cree C503B-WAN-CBBDB231 (5 mm white)<br>$0.28/each (Mouser)<br>[C503B-WAN at Mouser](https://www.mouser.com/ProductDetail/941-C503BWANCBBDB231) | • The brightest 5 mm option: 20,000–34,000 mcd at 20 mA<br>• The cheapest option<br>• Its pins go through the board | • Very narrow 15° beam, so it is hard to see from the side<br>• White light doesn't say "alert" as clearly as red<br>• Only 25 mA max |
| <img src="https://mm.digikey.com/Volume0/opasdata/d220001/medias/images/3964/MFG_XPGDRY-L1-0000-00601-SB01.jpg" width="200"><br>**Option 3.** Cree XLamp XP-G3 star LED (white)<br>$11.40/each (Mouser)<br>[XP-G3 star LED at Mouser](https://www.mouser.com/ProductDetail/416-XPGDWT01LE1B1) | • Extremely bright (about 165 lumens) with a wide 125° beam<br>• Can be seen from anywhere in the room | • Needs 350 mA, which would add about 1.75 W of heat to my 5 V regulator<br>• Mounted on a metal star board, so it has to be wired by hand and needs a heatsink<br>• Costs about 15× more than a 5 mm LED |

**Choice:** Option 1, Kingbright WP7113SEC/J3

**Rationale:** I picked this LED because it is bright enough to notice across a room, and red clearly tells the user it is time for a dose. At only 20 mA it keeps my 5 V regulator cool, and it is a cheap through-hole part. The XP-G3 star LED is much brighter, but its 350 mA draw would make the regulator way too hot. Since the LED is controlled by the AO3400A switch, I could swap in the star LED later without changing the board.

---

## 7. 5 V Voltage Regulator — **Power (Hub board)**

Turns the 9 V from the wall adapter into a steady 5 V for the Curiosity Nano, the amplifier, and the alert LED. The course requires a linear regulator.

| Solution | Pros | Cons |
|---|---|---|
| <img src="https://mm.digikey.com/Volume0/opasdata/d220001/medias/images/2660/497%7ETO220-3TO220AB%7E%7E3.JPG" width="200"><br>**Option 1.** STMicroelectronics L7805CV (TO-220)<br>$0.50/each<br>[L7805CV at DigiKey](https://www.digikey.com/en/products/detail/stmicroelectronics/L7805CV/585964) | • It is a linear regulator, so it meets the course rule<br>• Can supply up to 1.5 A, about 3× the most my board needs<br>• Works with small, cheap capacitors (0.33 µF in, 0.1 µF out)<br>• The cheapest option, with built-in protection if it overheats or shorts | • Needs at least 7 V coming in (my 9 V adapter is fine)<br>• Turns the extra 4 V into heat, so it needs a heatsink when everything is on |
| <img src="https://mm.digikey.com/Volume0/opasdata/d220001/medias/images/3642/296%7ET03B%7ENDE%7E3.JPG" width="200"><br>**Option 2.** Texas Instruments LM2940CT-5.0/NOPB (TO-220)<br>$1.94/each<br>[LM2940CT-5.0 at DigiKey](https://www.digikey.com/en/products/detail/texas-instruments/LM2940CT-5-0-NOPB/32575) | • Keeps working even if the input drops to about 5.5 V<br>• Protected if the power is hooked up backwards<br>• It is a linear regulator, so it meets the course rule | • Needs a large output capacitor of a specific type, or it can become unstable<br>• Makes the same amount of heat as the 7805, because the heat depends on 9 V − 5 V<br>• Uses more power itself and costs about 4× more |
| <img src="https://mm.digikey.com/Volume0/opasdata/d220001/medias/images/2584/MFG_R-78-e%20series.jpg" width="200"><br>**Option 3.** RECOM R-78E5.0-1.0 (switching)<br>$3.97/each<br>[R-78E5.0-1.0 at DigiKey](https://www.digikey.com/en/products/detail/recom-power/R-78E5-0-1-0/4930585) | • About 92% efficient, so it barely gets warm and needs no heatsink<br>• Same pin layout as a 7805, so it can drop right in | • It is a switching regulator, not linear, so it does not meet the course rule<br>• Adds a small ripple to the output that could add noise to sensor readings<br>• Costs about 8× more |

**Choice:** Option 1, STMicroelectronics L7805CV (with a clip-on TO-220 heatsink)

**Rationale:** I picked the L7805CV because it meets the course's linear-regulator rule, can supply 1.5 A when my board only needs about 0.5 A, and works with small, cheap capacitors. The LM2940's ability to work at a lower input voltage doesn't help me since I have a 9 V adapter, and it needs a special output capacitor. Both linear regulators make the same heat, so I will add a clip-on heatsink (worked out in my Power Budget). The switching regulator would stay cool, but the course doesn't allow it.

---

## 8. External Power Supply — **Power (Hub board)**

Plugs into the wall and gives 9 V DC to the board through the PJ-102AH barrel jack. It needs a 5.5 × 2.1 mm plug with positive in the center, and must supply at least the board's ~0.5 A worst case.

| Solution | Pros | Cons |
|---|---|---|
| <img src="https://mm.digikey.com/Volume0/opasdata/d220001/medias/images/1875/MFG_WSU-Series.jpg" width="200"><br>**Option 1.** Triad Magnetics WSU090-2000 (9 V, 2 A)<br>$12.43/each (Mouser)<br>[WSU090-2000 at Mouser](https://www.mouser.com/ProductDetail/553-WSU090-2000) | • Supplies 2 A, about 4× the most my board needs<br>• Plugs straight into the wall<br>• Has the right size plug with positive in the center<br>• The cheapest of the three | • Not many in stock, and more take a long time to arrive<br>• A very similar "-R" version has the polarity flipped, so I have to make sure not to order that one |
| <img src="https://mm.digikey.com/Volume0/opasdata/d220001/medias/images/2158/MFG_GST18A.jpg" width="200"><br>**Option 2.** MEAN WELL GST18A09-P1J (9 V, 2 A)<br>$14.10/each (Mouser)<br>[GST18A09-P1J at Mouser](https://www.mouser.com/ProductDetail/709-GST18A09-P1J) | • High-quality brand with a 2 A output<br>• Has the right size plug with positive in the center | • It is a desktop power brick, not a wall plug, so it needs a separate AC cord<br>• Low stock at both Mouser and DigiKey |
| <img src="https://www.mouser.com/images/cuiinc/images/swi12-12-n-p6_SPL.jpg" width="200"><br>**Option 3.** CUI SWI12-9-N-P5 (9 V, 1.2 A)<br>$17.59/each (Mouser)<br>[SWI12-9-N-P5 at Mouser](https://www.mouser.com/ProductDetail/490-SWI12-9-N-P5) | • Lots in stock (800+)<br>• Plugs into the wall and has the right plug | • The most expensive<br>• Supplies the least current (1.2 A), the least room for error |

**Choice:** Option 1, Triad Magnetics WSU090-2000

**Rationale:** I picked this adapter because it is the cheapest, plugs right into the wall, and supplies 2 A, which is way more than my worst case of about 0.52 A (with the 25% safety margin). It has the right plug for my barrel jack. I will make sure to order the WSU090-2000 and not the "-R" version, which has the polarity flipped and would send power backwards into the board. If it goes out of stock, the CUI adapter is my backup.

---

## Microcontroller Pin Table — **Reminder & Alerts (Hub)**

These are the PIC18F57Q43 Curiosity Nano pins I use on my hub board. They match my [Block Diagram](../01-Block-Diagram/Block-Diagram.md).

| PIC pin | Type | Direction | Connects to | Signal |
|---|---|---|---|---|
| RB0 | Digital input | In | Take Dose button | Digital (3.3 V, 1 pin) |
| RB1 | Digital input | In | Set / Mode button | Digital (3.3 V, 1 pin) |
| RB2 | Digital input (interrupt) | In | MCP7940N alarm | Digital (3.3 V, 1 pin) |
| RC3 | I²C clock | Out | MCP7940N | Digital - Serial (I²C, 2 pins) |
| RC4 | I²C data | In/Out | MCP7940N | Digital - Serial (I²C, 2 pins) |
| RA3–RA5 | Digital outputs | Out | Ready / Taken / Error LEDs | Digital (3.3 V, 3 pins) |
| RC5 | Digital output | Out | AO3400A → alert LED | Digital (3.3 V, 1 pin) |
| RC2 | PWM | Out | LM386N-1 → speaker | Analog (0–3.3 V PWM, 1 pin) |
| RD0 | Digital output | Out | J1-1 → Weight board (DOSE_READY) | Digital (3.3 V, 1 pin) |
| RD1 | Digital input | In | J1-2 ← Weight board (DOSE_REMOVED) | Digital (3.3 V, 1 pin) |
| RD2 | Digital input | In | J1-3 ← Weight board (WEIGHT_FAULT) | Digital (3.3 V, 1 pin) |
| RD3 | Digital output | Out | J1-4 → Weight board (TARE_REQ) | Digital (3.3 V, 1 pin) |
| RD4 | Digital input | In | J1-5 ← Weight board (HEARTBEAT_A) | Digital (3.3 V, 1 pin) |
| RA0 | ADC | In | J1-6 ← Weight board (WEIGHT_LEVEL) | Analog (0–3.3 V, 1 pin) |
| RD5 | Digital output | Out | J2-1 → Cap board (DOSE_READY) | Digital (3.3 V, 1 pin) |
| RD6 | Digital input | In | J2-2 ← Cap board (LID_OPEN) | Digital (3.3 V, 1 pin) |
| RD7 | Digital input | In | J2-3 ← Cap board (LID_FAULT) | Digital (3.3 V, 1 pin) |
| RE0 | Digital input | In | J2-5 ← Cap board (HEARTBEAT_B) | Digital (3.3 V, 1 pin) |
| RE1 | Digital input | In | J3-2 ← Environment board (TEMP_ALERT) | Digital (3.3 V, 1 pin) |
| RE2 | Digital input | In | J3-3 ← Environment board (LIGHT_ALERT) | Digital (3.3 V, 1 pin) |
| RF2 | Digital input | In | J3-5 ← Environment board (HEARTBEAT_D) | Digital (3.3 V, 1 pin) |
| RA1 | ADC | In | J3-6 ← Environment board (TEMP_LEVEL) | Analog (0–3.3 V, 1 pin) |
| VBUS | Power in | In | L7805CV 5 V output | Power |
| GND | Ground | — | Board ground, J1–J3 pin 8 | Ground |

Not used (the Nano already uses these for its own button, LED, programming, and debugging): RB4, RB6, RB7, RE3, RF0, RF1, RF3.
