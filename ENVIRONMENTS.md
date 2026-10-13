# Environment policy

- The benchmark uses Omnibenchmark's native `conda` software backend.
- Versioned YAML files under `envs/` are the environment source of truth.
- Publicly packaged dependencies come from `conda-forge` and `bioconda`.
- Exact Git-only method revisions are archived with their owning module and
  loaded from that module; runtime network and personal libraries are not
  required.
- Method implementation and environment declaration remain separate: module
  repositories own executable method code, while the benchmark plan selects
  the matching Conda environment.
- Input dataset paths are intentionally outside this policy and remain the only
  machine-local part pending a separate data-distribution decision.
