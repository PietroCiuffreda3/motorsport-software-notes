---
layout: post
title: Structuring Uncertainty: Building a Data-Driven Endurance Strategy Model
date: 2026-03-02

---
# Structuring Uncertainty: Building a Data-Driven Endurance Strategy Model
## Summary

Endurance racing rarely fails because of a single mistake.
It fails because small uncertainties accumulate over hours.

This project began with a simple objective:
transform lap-by-lap data into structured strategic decisions during long-distance races.

What emerged was not a spreadsheet, but a modular decision-support framework.

# The problem: instinct vs structure

In endurance racing, decisions are often made under pressure:

Is the tyre still stable?

Can we extend the stint?

Are we fuel-safe for the next window?

Is the pace drop degradation or traffic?

Instinct matters.
Experience matters.

But instinct without structure introduces bias.

The goal was not to eliminate human judgment.
It was to support it with consistent logic.

# Phase 1 — Building the architecture

The model was structured into four layers:

## 1. Lap Layer

Raw data for every lap:

stint ID

driver

lap time

tyre percentage

traffic flags

dirty lap filtering

This layer isolates noise from usable information.

## 2. Stint Layer

Aggregation of clean laps to extract:

core pace

end-of-stint pace

degradation delta

fuel consumption trend

tyre end percentage

At this stage, the model moved beyond simple averages.

Trend direction began to matter more than raw values.

## 3. Decision Console

A scenario-based interface simulating:

driver selection

traffic assumptions

push mode

compound selection

target stint length

The objective was to test decisions before executing them.

## 4. Adjustable Inputs

Thresholds and multipliers allow adaptation to:

compound behaviour

traffic intensity

push level

degradation sensitivity

This transforms the model from static to adaptive.

# Phase 2 — Moving beyond averages

Endurance performance degradation is rarely linear.

The model introduced:

Degradation slope analysis
Detecting trend acceleration rather than waiting for a drop.

Consistency index
Monitoring variance increase before potential tyre cliff.

Multi-factor cliff detection logic
Combining trend, delta vs core pace, and tyre state.

Fuel–tyre interaction modelling
Recognising that load influences degradation.

Strategy confidence indicator
Estimating how reliable the dataset is before suggesting decisions.

The shift was conceptual.

From: “What is the average pace?”
To: “How stable is performance, and how likely is deterioration?”

# Phase 3 — Real race application

The framework was used as decision support during a 12-hour endurance race at the Circuit de la Sarthe.

It was not an automated strategy engine.

It was a structured reasoning tool.

During the race, it supported:

validation of expected degradation behaviour

anticipation of potential cliff windows

stint extension or reduction decisions

fuel vs tyre trade-offs under evolving conditions

Its primary contribution was not prediction.

It was clarity.

What this project is — and is not

This is not a finished product.
It is not a black-box solution.

It is a structured approach to managing uncertainty in long-distance racing.

The framework remains private at operational level.
The conceptual development, however, will continue to be documented.

# Open questions

Several areas remain under exploration:

probabilistic cliff modelling

uncertainty quantification through scenario simulation

robustness metrics across compounds

transition from spreadsheet logic to software implementation

Endurance strategy is not about certainty.
It is about controlled risk over time.

This project aims to formalise that process.


---
<a href="https://pietrociuffreda3.github.io/motorsport-software-notes/">HOME</a>