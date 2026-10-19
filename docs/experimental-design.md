# Preliminary Experimental Design

**Status:** Initial proposal. Scenes, final configurations, and environment
feasibility remain pending. This document reports no experimental results.

## Objective and motivation

Compare PBRT v3 CPU rendering time across eight candidate execution conditions
and study the effects of environment, scene, and accelerator (`kdtree` or
`bvh`). In particular, evaluate Docker against direct execution in the
corresponding Linux environments and explicitly investigate whether invoking
Docker from Windows through Docker Desktop differs from invoking it in a WSL2
terminal.

The planned host is a Windows 10 computer with an AMD Ryzen 7 5700X and 16 GB
of RAM; no GPU will be used. Confirm the actual hardware and virtualization
availability before configuring any environment. All viable conditions must
use the same physical machine.

## Research questions

- **RQ1.** Are there differences in PBRT execution time among native Windows,
  native Linux, Linux in a VM, and WSL2?
- **RQ2.** How does performance differ between `kdtree` and `bvh`, and does
  that difference depend on the scene or environment?
- **RQ3.** What is the effect of running PBRT in Docker compared with running
  it directly in the corresponding Linux environment?
- **RQ4.** How does the effect of Docker differ among native Linux, the Linux
  VM, and WSL2?
- **RQ5.** Does the environment from which Docker is invoked—Windows through
  Docker Desktop or WSL2 through a Linux terminal—affect PBRT performance when
  the backend, image, resources, and files are equivalent?

RQ5 supports attribution to the invocation or access mechanism only if the
components actually shared between conditions are verified. A difference must
not be attributed to the backend if the backend did not change.

## Candidate factors and levels

| Factor | Preliminary levels | Status |
|---|---|---|
| Execution environment | Eight conditions listed in [environment-configurations.md](environment-configurations.md) | Feasibility pending |
| Scene | Four scenes from the official PBRT repository, not yet selected | Pending; meet the course duration requirements |
| Accelerator | `kdtree`, `bvh` | Required for every scene |
| Repetition | At least five per combination | Required; adequacy must be justified |

The candidate design is factorial: each scene and accelerator will be run in
each technically viable condition. The eight environments are not considered
confirmed or necessarily independent before technical characterization.

## Response variables

**Primary:** PBRT execution time in seconds. Before the official experiment,
the protocol must specify a consistent measurement method, including exact
start and stop boundaries and how scene preparation is handled.

**Candidate secondary responses, subject to feasibility:** peak memory usage,
CPU utilization, scene preparation time, and exit code/execution status. These
are not definitive requirements until a comparable measurement method has
been defined for all environments.

## Preliminary hypotheses

For RQ5:

- **H0:** There is no systematic difference in execution time between
  conditions 7 and 8 under equivalent configurations.
- **H1:** There is a difference in execution time between conditions 7 and 8.

Failure to achieve statistical significance does not demonstrate equivalence.
A claim of practical equivalence would require a justified equivalence margin
defined in advance and an appropriate statistical procedure.

For RQ1–RQ4, compare factor effects and relevant interactions (especially
environment × accelerator, environment × scene, and Docker × environment).
Expected directions and magnitudes are not assumed; they must be specified
before analyzing official results.

## Provisional number of runs

With eight conditions, four scenes, two accelerators, and five repetitions:

**N = 8 × 4 × 2 × 5 = 320 official runs.**

A run is one individual PBRT execution for a specific condition, scene, and
accelerator combination. This count excludes pilot runs, installations, and
compilations; it does not guarantee that five repetitions are sufficient and
depends on validating all conditions. If a condition is infeasible or cannot
be distinguished through a reproducible intervention, document the issue and
explicitly revise the design; do not silently alter the total.

## Pilot, sample size, and analysis

The pilot is intended to validate the technical workflow, candidate scenes,
time measurement, resource logging, and observed variability. Label and store
pilot runs separately from official runs. Do not count them as official
repetitions.

Five repetitions are the course minimum, not a statistical justification of
adequacy. Before fixing the final number, estimate variability from the pilot
and justify sample size based on the effect of interest and an appropriate
method. Document assumptions and the decision before official runs begin.

Final analysis is outside the scope of this phase. It must check the assumptions
of the selected method, including independence, residual distribution, and
variance homogeneity where applicable. If a transformation (for example, a
log transformation) is used, justify it and explain its interpretive
implications. Account for repeated measurements on the same machine and
temporal or session blocks when selecting a model.

## Controls, randomization, and sources of noise

Keep the physical hardware, scenes and their files, PBRT version, arguments
(except the factor under study), resource policy, and measurement method
constant. Record operating system, versions, CPU and memory limits, VM/Docker
configuration, backend, storage, and file-access mechanism.

Randomize the order of official runs using a procedure with a recorded seed.
If technical constraints require blocks (for example, by session or active
environment), record the block and randomize within it. Control and record
concurrent workloads, temperature/thermal state if measured comparably,
background processes, power settings, and any relevant restart or
configuration change.

## Assumptions and threats to validity

- **Treatment comparability:** Conditions may differ in operating system,
  virtualization, backend, file access, or resource limits. Record the
  effective architecture before interpreting contrasts.
- **Internal validity:** Host load, warm-up, caches, run order, and thermal
  changes may confound execution times.
- **Measurement validity:** Clocks, measurement boundaries, and resource
  metrics must be consistent across systems.
- **Construct validity:** CPU rendering time is the primary response but does
  not, by itself, represent every dimension of performance.
- **External validity:** Using one physical machine limits generalization to
  other processors, memory configurations, operating-system versions, and
  devices.
- **Power and multiplicity:** Five repetitions may be insufficient; multiple
  scenes, factors, and contrasts increase inferential complexity.
- **Scene resources:** File sizes and access paths may affect time; use the
  same verified copy for comparisons.

## Open decisions

1. Confirm the hardware model, virtualization status, and actual system
   configuration without changing it during this phase.
2. Select four official scenes and verify their durations and resource
   requirements in the pilot; minimum durations apply under final experimental
   conditions.
3. Validate PBRT v3, compiler, OS, VM, WSL2, Docker, and backend versions.
4. Define comparable CPU/memory allocation and data location/path.
5. Characterize conditions 7 and 8 to identify the actual invocation or access
   variable that differs.
6. Operationally define the primary time measurement, feasible secondary
   responses, and run-log format.
7. Set validity, final repetition, analysis, and exclusion procedures based on
   pilot evidence.
8. Document how to obtain and verify the integrity of resources too large to
   version in Git; do not upload them automatically.
