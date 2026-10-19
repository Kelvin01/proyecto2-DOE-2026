# Preliminary Experimental Protocol

**Status:** Planning document. Do not install software or conduct official
experiments based solely on this draft. Conditions, scenes, measurement
procedures, and final criteria require validation.

## 1. Hardware and software preparation

1. Confirm the physical machine and record its CPU, memory, host, and
   virtualization status. Check virtualization before planning a VM, WSL2, or
   Docker Desktop.
2. Review the feasibility and dependencies of all eight candidate conditions.
   Do not modify BIOS, Windows, partitions, or machine settings without
   authorization.
3. After environment decisions are approved, record the OS and version, PBRT
   v3 and build provenance/version, compiler if applicable, hypervisor, WSL2
   distribution, Docker engine, backend, and image.
4. Document configured and effective CPU and memory limits; record concurrent
   processes, power policy, and any configuration that may affect performance.
5. Do not download, compile, or install software as part of the current phase.
   Any later installation requires review and authorization.

## 2. Run logging

Assign each run a unique identifier and record at least:

- date and time, pilot/official label, repetition number, and block or session;
- environment condition, scene, and accelerator configuration;
- exact command, arguments, working directory, and exit code;
- relevant versions, image/digest, and allocated resources;
- paths, locations, and integrity verification for scenes and other data;
- execution time in seconds, measurement method, and start/stop timestamps;
- secondary metrics only if their measurement is consistent and defined in
  advance;
- status, relevant messages, errors, interruptions, concurrent workload, and
  protocol deviations.

Before official runs, define whether the measured time includes initialization,
scene loading, or preparation, and how the timer is started and stopped. Apply
the same rule in every environment. Do not combine preparation time with the
primary response if it cannot be measured consistently.

## 3. Scenes and accelerators

Select four scenes from the official PBRT v3 repository during pilot
validation. Verify each scene's provenance, integrity, dependencies, and
rendering options. Do not finalize scenes until their timing has been
evaluated under the final conditions: none may take less than five minutes,
and at least one must take around 30 minutes or longer.

For each scene, verify how to configure `kdtree` and `bvh`, record the exact
argument/configuration, and confirm PBRT uses the requested setting. Keep all
other rendering parameters constant unless they are an explicit part of the
design.

If a scene or resource is too large for Git, document reproducible retrieval
instructions and an integrity check before using it. Do not upload large
resources automatically.

## 4. Pilot

Conduct the pilot only after authorization and technical validation of the
environments. Use it to test commands, scene access, time and resource capture,
exit status, the run log, and measurement variability. Confirm that both
accelerator configurations are applied.

Label and store pilot runs separately. Do not include them in the provisional
320 official runs. Document failures and corrections, and review the design
before finalizing scenes, procedures, and sample size.

## 5. Run order and official execution

After approval of the final design, generate a randomized order for condition,
scene, and accelerator combinations and repetitions. Record the procedure and
seed. If environment changes prevent global randomization, define blocks (for
example, by session or active environment) and randomize within each block,
recording the reason.

The planned minimum is five repetitions per combination. Approve the final
sample size only after justifying its adequacy based on pilot variability and
the effect of interest; five repetitions alone do not guarantee adequate
power.

Run all conditions on the same physical machine. Avoid workloads unrelated to
the protocol and record every exception, restart, interruption, or system
change. Apply the same start, stop, and recovery rules to each treatment.

## 6. Validity, exclusions, and reruns

Before official runs, define and version validity and exclusion criteria
without introducing unjustified numerical thresholds. At a minimum, verify
that a run matches its planned combination, completed execution, produced the
expected code/status, and has enough information to determine its time and
configuration.

Do not delete failed, interrupted, misconfigured, or incomplete runs. Preserve
their records, mark their status and reason, document any exclusion decision,
and link every rerun to its original. Do not exclude values as outliers without
predefined criteria and documented evidence. Distinguish technical failures
from unusual but valid results.

## 7. Preservation and traceability

Keep original data immutable in `data/raw/` and run logs in `logs/`; store
derived data in `data/processed/` with instructions to regenerate it. Do not
replace original records with corrected versions. Record methodological and
configuration changes with their rationale and maintain traceability through
GitLab. Review changes before commits; do not create commits or pushes
automatically.

## 8. Decisions required before official execution

- Feasibility of each condition and the actual architecture of conditions 7
  and 8.
- Selection of four scenes and verification of duration and resources.
- Versions, commands, rendering parameters, and `kdtree`/`bvh` configuration.
- Operational definition of execution time and measurement method.
- Run-log format, identifiers, and feasible secondary metrics.
- Resource limits and file locations/access.
- Randomization, blocking, and noise-control procedure.
- Validity/exclusion criteria and rerun procedure.
- Sample-size justification and statistical analysis plan.
