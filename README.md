# GHK Simulator

An interactive, browser-based calculator for the Goldman-Hodgkin-Katz (GHK) equations, built as a single self-contained HTML file.

## What it does

The GHK equation predicts the membrane potential (Vm) of a cell from ionic concentrations and relative permeabilities. This tool makes it interactive — enter values, pick what to solve for, and get results instantly with charts and Nernst potential breakdowns.

## Tabs

| Tab | Description |
|-----|-------------|
| **GHK 2-Ion** | Classic K⁺/Na⁺ equation. Solve for Vm or back-calculate any unknown (concentration, permeability, or ratio). |
| **GHK 3-Ion** | Adds Cl⁻ (z = −1). Covers GABA-A receptor effects and shunting inhibition scenarios. |
| **GHK 4-Ion** | Adds Ca²⁺ (z = +2). Because the equation becomes implicit with divalent ions, Vm is solved numerically via bisection. |
| **P Ratio Solver** | Given a measured Vm and concentrations, back-calculates permeability ratios. Five modes: analytical 2-ion, numerical 3-ion/4-ion, full ratio matrix, and ratio-vs-Vm sweep curve. |
| **Sweep** | Sweeps any single parameter over a range and plots Vm. Supports multiple overlay curves, linear/log axes, PNG export, and CSV download. |
| **Batch** | Run GHK on many parameter sets at once. Three input modes: manual table, CSV paste, and auto-grid (2-variable factorial with heatmap output). |

## Features

- **Solve for anything** — every tab lets you pick the unknown and provide the target value; the tool inverts the equation analytically or numerically
- **Live equation substitution** — shows the actual numbers plugged into the formula after each calculation
- **Nernst potentials & driving forces** — displayed for each ion with inward/outward direction
- **Physiological presets** — one-click defaults for mammalian neurons (37 °C)
- **Global temperature control** — adjustable in the top bar; RT/F updates everywhere in real time
- **Charts** — bar, pie, scatter, heatmap, and I-V curves via Chart.js; all exportable as PNG
- **CSV export** — sweep and batch results downloadable as CSV
- **Responsive layout** — works on mobile (single-column below 900 px)
- **Zero dependencies** — Chart.js loaded from CDN; everything else is vanilla JS/HTML/CSS

## Running locally

```bash
# No build step needed — just open the file
open ghk-simulation/index.html
```

Or serve it:

```bash
npx serve ghk-simulation
# → http://localhost:3000
```

## Deployment

The project is configured for Vercel. `vercel.json` sets `ghk-simulation/` as the output directory.

```bash
vercel deploy
```

## Background

The GHK voltage equation (Goldman 1943; Hodgkin & Katz 1949) predicts membrane potential under the constant-field assumption:

```
Vm = (RT/F) · ln[ (P_K·[K⁺]ₒ + P_Na·[Na⁺]ₒ + P_Cl·[Cl⁻]ᵢ) /
                  (P_K·[K⁺]ᵢ + P_Na·[Na⁺]ᵢ + P_Cl·[Cl⁻]ₒ) ]
```

At rest, P_K ≫ P_Na, so Vm sits near E_K (≈ −90 mV). During an action potential, Na⁺ channels open, P_Na dominates, and Vm swings toward E_Na (≈ +67 mV).
