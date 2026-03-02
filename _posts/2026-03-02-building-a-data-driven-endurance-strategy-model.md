---
layout: post
title: "Building a Data-Driven Endurance Strategy Model"
subtitle: "Transforming lap-by-lap data into structured strategic decisions during long-distance races."
nav_title: Strategy Model
hero: /assets/img/excel.png
hero_alt: "Endurance strategy: data-driven decisions"
hero_caption: "Turning uncertainty into structured choices across stints, traffic, fuel and tyre degradation."
---

## Summary

Endurance racing rarely fails because of one mistake.  
It fails because small uncertainties accumulate over time.

This article describes a framework designed to reduce that uncertainty by turning lap data into a consistent decision process — without replacing human judgment.

## The problem: instinct vs structure

In endurance racing, decisions are made under pressure:

- Is the tyre still stable?
- Can we extend the stint?
- Are we fuel-safe for the next window?
- Is the pace drop degradation or traffic?

Instinct matters.  
Experience matters.

But instinct without structure introduces bias.

The goal was not to eliminate human judgment.  
It was to support it with consistent logic.

## Phase 1 — Building the architecture

The model was structured into four layers.

### 1) Lap layer

Raw data for every lap:

- stint ID
- driver
- lap time
- tyre percentage
- traffic flags
- dirty lap filtering

This layer isolates noise from usable information.

### 2) Stint layer

Aggregation of clean laps to extract:

- core pace
- end-of-stint pace
- degradation delta
- fuel consumption trend
- tyre end percentage

At this stage, trend direction mattered more than raw averages.

### 3) Decision console

A scenario-based interface simulating:

- driver selection
- traffic assumptions
- push mode
- compound selection
- target stint length

The objective: test decisions before executing them.

### 4) Adjustable inputs

Thresholds and multipliers allowed adaptation to:

- compound behaviour
- traffic intensity
- push level
- degradation sensitivity

This transformed the model from static to adaptive.

## Phase 2 — Moving beyond averages

Endurance degradation is rarely linear.

The model introduced:

- **Degradation slope analysis**  
  Detecting acceleration before visible drop.

- **Consistency index**  
  Monitoring variance increase before a tyre cliff.

- **Multi-factor cliff detection logic**  
  Combining trend, delta vs core pace, and tyre state.

- **Fuel–tyre interaction modelling**  
  Recognising that load influences degradation.

- **Strategy confidence indicator**  
  Estimating dataset reliability before suggesting decisions.

The shift was conceptual.

From: “What is the average pace?”  
To: “How stable is performance, and how likely is deterioration?”

## Phase 3 — Real race application

The framework was used during a 12-hour endurance race at the Circuit de la Sarthe.

It was not an automated strategy engine.  
It was a structured reasoning tool.

During the race, it supported:

- validation of expected degradation behaviour
- anticipation of potential cliff windows
- stint extension or reduction decisions
- fuel vs tyre trade-offs

Its primary contribution was not prediction.

It was clarity.

## What this project is — and is not

This is not a finished product.  
It is not a black-box solution.

It is a structured approach to managing uncertainty in long-distance racing.

The operational framework remains private.  
The conceptual development will continue to be documented.

## Open questions

- probabilistic cliff modelling
- uncertainty quantification via scenario simulation
- robustness metrics across compounds
- transition from spreadsheet logic to software implementation

Endurance strategy is not about certainty.  
It is about controlled risk over time.

This project aims to formalise that process.

[HOME]({{ '/' | relative_url }})