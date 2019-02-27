# Sample Description {#sampledesc}

`bcbio` expects a sample description file that tells it which files map to which samples. The file should be in the .csv format and have at least two columns. An example file for four samples might look like this:

```
samplename,description
S1.fastq.gz,S1
S2.fastq.gz,S2
S3.fastq.gz,S3
S4.fastq.gz,S4
```

where file `S1.fastq.gz` is mapped to the sample named `S1`, and so on. Additional columns can be included in this file and get preserved by bcbio as sample metadata.

The rest of the guide assumes that your sample description file is named `alignment.csv`.

## Digital Gene Expression

When working with DGE data, you will typically have two matching files with suffixes `R1` and `R2`. Only the `R1` file needs to be specified in the sample description file. For example, your `alignment.csv` might look like

```
samplename,description
DGE1_XT_S1_R1_001.fastq.gz,MasterPlate
```

where the matching `DGE1_XT_S1_R2_001.fastq.gz` is not listed explicitly.

## Deep RNAseq

In the case of deep RNAseq data, you may have multiple FASTQ files per sample. Prior to running the aligner, these files need to be merged. `bcbio` provides a script for doing so, but it needs to know which files map to which samples. Compose a file named `toMerge.csv` that provides such a mapping. For example,

```
samplename,description
/n/scratch2/abc123/myProject/TRA00140445_S1_L001_R1.fastq.bz2,S1
/n/scratch2/abc123/myProject/TRA00140445_S1_L002_R1.fastq.bz2,S1
/n/scratch2/abc123/myProject/TRA00140445_S1_L003_R1.fastq.bz2,S1
/n/scratch2/abc123/myProject/TRA00140445_S1_L004_R1.fastq.bz2,S1
/n/scratch2/abc123/myProject/TRA00140445_S2_L001_R1.fastq.bz2,S2
/n/scratch2/abc123/myProject/TRA00140445_S2_L002_R1.fastq.bz2,S2
/n/scratch2/abc123/myProject/TRA00140445_S2_L003_R1.fastq.bz2,S2
/n/scratch2/abc123/myProject/TRA00140445_S2_L004_R1.fastq.bz2,S2
```

lists the mapping for two samples `S1` and `S2`, each having data collected across four sequencer lanes.

Once you have prepared the file `toMerge.csv`, run the following command to execute the merge:
```
bcbio_prepare_samples.py --out merged --csv toMerge.csv
```

The merging operation might take a while. When it finishes, your merged files will reside in the `merged/` subdirectory. You will also have a new filename-to-samplename mapping file `toMerge-merged.csv`. For consistency with the remainder of this guide, rename this file to `alignment.csv` using the `mv` command:

```
mv toMerge-merged.csv alignment.csv
```
