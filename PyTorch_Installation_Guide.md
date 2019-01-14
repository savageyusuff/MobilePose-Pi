# PyTorch Installation Guide  

There are some documents explaining PyTorch installation into Raspberry Pi, but most of them are not straightforward for this project.  
Here, I explain my actual procedure. So you can follow it.  

## 1.Swap  
At Pi terminal, open 'dphys-swapfile'.   
```shell
sudo nano /etc/dphys-swapfile
```
and change CONF_SWAPSIZE. (default is set to 100.)  
```shell
CONF_SWAPSIZE=2048
```
Activate it.  
```shell
sudo /etc/init.d/dphys-swapfile stop
sudo /etc/init.d/dphys-swapfile start
```

## 2.Dependencies

Install libraries.  
```shell
sudo apt-get install libopenblas-dev cython3 libatlas-dev \
    m4 libblas-dev cmake
pip install --user pyyaml numpy mkl mkl-include setuptools cmake cffi typing
```

## 3.PyTorch installation

Just follow below.  

```shell
git clone --recursive https://github.com/pytorch/pytorch
cd pytorch
git checkout tags/v1.0.0 -b build
git submodule update --init --recursive
export NO_CUDA=1
export NO_DISTRIBUTED=1
python setup.py build
pip install --user wheel
python setup.py bdist_wheel
cd dist
ls
pip install --user torch-1.0.0-cp27-cp27m-linux_armv7l.whl
cd ..
sudo -E python setup.py install
```

## 4.Check
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
I mainly follwed 'Pytorch on RaspberryPi | 叶某人的碎碎念'.  
If something goes wrong, please take a look on it.  

Pytorch on RaspberryPi | 叶某人的碎碎念:  
https://wormtooth.com/20180617-pytorch-on-raspberrypi/

[Raspbian][Pytorch]Raspberry Pi 3 Bに人工知能Pytorch入れてみた。:  
https://tsumikiasobi.net/wordpress/?p=1839
