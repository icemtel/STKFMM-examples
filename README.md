# STKFMM-examples
Examples of use of STKFMM library (https://github.com/wenyan4work/STKFMM) via the python interface.


# Installation of STKFMM

- Installed on Ubuntu 16.04 system.
- Steps: install dependencies via conda, install PVFMM, install SKFMM.


1. Install prerequisites in a conda virtual environment 
  (for reproducibility: I use `conda-forge` as the main [channel](https://docs.conda.io/projects/conda/en/latest/user-guide/concepts/channels.html))
  ```
  conda create -n stkfmm python=3.7 # create environment named stkfmm
  conda activate  stkfmm            # switch to the new environment
  conda install mkl-devel scipy numpy openmpi mpi4py gcc_linux-64 gxx_linux-64 gfortran_linux-64 boost
  pip install pybind11-cmake # will be used to bind STKFMM and python
  conda install cmake
  ```  
  Optional:  
  ```
  conda install matplotlib # for visualization
  conda install numba # to run examples.py and kernels.py
  conda install tbb # for numba + threading
  ```

2. Install PVFMM -> I followed steps in https://github.com/wenyan4work/Environment
    ```
    git clone https://github.com/wenyan4work/Environment
    cd Environment
    ```
    1. Comment out in Compile.py everything, except parts connects to PVFMM  (TODO: test if Eigen and gcc are needed).

    2. Set variables

    ```
    export MKL_THREADING_LAYER=GNU         # necessary because conda uses gcc
    export MKL_INTERFACE_LAYER=GNU,LP64    # necessary because conda uses gcc
    export MKLROOT=/home/icemtel/miniconda3/envs/stkfmm/ # SET THE PATH TO THE CODNA ENVIRONMENT
    ```
    3. Run installation script
    ```
    python Compile.py 2>&1 | tee Compile.log # 
    ```

3. Install STKFMM
  ```
  git clone https://github.com/wenyan4work/STKFMM.git
  cd STKFMM
  ```
  1. Adjust parameters in the cmake script
    - `PyInterface=ON`
    -  `BUILD_DOC=ON` - a doxygen (documentation utility) html file will be generated
  (to edit and change execution rights)
  ```
  nano do-cmake.sh
  chmod 777 do-cmake.sh
  ```
  2. Run `cmake` and `make`
  ```
  mkdir build
  cd build
  ../do-cmake.sh
  make
  ```
  3. Download precomputed data from https://users.flatironinstitute.org/~wyan/pdata.7z and unzip to `$PVFMM_DIR/pdata` -> weights >3.5 GB
  
  Q: where is "$PVFMM_DIR"? I don't have such variable.
