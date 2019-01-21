# PyTorch Installation Guide  

This is a documentation on how to install pytorch on Rapberry Pi.

## Add SWAP memory




## Dependencies

Install libraries.  
```shell
sudo apt-get install libopenblas-dev cython3 libatlas-dev \
    m4 libblas-dev cmake python-setuptools python-cffi
pip install --user pyyaml numpy typing
```

## PyTorch installation

Just follow below.  

```shell
git clone --recursive https://github.com/pytorch/pytorch
cd pytorch
git checkout tags/v1.0.0 -b build
git submodule update --init --recursive
export NO_CUDA=1
export NO_DISTRIBUTED=1
export NO_MKLDNN=1
python setup.py build
pip install --user wheel
python setup.py bdist_wheel
cd dist
ls
pip install --user torch-1.0.0-cp27-cp27m-linux_armv7l.whl
cd ..
sudo -E python setup.py install
```

## Check
```shell
cd ~ && python
```
Then, do this.
```shell
import torch
print(torch.__version__)
```
If you get something like ```0.2.0+0b92e5c```, you are successful!  

## Citations
The documentation is based on the following websites.

Main Reference:
https://medium.com/hardware-interfacing/how-to-install-pytorch-v4-0-on-raspberry-pi-3b-odroids-and-other-arm-based-devices-91d62f2933c7

Pytorch on RaspberryPi | 叶某人的碎碎念:  
https://wormtooth.com/20180617-pytorch-on-raspberrypi/ 

[Raspbian][Pytorch]Raspberry Pi 3 Bに人工知能Pytorch入れてみた。:  
https://tsumikiasobi.net/wordpress/?p=1839
