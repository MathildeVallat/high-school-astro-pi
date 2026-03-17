# ISS Day/Night Detector

## What is Astro Pi?

Astro Pi is a small Raspberry Pi computer developed by the Raspberry Pi Foundation in
collaboration with the UK Space Agency and the European Space Agency (ESA). Two special
Astro Pi units — nicknamed **Ed** and **Izzy** — have been qualified for spaceflight and
are permanently aboard the International Space Station (ISS). The Sense HAT is the core
component of the Astro Pi units.

The **European Astro Pi Challenge** is an ESA Education project run in collaboration with
the Raspberry Pi Foundation, offering young people the opportunity to conduct scientific
investigations in space by writing computer programs that run on board the ISS. The
challenge has two missions: **Mission Zero**, suited for beginners, and **Mission Space
Lab**, for more experienced coders carrying out a real scientific task.

This project was created as part of a high school submission to the Astro Pi Challenge.

---

## Overview

This program captures camera frames, reads environmental data from the Sense HAT, and
determines whether the ISS is currently in **daylight or darkness** by comparing the
angular positions of the ISS and the Sun.

---

## Hardware Requirements

- Raspberry Pi with camera module (Astro Pi Ed/Izzy)
- Sense HAT

---

## Dependencies
```
ephem, picamera, opencv-python, numpy, sense-hat
```

Install with:
```bash
pip install ephem opencv-python numpy
```

---

## What It Does

- Captures continuous camera frames and computes average **brightness**
- Reads **temperature, pressure, and humidity** from the Sense HAT
- Uses TLE orbital data to compute ISS and Sun positions via `ephem`
- Compares their right ascension angle to classify each moment as **day or night**
- Logs all readings to `Data.csv` every ~1 second
- Runs for **3 hours** (10,800 seconds), then stops automatically

---

## Output

`Data.csv` with columns:

| Time | Duration | Temperature | Pressure | Humidity | Brightness | Day/Night |
|------|----------|-------------|----------|----------|------------|-----------|

---

## Known Issues

> **`moon` is referenced in the print statements but never defined — this will raise a
`NameError`.**

- TLE data is hardcoded and will become inaccurate over time; update `line1`/`line2`
regularly
