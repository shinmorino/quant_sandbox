# Sqaod

Collections of solvers/annealers for simulated quantum annealing on CPU and CUDA(NVIDIA GPU).

## Project status (as of 4/22)
Alpha2 has been released on 4/22.<BR>
 * important fixes and updates:
   - Fixed: In alpha1, CPU/CUDA annealers with FP32 did not work due to incorrect numerical type conversion in python c-extension.  In alpha2, this issue has been fixed and tested.
   - API change : set_x() is used to set initial bit vectors to annealers in alpha1.  In alpha2, set_q() is used intead.  The set_q() accepts one spin vector or an array of spin vectors.
   - Several fixes in python code and c-extensions.
   - Current versions are 1.0.1 for debs and 1.0.1a2 for whl in pypi.
   
The next release is Beta1 planned in the end of this month.<BR>
Please visit milestones [here](https://github.com/shinmorino/sqaod/milestones?direction=asc&sort=due_date&state=open) for further development plan.

## Installation  
Here's an instruction to install alpha2 binary distribution of sqaod.  Alpha2 binary distribuion is provided only for Ubuntu 16.04.<BR>
If you want to use other Linux distribution, currently you need to build from source. See wiki, [Build from source](https://github.com/shinmorino/sqaod/wiki/Build-from-source).<BR>
Or if you need a binary distribution for your linux distro, please file a request to [Issues](https://github.com/shinmorino/sqaod/issues).  Windows version and/or docker images are possible as well.

### 1. Installing NVIDIA Driver<BR>
If you want to run CUDA-based solvers, you need NVIDIA GPU and NVIDIA driver installed on your machine.<BR>
GPUs of compute capabiity 3.5 (2nd gen Kepler) or later is required. Recommendation is Maxwell(compute capability 5.0) or later.  Please visit [CUDA GPUs](https://developer.nvidia.com/cuda-gpus) to check compute capability of GPUs.

To install CUDA packages required for sqaod, please visit [CUDA downloads](https://developer.nvidia.com/cuda-downloads), and download 'deb(network)' or 'deb(local)' package.<BR>
Afer downloading the deb package, run the following commands.  Here, CUDA 9.1, deb(network) package is assumed.
~~~
 $ sudo dpkg -i cuda-repo-ubuntu1604_9.1.85-1_amd64.deb
 $ sudo apt-key adv --fetch-keys http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/7fa2af80.pub
 $ sudo apt-get update
 $ sudo apt--get install cuda-drivers
~~~

### 2. Installing native libraries.
Sqaod has its own C++ native libraries which are invoked via python c-extensions.  These libraries are released as deb packages.  Please use apt-get to install them.

~~~
 $ sudo apt-get install apt-transport-https apt-utils
 # adding sqaod repository
 $ echo 'deb [arch=amd64] https://shinmorino.github.io/sqaod/ubuntu xenial main' | \
   sudo tee /etc/apt/sources.list.d/sqaod.list
 $ sudo apt-get update

 # install sqaodc native library.
 # if your CPU has avx2 feature, installl libsqaodc-avx2, otherwise install libsqaodc.
 $ sudo apt-get install libsqaodc-avx2   # AVX2 enabled.
 $ sudo apt-get install libsqaodc        # otherwise (SSE2 enabled).
 
 # install CUDA native library if you need CUDA-based solvers.
 $ sudo apt-get install libsqaodc-cuda-9-0
~~~

**Note:** You may see some warnings during installation.  Ex.: "W: The repository 'https://shinmorino.github.io/sqaod/ubuntu xenial Release' does not have a Release file."<BR>
If you get a confirmation like "Install these packages without verification? [y/N]", answer y to proceed installation.<BR>
It will be fixed by beta1 release.


### 3. installing python package

Sqaod is currently supporting python 2.7 and python 3.3 - 3.5.  For details, please visit the project [sqaod project page](https://pypi.python.org/pypi/sqaod/) on PyPI.<BR>
To install sqaod python package, use pip as shown below.
~~~
 $ pip install -U sqaod
~~~


### 4. Running examples

Python examples are in [sqaod/sqaodpy/examples](https://github.com/shinmorino/sqaod/tree/master/sqaodpy/example).  The below is an example to run dense graph annealer.

~~~
$ wget https://raw.githubusercontent.com/shinmorino/sqaod/master/sqaodpy/example/dense_graph_annealer.py
$ python dense_graph_annealer.py
~~~

### Feedback and requests
I welcome your feedback and requests.<BR>
Please file your feedback and/or requests to [Issues](https://github.com/shinmorino/sqaod/issues).<BR>

### Opensource libraries used in sqaod.

- [Eigen](http://eigen.tuxfamily.org/index.php?title=Main_Page) ([MPL2](https://www.mozilla.org/en-US/MPL/2.0/))
- [CUB](http://nvlabs.github.io/cub/) ([BSD 3-Clause "New" or "Revised" License](https://github.com/NVlabs/cub/blob/1.8.0/LICENSE.TXT))
- [libblas](https://packages.ubuntu.com/xenial/libblas3) ([Modified BSD License](http://www.netlib.org/lapack/LICENSE.txt))

### Enjoy !!!