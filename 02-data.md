# Data Storage {#data}

<script src="./libs/ext/highlight.pack.js"></script>
<script>hljs.initHighlightingOnLoad();</script>

All of the steps in this section must be performed from the Unix system `transfer.rc.hms.harvard.edu`,
which you access via SSH using your eCommons username and password. The examples below use
the username `abc123`, so in the typed commands after the `$` you must substitute your own
username (or the username of whomever you're working on behalf of).

## Download the primary sequence data to ImStor

```
[abc123@transfer ~]$ cd /n/files/ImStor/sorger/data/rnaseq
[abc123@transfer rnaseq]$ mkdir abc123
[abc123@transfer rnaseq]$ cd abc123
[abc123@transfer abc123]$ mkdir project_name
[abc123@transfer abc123]$ cd project_name
```

Now, follow the data download instructions from your sequencing facility. At HMS, the sequencing core will often share a web URL that contains your data and additional QC reports. You can download the entire directory (or a subfolder with just your FASTQ files) using a recursive `wget` command:

```
[abc123@transfer project_name]$ wget -r --no-parent http://facility-url/
```

replacing `http://facility-url/` with the link to the directory containing all the files you want to download. Several caveats should be kept in mind:

* It is important to include the trailing slash at the end of the URL provided by the sequencing core.
* The certificate or credentials of the Bauer core file server are not always up to date. When pulling data off their server, sometimes it's necessary to include the `--no-check-certificate` flag to avoid errors. For example, the above command would look as 
```
wget -r --no-parent --no-check-certificate http://facility-url/
```

## Copy the sequence data to /n/scratch2

After creating a permanent copy of your data on ImStor, you will want to also create a secondary working copy on `/n/scratch2`, where all `bcbio` analysis will actually be performed.

```
[abc123@transfer project_name]$ cd ..
[abc123@transfer abc123]$ mkdir /n/scratch2/abc123
[abc123@transfer abc123]$ rsync -avP project_name /n/scratch2/abc123
[abc123@transfer abc123]$ exit
```

It's important not to put a trailing `/` on `project_name` in the `rsync` command. (If you include
the `/`, the files will end up one directory level too high)

## (Optional) Convert BCL files to FASTQ

Typically, the conversion from BCL to FASTQ is done by the sequencing core. However, occasionally you may need to perform a custom conversion. To do so, you will want to use [Illumina's bcl2fastq tool](https://support.illumina.com/sequencing/sequencing_software/bcl2fastq-conversion-software.html). The tool accepts many parameters, the precise value of which is highly dependent on the sequencer and the library prep. Consult the [tool guide](https://support.illumina.com/content/dam/illumina-support/documents/documentation/software_documentation/bcl2fastq/bcl2fastq2-v2-20-software-guide-15051736-03.pdf) to identify the proper parameter settings that match your library preparation protocol. 

You will then want to logout of `transfer.rc.hms.harvard.edu`, log back in to `o2.hms.harvard.edu` and request a compute node using [the previously defined `soar` command](#prereqs):

```
[abc123@login01 ~]$ soar
[abc123@compute-a-01-02 ~]$
```

On the compute node, navigate to your data location that contains BCL files and run the `bcl2fastq` tools:

```
module load bcl2fastq
cd /n/scratch2/abc123/project_name/bcl
mkdir ../fastq
bcl2fastq <settings parameters> --sample-sheet <path/to/sample/sheet> --runfolder-dir . --output-dir ../fastq
```
