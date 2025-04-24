# Software
!!! warning "Apptainer support is currently in Beta."
    If you encounter issues please reach out via Slack for support.

## What is Apptainer?
Apptainer is a container platform. It allows you to create and run containers that package up pieces of software in a way that is portable and reproducible. It's like Docker, but for HPC systems.

!!! tip "There is no setup required but Apptainer is only available on compute nodes."

## How to import an image
1.	Select a Docker image on Docker Hub or another registry.  
2.	Pull and convert it with  
```sh
# request a CPU job
srun -p {partition} -c 1 --pty bash
# example
apptainer pull docker://{repository}/{image}:{tag}      
# import ubuntu image  
apptainer pull docker://ubuntu:24.04   
```
3.	Apptainer downloads the layers and transparently bundles them into a `.sif` file.

## How to build an image
Start by connecting to a compute node; a single CPU will be enough but requesting more can speed up the build.
```sh
srun -p {partition} -c 1 --pty bash
``` 

Next, make a directory on your home dir for container building:
```sh
mkdir -p "/data/$USER/apptainer/build/"
cd "/data/$USER/apptainer/build/"
```

Now pull an existing image to a new folder for building the new image. We will use a stock docker image with cuda 12.8 support. We name this image `pytorch_container`, but that can be replaced as you like:

this step pulls the docker image
```sh
apptainer build --sandbox pytorch_container docker://nvidia/cuda:12.8.1-cudnn-devel-ubuntu24.04
```
After getting the base image, we need to start up the container in `writable` mode to install the software we want:
```sh
# --writable allows for writing to the container, necessary for installing new software
# --no-home prevents issues with NFS home directories and writable containers
# --nv allows for gpu support
# --fakeroot is required for installing packages in the container as root, in particular using apt
apptainer shell --no-home --nv --writable --fakeroot pytorch_container
```
Now we should have a shell inside the container, where we will install software. In general the flow should be apt packages first, then conda packages, and then finally pip packages.
```sh
# make sure package lists are current
apt update -y && apt upgrade -y

# install generally useful packages
apt install -y git wget vim
apt clean && rm -rf /var/lib/apt/lists/*

# create a location inside the container for a miniconda installation
mkdir /conda_tmp
cd /conda_tmp

# install miniconda
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
bash Miniconda3-latest-Linux-x86_64.sh -b -p /conda_tmp/mc3
rm Miniconda3-latest-Linux-x86_64.sh
eval "$(/conda_tmp/mc3/bin/conda 'shell.bash' 'hook')"

# install pytorch with cuda 12.8 support
conda install -y -c pytorch -c nvidia pytorch pytorch-cuda=12.8 torchvision torchaudio

# install any other python packages needed

# exit the container
exit
```
After we install software in the container in writable mode, we need to build the container to an image so that we can use it for running software in readable mode. To do this, outside the container run, this step will take a while:
```sh
apptainer build pytorch_container.sif pytorch_container
```
After the build has finished, we should have a single image file that is the whole container. Typically this file is quite large (~10G).
```sh
# clear the apptainer cache which takes up a lot of space
rm -r /data/$USER/.apptainer/cache

# copy the image
mkdir /data/$USER/apptainer/build/
cp pytorch_container.sif /data/$USER/apptainer/pytorch_container.sif

# (optional) clean up build directory 
cd ~
rm -r /data/$USER/apptainer/build/
```
After this step has finished, logout from the compute node:
```sh
exit  # logout
```

## How to run a container
There are two ways to use the container, interactive and non-interactive. We will go through examples of both.

### Interactive jobs

First, allocate a compute node in interactive mode:
```sh
srun -p {partition} -G 1 --pty bash
```
Next, enter the container and activate the python environment we installed:
```sh
# enter the container:
# --nv is needed for gpu access
apptainer shell --nv /data/$USER/apptainer/pytorch_container.sif
# activate miniconda environment
eval "$(/conda_tmp/mc3/bin/conda 'shell.bash' 'hook')"
```
A simple test of our install is to run the python shell and see if we have GPU access:
```sh
python
import torch
a = torch.ones(1)
a.cuda()
```
If this works and a is on the GPU, all is well!

### Batch jobs
To run the container in batch mode we will need two scripts: the first will be an sbatch script to launch the job on the cluster, and the second will be a script that runs inside the container environment, containing all of the python code.

First, create a `test_pytorch.py` file to test our python environment:
```py
import torch
a = torch.ones(1)
print(a.cuda())
```

Then, create a `test_pytorch.sh` script to run inside the container:
```sh
#!/bin/bash
eval "$(/conda_tmp/mc3/bin/conda 'shell.bash' 'hook')"
cd ~
python test_pytorch.py
```

Next, create an `test_pytorch.sbatch` script to launch our job, which should look like:
```sh
#!/bin/bash
#SBATCH --partition={gpu-enabled-partition}
#SBATCH --gpus=1

cd ~
apptainer exec --nv /data/$USER/apptainer/pytorch_container.sif bash test_script.sh
```

Finally, launch the job
```sh
sbatch test_pytorch.sbatch
```