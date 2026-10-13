# Consistency validation

The Omnibenchmark modules preserve the benchmark algorithms while adapting
file handling to the standard module interface. Published labels are treated as
references, and metric names follow the current methodology without legacy
tier terminology.

Validated properties:

- all method and metric repositories are pinned to immutable Git commits;
- the plan and environment files parse as YAML;
- module entrypoints expose the Omnibenchmark `--output_dir` and `--name`
  contract;
- assignment outputs remain `assignments.csv` plus `monitoring.json`;
- metric aggregation produces separate main and supplementary tables;
- the vendored fishash 0.99.0 implementation reproduces the installed 0.99.0
  package exactly for assignment matrix, log-p values and assignment labels;
- the concise fishash R 4.5.3 Conda environment resolves successfully from
  public channels.

Full data execution still requires the explicit local inputs declared by the
data stage. Those input paths are intentionally outside the scope of this
software-structure validation.
