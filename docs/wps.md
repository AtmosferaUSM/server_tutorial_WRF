# WPS Installation

```
cat <<EOF > wps-install.sbatch
#!/bin/bash
#SBATCH -N 1
#SBATCH --exclusive


spack install -j 1 wps%intel ^intel-oneapi-mpi+external-libfabric
EOF
```

    sbatch wps-install.sbatch


## **Checking the Clusters**

    squeue

![Alt Text](images/wps installation/squeue.png)

    cat slurm-<jobID>.out

-- or

    tail slurm-<jobID>.out

![Alt Text](images/WRF_WPS successful installation/output.png)

    spack find

![Alt Text](images/WRF_WPS successful installation/spack.png)