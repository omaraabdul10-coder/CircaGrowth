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
