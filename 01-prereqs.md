# Prerequisites in O2 environment {#prereqs}

* If this is your first time using a linux command shell, make sure you type the commands in exactly as is. Things like spaces and quotes matter. The easiest way to do this is to copy and paste the commands from these instructions into your command shell.

* Login to O2 using the instructions available at https://wiki.rc.hms.harvard.edu/display/O2/Using+Slurm+Basic

* Familiarize yourself with [nano](https://www.nano-editor.org/dist/v2.2/nano.html), a text editor in linux. Specifically, make note of keyboard shortcuts `CTRL+O` to save, `CTRL+X` to exit.

* Use `nano ~/.bashrc` to open your `.bashrc` file and add the following lines:

    ```{bash, eval=FALSE}
    # Defines a new command, soar, for requesting an interactive compute shell
    alias 'soar=srun -p interactive -t 0-12:00 -n 2 --pty /bin/bash'
    ```

    Save and exit (`CTRL+O` and `CTRL+X` in `nano`). This defines a new command `soar`, which you will use to request an interactive compute shell after logging into O2. **This needs to be done only once.**
	
* Log out of O2 and log back in. This will ensure that the new lines in `.bashrc` take effect. (Alternatively, you can type `source ~/.bashrc` without logging out.)

* When you first log into O2, you are given a login shell. While you will be able to submit jobs (like `bcbio`) from the login shell, you will not be able to run resource intensive jobs, such as merging of fastq files. To do the latter, you need to request an interactive compute shell using the new `soar` command you just defined. Simply type `soar` and you should get an output that looks something like this:

    ```
    [abc123@login01 ~]$ soar
    srun: job 6094734 queued and waiting for resources
    srun: job 6094734 has been allocated resources
    [abc123@compute-a-01-02 ~]$
    ```

* Lastly, load the bcbio module by typing `module load bcbio` in your shell prompt:

    ```
    [abc123@compute-a-01-02 ~]$ module load bcbio
    ```
