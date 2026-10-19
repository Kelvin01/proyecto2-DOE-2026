# Candidate Execution Environments

**Status:** No condition is declared installed or validated. Virtualization,
WSL2, a Linux distribution, Docker, Docker Desktop, and PBRT have not been
verified. Technical feasibility will be determined through an authorized
review and pilot; this document does not initiate installations.

## Common hardware and logging

The planned machine is Windows 10 with an AMD Ryzen 7 5700X and 16 GB of RAM;
no GPU will be used. Confirm the actual inventory before beginning the study.
All comparisons will run on the same physical hardware.

For each run or group of runs, record the host and OS, PBRT version and build,
guest OS version if applicable, Docker engine and version, effective backend,
image and identifier/digest, command and invocation method, CPU and memory
limits, VM resource policy, file paths and locations, storage type, and
input/output configuration. Also record configuration changes and verify which
components are shared between treatments.

The capabilities and constraints below are items to verify, not claims that
the software is installed or available on the machine.

## Candidate treatments

| # | Condition | Host / execution OS | Virtualization, WSL2, or Docker | Resources and files | Status and risks |
|---|---|---|---|---|---|
| 1 | Native PBRT on Windows, without Docker | Physical Windows machine / Windows | None | Use the same hardware; record CPU, memory, scene location, and paths | Pending; verify PBRT v3 availability and compatibility on Windows |
| 2 | Native PBRT on Linux installed directly on the hardware, without Docker | Same physical machine / Linux booted directly | No VM or container; may require an alternative boot configuration to Windows | Record effective CPU/memory allocation and storage/path | Pending; verify a safe, reproducible approach. Do not install or modify partitions during this phase |
| 3 | PBRT on Linux in a VM on Windows, without Docker | Physical Windows machine / Linux guest | VM on the Windows host | Record hypervisor, allocated CPU and RAM, virtual storage, and scene location | Pending; verify virtualization is enabled and resources are available. VM overhead and virtual disk can confound results |
| 4 | PBRT directly in WSL2, without Docker | Physical Windows machine / Linux distribution under WSL2 | WSL2, without Docker for PBRT execution | Record distribution/version, resource limits, Linux or Windows-mounted paths, and filesystem | Pending; verify WSL2 and distribution. Cross-system file access may affect time |
| 5 | PBRT in Docker on native Linux | Same physical machine / Linux | Docker engine running on Linux; Linux container | Record engine/backend, image, container limits, and paths/mounts | Pending; depends on validating condition 2 and the engine. Compare with native Linux using equivalent resources and files |
| 6 | PBRT in Docker inside the Linux VM | Physical Windows machine / Linux guest | Linux VM and Docker engine in the guest | Record hypervisor, VM resources, engine/backend, container resources, storage, and mounts | Pending; depends on VM and Docker. Do not assume nested virtualization; verify the effective architecture |
| 7 | PBRT in Docker, invoked from a WSL2 terminal | Physical Windows machine / WSL2 and Linux container | Invocation from a WSL2 Linux terminal; record effective engine and backend | Record image, resource limits, Linux/mounted paths, and access to engine and files | Explicit candidate treatment; characterization pending. It may share an engine/backend with condition 8 |
| 8 | PBRT in Docker Desktop, invoked from Windows through PowerShell using a Linux container | Physical Windows machine / Linux container | Docker Desktop and backend to be verified; invocation from PowerShell | Record image, limits, mount type, Windows/shared paths, and Desktop resource settings | Explicit candidate treatment; characterization pending. Do not discard because it may share a backend with condition 7 |

## Interpreting conditions 7 and 8

Do not assume treatments 7 and 8 are independent environments or equivalent.
Before the pilot, identify and record the Docker engine, backend, their
versions, host, resource configuration, image, mounts and file locations, and
invocation path.

If both commands use exactly the same engine, backend, resources, image, and
files, the remaining intervention may be only the invocation or access
mechanism. In that case, describe RQ5 accordingly and do not attribute any
difference to the backend. Also assess whether differing paths or mounts offer
an alternative explanation.

If a reproducible intervention distinguishing the conditions cannot be
defined, document the issue and propose an explicit design revision. Do not
silently merge or remove treatments.

## Comparability requirements

- Run comparisons on the same physical machine and record any host restart or
  configuration change.
- Document configured and effective CPU and memory allocation for the host,
  VM, and container; do not assume configured values equal effective resources.
- Verify the same scenes and files are used in each treatment; record their
  location, filesystem, and access method.
- Separate the effect of running in Docker from storage, resources, backend,
  or build effects where the design allows.
- Keep all eight candidate conditions in the preliminary design until
  validation is complete.
