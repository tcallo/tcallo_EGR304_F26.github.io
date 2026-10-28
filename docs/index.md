<div style="text-align:center; margin: 0 0 2.5rem;">

  <p style="font-size:0.95rem; letter-spacing:0.08em; text-transform:uppercase; color:#2196F3; margin:0;">Individual Datasheet</p>
  <h1 style="font-size:2.6rem; font-weight:600; margin:0.2rem 0 0.3rem;">Taylor Callo</h1>
  <p style="font-size:1.15rem; color:#555; margin:0 0 1.2rem;">
    Member C · Reminder &amp; Alerts Hub
  </p>

  <hr style="width:60px; border:0; border-top:3px solid #2196F3; margin:0 auto 1.2rem;">

  <p style="font-size:1rem; margin:0.2rem 0;">Part of <b>Project Aurora</b> · Team 102</p>
  <p style="font-size:0.95rem; color:#555; margin:0.2rem 0;">EGR 304 Embedded Systems Design · Fall 2026 · Arizona State University</p>

  <p style="font-size:0.95rem; margin:1rem 0 0;">
    <a href="https://asu-egr304-2026-f-102.github.io/">← Back to the Team 102 website</a>
  </p>

  <img src="taylor-datasheet-qr.png" alt="QR code to Taylor Callo's datasheet" width="150" style="margin-top:1.5rem;">
  <p style="font-size:0.85rem; color:#777; margin:0.3rem 0 0;">Scan to open this datasheet</p>

</div>
## Introduction

This is my individual datasheet site for Project Aurora, a smart medication holder built by Team 102. It documents my subsystem from the block diagram through parts selection, schematic, and power budget.

### Project Summary

Project Aurora helps a user take their medication on time. Four connected boards share the job: a weight board detects when a dose is removed, a cap board detects when the bottle is opened, an environment board watches storage temperature and light, and a hub board keeps the schedule and gives reminders. The boards talk to each other over 8-pin ribbon cables. See the [team website](https://asu-egr304-2026-f-102.github.io/) for the full system.

### My Contribution

I am designing the **Reminder & Alerts hub board (Member C)**. My main subsystem is the **audio alert**: an LM386 audio amplifier that drives a speaker to remind the user when a dose is due. The hub also has a high-brightness alert LED, three status LEDs, user buttons, and connects to the three sensing boards. A battery-backed **real-time clock (MCP7940N)** that keeps the dose schedule is a **stretch goal**.

**Datasheet sections:**

- [Block Diagram](01-Block-Diagram/Block-Diagram.md): how my board is laid out, its power supplies, parts, and microcontroller pin use
- [Component Selection](02-Component-Selection/Component-Selection.md): three options compared for each major part, and my choices
    - [Decision-Making Process](02-Component-Selection/Component-Selection.md#decision-making-process)
    - [How My Parts Meet the Product Requirements](02-Component-Selection/Component-Selection.md#how-my-parts-meet-the-product-requirements)
    - [MCC Configuration](02-Component-Selection/Component-Selection.md#mcc-configuration-pic18f57q43-pins-and-peripherals)
- [Schematic](04-Schematic/Schematic.md): the full hub schematic with PDF and KiCad downloads
    - [How the Schematic Works](04-Schematic/Schematic.md#how-the-schematic-works)
    - [How It Meets User Needs and Product Requirements](04-Schematic/Schematic.md#how-it-meets-user-needs-and-product-requirements)
- [Power Budget](05-Power-Budget/Power-Budget.md): current needed on each power rail, and regulator and adapter checks
    - [What the Power Budget Told Me](05-Power-Budget/Power-Budget.md#what-the-power-budget-told-me)
