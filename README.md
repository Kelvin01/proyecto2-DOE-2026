# Project MP-6104 — Experimental Design

Project for MP-6104 Design of Experiments in the Master's Program in Computer
Science at the Costa Rica Institute of Technology (TEC). The study will
investigate the CPU rendering performance of PBRT v3 for image synthesis.

## Objective

Compare eight candidate execution conditions, study the effects of the `kdtree`
and `bvh` accelerators across four scenes from the official PBRT repository, and
evaluate the impact of Docker. This includes two candidate ways of invoking
Docker from Windows and WSL2. Comparisons will use the same physical hardware,
subject to technical validation of each condition.

## Course context

The design must meet the MP-6104 requirements: four scenes, at least five
repetitions per combination, scenes that take at least five minutes under the
final experimental conditions and at least one scene taking around 30 minutes
or longer, a reproducible run log, and a justification of sample-size
adequacy. The paper will be written in English using LaTeX and the IEEE
Transactions template.

## Key requirements

- PBRT v3 and the `kdtree` and `bvh` accelerators.
- Eight candidate conditions, all pending technical validation.
- PBRT execution time in seconds as the primary response variable.
- Reproducible recording of versions, configurations, results, and errors.
- Change traceability through GitLab; contributors, not this assistant, will
  create commits and pushes.
- No official experimental results exist at this stage.

## Repository structure

```text
.
├── AGENTS.md
├── README.md
├── analysis/
├── configs/
├── data/
│   ├── processed/
│   └── raw/
├── docker/
├── docs/
├── figures/
├── logs/
├── paper/
└── scripts/
```

The scope and preliminary protocol are described in
[`docs/experimental-design.md`](docs/experimental-design.md),
[`docs/environment-configurations.md`](docs/environment-configurations.md),
and [`docs/protocol.md`](docs/protocol.md).

## Status

**Preliminary design; execution environments and configurations have not yet
been validated.** No scenes have been selected, no pilot has been run, and no
official results are available. The provisional total of 320 official runs
depends on validation of the design.

## Getting started for collaborators

1. Review `AGENTS.md` and the three documents in `docs/`.
2. Before installing software or changing system settings, validate and agree
   on the technical requirements and the protocol's open decisions.
3. Document versions, configurations, and methodological changes; preserve
   original data and log failed runs as well.
4. Use GitLab to maintain project traceability. Review changes before creating
   commits; commits and pushes are not performed automatically.

Do not download, install, or compile software, or start experimental runs, as
part of this repository-setup phase.
