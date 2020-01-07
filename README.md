# Install-Tensorflow-GPU-2.0-on-Linux-Ubuntu-18.04<br>
Easily Install Tensorflow-GPU 2.0 on Linux Ubuntu 18.04 -Cuda 10 &amp; Cudnn 7.6.5<br>

### Requirements: <br>
An NVIDIA GPU with a compute capability of 3.0 or higher<br>
Python installed (Install Python 3.4+)<br>

```
sudo add-apt-repository ppa:jonathonf/python-3.6
sudo apt-get update
sudo apt-get install python3.6
```
Install Pip3 <br>
```sudo apt install python3-pip```<br>

Install Python and the TensorFlow package dependencies<br>

```(https://www.tensorflow.org/install/source) ✔️ ```

<img src = 'https://miro.medium.com/max/1809/1*anNVCRsxyx-GJWBHeW6ThQ.png' width= 600 alt='install pakage'></img> <br>

Tested build configurationsDownload Build Tools: 
[Download Bazel 0.26.1](https://github.com/bazelbuild/bazel/releases/download/0.26.1/bazel-0.26.1-installer-linux-x86_64.sh).<br>

Download Compiler GCC 7.3.1: 
[GCC 7.3.1](https://ftp.gnu.org/gnu/gcc/gcc-7.3.0/gcc-7.3.0.tar.xz).  <br>

### Overview <br>
<b>Step 1:</b> Update your GPU driver (should be higher than version 390)<br>
<b>Step 2:</b> Install the CUDA Toolkit version 10.0<br>
<b>Step 3:</b> Install CUDNN 7.6.5<br>
<b>Step 4:</b> Install Tensorflow GPU 2.0v with pip<br>
<b>Step 5:</b> Test Run GPU<br>
<br>

### Step 1: Update your GPU driver <br>
Open a terminal and run the following 3 commands<br>
```
sudo add-apt-repository ppa:graphics-drivers/ppa
sudo apt update
sudo apt install nvidia-390 or higher version
```
<b>Reboot</b> your computer. To verify the installation, open a terminal and run the following command<br>

```nvidia-smi```
The output should show the GPU name and the driver.show the GPU name and the driver

### Step 2: Install the CUDA Toolkit (10.0) <br>

CUDA Toolkit Archive " https://developer.nvidia.com/cuda-toolkit-archive"
go to https://developer.nvidia.com/cuda-10.0-download-archive and download the toolkit for Linux, x86_64, ubuntu, 18.04, deb(local)
once the download is complete, open a terminal in the directory the base installer is and run the following commands
<br>
```
sudo dpkg -i cuda-repo-ubuntu1804-10-0-local-10.0.130-410.48_1.0-1_amd64.deb
sudo apt-key add /var/cuda-repo-<version>/7fa2af80.pub
sudo apt-get update
sudo apt-get install cuda
```
 
download patch 1 and install (you should get a prompt to install once its done downloading)<br>
download patch 2 and install (you should get a prompt to install once its done downloading)<br>

open your .bashrc file with nano<br>

``` sudo nano ~/.bashrc```

go to the last line and add the following lines (this will set your PATH variable)<br>
```
export PATH=/usr/local/cuda-10.0/bin${PATH:+:$PATH}}
export LD_LIBRARY_PATH=/usr/local/cuda 10.0/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}
```
### Step 3: Install CUDNN 7.6.5<br>

go to https://developer.nvidia.com/cudnn<br>
Select CUDNN 7.6.5 for CUDA 10.0<br>
download the cuDNN v7.6.5 Library for Linux (Download with Link)<br>
open a terminal in the directory the tar file is located<br>
unzip the tar file using the command<br>
```
tar -xzvf cudnn-10.0-linux-x64-v7.6.5.32.tgz
```
run the following commands to move the appropriate files to the CUDA folder
```
sudo cp cuda/include/cudnn.h /usr/local/cuda/include
sudo cp cuda/lib64/libcudnn* /usr/local/cuda/lib64
sudo chmod a+r /usr/local/cuda/include/cudnn.h /usr/local/cuda/lib64/libcudnn*
```
### Step 4: pip install TensorFlow-GPU 2.0 <br>

I will be using a conda environment for installing TensorFlow<br>
create a conda environment by using the following command<br>
```
conda create -n tf python=3.7 pip
```
activate your environment using
```
source activate tf
```
create an environment without conda
```
sudo pip3 install virtualenv

virtualenv venv (you can use any name insted of venv)
source venv/bin/activate (Active your virtual environment)
```

install TensorFlow-GPU 2.0 with pip3 <br>
```
sudo pip3 install tensorflow-gpu==2.0.0
```
### Step 5: Test it! <br>

```
import tensorflow as tf
tf.test.is_gpu_available(
    cuda_only=False,
    min_cuda_compute_capability=None
)
```
if the output was True then everything OK!<br>
<img src='https://miro.medium.com/max/2066/1*g3cN7zze0AmXzOdRSAtYXg.png' width=650 alt='tensorflow gpu'></img> <br>

References:<br>
https://medium.com/@m_farzalizadeh/easily-install-tensorflow-gpu-2-0-on-linux-ubuntu-18-04-cuda-10-cudnn-7-6-5-1ecb354e68bc
