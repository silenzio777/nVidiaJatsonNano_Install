## ROS Lidars:

https://github.com/YDLIDAR/YDLidar-SDK/tree/master
https://github.com/YDLIDAR/ydlidar_ros_driver/tree/master

___

## add package to ROS:

```
cd ~/[PROJECT]/src

git clone https://github.com/ros-planning/navigation_msgs.git

sudo apt-get install ros-noetic-slam-gmapping

sudo apt-get install ros-noetic-move-base

```
____

## ROS2 projects:

https://github.com/silenzio777/jetbot-ros2


## ROS projects:

https://github.com/elephantrobotics

## OMNI WHEELS CAR:
https://github.com/elephantrobotics/myagv_ros

https://github.com/elephantrobotics/mycobot_ros


https://github.com/silenzio777/jetbot-ros2

___

### ROS2 install:
## ROS2 versions:

https://docs.elephantrobotics.com/docs/gitbook-en/12-ApplicationBaseROS/12.2-ROS2/12.2.1-ROS2%E7%9A%84%E5%AE%89%E8%A3%85.html

ROS2 version        Ubuntu version<br>
Foxy	            Ubuntu 20.04(Focal Fossa)<br>
**Galactic	        Ubuntu 20.04(Focal Fossa)**<br>
Humble	            Ubuntu 22.04(Jammy Jellyfish)<br>

http://docs.ros.org/en/foxy/Releases.html


https://docs.ros.org/en/iron/Installation/Ubuntu-Install-Debians.html


# Ubuntu 20.04 galactic version
```
sudo apt install ros-galactic-desktop

echo "source /opt/ros/galactic/setup.bash" >> ~/.bashrc

source ~/.bashrc

sudo apt install ros-galactic-joint-state-publisher-gui

ros2

...

roslaunch myagv_navigation myagv_slam_laser.launch

```

________

### OMNI weels ROS platform:


## Mobile Robot MPO-500
https://github.com/neobotix/neo_kinematics_mecanum2<br>
https://neobotix-docs.de/ros/ros2/installation.html

## neo_kinematics_mecanum2<br>
https://github.com/pal-robotics/omni_base_robot/tree/melodic-devel
__________
<br>

### Install Ubuntu on MAC M2
https://www.youtube.com/watch?v=O19mv1pe76M&t=0s

Ubuntu 22.04 ARM64 -
https://ubuntu.com/download/server/arm

UTM - https://mac.getutm.app/

Enable Directory Sharing -  https://docs.getutm.app/guest-support...

https://docs.getutm.app/guest-support/linux/


__________________________
 **  Commands **
______________________________
```
sudo apt update && sudo apt upgrade -y

sudo apt install ubuntu-desktop

reboot

sudo apt install spice-vdagent spice-webdavd
```

```
sudo mkdir [mount point]

sudo mount -t 9p -o trans=virtio share [mount point] -oversion=9p2000.L
```

>add this line to /etc/fstab
```
share	[mount point]	9p	trans=virtio,version=9p2000.L,rw,_netdev,nofail	0	0

sudo nano /etc/fstab
```
>save and exit

```
sudo chown -R $USER [mount point]

reboot
```






__________
<br>

-----------

https://forums.developer.nvidia.com/t/unreliable-serial-communcation-via-the-uart-tx-rx-gpio-pins/158249/21
!!!
This helped me to get correct data. You need to connect pull down ~10 kOhm resistor from RX and TX (GPIO 8, 10 pins) to the jetson nano’s ground.
!!!
_
You can plug the UART into another TTL type of device by just wiring the two directly together, but note the 3.3V signal. Many serial devices, such as some Arduinos, use 5V. The Jetson Nano is not tolerant of 5V, and if you connect directly bad things can happen. If you are using a 5V device with the Jetson Nano, you will need to do some level shifting to get the levels to match.
_


https://forums.developer.nvidia.com/t/connecting-jetson-nano-to-arduino-uno/172775/9


Python script:

import serial

print("UART Demonstration Program")
print("NVIDIA Jetson Nano Developer Kit")


serial_port = serial.Serial(
    port="/dev/ttyTHS1",
    baudrate=115200,
    bytesize=serial.EIGHTBITS,
    parity=serial.PARITY_NONE,
    stopbits=serial.STOPBITS_ONE,
)
# Wait a second to let the port initialize
time.sleep(1)

try:
    # Send a message to the Arduino
    serial_port.write("500 500".encode())
    while True:
        if serial_port.inWaiting() > 0:
            data = serial_port.readline().decode()
            print(data)
            
except KeyboardInterrupt:
    print("Exiting Program")

except Exception as exception_error:
    print("Error occurred. Exiting Program")
    print("Error: " + str(exception_error))

finally:
    serial_port.close()
    pass

Arduino script:

int data1;
int data2;

void setup() {
  // put your setup code here, to run once:
  Serial.begin(115200);
}

void loop() {
  // put your main code here, to run repeatedly:
  if (Serial.available())
  {
    delay(10);
    data1 = Serial.readStringUntil(' ').toInt();
    data2 = Serial.readStringUntil(' ').toInt();
    delay(10);
    Serial.print("\nReceived Data:");
    Serial.print(data1, data2);
  }
}

    

__
I would suggest you use the jetson nano 40 pin header to communicate with the Uno tx/rx pins. Have you checked the pin assignments of the 40 pin header with:

$ sudo /opt/nvidia/jetson-io/jetson-io.py

_____________

Porting OpenAI Whisper speech recognition to edge devices with hardware ML accelerators, enabling always-on live voice transcription. Current work includes Jetson Nano and Coral Edge TPU.
https://github.com/silenzio777/whisper-edge

https://www.youtube.com/watch?v=WHiAPA1pib4

https://github.com/maxbbraun/whisper-edge/issues/3

https://github.com/openai/whisper/discussions/1124

_____________________________________
Real-time object detection
https://youtu.be/fwoonl5JKgo
https://www.youtube.com/watch?v=PkRE10YPt3I


The World's Leading Cross Platform AI Engine for Edge Devices, with over 10 million installs on Docker Hub.
https://github.com/johnolafenwa/DeepStack




60$ face recognision Python and Nvidia Jetson Nano 2GB
https://habr.com/ru/companies/skillfactory/articles/544430/
origin- 
https://medium.com/@ageitgey/build-a-face-recognition-system-for-60-with-the-new-nvidia-jetson-nano-2gb-and-python-46edbddd7264



Real-time Face detection on Jetson Nano using OpenCV
https://maker.pro/nvidia-jetson/tutorial/real-time-face-detection-on-jetson-nano-using-opencv



Using Jetson Nano and a Raspberry Pi Camera for Video Streaming
https://maker.pro/nvidia-jetson/tutorial/streaming-real-time-video-from-rpi-camera-to-browser-on-jetson-nano-with-flask


A simple to use camera interface for the Jetson Nano for working with USB, CSI, IP and also RTSP cameras or streaming video in Python 3.
https://github.com/thehapyone/NanoCamera

https://github.com/AarohiSingla/python_examples/tree/main



This Getting Started will guide you through setting up your Jetson Nano and configuring it for AI image processing using the Pi Camera Module V2 with Python
https://www.okdo.com/getting-started/get-started-with-jetson-nano-4gb-and-csi-camera/



ArduCam - https://docs.arducam.com/Nvidia-Jetson-Camera/Jetvariety-Camera/Quick-Start-Guide/

How to install OpenCV 4.5.2 with CUDA 11.2 and CUDNN 8.2 in Ubuntu 20.04
https://gist.github.com/raulqf/f42c718a658cddc16f9df07ecc627be7


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
