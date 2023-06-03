### enable screen sharing on jetson
```
gsettings set org.gnome.Vino require-encryption false
```
### jetson-stats is a package for monitoring and control
```
sudo pip3 install -U jetson-stats
```


# Install PyTorch on Jetson Nano.
Installing process based on: 
https://qengineering.eu/install-pytorch-on-jetson-nano.html
<br><br>
Pytorch 2.0 and above uses CUDA 11. The Jetson Nano has CUDA 10.2.
Due to low-level GPU incompatibility, installing CUDA 11 on your Nano is impossible.
Pytorch 2.0 can only be installed on Jetson family members using a JetPack 5.0 or higher, such as the Jetson Nano Orion.
Unfortunately, it does not appear that this version will also be available for the Jetson Nano soon.
<br><br>
PyTorch 1.13, 1.12, 1.11.
PyTorch version 1.11 and above requires Python 3.7, found in JetPack 5.0.
Since JetPack 4.6 has Python 3.6, you cannot install PyTorch 1.11.0 on a Jetson Nano.
It looks like Nvidia has no plans to release the new JetPack 5.0 for the Jetson Nano for now. It's only available for the Xavier series.
<br><br>
However, you can use the current version of Jetson Nano with Ubuntu 20.04. We supply the wheels for this version at GitHub.
<br><br>

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
cd pytorch
```
### one command to install several dependencies in one go
installs future, numpy, pyyaml, requests
setuptools, six, typing_extensions, dataclasses
```
sudo pip3 install -r requirements.txt
```

# Enlarge memory swap.
<br><br>
Building the full PyTorch requires more than 4 Gbytes of RAM and the 2 Gbytes of swap space delivered by zram usually found on your Jetson Nano. We have to install dphys-swapfile to get the additional space from your SD card temporarily. After the compilation, the mechanism will be removed, eliminating swapping to the SD card.
<br><br>
You need to increase the dphys swap beyond the regular 2048 limit. It is done by first changing the maximum boundary in /sbin/dphys-swapfile to 4096. Next, set the /etc/dphys-swapfile. The slideshow will guide you. If there is not enough swap memory, the compilation will generate obcure CalledProcessErrors.
<br><br>
We do not recommend increasing the zram swap limits. You can't just keep compressing system memory in the hopes of getting some extra space. There are limits. It is better that you temporarily use the SD memory. Once PyTorch is installed, you can remove dphys-swapfile again.
Please follow the next commands. Note also the installation of nano, a tiny text editor.
<br><br>
If you don't want to swap to SD memory, you can reduce the number of working cores with the $ export MAX_JOBS variable. If you use two instead of four cores, the compilation will succeed without dphys-swapfile, but it will take much longer to complete. It is up to you.
<br><br>

# a fresh start, so check for updates
```
sudo apt-get update
sudo apt-get upgrade
```
# install nano
```
sudo apt-get install nano
```
# install dphys-swapfile
```
sudo apt-get install dphys-swapfile
```
# enlarge the boundary
```
$ sudo nano /sbin/dphys-swapfile
```
# give the required memory size
$ sudo nano /etc/dphys-swapfile
# reboot afterwards
$ sudo reboot.
