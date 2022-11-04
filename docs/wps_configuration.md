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

# WPS Configuration

## **Create a soft link for the WPS**
    
    spack load intel-oneapi-compilers
    spack load intel-oneapi-mpi

{>>COPY INSTEAD OF USING THE SOFT LINK<<}

    cd /shared/scratch
    mkdir WPS
    cp -a $(spack location -i wps%intel)/. WPS/
    cd WPS
    ls

## **Jasper Installation**

    spack install jasper@2.0.31%intel

--

    spack find

## **Export**   

    export JASPERLIB=$(spack location -i jasper@2.0.31%intel)/lib64
    export JASPERINC=$(spack location -i jasper@2.0.31%intel)/include
    export WRF_DIR=$(spack location -i wrf%intel)
    export NETCDFINC=$(spack location -i netcdf-fortran%intel)/include
    export NETCDFLIB=$(spack location -i netcdf-fortran%intel)/lib
    export NETCDF=$(spack location -i netcdf-fortran%intel)
    export NETCDFF=$(spack location -i netcdf-fortran%intel)

--

    echo $NETCDFINC
    echo $NETCDFLIB
    
--

    cp -a $(spack location -i netcdf-c%intel)/include/. $(spack location -i netcdf-fortran%intel)/include/
    cp -a $(spack location -i netcdf-c%intel)/lib/. $(spack location -i netcdf-fortran%intel)/lib/ 
--



## **Edit configure.wps File**   

    ./configure

Type Y Then paste the NETCDFINC path , ...


    nano configure.wps

Add {== -lnetcdff -lnetcdf -qopenmp ==} then save



-- 

## **Compile**  
    
    ./compile > log.compile


> **Clean** - to reset WPS settings!

    ./clean -a

