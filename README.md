# CircaGrowth — Interactive Research Website

This is a GitHub Pages-ready, dependency-free research showcase for the CircaGrowth V2 computational model.

## Run locally
Open `index.html` in a browser.

## Publish on GitHub Pages
1. Create a new GitHub repository, e.g. `circagrowth`.
2. Upload `index.html` and the `README.md`.
3. Open **Settings → Pages**.
4. Under **Build and deployment**, choose **Deploy from a branch**.
5. Select `main` and `/ (root)`, then save.
6. GitHub will provide the public Pages URL.

## What is included
- Research-focused landing page
- Mathematical equations and state variables
- Interactive 24-hour RK4 simulation
- Dinner-time and STH-peak controls
- Glucose / insulin / STH charts
- V2 debugging story
- Validation table using the project report's reported values
- Limitations and references

## Scientific scope
The website communicates the supplied CircaGrowth V2 model as a computational proof-of-concept. It does not present the simulation as clinical validation or a medical recommendation.

## Source basis
The implementation follows the supplied V2 Python model and methodology report, including the five-state ODE system, Gaussian meal input, circadian signal, PK insulin compartment, and 24-hour RK4 browser simulation.


## Academic framing

The website is intentionally structured to demonstrate both the applied-mathematics and computer-science sides of the project:

- **Applied mathematics:** state-space ODE formulation, equilibrium consistency, nonlinear coupling, numerical integration, parameter sensitivity, control comparisons, and model validation.
- **Computer science:** deterministic numerical solver, modular computational architecture, interactive parameterization, data transformation, visualization, and reproducibility.
- **Research methodology:** face-validity testing, failure analysis, root-cause debugging, controlled scenarios, explicit limitations, and proposed robustness experiments.

The site should be presented as a computational modeling/research artifact rather than as a clinical application.
