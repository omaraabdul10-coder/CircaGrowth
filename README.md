# CircaGrowth

### Circadian Rhythm × Glucose × Insulin × Growth Hormone

**Created by Omar Abdullayev**  
High School Student  
Ganja School No. 39 named after M. C. Pasheyev

---

## Overview

CircaGrowth is a computational physiology research project that uses a coupled system of ordinary differential equations (ODEs) to investigate the interaction between:

- Circadian rhythm
- Glucose dynamics
- Insulin dynamics
- Insulin tissue action
- Growth hormone (STH) secretion

The central research question is:

> How can the timing of food intake interact with the physiological dynamics surrounding nocturnal growth-hormone secretion?

The project approaches this question through mathematical modeling and numerical simulation rather than through a clinical experiment.

---

## Why Does This Matter?

Growth hormone is involved in physiological processes associated with childhood and adolescent growth, tissue development, metabolism, and other biological processes.

CircaGrowth does **not** directly predict human height or muscle growth.

Instead, it models growth-hormone dynamics as an intermediate physiological component and investigates how meal timing can affect the simulated STH signal under a defined mathematical model.

Potential research directions include:

- studying meal timing during childhood and adolescence;
- investigating the relationship between metabolic signals and nocturnal STH secretion;
- exploring physiological timing around sleep;
- developing more individualized computational models;
- extending the model toward tissue or muscle-growth dynamics in future work.

The project should therefore be understood as a **computational modeling and hypothesis-generation framework**, not as medical advice or clinical validation.

---

## Mathematical Model

The model consists of five state variables:

- `G(t)` — blood glucose concentration
- `X(t)` — tissue-level insulin activation
- `A(t)` — insulin absorption compartment
- `I(t)` — active plasma insulin
- `H(t)` — growth hormone / STH

The system is:

```text
dG/dt = R_G(t) − (p1 + X)G + p1G_b

dX/dt = −p2X + p3(I − I_b)

dA/dt = k_a,amp R_G(t) − k_aA

dI/dt = k_aA + nI_b − nI

dH/dt = S_H C(t) [K_I / (K_I + I)] − k_HH
```

where `C(t) = max(0, cos(2π(t − t_peak)/1440))` is the circadian STH drive and `R_G(t)` is a sum of Gaussian meal pulses.

---

## Simulation convention

- `t` is wall-clock time in minutes from 00:00. Meals at 08:00 and 13:00 every day, plus an optional dinner; default STH peak at 02:00.
- Fixed-step RK4, 1-minute step, run for 3 days; the night of day 2 → 3 is reported, so results do not depend on the initial state.

## Results (current model, `index.html`)

| Scenario | STH peak (ng/mL) | vs. no-dinner control |
|---|---|---|
| No dinner (control) | 13.42 | — |
| Dinner 15:00 | 13.42 | 0.0% |
| Dinner 21:00 | 13.42 | 0.0% |
| Dinner 23:00 | 13.28 | −1.0% |
| Meal 00:00 | 12.84 | −4.3% |
| Meal 01:18 (≈45 min before the STH peak) | 11.54 | −14.0% |

Because modeled insulin is cleared quickly (half-life ≈ 5 min), suppression is confined to roughly the last 2 hours before the STH peak.

**Correction (October 2026).** An earlier version labeled the −14% scenario as a "23:18 dinner". That label came from a clock-offset error (the code treated t = 0 as 08:00 while meals were placed as if t = 0 were 00:00). The −14% case is a meal at about 01:18; a 23:00 dinner changes the peak by about 1% in this model.

## Known limitations

- **One-way coupling.** Insulin is driven directly by the meal signal (compartment `A`), not by glucose, and STH depends only on insulin. Glucose and `X` therefore do not affect the STH result; the glucose equations are descriptive only.
- After each meal, simulated glucose undershoots baseline (to about 60 mg/dL), an artifact of combining Bergman IVGTT parameters with a meal-driven insulin input.
- Bergman minimal-model parameters come from IVGTT studies, not mixed-meal data; `k_a`, `k_a,amp` and `S_H` are set by hand.
- `C(t)` is a single broad nightly cosine; real GH secretion is pulsatile.
- Single-person model, no inter-individual variation, not validated against human data. Not medical advice.
