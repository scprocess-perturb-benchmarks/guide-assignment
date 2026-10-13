# guide-assignment

Omnibenchmark for Perturb-seq **guide assignment**: assignment configurations
evaluated by reference agreement, transcriptomic agreement, discovery,
computational-resource and supplementary analyses.

```
data ─► guide_assignment ─► metrics_reference / metrics_gex / metrics_discovery
│                              + metrics_resources / metrics_supplementary
│                              + cross-method collectors and aggregation
└── data.difficulty_table (per-cell, method-independent)
```

## Repositories

| Repo | Role |
|---|---|
| [guide-assignment](https://github.com/tmp-perturb/guide-assignment) | benchmark plan + docs |
| [guide-assignment-data](https://github.com/tmp-perturb/guide-assignment-data) | data importer + difficulty table |
| [guide-assignment-pgmm](https://github.com/tmp-perturb/guide-assignment-pgmm) | PGMM-EM |
| [guide-assignment-umi](https://github.com/tmp-perturb/guide-assignment-umi) | UMI threshold |
| [guide-assignment-crispat](https://github.com/tmp-perturb/guide-assignment-crispat) | crispat |
| [guide-assignment-fishash](https://github.com/tmp-perturb/guide-assignment-fishash) | fishash (R) |
| [guide-assignment-metrics](https://github.com/tmp-perturb/guide-assignment-metrics) | metrics + difficulty + collectors |

## Software environments

The benchmark uses the native Omnibenchmark `conda` backend. Environment YAML
files are versioned under `envs/` and selected through `software_environment`.
Method repositories contain their execution code; no external `project_root` or
personal software library is required. The fishash module vendors the exact
benchmarked fishash 0.99.0 runtime source, and its concise Conda file declares
the required R/Bioconductor packages.

## Run

```bash
ob validate plan benchmark.yaml
ob run benchmark.yaml --cores N
```

## Methods & metrics

See `METHODS.md`. Method selection is by module + `parameters`; metric selection is
by the `--metric` parameter value.
