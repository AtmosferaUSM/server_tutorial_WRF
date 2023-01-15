# WPS Configuration

## **Create a soft link for the WPS**

Load the compilers before you start doing anything.
    
    spack load intel-oneapi-compilers
    spack load intel-oneapi-mpi

!!! Warning

    Copy WPS folder instead of using the soft link.


```
cd /shared/scratch
mkdir WPS
cp -a $(spack location -i wps%intel)/. WPS/
cd WPS
ls
```

## **Jasper Installation**

    spack install jasper@2.0.31%intel

Check if the `jasper version 2.0.31` is installed.

    spack find

![Alt Text](images/WPS configuration/jasper_2.0.31.png)

## **Export**   

    export JASPERLIB=$(spack location -i jasper@2.0.31%intel)/lib64
    export JASPERINC=$(spack location -i jasper@2.0.31%intel)/include
    export WRF_DIR=$(spack location -i wrf%intel)
    export NETCDFINC=$(spack location -i netcdf-fortran%intel)/include
    export NETCDFLIB=$(spack location -i netcdf-fortran%intel)/lib
    export NETCDF=$(spack location -i netcdf-fortran%intel)
    export NETCDFF=$(spack location -i netcdf-fortran%intel)
    export LD_LIBRARY_PATH=/shared/spack/opt/spack/linux-amzn2-zen2/intel-2021.5.0/jasper-2.0.31-skcu73p6hnlgov6teechaq6muly2xrez/lib64=/shared/spack/opt/spack/linux-amzn2-zen2/intel-2021.5.0/netcdf-fortran-4.5.4-izf5fn4mw4y4mcgdjed7jp7bypsfi3s2/lib:\$LD_LIBRARY_PATH

Check if the variables are imported correctly.

    echo $NETCDFINC
    echo $NETCDFLIB
    
Then, copy the contents of lib and include of `netcdf-c` to `netcdf-fortran` of the intel compilers.

    cp -a $(spack location -i netcdf-c%intel)/include/. $(spack location -i netcdf-fortran%intel)/include/
    cp -a $(spack location -i netcdf-c%intel)/lib/. $(spack location -i netcdf-fortran%intel)/lib/ 




## **Edit configure.wps File**   

    ./configure

Type '17'.
If you did not set the path for `NETCDFINC`, type `Y` then paste the `NETCDFINC` path as given above.


    nano configure.wps


Look for `WRF_LIB` and add `-qopenmp` after `-lnetcdff -lnetcdf` then save.

![Alt Text](images/WPS configuration/add_qopenmp.png)

## **Compile**  
    
    ./compile > log.compile

![Alt Text](images/WPS configuration/wpsconfiguration_sucessful.png)


## **Clean**

!!! note

    to reset WPS settings!
        
        ./clean -a


