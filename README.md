
This Getting Started will guide you through setting up your Jetson Nano and configuring it for AI image processing using the Pi Camera Module V2 with Python
https://www.okdo.com/getting-started/get-started-with-jetson-nano-4gb-and-csi-camera/



ArduCam - https://docs.arducam.com/Nvidia-Jetson-Camera/Jetvariety-Camera/Quick-Start-Guide/



How to Install OpenCV 4.5 on NVIDIA Jetson Nano
https://automaticaddison.com/how-to-install-opencv-4-5-on-nvidia-jetson-nano/

__________
<br>

## Enable screen sharing on jetson
```
gsettings set org.gnome.Vino require-encryption false
```
__________
<br>

## Jetson-stats is a package for monitoring and control
```
sudo pip3 install -U jetson-stats
```
__________
<br>

# Syncthing
## Jatson side:
https://apt.syncthing.net/ -- WORK!

To allow the system to check the packages authenticity, you need to provide the release key.
Add the release PGP keys:
```
sudo curl -o /usr/share/keyrings/syncthing-archive-keyring.gpg https://syncthing.net/release-key.gpg
```

The stable channel is updated with stable release builds, usually every first Tuesday of the month.
Add the "stable" channel to your APT sources:
```
echo "deb [signed-by=/usr/share/keyrings/syncthing-archive-keyring.gpg] https://apt.syncthing.net/ syncthing stable" | sudo tee /etc/apt/sources.list.d/syncthing.list
```

The candidate channel is updated with release candidate builds, usually every second Tuesday of the month. These predate the corresponding stable builds by about three weeks.
Add the "candidate" channel to your APT sources:
```
echo "deb [signed-by=/usr/share/keyrings/syncthing-archive-keyring.gpg] https://apt.syncthing.net/ syncthing candidate" | sudo tee /etc/apt/sources.list.d/syncthing.list
```

And finally.
Update and install syncthing:
```
sudo apt-get update
```
```
sudo apt-get install syncthing
```
<br>

## Mac side:
### Mac install server:
https://syncthing.net/downloads/

### Run server in terminal:
```
cd <syncthing-macos-universal-v1.23.4>
./syncthing
```

### Browser goto:
http://127.0.0.1:8384/


### 



__________
<br>


## CV2 Python
https://pypi.org/project/opencv-python/ - WORK!
### Option 2 - Full package (contains both main modules and contrib/extra modules): 
```
pip install opencv-contrib-python
```
__________
<br>


## Installing Sublime Text 3 on Ubuntu 20.04:
https://linuxize.com/post/how-to-install-sublime-text-3-on-ubuntu-20-04/  - WORK!
```
sudo apt update
sudo apt install dirmngr gnupg apt-transport-https ca-certificates software-properties-common
```

```
curl -fsSL https://download.sublimetext.com/sublimehq-pub.gpg | sudo apt-key add -
sudo add-apt-repository "deb https://download.sublimetext.com/ apt/stable/"
```
```
sudo apt install sublime-text
```
__________
<br>

# Install PyTorch on Jetson Nano. - WORK!

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

===============

Only for a Jetson Nano with Ubuntu 20.04

### install the dependencies (if not already onboard)
$ sudo apt-get install python3-pip libjpeg-dev libopenblas-dev libopenmpi-dev libomp-dev
$ sudo -H pip3 install future
$ sudo pip3 install -U --user wheel mock pillow
$ sudo -H pip3 install testresources
### above 58.3.0 you get version issues
$ sudo -H pip3 install setuptools==58.3.0
$ sudo -H pip3 install Cython
### install gdown to download from Google drive
$ sudo -H pip3 install gdown
### download the wheel
$ gdown https://drive.google.com/uc?id=1e9FDGt2zGS5C5Pms7wzHYRb0HuupngK1
###  install PyTorch 1.13.0
$ sudo -H pip3 install torch-1.13.0a0+git7c98e70-cp38-cp38-linux_aarch64.whl
### clean up
$ rm torch-1.13.0a0+git7c98e70-cp38-cp38-linux_aarch64.whl

this work!

__________
<br>

# Installation from scratch.  - !NOT WORK!

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

__________
<br>

# Enlarge memory swap.
<br>
Building the full PyTorch requires more than 4 Gbytes of RAM and the 2 Gbytes of swap space delivered by zram usually found on your Jetson Nano. We have to install dphys-swapfile to get the additional space from your SD card temporarily. After the compilation, the mechanism will be removed, eliminating swapping to the SD card.
<br><br>
You need to increase the dphys swap beyond the regular 2048 limit. It is done by first changing the maximum boundary in /sbin/dphys-swapfile to 4096. Next, set the /etc/dphys-swapfile. The slideshow will guide you. If there is not enough swap memory, the compilation will generate obcure CalledProcessErrors.
<br><br>
We do not recommend increasing the zram swap limits. You can't just keep compressing system memory in the hopes of getting some extra space. There are limits. It is better that you temporarily use the SD memory. Once PyTorch is installed, you can remove dphys-swapfile again.
Please follow the next commands. Note also the installation of nano, a tiny text editor.
<br><br>
If you don't want to swap to SD memory, you can reduce the number of working cores with the $ export MAX_JOBS variable. If you use two instead of four cores, the compilation will succeed without dphys-swapfile, but it will take much longer to complete. It is up to you.
<br><br>

### a fresh start, so check for updates
```
sudo apt-get update
sudo apt-get upgrade
```
### install nano
```
sudo apt-get install nano
```
### install dphys-swapfile
```
sudo apt-get install dphys-swapfile
```
### enlarge the boundary
```
sudo nano /sbin/dphys-swapfile
```
![SwapMaxJetsonPy1](https://github.com/silenzio777/nVidiaJatsonNano_Install/assets/7931919/1c16fd46-367c-4e81-b86b-884009f3e8f2)

in line "CONF_SWAPSIZE="
change add 4096

### give the required memory size
```
sudo nano /etc/dphys-swapfile
```
![SwapMaxJetsonPy2](https://github.com/silenzio777/nVidiaJatsonNano_Install/assets/7931919/ff9aaba6-d87b-4e87-9445-a103807ac233)

in line "CONF_MAXSWAP=2048"
change 2048 to 4096

```
free -m
```
![SwapMaxJetsonPy3](https://github.com/silenzio777/nVidiaJatsonNano_Install/assets/7931919/dd4f279c-e100-4a8d-ad31-ddf31baead1b)


### reboot afterwards

```
sudo reboot
```
__________
<br>

++++++

https://gist.github.com/raulqf/f42c718a658cddc16f9df07ecc627be7

++++++


https://stackoverflow.com/questions/74600691/nvidia-jetson-nano-vnc-connection-without-hdmi-plugged-in-headless

https://forums.developer.nvidia.com/t/jetson-nano-vnc-headless-connections/77399/17
__

__________
<br>
