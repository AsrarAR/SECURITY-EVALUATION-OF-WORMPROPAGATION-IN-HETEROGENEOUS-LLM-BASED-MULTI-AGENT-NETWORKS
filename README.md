# Security Evaluation of Worm Propagation in Heterogeneous LLM-Based Multi-Agent Networks

**Research focus:** Security evaluation of self-propagating behaviour in heterogeneous large language model (LLM)-based multi-agent systems.

## Overview

LLM-based agents are increasingly deployed in environments where they can interact with other agents, consume external information, use tools, and maintain persistent state. Although these capabilities enable complex workflows, they also introduce security questions around trust boundaries, persistent instructions, tool-mediated execution, and interactions between agents using different language models.

This project investigates the security implications of worm-like propagation behaviour in heterogeneous LLM-based multi-agent networks. It focuses on evaluating how observed behaviours vary across agent configurations and models, and on measuring outcomes using a structured, multi-phase experimental methodology.

The project separates initial attack-vector evaluation from subsequent chain-level evaluation. Phase I results are used to inform the selection of an attack-vector and payload combination for Phase II. The Phase II dataset is summarised in the supplied results tables as containing 1,950 trials across 38 configurations.

The objective is to support systematic security evaluation, transparent reporting, and further research into the risks associated with interconnected LLM agents.

## Research Objectives

The project is organised around the following objectives:

1. **Evaluate heterogeneous configurations:** Examine how measured outcomes vary across configurations involving different LLM-based agents.
2. **Measure multiple stages of behaviour:** Distinguish persistence, execution, and propagation outcomes rather than treating them as a single success condition.
3. **Compare experimental configurations:** Aggregate trial-level observations into configuration-level and model-level metrics.
4. **Characterise stopping behaviour and latency:** Examine where observed chains stop and how long measured interactions take.
5. **Support reproducible analysis:** Preserve analysis code, metric summaries, and structured CSV outputs so that reported findings can be inspected and independently evaluated.

These objectives describe the intended evaluation scope; they should not be interpreted as claims that every security property has been established or that all results generalise to other agent platforms.

## Experimental Methodology

### Phase I: Attack-Vector Evaluation

Phase I compares candidate attack-vector and payload combinations using measured outcomes from the initial experiments.

According to the supplied Phase II summary, the selected combination was **VE + P1**, described in the source data as *Indirect Tool Injection + Minimal Payload*. The summary states that this combination was selected based on the highest reported φ₁ gain at the lowest payload severity.

The underlying experimental records and selection calculations should be consulted when independently verifying this selection.

### Phase II: Chain-Level Evaluation

Phase II evaluates selected behaviour across multi-agent chains. The supplied summary describes the following experimental scope:

- **Reported trial count:** 1,950
- **Reported configurations:** 38
- **Configuration breakdown:** 5 homogeneous and 33 heterogeneous
- **Chain length:** Varies by experimental configuration; see the corresponding trial records.
- **Selected attack-vector and payload combination:** VE + P1

These figures are reproduced from the supplied summary CSV and have not been independently recalculated from all trial-level records as part of this repository release.

### Evaluation Stages

The analysis uses three phase indicators:

| Indicator | Interpretation in this project |
|---|---|
| φ₁ | Persistence |
| φ₂ | Execution |
| φ₃ | Propagation |

The indicators represent distinct observed outcomes in the experimental framework. Their exact operational definitions, success criteria, and measurement limitations should be interpreted alongside the experiment implementation and research paper.

## Repository Structure

```text
.
├── README.md
├── RESULTS_README.md
├── analyze_1950.py
└── results/
    ├── attack_vectors.csv
    ├── model_comparison_phase1_phase2.csv
    ├── phase1_per_model.csv
    ├── phase2_per_model.csv
    ├── secure_scores.csv
    └── summary_metrics.csv
```

The repository intentionally contains a limited public release. Experiment runners, agent workspaces, raw payloads, command-and-control scripts, and raw trial logs are not included in this initial version.

## Results and Data

The `results/` directory contains six CSV files.

| File | Purpose |
|---|---|
| `attack_vectors.csv` | Phase I attack-vector comparison |
| `phase1_per_model.csv` | Supplied Phase I per-model metrics |
| `phase2_per_model.csv` | Supplied Phase II per-model metrics |
| `secure_scores.csv` | Supplied security-score ranking and recommended roles |
| `summary_metrics.csv` | Reported overall metrics and experimental metadata |
| `model_comparison_phase1_phase2.csv` | Derived comparison joining the supplied phase tables by model |

The Phase I and Phase II CSVs preserve the supplied source values. The combined comparison is a derived table; it joins records by model and does not independently recalculate the underlying metrics.

### Reported Summary Metrics

The supplied `summary_metrics.csv` reports:

| Metric | Reported value |
|---|---:|
| Phase II overall ASR | 48.4% |
| R₀-style measure | 1.453 |
| Heterogeneity Impact Score (HIS) | −5.22% |
| Phase II trial count | 1,950 |
| Configuration count | 38 |
| Chain length | Varies by experimental configuration; see the corresponding trial records. |

These are reported values from the supplied results, not independently verified findings in this repository release.

## Metrics and Interpretation

The analysis script calculates configuration-level and model-level summaries, latency, stopping rates, a composite security score, a heterogeneity-related latency comparison, and an R₀-style measure.

Metric names and values must be interpreted in the context of their formulas and experimental definitions.

In particular:

- **ASR:** The precise aggregation level and denominator should be checked against the analysis implementation and paper.
- **φ₁, φ₂, and φ₃:** These measure distinct stages and should not be treated as interchangeable outcomes.
- **Stopping rate:** Its interpretation depends on the implementation's stopping criteria.
- **Security score:** A composite score depends on its component metrics, normalisation procedure, and weights. It should not be interpreted as a universal measure of model security.
- **HIS:** The sign and magnitude depend on the comparison groups and latency aggregation method.
- **R₀-style measure:** The supplied summary defines this as three times the average ASR expressed as a proportion. This project-specific calculation should not automatically be interpreted as a validated epidemiological reproduction number or evidence of an epidemic regime.

Independent reproduction requires checking the metric definitions, denominators, missing-data handling, trial exclusions, and aggregation rules against the final experiment records.

## Analysis

The public analysis entry point is:

```bash
python3 analyze_1950.py path/to/trials.csv
```

The script expects a CSV compatible with the schema used by the experiment runner. It reads trial-level records, groups observations by configuration and trial, computes summaries, and writes a text report to the configured results directory.

**Important:** The current script uses a project-specific default path under `~/LLM-Worm-Research/results_1950`. The raw trial dataset and experiment runners are not included in this public release, so the command above is illustrative rather than a guarantee of immediate end-to-end reproduction. The input schema, output directory, and dependencies should be checked before attempting to reproduce the reported tables.

## Reproducibility

The repository provides analysis code and aggregated results, but it does not currently contain every artefact required to reproduce the complete experiments from scratch.

A full reproduction would require access to the relevant trial-level data, a compatible experimental environment, model and agent configuration details, the precise metric definitions, and the versioned dependencies used during evaluation.

For reliable comparison, researchers should record:

- Model names and versions
- Agent configuration and chain topology
- Trial counts and exclusion criteria
- Exact success criteria for each phase
- Latency measurement boundaries
- Aggregation formulas and denominators
- Software dependencies and environment details

The aggregated CSVs should be treated as supplied research outputs until they have been reconciled against the canonical trial records.

## Security and Responsible Research

This repository concerns security risks in LLM-based agent systems. The initial public release is deliberately limited to analysis code, documentation, and aggregated results.

Raw payloads, agent memory files, operational command-and-control scripts, and experimental execution runners are excluded from this release.

Research involving agent propagation should be performed only in isolated, authorised test environments. Results should be reported with sufficient methodological detail to support scrutiny without unnecessarily exposing operational artefacts that could enable misuse.

## Limitations

The current release has several limitations:

- Trial-level source records are not included.
- The aggregated metrics have not all been independently recalculated.
- The combined Phase I–Phase II comparison is derived from the supplied tables.
- The complete experiment execution environment is not provided.
- Metric validity and generalisability depend on the experimental design, model versions, configuration choices, and success criteria.

These limitations should be considered when interpreting the reported comparisons or drawing conclusions about real-world agent ecosystems.

## Future Work

Potential next steps include independent verification of all aggregated metrics, improved experiment documentation, sensitivity analysis for composite metrics, expanded evaluation across model and agent configurations, and the development of safer, reproducible simulation-based test harnesses.

## Citation

If you use this repository in academic work, cite the associated research paper once its bibliographic details are finalised.

Until then, please refer to the repository URL and identify the specific version or commit used.

## Licence

No licence has been specified in this initial release. Reuse and redistribution permissions should be established before the repository is treated as an openly licensed research artefact.
