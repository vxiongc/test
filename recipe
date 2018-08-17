Bootstrap: shub
From: ISU-HPC/centos7-base

### Container help  ###
%help
Quick diag testsuite

### Create diag directories ###
%setup
mkdir -p ${SINGULARITY_ROOTFS}/diag
mkdir -p ${SINGULARITY_ROOTFS}/diag/bin
mkdir -p ${SINGULARITY_ROOTFS}/diag/lib

### Put diags in /diag/* ###
%files
dgemm /diag/bin
libiomp5.so /diag/lib

mpi_diag /diag/bin
libmpi.so.0 /diag/lib
libpciaccess.so.0 /diag/lib

### Dgemm app ###
%apprun dgemm
printf "Running Dgemm Test\n"
/diag/bin/dgemm

%appenv dgemm
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/diag/lib
#################

### MPI app ###
%apprun mpi
printf "Running MPI Test\n"
/diag/bin/mpi_diag

%appenv mpi
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/diag/lib
#################

### Default library path ##
%environment
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/diag/lib

%post

%check

### Run all diags ###
%runscript
printf "Running Dgemm Test\n"
/diag/bin/dgemm
printf "\nRunning MPI Test\n"
/diag/bin/mpi_diag

%labels
Maintainer vxiong
Version v0.01
