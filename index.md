---
title: "Aligning deep RNAseq and Digital Gene Expression (DGE) reads using bcbio"
author: Laboratory of Systems Pharmacology
date: "`r Sys.Date()`"
site: bookdown::bookdown_site
output: bookdown::gitbook
github-repo: labsyspharm/rnaseq
---

# Quick Start {-}

1. [Ensure your O2 environment is properly setup to run `bcbio`.](#prereqs) This only needs to be done once.
2. [Put your data in permanent storage and create a copy on `/n/scratch2/`.](#data)
3. Do you have multiple fastq files that need to be merged for each sample?
    - If yes, run `bcbio_prepare_samples.py` to merge the files. Rename the resulting `merged_*.csv` to `alignment.csv`.
	- If not, compose `alignment.csv` that maps filenames to corresponding sample descriptions.
4. Download the latest human genome reference.
5. Compose a setting YAML file.
6. Instantiate the `bcbio` workspace. Descend into `alignment/work` subdirectory.
7. Kick off a `bcbio` run.
