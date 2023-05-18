# WPS Installation

Now, we will be creating a Slurm job submission script to install WPS using Spack.

``` linenums="1" title="wps-install.sbatch"
cat <<EOF > wps-install.sbatch
#!/bin/bash
#SBATCH -N 1
#SBATCH --exclusive

spack install -j 1 wps%intel ^intel-oneapi-mpi+external-libfabric
EOF
```

Submit the job by copy the following to your CLI.

    sbatch wps-install.sbatch


## **Checking the Clusters**

You may check the progress of the installation. `CF` indicates that the nodes is currently under configuration while `R` indicates running nodes.

    squeue

![Alt Text](images/wps installation/squeue.png)

Use `cat` or `tail` to see the output of the installation. You shall see the successful installation message at the end of the output upon successful installation.

=== "cat"

    ``` 
    cat slurm-<jobID>.out
    ```

=== "tail"

    ``` 
    tail slurm-<jobID>.out
    ```

Use Spack find to check if the version of WPS is correctly installed under the intel compilers.

![Alt Text](images/WRF_WPS successful installation/output.png)

    spack find

![Alt Text](images/WRF_WPS successful installation/spack.png)