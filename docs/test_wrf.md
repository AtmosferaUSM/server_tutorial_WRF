<!--- 

[atmosfera website](https://atmosfera.usm.my/)

**Bold Text** 

> following points:
- list
- list

{--deleted--}
{++added++}
{~~one~>a single~~}
{==Highlighting==}
{>>and comments can be added inline<<}
---> 

# Testing WRF

## **Load WRF**


    spack load wrf

Find WRF location

    ls `spack location -i wrf`/run/wrf.exe

--

    cd /shared
    mkdir scratch
    cd scratch  

--

    curl -O https://www2.mmm.ucar.edu/wrf/OnLineTutorial/wrf_cloud/wrf_simulation_CONUS12km.tar.gz
    tar -xzf wrf_simulation_CONUS12km.tar.gz

--

    cd conus_12km
    WRF_ROOT=$(spack location -i wrf%intel)/test/em_real/
    ln -s $WRF_ROOT* .

--

```
cat <<EOF > slurm-wrf-conus12km.sh
#!/bin/bash
#!/bin/bash
#SBATCH --job-name=WRF
#SBATCH --output=conus-%j.out
#SBATCH --nodes=2
#SBATCH --ntasks-per-node=16
#SBATCH --exclusive

spack load wrf
set -x
wrf_exe=\$(spack location -i wrf)/run/wrf.exe
ulimit -s unlimited
ulimit -a

export OMP_NUM_THREADS=6
export FI_PROVIDER=efa
export I_MPI_FABRICS=ofi
export I_MPI_OFI_LIBRARY_INTERNAL=0
export I_MPI_OFI_PROVIDER=efa
export I_MPI_PIN_DOMAIN=omp
export KMP_AFFINITY=compact
export I_MPI_DEBUG=4

set +x
module load intelmpi
set -x
time mpirun -np \$SLURM_NTASKS --ppn \$SLURM_NTASKS_PER_NODE \$wrf_exe
EOF
```

--

    sbatch slurm-wrf-conus12km.sh


--

##**DCV**

    cd /shared/scratch/conus_12km 
    spack load ncl
    ncl ncl_scripts/surface.ncl

![Alt Text](images/Testing WRF/output.png)
