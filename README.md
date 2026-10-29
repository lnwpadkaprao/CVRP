# CVRP Hybrid Solver

A Python implementation of a heuristic solver for the **Capacitated Vehicle Routing Problem (CVRP)**, combining randomized multi-start construction with **Adaptive Large Neighborhood Search (ALNS)** and optional **Held–Karp exact TSP optimization** for small individual routes.

## Overview

The solver seeks short routes serving customers while respecting vehicle capacity constraints. Its approach includes:

- **Initial solution exploration:** randomized nearest neighbor, noisy Clarke–Wright savings, and randomized sweep constructions.
- **Local improvement:** neighborhood search applied to candidate routes.
- **Elite solution pool:** keeps structurally distinct promising solutions.
- **ALNS refinement:** adaptive destroy-and-repair iterations to improve selected candidates.
- **Route-level exact check:** Held–Karp optimization for eligible routes of up to 12 customers by default. This **does not** prove global optimality of the CVRP solution.

## Repository structure

```text
CVRP-Hybrid-Solver/
├── cvrp_final.py          # Main solver
├── instances/             # CVRP benchmark input files (.vrp)
│   ├── A-n32-k5.vrp
│   ├── B-n31-k5.vrp
│   ├── P-n40-k5.vrp
│   └── Self Case_VVV.vrp
├── results/               # Saved solver output logs
│   ├── A-n32-k5_result.txt
│   ├── B-n31-k5_result.txt
│   ├── P-n40-k5_result.txt
│   └── Self Case_VVV_result.txt
├── README.md
└── .gitignore
```

## Requirements

- Python 3
- No third-party packages are required for the core solver (Python standard library).

## Run locally

From the repository root:

```bash
python cvrp_final.py instances/A-n32-k5.vrp --seed 42
python cvrp_final.py instances/B-n31-k5.vrp --seed 42
python cvrp_final.py instances/P-n40-k5.vrp --seed 42
```

You can also run the solver in Google Colab after uploading `cvrp_final.py` and an instance file:

```python
%run /content/cvrp_final.py /content/A-n32-k5.vrp --seed 42
```

## Benchmark and reproducibility

The `results/` directory contains saved output logs provided with the original project. The original package documents runs using `--seed 42` and default settings of 60 restarts, 3 elite solutions, and an ALNS budget of 6,000 iterations. These logs are **supplied results**, not independently revalidated here; runtime may differ by machine and environment.

## Notes and limitations

- The solver uses heuristic search, so it does not guarantee a globally optimal CVRP solution.
- Held–Karp checks route ordering for small routes, not the globally optimal assignment of customers to vehicles.
- The original Python solver and benchmark inputs/results are preserved without changes in this GitHub-ready package.
- The supplied source contains its own additional usage and configuration notes.

## Project purpose

A programming and operations-research portfolio project demonstrating combinatorial optimization, heuristic search, reproducible experiments, and evaluation on CVRP instances.
