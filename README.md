# MTB Suspension Kinematics + AI Optimizer

**A browser-based four-bar suspension solver with a Mistral-API optimization loop.** The signature pattern: **the LLM proposes geometry, a local search refines it, and a deterministic physics solver validates every iteration as ground truth.**

> *LLM proposes → local search refines → simulation validates.*

---

## ▶ Demo

[![Watch the Demo](https://img.shields.io/badge/Demo-Watch%20on%20Loom-625df5?style=for-the-badge&logo=loom)](https://www.loom.com/share/7ca6e38c9535469b9913d11837b9e364)

**[Try it live ➔](https://mtb-suspension-calculator-ai-optimi.vercel.app/)** *Note: The deployment is password protected — password available on request.*

![Solver + optimizer screenshot](docs/screenshot.png)

---

## What it is

A from-scratch reimplementation of the core of the commercial tool **Linkage X3**: a single-degree-of-freedom **Horst-link four-bar** solved through the full suspension travel, producing the curves a frame engineer actually cares about:

* **Leverage ratio** & progression
* **Anti-squat** (with chain-line / instant-force-centre construction) and **anti-rise**
* **Pedal kickback** / chain growth
* **Axle path** and the live **instantaneous centre** over travel

Coordinate system: origin at the bottom bracket, +x forward, +y up, all lengths in mm. The linkage is driven by the **rocker angle** (a monotone input that avoids dead points), and each step solves the four-bar by circle–circle intersection, then derives the axle, instant centre, anti-squat / anti-rise and the rest.

## The AI × physics loop

A geometry **optimizer** sits on top of the solver. You give it target curves (e.g. *anti-squat at sag = 100 %, leverage progression = 25 %*) and it closes the loop:
