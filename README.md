
# Heterojunction 1D Modeling using COMSOL Multiphysics

This repository contains a **1D semiconductor heterojunction device model** implemented in **COMSOL Multiphysics 6.2**, based on the official Semiconductor Module benchmark example.

The work focuses on **understanding carrier transport across heterojunction interfaces** and comparing two widely used physical formulations:

* **Continuous quasi-Fermi level model**
* **Thermionic emission model**

The study is motivated by device-level modeling needs in **semiconductor devices, optoelectronics, and photonics**, where interface physics plays a dominant role.



## Problem Overview
Semiconductor **heterojunctions** occur when two dissimilar semiconductor materials are brought into contact, leading to:

* Band discontinuities
* Interface barriers
* Carrier-selective transport mechanisms

This repository simulates **GaAs / Al₀.₂₅Ga₀.₇₅As heterojunctions** under **forward and reverse bias**, capturing how:

* Band alignment
* Doping configuration
* Interface modeling assumptions

affect **I–V characteristics** and **energy band diagrams**.



## Heterojunction Configurations Studied

Three heterojunction configurations are modeled:

| Configuration | Type      | Dominant Carrier |
| ------------- | --------- | ---------------- |
| n–n           | Isotype   | Electrons        |
| p–n           | Anisotype | Electrons        |
| n–p           | Anisotype | Holes            |

Each configuration highlights how **band bending and barrier formation** determine whether electrons or holes dominate current transport.



## Physical Models Implemented

### 1️ Continuous Quasi-Fermi Level Model

* Enforces continuity of electron and hole quasi-Fermi levels across the interface
* Assumes ideal carrier transmission
* Can slightly overestimate current when interface barriers are significant

**Best suited for:**
Low-resistance interfaces or preliminary modeling



### 2️ Thermionic Emission Model

* Models carrier transport via **thermally activated emission over band offsets**
* Explicitly captures conduction-band and valence-band barriers
* Shows excellent agreement with published reference data

**Best suited for:**
Realistic heterojunctions and device-grade simulations


### 3️ Shockley–Read–Hall (SRH) Recombination

* Included in all domains to model trap-assisted recombination
* Influences carrier lifetime, leakage current, and I–V slope
* Adds numerical stiffness, making solver configuration critical



## Key Results

* **Thermionic emission model** closely matches literature-reported I–V curves
* Carrier dominance depends on **band alignment**, not just doping
* Energy band diagrams clearly show:

  * Conduction-band barriers → electron-dominated transport
  * Valence-band barriers → hole-dominated transport
* Proper solver strategies (scaling, continuation, equilibrium initialization) are essential for convergence



## Numerical Techniques Used

To handle the highly nonlinear semiconductor equations:

* Manual scaling of carrier density variables
* Continuation (ramping) of doping and thermionic current
* Reuse of equilibrium solutions as initial conditions
* Tight solver tolerances for accurate current extraction

These techniques are critical for **robust TCAD simulations**.





## Reference

K. Horio and H. Yanai,
**“Numerical Modeling of Heterojunctions Including the Thermionic Emission Mechanism at the Heterojunction Interface,”**
*IEEE Transactions on Electron Devices*, vol. 37, no. 4, pp. 1093–1098, 1990.

---

##  Relevance & Applications

This work is directly relevant to:

* Semiconductor device modeling (TCAD)
* Photonics and optoelectronics
* Silicon photonics interface studies
* III–V / CMOS integration
* Graduate-level device physics education



## 📬 Author

**Som Mudgil**
ECE Undergraduate | Device Modeling | Photonics | TCAD



