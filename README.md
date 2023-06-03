# Install PyTorch on Jetson Nano.
Installing process based on: 
https://qengineering.eu/install-pytorch-on-jetson-nano.html

Pytorch 2.0 and above uses CUDA 11. The Jetson Nano has CUDA 10.2.
Due to low-level GPU incompatibility, installing CUDA 11 on your Nano is impossible.
Pytorch 2.0 can only be installed on Jetson family members using a JetPack 5.0 or higher, such as the Jetson Nano Orion.
Unfortunately, it does not appear that this version will also be available for the Jetson Nano soon.
<br>
PyTorch 1.13, 1.12, 1.11.
PyTorch version 1.11 and above requires Python 3.7, found in JetPack 5.0.
Since JetPack 4.6 has Python 3.6, you cannot install PyTorch 1.11.0 on a Jetson Nano.
It looks like Nvidia has no plans to release the new JetPack 5.0 for the Jetson Nano for now. It's only available for the Xavier series.

However, you can use the current version of Jetson Nano with Ubuntu 20.04. We supply the wheels for this version at GitHub.
</br>
## Enable Screen Sharing
```
gsettings set org.gnome.Vino require-encryption false
```

# Installation from scratch.

## Install PyTorch for Python 3.

### Only for a Jetson Nano with Ubuntu 20.04

### get a fresh start
```
sudo apt-get update
sudo apt-get upgrade
```
### the dependencies
```
sudo apt-get install ninja-build git cmake
sudo apt-get install libjpeg-dev libopenmpi-dev libomp-dev ccache
sudo apt-get install libopenblas-dev libblas-dev libeigen3-dev
sudo pip3 install -U --user wheel mock pillow
sudo -H pip3 install testresources
```
### above 58.3.0 you get version issues
```
sudo -H pip3 install setuptools==58.3.0
sudo -H pip3 install scikit-build
```
### download PyTorch 1.13.0 with all its libraries
```
git clone -b v1.13.0 --depth=1 --recursive https://github.com/pytorch/pytorch.git
$ cd pytorch
```
### one command to install several dependencies in one go
### installs future, numpy, pyyaml, requests
### setuptools, six, typing_extensions, dataclasses
```
$ sudo pip3 install -r requirements.txt
```

# Enlarge memory swap.


