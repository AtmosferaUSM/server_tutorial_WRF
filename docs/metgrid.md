# METGRID


## **Export the library path**

    export LD_LIBRARY_PATH=/shared/spack/opt/spack/linux-amzn2-zen2/intel-2021.5.0/netcdf-fortran-4.5.4-a3txw6pecfmvci7zgwpr3p7nzlqt2k2m/lib


## **Load the compilers**

    spack load intel-oneapi-compilers
    spack load intel-oneapi-mpi


## **Run metgrid**

    ./metgrid.exe 

![Alt Text](images/metgrid/cut_successful_met_em_files.png)