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

# Intel Compiler Installation

    spack install --no-cache intel-oneapi-compilers@2022.0.2

--

    spack find

--

    spack load intel-oneapi-compilers
    spack compiler find
    spack unload

--

    spack compilers

![Alt Text](images/intel compilers/spack compilers.png)

## **Install Intel MPI**

    spack install --no-cache intel-oneapi-mpi+external-libfabric%intel

