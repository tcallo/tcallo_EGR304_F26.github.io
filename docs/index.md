---
title: Welcome
---

<center>
<font size="5">Taylor Callo Datasheet</font><br>
as part of<br>
<font size="7">Project Aurora</font><br>
for<br>
<font size="4">Team 102</font><br>
EGR 304 · Fall 2026 · Arizona State University
</center>

## Introduction

This is my individual datasheet site for Project Aurora, a smart medication holder built by Team 102. It documents my subsystem from the block diagram through parts selection, schematic, and power budget.

### Project Summary

Project Aurora helps a user take their medication on time. Four connected boards share the job: a weight board detects when a dose is removed, a cap board detects when the bottle is opened, an environment board watches storage temperature and light, and a hub board keeps the schedule and gives reminders. The boards talk to each other over 8-pin ribbon cables. See the [team website](https://asu-egr304-2026-f-102.github.io/) for the full system.

### My Contribution

I am designing the **Reminder & Alerts hub board (Member C)**. It keeps the dose schedule with a real-time clock, alerts the user with a speaker and a high-brightness LED, shows status on three LEDs, and connects to the three sensing boards.

**Datasheet sections:**

- [Block Diagram](01-Block-Diagram/Block-Diagram.md): how my board is laid out, its power supplies, parts, and microcontroller pin use
