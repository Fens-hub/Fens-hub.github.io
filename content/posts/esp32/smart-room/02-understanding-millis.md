---
title: "Understanding millis(): The Mathematics Behind Time-Based Logic"
date: 2026-10-20
subject: "ESP32 & IoT"
topic: "Smart Room Series"
weight: 2
series: "Smart Room"
tags: [esp32, embedded-programming, millis, mathematics]
summary: "How subtraction and millis() let my smart room system decide when a room is vacant, without blocking the rest of the program."
---

## Overview

One of the most interesting challenges in my smart room project was the occupancy timeout.

At first, using `millis()` and calculating elapsed time did not come easily. The system had to remember the last time motion was detected, and only mark the room vacant after a set period with no further movement.

It turned into a chance to explore time-based programming, arithmetic and non-blocking execution in embedded systems.

## What I did

- Explored how the ESP32's `millis()` function works.
- Added a variable to store the last time motion was detected.
- Set a vacancy timeout of 5,000 milliseconds.
- Used subtraction to calculate elapsed time.
- Wrote a conditional statement to decide when the room becomes vacant.
- Tested the behaviour in a Wokwi simulation.

The central calculation is:

```cpp
if (millis() - lastMotionTime >= vacancyTimeout) {
    // Mark room as VACANT
}
```

## The mathematics

The elapsed time is the difference between the current time and the last time motion was detected:

```text
ElapsedTime = CurrentTime - LastMotionTime
```

The room is marked vacant when that difference reaches the timeout:

```text
ElapsedTime >= VacancyTimeout
```

## A worked example

These numbers are illustrative. The timeout is 5,000 ms, and the last motion was detected at 12,000 ms:

| Current time (ms) | Last motion (ms) | Elapsed (ms) | Elapsed ≥ 5,000? | Room status |
|---|---|---|---|---|
| 12,000 | 12,000 | 0 | No | Occupied |
| 14,000 | 12,000 | 2,000 | No | Occupied |
| 16,500 | 12,000 | 4,500 | No | Occupied |
| 17,000 | 12,000 | 5,000 | Yes | Vacant |
| 20,000 | 12,000 | 8,000 | Yes | Vacant |

Here it is as a timeline:

```text
12,000 ms  Motion detected   lastMotionTime = 12,000   OCCUPIED
14,000 ms  No motion         elapsed = 2,000           OCCUPIED
17,000 ms  No motion         elapsed = 5,000           VACANT
21,000 ms  Motion detected   lastMotionTime = 21,000   OCCUPIED
```

Every time motion is detected, `lastMotionTime` is reset, so the elapsed time starts again from zero.

## From mathematics to code

A simplified sketch of the logic:

```cpp
const int PIR_PIN = 27;
const unsigned long vacancyTimeout = 5000;  // 5 seconds, in milliseconds
unsigned long lastMotionTime = 0;

void loop() {
  if (digitalRead(PIR_PIN) == HIGH) {
    lastMotionTime = millis();  // remember when motion was last seen
  }

  if (millis() - lastMotionTime >= vacancyTimeout) {
    // Mark room as VACANT
  } else {
    // Mark room as OCCUPIED
  }
}
```

Both time values are `unsigned long`, so the subtraction still gives the right answer when `millis()` wraps back to zero after about 49 days.

## What I learnt

- `millis()` measures the time since the microcontroller started running.
- Time values should be stored as `unsigned long`.
- Elapsed time is calculated by subtraction.
- Conditional statements control how the system behaves.
- Non-blocking timing keeps the program responsive, while using `delay()` for long waits can get in the way of other tasks.
- Mathematical ideas translate directly into practical programming logic.
