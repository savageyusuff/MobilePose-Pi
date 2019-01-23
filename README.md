# MobilePose-Pi

 This is a deployment of [MobilePose-pytorch](https://github.com/YuliangXiu/MobilePose-pytorch) for Raspberry Pi.  
 You can download this repo into PC using ```git clone https://github.com/ba-san/MobilePose-Pi```.  

## Architecture  

 cocoapi 	                         this is from https://github.com/cocodataset/cocoapi  
	mobilepose-pi 	                   run file for mobile device  
	models 	                          pretrained models  
	pose_dataset 	                    mpii dataset  
	results 	                         keypoints of each model's groundtruth & prediction  
	OpenCV_Installation_Guide.md 	    OpenCV installation guide  
	PyTorch_Installation_Guide.md 	   PyTorch installation guide  
	README.md 	                       general explanation about this repo  
	ShuffleNetV2.py 	                 network architecture of ShufflenetV2  
	Study_on_results.md 	             study on validation of our results  
	coco_utils.py 	                   generating groundtruth&prediction json files  
	dataloader.py                     multi-thread dataloader with augmentations  
	dataset_factory.py 	              get dataset's keypoint from csv files  
	estimator.py 	                    this is for run_webcam.py  
	eval_pc.py 	                      scripts to evaluate each model  
	mobilenetv2.py 	                  network architecture of MobilenetV2  
	networks.py 	                     get model's path and input's height&wid & network architecture of Resnet  
	pycocotools                       link to cocoapi/PythonAPI/pycocotools  
	requirements.txt 	                libraries needed to run scripts here  
	run_webcam.py 	                   real-time pose estimation using webcam  
	training.py                       training models  

Note: MPII is used for training and COCO is used for evaluation.  

## Results
*FPS is execution time of forward pass per image.  
**Note**:As you can see, each model has room to be improved. I'd appreciated if any ideas or opinions provided!  

1.0 ShufflenetV2: FPS is 1.09 and Model size is 5.3MB  
```python 
 Average Precision  (AP) @[ IoU=0.50:0.95 | area=   all | maxDets= 20 ] = 0.000
 Average Precision  (AP) @[ IoU=0.50      | area=   all | maxDets= 20 ] = 0.000
 Average Precision  (AP) @[ IoU=0.75      | area=   all | maxDets= 20 ] = 0.000
 Average Precision  (AP) @[ IoU=0.50:0.95 | area=medium | maxDets= 20 ] = -1.000
 Average Precision  (AP) @[ IoU=0.50:0.95 | area= large | maxDets= 20 ] = 0.000
 Average Recall     (AR) @[ IoU=0.50:0.95 | area=   all | maxDets= 20 ] = 0.000
 Average Recall     (AR) @[ IoU=0.50      | area=   all | maxDets= 20 ] = 0.000
 Average Recall     (AR) @[ IoU=0.75      | area=   all | maxDets= 20 ] = 0.000
 Average Recall     (AR) @[ IoU=0.50:0.95 | area=medium | maxDets= 20 ] = -1.000
 Average Recall     (AR) @[ IoU=0.50:0.95 | area= large | maxDets= 20 ] = 0.000
```

1.0 MobilenetV2: FPS is 0.66 and Model size is 9.3MB
```python
 Average Precision  (AP) @[ IoU=0.50:0.95 | area=   all | maxDets= 20 ] = 0.045
 Average Precision  (AP) @[ IoU=0.50      | area=   all | maxDets= 20 ] = 0.267
 Average Precision  (AP) @[ IoU=0.75      | area=   all | maxDets= 20 ] = 0.000
 Average Precision  (AP) @[ IoU=0.50:0.95 | area=medium | maxDets= 20 ] = -1.000
 Average Precision  (AP) @[ IoU=0.50:0.95 | area= large | maxDets= 20 ] = 0.052
 Average Recall     (AR) @[ IoU=0.50:0.95 | area=   all | maxDets= 20 ] = 0.115
 Average Recall     (AR) @[ IoU=0.50      | area=   all | maxDets= 20 ] = 0.500
 Average Recall     (AR) @[ IoU=0.75      | area=   all | maxDets= 20 ] = 0.000
 Average Recall     (AR) @[ IoU=0.50:0.95 | area=medium | maxDets= 20 ] = -1.000
 Average Recall     (AR) @[ IoU=0.50:0.95 | area= large | maxDets= 20 ] = 0.115
 ```
 
 Resnet18: FPS is 0.39 and Model size is 44.9MB
 ```python
 Average Precision  (AP) @[ IoU=0.50:0.95 | area=   all | maxDets= 20 ] = 0.257
 Average Precision  (AP) @[ IoU=0.50      | area=   all | maxDets= 20 ] = 0.642
 Average Precision  (AP) @[ IoU=0.75      | area=   all | maxDets= 20 ] = 0.208
 Average Precision  (AP) @[ IoU=0.50:0.95 | area=medium | maxDets= 20 ] = 0.309
 Average Precision  (AP) @[ IoU=0.50:0.95 | area= large | maxDets= 20 ] = 0.269
 Average Recall     (AR) @[ IoU=0.50:0.95 | area=   all | maxDets= 20 ] = 0.410
 Average Recall     (AR) @[ IoU=0.50      | area=   all | maxDets= 20 ] = 0.800
 Average Recall     (AR) @[ IoU=0.75      | area=   all | maxDets= 20 ] = 0.450
 Average Recall     (AR) @[ IoU=0.50:0.95 | area=medium | maxDets= 20 ] = 0.500
 Average Recall     (AR) @[ IoU=0.50:0.95 | area= large | maxDets= 20 ] = 0.400
 ```
 You can get more detailed info for this results [here](https://github.com/ba-san/MobilePose-Pi/blob/master/Study_on_results.md).  
 
## Requirements

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
First of all, please put 'mobilepose-pi' directory on your Pi.
Please note that this directory's size is around 80MB.

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
 
**Note**: I use 20 images picked up from [MPII](http://human-pose.mpi-inf.mpg.de/) randomly for test dataset.
 
## Training
You can train three models (shufflenet/mobilenet/resnet) at your **PC**.  
For instllation, please follow instructions written in there.  

You need to download mpii training [Images(12.9GB)](https://datasets.d2.mpi-inf.mpg.de/andriluka14cvpr/mpii_human_pose_v1.tar.gz). This is from [here](http://human-pose.mpi-inf.mpg.de/#download).  
After extraction, please set ROOT_DIR at dataloader.py line.197  

Different from [MobilePose-pytorch](https://github.com/YuliangXiu/MobilePose-pytorch)(original repo), the command is  
```python train.py --model=[name_of_model_you_want_to_train] --retrain=[bool]```

If you want to train shufflenet, you can do it just change model name.  
(i.e. ```python train.py --model=shufflenet```)  

## Model conversion
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
