# PyTorch Installation Guide  


This is a documentation on how to install the latest version of pytorch on Rapberry Pi.
This instructions should work on any Raspbery Pi version. This guide is, however, still under edit. Use with caution.

## Pre-Installation

It is recommended to use a 16 GB or 32 GB SD card and load the latest version of the [Raspian OS](https://www.raspberrypi.org/downloads/raspbian/).

Before starting the installation, update and upgrade the OS and ensure that there is a text editor 
install(vim,nano,gedit or other text editor). For this guide, we will be using nano.(nano should be 
pre-installed in the OS)
```shell
sudo apt-get update && sudo apt-get upgrade
```

## Add SWAP memory

To prevent any occurance of ‘Memory exhausted’ or ‘Cannot Allocate Memory’, we would need to increase the swap memory.
```shell
sudo dd if=/dev/zero of=/swap1 bs=1M count=2048
sudo mkswap /swap1
sudo nano /etc/fstab
```
This will open up the fstab file. You may or may not have a swap file. If you see a line of code like,
```shell
/swap0 swap swap
```
You already had a swap. Replace that line with the line of code below. If you dont, add the line of code below.
```shell
/swap1 swap swap
```

Reboot your machine so that raspberry pi recognize the new swap space
```shell
sudo reboot now
```

## Dependencies

Install libraries.  
```shell
sudo apt-get install libopenblas-dev libblas-dev m4 cmake cython python3-dev python3-yaml python3-setuptools
pip3 install --user pyyaml numpy wheel
```

For this installation, we would be using Python 3 as the Pytorch developer recommends to do so. (There is currently some problems that are encountered using Python 2)

## PyTorch installation

Follow the steps below. Bare in mind that the installation takes a few hours when running the 'setup.py' script.

```shell
mkdir pytorch_install && cd pytorch_install
git clone --recursive https://github.com/pytorch/pytorch
cd pytorch
export NO_CUDA=1
export NO_DISTRIBUTED=1
export NO_MKLDNN=1 
export NO_NNPACK=1
export NO_QNNPACK=1
python3 setup.py build && python3 setup.py bdist_wheel
cd dist
ls
pip3 install --user torch-1.1.0a0+dfcafb1-cp35-cp35m-linux_armv7l.whl
cd ..
sudo -E python3 setup.py install
```
In case you want to reinstall, make sure that you uninstall PyTorch first by running ```pip3 uninstall torch``` and ```python3 setup.py clean```

## Check

Once the installation is complete, check if the installation is successful by checking the Pytorch version.

```shell
cd ~ && python3
import torch
print(torch.__version__)
```

If you get something like ```1.1.0a0+dfcafb1```, your installation is successful.  

## Citations
The documentation is based on the following websites.

Main Reference:  
https://medium.com/hardware-interfacing/how-to-install-pytorch-v4-0-on-raspberry-pi-3b-odroids-and-other-arm-based-devices-91d62f2933c7

Pytorch on RaspberryPi | 叶某人的碎碎念:  
https://wormtooth.com/20180617-pytorch-on-raspberrypi/ 

[Raspbian][Pytorch]Raspberry Pi 3 Bに人工知能Pytorch入れてみた。:  
https://tsumikiasobi.net/wordpress/?p=1839
