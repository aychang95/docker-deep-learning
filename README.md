# GPU-accelerated Python Docker Images for Deep Learning

### Image Types

The images are based on [nvidia/cuda](https://hub.docker.com/r/nvidia/cuda), and are intended to be drop-in replacements for the corresponding CUDA
images in order to make it easy to add FastAI libraries while maintaining support for existing CUDA applications.

Images come in two types.

The [aychang/deep-learning](https://hub.docker.com/r/aychang/deep-learning/tags) repo contains the following:
- `runtime` - extends the `base` image by adding a notebook server and example notebooks.
  - **TIP: Use this image if you want to explore the image environment through notebooks and examples.**
- `devel` - contains the full Python source tree including CUDA development libraries.
  - **TIP: Use this image to develop Python and CUDA-based libraries from source.**

### Image Tag Naming Scheme

The tag naming scheme for th images incorporates key platform details into the tag as shown below:
```
cuda10.1-runtime-ubuntu18.04-py3.7
     ^    ^        ^         ^
     |    type     |         python version
     |             |
     cuda version  |
                   |
                   linux version
```

## Prerequisites

* NVIDIA Pascal™ GPU architecture or better
* CUDA [10.1/10.2/11.0](https://developer.nvidia.com/cuda-downloads) with a compatible NVIDIA driver
* Ubuntu 16.04/18.04 or CentOS 7
* Docker CE v18+
* [nvidia-docker](https://github.com/nvidia/nvidia-docker/wiki/Installation-(version-2.0)) v2+

## Usage

### Start Container and Notebook Server

#### Preferred - Docker CE v19+ and `nvidia-container-toolkit`
```bash
$ docker pull aychang/deep-learning:cuda10.2-runtime-ubuntu18.04-py3.7
$ docker run --gpus all --rm -it -p 8888:8888 \
         aychang/deep-learning:cuda10.2-runtime-ubuntu18.04-py3.7
```

#### Legacy - Docker CE v18 and `nvidia-docker2`
```bash
$ docker pull aychang/deep-learning:0.0.1-cuda10.2-runtime-ubuntu18.04-py3.7
$ docker run --runtime=nvidia --rm -it -p 8888:8888 \
         aychang/deep-learning:cuda10.2-runtime-ubuntu18.04-py3.7
```

### Container Ports

The following ports are used by the **`runtime` containers only** (not `base` containers):

- `8888` - exposes a [JupyterLab](https://jupyterlab.readthedocs.io/en/stable/) notebook server

### Acknowledgement

Docker image setup based off of [FastNN's](https://github.com/aychang95/fastnn/tree/main/docker) docker component

Docker readme heavily influenced by RAPIDS docker readme [here](https://github.com/rapidsai/docker/blob/branch-0.17/dockerhub-readme/Dockerhub_rapidsai.md)
