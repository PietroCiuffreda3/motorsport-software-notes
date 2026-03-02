---
title: Endurance Stint Decision System
subtitle: An Excel-based pit wall tool for fuel risk, tyre degradation, and stint stability.
date: 2026-03-03
status: MVP (Excel)
hero: /assets/img/tel.png
---

## What this is

**Endurance Stint Decision System** is a practical pit wall-style workbook that turns stint data into actionable calls.

It is built around one idea: in GT/endurance (and serious eRacing), performance is not the best lap — it is **controlled degradation, consistency, and risk management**.

## Who it is for

- GT / endurance teams (real or sim)
- eRacing teams with structured stints and driver swaps
- Anyone who needs repeatable, decision-oriented reporting from lap/stint data

## Core workflow

1. **Input**
   - Stint/lap table (lap time, sectors if available)
   - Fuel metrics (baseline, deltas)
   - Tyre state and/or estimated “grip end” markers

2. **Processing**
   - Core pace extraction (stable stint segment)
   - Late-stint performance check (last-laps vs core)
   - Fuel delta/risk flags
   - Cliff logic (tyre drop threshold)

3. **Output**
   - Stint summary dashboard
   - Automated flags and recommended actions
   - Comparable metrics across drivers/stints

## Why it matters (GT / endurance reality)

In endurance, decisions are typically made under time pressure. A useful tool should answer:

- *Are we trending into a tyre cliff?*
- *Is pace loss driven by fuel mass, tyres, or driver inconsistency?*
- *Is the driver stable enough to extend?*
- *What is the risk if we stay out?*

This workbook is structured to be used exactly that way: it turns data into **calls**, not charts.

## Current capabilities (MVP)

### Fuel and risk

- Baseline fuel model per driver
- Fuel delta vs baseline
- Fuel flag logic to identify risk conditions

### Tyre/grip end logic

- “Grip end” estimation / thresholds
- Tyre end percentage approximation
- Cliff detection logic

### Pace logic

- **Core lap time** (stable segment reference)
- Last 2 laps vs core pace comparison
- “Grip final” decision rules

## Roadmap (what will make it recruiter-proof)

These are the modules that will push this from “good workbook” to “junior telemetry analyst portfolio piece”.

### 1) Fuel-corrected pace

Goal: isolate fuel mass effect from pace.

Model (first iteration, linear):

> `LapTime_corrected = LapTime_raw - k * FuelMass`

Where **k** is a fuel time penalty coefficient (sec/kg) tuned per car/series.

### 2) Degradation regression per stint

Run a simple regression on fuel-corrected lap times within a stint:

- **Degradation rate** (sec/lap)
- **Fit quality** (R²)

### 3) Consistency index

Add a stability KPI for each stint/driver:

- Std dev of clean laps
- Outlier rate
- Rolling variance

## What I learned

- A tool is only valuable if it supports decisions under pressure.
- The most useful telemetry outputs are often simple, but repeatable.
- Endurance pace analysis must be **stint-aware** (core pace, late-stint drop, consistency) rather than “best lap” driven.

## Want to use it

If you want this published as a downloadable template in the repo, add the workbook under `assets/downloads/` and link it here.
