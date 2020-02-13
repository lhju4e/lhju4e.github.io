---
title: "how to switch cuda version by conda"
permalink: /develop/intern3
layout: category
---



--------------------------
# conda에서 cuda버전 다르게 쓰기

-----------------------------

`cd $CONDA_PREFIX` 를 통해 ~/anaconda3/envs/*[가상환경이름]* 으로 옴

`mkdir -p ./etc/conda/activate.d`

`mkdir -p ./etc/conda/deactivate.d`

`touch ./etc/conda/activate.d/env_vars.sh`

`touch ./etc/conda/deactivate.d/env_vars.sh`



*참고 : (etc/profile.d/conda.sh는 전체콘다 환경설정)* 

*activate.d폴더에 있는 스크립트는 conda activate할 때 실행.*

*deactivate는 deactivate할때 실행.*

 

**이전에 생성한 activate.d  폴더 안의 env_vars.sh   스크립트 작성**                                    

 `_OLD_VIRTUAL_CUDAHOME="${CUDA_HOME:-}"`

 `unset CUDA_HOME`

 `CUDA_HOME="/usr/local/cuda-9.0"`

 `export CUDA_HOME`

 `_OLD_PATH="${PATH:-}"`

 `export PATH=${CUDA_HOME}/bin:${PATH}`

 `echo $PATH`

`` 

 `_OLD_LD_LIBRARY_PATH="${LD_LIBRARY_PATH:-}"`

 `unset LD_LIBRARY_PATH`

 `export LD_LIBRARY_PATH=${CUDA_HOME}/lib64`

 `export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:${CUDA_HOME}/extras/CUPTI/lib64`

 `export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/home/qisens/Downloads/TensorRT-5.1.5.0/lib`

 `echo $LD_LIBRARY_PATH`

 

**마찬가지로 deactivate.d 폴더 안의 env_vars.sh  스크립트 작성**                                         

 `CUDA_HOME="${_OLD_VIRTUAL_CUDAHOME:-}"`

 `unset _OLD_VIRTUAL_CUDAHOME`

 `export CUDA_HOME`



 `LD_LIBRARY_PATH="${_OLD_LD_LIBRARY_PATH:-}"`

 `echo $_OLD_LD_LIBRARY_PATH`

 `unset _OLD_LD_LIBRARY_PATH`

 `export LD_LIBRARY_PATH`



 `PATH="${_OLD_PATH:-}"`

 `unset _OLD_PATH`

 `export PATH`