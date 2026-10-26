# Heterogeneous LLM-Based Multi-Agent Worm Evaluation

## Overview

This repository contains selected experiment and analysis scripts, together
with aggregated CSV results for research into worm propagation behaviour
across heterogeneous LLM-based multi-agent configurations.

## Contents

- `trial_runner_1950.py` — Phase II trial runner.
- `full_trial_runner.py` — full experiment runner.
- `analyze_1950.py` — analysis and metric calculation script.
- `results/` — aggregated results tables supplied with the project.

## Results

The `results/` directory contains Phase I and Phase II per-model metrics,
attack-vector comparisons, security-score tables, summary metrics, and a
derived Phase I–Phase II model comparison.

See `RESULTS_README.md` for details about the CSV files and their provenance.

## Reproducibility and limitations

The published tables should be interpreted according to the methodology
and metric definitions documented in the accompanying research paper.
The aggregated results have not necessarily been independently recalculated
from every trial-level record.

## Security

This repository intentionally excludes raw payloads, command-and-control
scripts, agent memories, and raw trial logs from the initial release.
