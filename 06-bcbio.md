# Submit `bcbio` job {#bcbio}

After composing the `O2.yaml` configuration file, you are ready to run `bcbio`. Instantiate the workspace by running

```
bcbio_nextgen.py -w template O2.yaml alignment.csv fastq
```

**OR**, if you had [merged multiple files per sample](#sampledesc-deep),

```
bcbio_nextgen.py -w template O2.yaml alignment.csv merged
```

You should now see the `alignment/` subdirectory, and the `work/` subdirectory inside of it. Descend into it:

```
cd alignment/work
```

All that remains to do is tell O2 the computational requirements for `bcbio`. Copy and paste the following lines into a file called `submit_bcbio.sh`:

```{bash, eval=FALSE}
#!/bin/sh
#SBATCH -p medium
#SBATCH -J bcbio_O2
#SBATCH -o run.o
#SBATCH -e run.e
#SBATCH -t 4-00:00
#SBATCH --cpus-per-task=1
#SBATCH --mem=8000

export PATH=/n/app/bcbio/tools/bin:$PATH
bcbio_nextgen.py ../config/alignment.yaml \
    -n 24 -t ipython -s slurm -q medium -r t=4-00:00 --timeout 2000
```

More information about these settings can be found in the [O2 wiki](https://wiki.rc.hms.harvard.edu/display/O2/How+To+Submit+Parallel+Jobs+in+O2). Once the file is ready, use it to kick off the run (after double-checking that you are currently in the `alignment/work/` subdirectory):

```
sbatch submit_bcbio.sh
```
