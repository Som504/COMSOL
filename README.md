
# Semiconductor Device Modeling using COMSOL Multiphysics

**Heterojunction 1D and Schottky Contact 2D Axisymmetric**

This repository contains two semiconductor device models implemented using **COMSOL Multiphysics 6.2 (Semiconductor Module)**. The models focus on **interface-dominated carrier transport**, a key aspect of modern electronic and optoelectronic devices.

The repository includes:

* **1D Heterojunction device model** (GaAs / Al₀.₂₅Ga₀.₇₅As)
* **2D Axisymmetric Schottky barrier diode model** (Tungsten / Silicon)

Both models are based on **official COMSOL benchmark examples**, extended and carefully studied to understand **physical modeling choices, numerical stability, and result interpretation**.



## 1. Heterojunction 1D Modeling

### Overview

The heterojunction model investigates **carrier transport across semiconductor–semiconductor interfaces** and compares two commonly used interface formulations:

* **Continuous quasi-Fermi level model**
* **Thermionic emission model**

The study highlights how **band offsets, doping configurations, and interface physics** affect current transport and energy band profiles.



### Device Structure

* Materials: **GaAs / Al₀.₂₅Ga₀.₇₅As**
* Geometry: **1D planar heterojunction**
* Bias conditions: **Forward and reverse bias**
* Recombination: **Shockley–Read–Hall (SRH)** included in all domains



### Heterojunction Configurations Studied

| Configuration | Junction Type | Dominant Carrier |
| ------------- | ------------- | ---------------- |
| n–n           | Isotype       | Electrons        |
| p–n           | Anisotype     | Electrons        |
| n–p           | Anisotype     | Holes            |

These configurations demonstrate that **carrier dominance is governed by band alignment**, not simply by doping type.



### Interface Transport Models

#### Continuous Quasi-Fermi Levels

* Enforces continuity of electron and hole quasi-Fermi levels
* Assumes ideal carrier transmission
* Tends to overestimate current when interface barriers are significant

#### Thermionic Emission

* Models carrier transport via thermal emission over band discontinuities
* Explicitly captures conduction-band and valence-band barriers
* Produces I–V curves in close agreement with literature



### Key Results

* Clear distinction between electron- and hole-dominated transport
* Energy band diagrams reveal the physical origin of current flow
* Thermionic emission model better represents realistic heterojunction behavior
* Solver continuation and equilibrium initialization are essential for convergence



## 2. Schottky Contact Modeling (2D Axisymmetric)

### Overview

The second model simulates an **ideal Schottky barrier diode**, consisting of a **tungsten metal contact deposited on n-type silicon**. The goal is to reproduce the **forward-bias J–V characteristics** and compare them with experimental data reported in literature.



### Why 2D Axisymmetric?

* The Schottky diode has **cylindrical symmetry**
* 2D axisymmetric modeling captures **true 3D current spreading**
* Achieves **3D-accurate results at significantly lower computational cost**



### Device Structure

* Metal: **Tungsten**
* Semiconductor: **n-type Silicon (Nd = 1×10¹⁶ cm⁻³)**
* Contact type: **Ideal Schottky**
* Barrier height determined by:
  [
  Phi_B = Phi_m - chi_0
  ]
* Bias range: **0 – 0.25 V (forward bias)**



### Importance of Integration Coupling

A critical step in this model is the creation of an **integration coupling variable**:

* Used to compute the **total current density across the Schottky contact**
* Integrates the **normal component of current density** over the metal–semiconductor interface
* Enables accurate extraction of **J–V characteristics**

This step is essential because:

* COMSOL solves **local current density**
* Device characterization requires **global current**
* Boundary integration converts flux into measurable device current

For 2D axisymmetric models, special care is taken to **disable revolved-geometry integration when required**, ensuring correct physical scaling.



### Numerical Strategy

To ensure stable convergence of the nonlinear semiconductor equations:

* Impurity concentration is **ramped gradually**
* Equilibrium solution reused for biased simulations
* Fine mesh applied near the **depletion region**
* Continuation methods used for voltage sweep

These techniques are critical for Schottky devices due to the **strong exponential dependence of current on barrier height**.



### Key Results

* Simulated **J–V curve closely matches experimental measurements**
* Confirms dominance of **thermionic emission** in ideal Schottky contacts
* Demonstrates correct barrier-controlled transport behavior



## Numerical and Physical Insights Gained

Across both models:

* Small modeling choices (feature order, domain selection, solver continuation) strongly affect convergence
* Interface physics dominates device behavior
* Numerical stability depends on **physical consistency**, not solver force
* Proper current extraction requires **integration coupling**, not point evaluation



## References

* K. Horio and H. Yanai, *IEEE Transactions on Electron Devices*, 1990
* C. R. Crowell, J. C. Sarace, and S. M. Sze, *Trans. Metallurgical Society of AIME*, 1965



## Relevance and Applications

This repository is relevant for:

* TCAD and semiconductor device modeling
* Optoelectronic and photonic devices
* Metal–semiconductor interfaces
* Graduate-level device physics education
* Research and industry-oriented COMSOL workflows



## Author

**Som Mudgil**
ECE Undergraduate | Semiconductor Devices | TCAD | Photonics


Just tell me.
