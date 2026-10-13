# Methods and metrics — guide assignment

This document describes the public Omnibenchmark implementation. The benchmark
uses published assignment labels as references and reports **reference
agreement**. Legacy tier terminology is not used.

## Assignment configurations

| Module | Configurations | Output ranking | Implementation |
|---|---|---|---|
| `pgmm` | MAP-EM (`map_e2`) | UMI count | Pinned Python module |
| `umi` | thresholds 3, 5 and 10 | UMI count | Pinned Python module |
| `crispat` | PGMM and 2-beta | native method score | Pinned Python module |
| `fishash` | GS-FDR 0.05, minimum count 2, refit 10 | log-p value | Vendored fishash 0.99.0 source at upstream commit `74220e8` |

All configurations consume the same MEX matrix, barcode and feature artifacts
for a dataset lineage. Each emits `assignments.csv` and `monitoring.json` through
the standard Omnibenchmark module interface.

## Metric stages

| Stage | Metric selector(s) | Purpose |
|---|---|---|
| `metrics_reference` | `reference_agreement`, `stratified_reference_agreement` | Cell- and label-level agreement with the published reference, including difficulty-stratified supplementary analysis |
| `metrics_gex` | `knockdown`, `stratified_knockdown` | Target-expression agreement and its difficulty-stratified supplementary analysis |
| `metrics_discovery` | `differential_expression_discovery` | Across-perturbation discovery analysis and supplementary false-positive diagnostics |
| `metrics_resources` | `method_resources` | Runtime and memory summaries under the fixed execution protocol |
| `metrics_supplementary` | `construct_set_agreement` | Construct-level reference agreement |

The pairwise collector computes Top-1 agreement between assignment
configurations. The aggregate collector emits separate main and supplementary
TSV and Parquet tables.

## Dataset semantics

The data module emits a dataset specification describing guide design, barcode
matching, lane collapsing, perturbation type and GEX availability. Metric
modules consume that specification instead of relying on machine-local project
configuration. Replogle includes HAM and simpleaf extraction lineages;
Papalexi 2021 and Norman 2019 are supplementary dataset lineages.

## Software

The plan uses the Omnibenchmark `conda` backend with environment YAML files
under `envs/`. Module repositories contain all execution code. Aside from the
explicit dataset paths in the data stage, execution has no external
`project_root` or personal library dependency.
