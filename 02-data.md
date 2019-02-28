# Data Storage {#data}

All of the steps in this section must be performed from the Unix system `transfer.rc.hms.harvard.edu`,
which you access via SSH using your eCommons username and password. The examples below use
the username `abc123`, so in the typed commands after the `$` you must substitute your own
username (or the username of whomever you're working on behalf of).

## Download the primary sequence data to ImStor

```
abc123@transfer:~$ cd /n/files/ImStor/sorger/data/rnaseq
abc123@transfer:/n/files/ImStor/sorger/data/rnaseq$ mkdir abc123
abc123@transfer:/n/files/ImStor/sorger/data/rnaseq$ cd abc123
abc123@transfer:/n/files/ImStor/sorger/data/rnaseq/abc123$ mkdir project_name
abc123@transfer:/n/files/ImStor/sorger/data/rnaseq/abc123$ cd project_name
```

Now, follow the data download instructions from your sequencing facility. At HMS, the sequencing core will often share a web URL that contains your data and additional QC reports. You can download the entire directory (or a subfolder with just your FASTQ files) using a recursive `wget` command:

```
abc123@transfer:/n/.../abc123/project_name$ wget -r --no-parent <URL to download>
```

replacing `<URL to download>` with the link to the directory containing all the files you want to download.

## Copy the sequence data to /n/scratch2

After creating a permanent copy of your data on ImStor, you will want to also create a secondary working copy on `/n/scratch2`, where all `bcbio` analysis will actually be performed.

```
abc123@transfer:/n/files/.../abc123/project_name$ cd ..
abc123@transfer:/n/files/.../abc123$ mkdir /n/scratch2/abc123
abc123@transfer:/n/files/.../abc123$ rsync -avP project_name /n/scratch2/abc123
abc123@transfer:/n/files/.../abc123$ exit
```

It's important not to put a trailing `/` on `project_name` in the `rsync` command. (If you include
the `/`, the files will end up one directory level too high)
