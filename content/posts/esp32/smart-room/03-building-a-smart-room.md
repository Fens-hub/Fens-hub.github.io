---
title: "Building a Smart Room with ESP32: Motion Detection and Automation"
date: 2026-11-02
subject: "ESP32 & IoT"
topic: "Smart Room Series"
weight: 3
series: "Smart Room"
tags: [iot, electronics, esp32, pir-sensor, oled]
summary: "A smart room occupancy monitor built with an ESP32, PIR motion sensor, LED and OLED display, simulated in Wokwi."
---

## Overview

A practical exploration of how an IoT system can respond to activity in an indoor space.

I built a smart room occupancy monitoring system using an ESP32, a PIR motion sensor, an LED and an OLED display. The idea was to detect movement, give visual feedback, and show the room's occupancy status.

The project let me apply what I learnt in my introduction to IoT, this time in a practical simulation.

## The components

| Component | Connection | Role |
|---|---|---|
| ESP32 | n/a | Main microcontroller |
| PIR motion sensor | GPIO 27 | Detects movement |
| LED | GPIO 13 | Visual indicator of room activity |
| SSD1306 OLED display | I2C | Shows occupancy information |

## What I did

- Designed a smart room occupancy monitoring concept.
- Connected the PIR sensor to GPIO 27 and the LED to GPIO 13.
- Added an SSD1306 OLED display over I2C.
- Programmed the system to detect motion, light the LED and show the occupancy status on the OLED.
- Set a vacancy timeout of 5 seconds, so the room is marked vacant after that long without motion.
- Simulated and tested the whole system in Wokwi.

## What I learnt

- How to bring several electronic components together into one system.
- How to read sensor input and control more than one output.
- How to use GPIO pins for different hardware functions.
- How I2C communication works with an OLED display.
- How to manage occupancy states in programming logic, using time-based conditions with `millis()`.
- How to troubleshoot interactions between different components.
- How to approach building a simple automation system.
