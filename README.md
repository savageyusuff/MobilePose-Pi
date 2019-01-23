# MobilePose-Pi

 This is a deployment of [MobilePose-pytorch](https://github.com/YuliangXiu/MobilePose-pytorch) for Raspberry Pi.  
 You can download this repo into PC using ```git clone https://github.com/ba-san/MobilePose-Pi```.  

## Structure  

|  Files  |  Explanation  |
| ---- | ---- |
|  cocoapi  |  this is from https://github.com/cocodataset/cocoapi  |
|  mobilepose-pi  |  run file for mobile device  |
|  models  |  pretrained models  |
|  pose_dataset  |  MPII dataset  |
|  results  |  keypoints of each model's grountruth & prediction  |
|  OpenCV_Installation_Guide.md  |  OpenCV installation guide  |
|  PyTorch_Installation_Guide.md  |  PyTorch installation guide  |
|  README.md  |  general explanation about this repo  |
|  ShuffleNetV2.py  |  network architecture of ShufflenetV2  |
|  Study_on_results.md  |  study on validation of our results  |
|  coco_utils.py  |  generating groundtruth&prediction json files  |
|  dataloader.py  |  multi-thread dataloader with augmentations  |
|  dataset_factory.p  |  get dataset's keypoint from csv files  |
|  estimator.py  |  this is for run_webcam.py  |
|  eval_pc.py  |  scripts to evaluate each model  |
|  mobilenetv2.py  |  network architecture of MobilenetV2  |
|  networks.py  |  get model's path and input's height&wid & network architecture of Resnet  |
|  pycocotools  |  link to cocoapi/PythonAPI/pycocotools  |
|  requirements.txt  |  libraries needed to run scripts  |
|  run_webcam.py  |  real-time pose estimation using webcam  |
|  training.py  |  training models  |


**Note**: MPII is used for training and COCO is used for evaluation.  

## Results
  
**Note**:As you can see, each model has room to be improved. Any ideas or opinions are welcome!  

|  Network  |  FPS  |  Size(MB)  |  mAP  |
| ---- | ---- | ---- | ---- |
|  1.0 ShufflenetV2  |  1.09  |  5.3  |  0.000  |
|  1.0 MobilenetV2  |  0.66  |  9.3  |  0.045  |
|  Resnet18  |  0.39  |  44.9  |  0.257  |
*FPS is execution time of forward pass per image.

 You can get more detailed info for this results [here](https://github.com/ba-san/MobilePose-Pi/blob/master/Study_on_results.md).  
 
## Requirements
For 'mobilepose-pi', you need following environment.

 Raspberry Pi (I used Pi 2 Model B for this repo)  
 Rasbian stretch (32bit)  
 Python 2.7  

## Installation
Before installation, please change swap size.

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
Now you can install following things into your Pi.

PyTorch-0.2.0(499MB) - Follow [my guide](https://github.com/ba-san/MobilePose-Pi/blob/master/PyTorch_Installation_Guide.md).  
torchvision-0.2.1(2.7MB)  - Please install it from **source**. Repo is [here](https://github.com/pytorch/vision).  
OpenCV-3.4.0(1.8GB) - Follow [my guide](https://github.com/ba-san/MobilePose-Pi/blob/master/OpenCV_Installation_Guide.md).  

Also, don't forget to install libraries.
```shell
pip install -r requirements.txt
```

At the end, change CONF_SWAPSIZE to 100 again.   
 
## Execution
You can evaluate your network on PC first.  
If the result seems to be good, you can try it on Pi using 'mobilepose-pi'.  

For mobilenet:   
 ```shell
python eval_pc.py --model mobilenet
```
For resnet:  
```shell
python eval_pc.py --model resnet
```
For shufflenet:  
```shell
python eval_pc.py --model shufflenet
```
 
 *I just reused the same models MobilePose-pytorch author provided. For shufflenet I used my original model.  
 Of course, you can use your own models also.  
 
 You can try real-time estimation using 'run_webcam.py'  
 (I didn't change this file from original repo.)  
 Please connect webcam to PC first. Then try this.  
 ```shell
python run_webcam.py --model [name of model]
```
Currently, this doesn't support shufflenet.  
 
## Training
You can train three models (shufflenet/mobilenet/resnet) at your **PC**.  

You need to download MPII training [Images(12.9GB)](https://datasets.d2.mpi-inf.mpg.de/andriluka14cvpr/mpii_human_pose_v1.tar.gz). This is from [here](http://human-pose.mpi-inf.mpg.de/#download).  
After extraction, please set ROOT_DIR at dataloader.py (line.197).  

Different from [MobilePose-pytorch](https://github.com/YuliangXiu/MobilePose-pytorch)(original repo), the command is  
```python train.py --model=[name_of_model_you_want_to_train] --retrain=[bool]```

If you want to train shufflenet, you can do it just change model name.  
(i.e. ```python train.py --model=shufflenet```)  

## Model conversion
**Note**: development of this feature is currently suspended.  

For conversion, I mainly adopted [this tutorial](https://pytorch.org/tutorials/advanced/super_resolution_with_caffe2.html#transfering-srresnet-using-onnx).  
I recommend to do this via conda.  

1.You need to set up PC environment.  

[Caffe2](https://caffe2.ai/docs/getting-started.html?platform=ubuntu&configuration=prebuilt)  
[ONNX](https://github.com/onnx/onnx)  
[PyTorch](https://github.com/pytorch/pytorch#from-source)  

## Things To Be Done  
1.Add shufflenet result&training scripts--**Done**  
2.Add my detailed experiment information    
3.Deploy PyTorch model  
4.Convert PyTorch to Caffe2 via ONNX  
5.Scripts to run by Caffe2 (C++)    

## Citation

Original Repo:  
https://github.com/YuliangXiu/MobilePose-pytorch  

ShufflenetV2 paper:  
https://arxiv.org/pdf/1807.11164.pdf

ShufflenetV2 implementation:  
https://github.com/ericsun99/Shufflenet-v2-Pytorch

ONNX:  
https://github.com/onnx/onnx

PyTorch installation:  
https://wormtooth.com/20180617-pytorch-on-raspberrypi/

torchvision installation:  
https://github.com/pytorch/vision  

OpenCV installation:  
https://www.pyimagesearch.com/2017/09/04/raspbian-stretch-install-opencv-3-python-on-your-raspberry-pi/  
