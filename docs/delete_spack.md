# Delete existing Spack for fresh installation

## **Export variable**

You can just remove the existing `$SPACK_ROOT` and install a new Spack environment. For example, if $SPACK_ROOT is `/shared/spack`, you can do:


    export SPACK_ROOT=/shared/spack


## **Remove spack from the system**


    rm -rf $SPACK_ROOT


## **Download Spack**

Now, you can download Spack and go through the steps of `Spack Installation` again.


    export SPACK_ROOT=/shared/spack
    mkdir -p $SPACK_ROOT
    git clone -b v0.18.0 -c feature.manyFiles=true https://github.com/spack/spack $SPACK_ROOT

