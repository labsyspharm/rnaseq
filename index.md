# Quick Start

- Ensure your O2 environment is properly setup to run `bcbio`. This only needs to be done once.
- Put your data in permanent storage and create a copy on `/n/scratch2/`.
- Do you have multiple fastq files that need to be merged for each sample?
    - If yes, run `bcbio_prepare_samples.py` to merge the files. Rename the resulting `merged_*.csv` to `alignment.csv`.
	- If not, compose `alignment.csv` that maps filenames to corresponding sample descriptions.
- Download the latest human genome reference.
- Compose a setting YAML file.
- Instantiate the `bcbio` workspace. Descend into `alignment/work` subdirectory.
- Kick off a `bcbio` run.
