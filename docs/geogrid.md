# Geogrid

## **Preliminary**

Before we start executing geogrid.exe, ungrib.exe and metgrid.exe, create a folder named `WRF_Resources` to put all the required input data for WPS. We will download all the required data under the `/scratch` folder.

    cd /shared/scratch
    mkdir WRF_Resources
    cd WRF_Resources

## **Download the geogrid data**   

You can download the mandatory high resolution data from the official website of UCAR: 
[Download data](https://www2.mmm.ucar.edu/wrf/users/download/get_sources_wps_geog.html){target=_blank}
 for the input of geogrid.There are two types of data sets available, each made up of the hightest and lowest resolution of each mandatory field. You may read the details on the official website to decide on the data that suits your need. In this case, we will be using the highest resolution of each mandatory field.

    wget https://www2.mmm.ucar.edu/wrf/src/wps_files/geog_high_res_mandatory.tar.gz
    tar -xf geog_high_res_mandatory.tar.gz

## **Edit the geog_data_path in namelist.wps**   

Point the directory of high resolution data to WRF_Resources in the `nameslist.wps`. To do that, you will first have to obtain the path to WPS_GEOG.

    cd WPS_GEOG
    pwd

Copy the path and go to the directory `/shared/scratch/WPS/WRF_Resources/WPS_GEOG/` where your WPS is compiled and edit the namelist.wps.

    cd /shared/scratch/WPS/
    nano namelist.wps

Under the &geogrid section, edit the geog_data_path and save it.

![Alt Text](images/geogrid/add path.png)

## **Edit the &geogrid section in namelist.wps** 

Before executing geogrid.exe, edit the information in the namelist according to your case. Read the description for each listed variables in the namelist, as well as [best practice](https://www2.mmm.ucar.edu/wrf/users/namelist_best_prac_wps.html){target=_blank} here. We will be using the information provided in the Resources tab in this tutorial. 

Export the LD_LIBRARY_PATH and run the geogrid.exe. Make sure you had load the `intel-oneapi-compilers` and `intel-oneapi-mpi` using spack to avoid issue missing libiomp5.so. 

    export LD_LIBRARY_PATH=$(spack location -i netcdf-fortran%intel)/lib/
    spack load intel-oneapi-compilers
    spack load intel-oneapi-mpi
    ./geogrid.exe

If your geogrid runs successfully, the following output will be printed: `Successful completion of geogrid.`

![Alt Text](images/geogrid/successful output.png)