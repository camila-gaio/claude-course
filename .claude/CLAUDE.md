# CLAUDE.md

## Project
Learning project for Claude Code: build a Nextflow (DSL2) workflow for QC of single-cell RNA-seq data.

## Working style
- This is a learning project: explain what you do and why, briefly.
- Work in small, incremental steps; propose a plan before large changes.
- Ask before adding new tools or dependencies.

## Conventions
- Nextflow DSL2; one process per file in `modules/`, composed in `workflows/`, entry point `main.nf`.
- Parameters in `nextflow.config` with sensible defaults; no hard-coded paths.
- Run each process in a Docker container (e.g. `satijalab/seurat`, BioContainers); keep a `singularity` profile for HPC. No conda.
- Analysis scripts in R using Seurat; keep them in `bin/` as executable `Rscript` files.
- Outputs go to `results/` (`params.outdir`); never commit data or results.

## QC scope
- Raw read QC (FastQC, MultiQC).
- Cell-level QC with Seurat: nFeature_RNA, nCount_RNA, percent.mt, doublet detection with DoubletFinder (expected doublet rate as a parameter).
- Filtering thresholds as parameters; produce summary plots and a report.

## Testing
- Keep a tiny test dataset and a `test` profile: `nextflow run main.nf -profile test,docker`.
- Run the test profile after every change.
