# MobilePose-Pi

 This is a deployment of [MobilePose-pytorch](https://github.com/YuliangXiu/MobilePose-pytorch) for Raspberry Pi.  
 You can download this repo into PC using ```git clone https://github.com/ba-san/MobilePose-Pi```.  

## Results
*FPS is execution time of forward pass per image.  
**Note**:As you can see, each model has room to be improved. I'd appreciated if there are any ideas or opinions!  

1.0 ShufflenetV2: FPS is 1.09 and Model size is 5.3MB  
From [paper](https://arxiv.org/pdf/1807.11164.pdf), I will calculate estimated FPS.

Author's environment:
>ARM.
> A Qualcomm Snapdragon 810. We use a highly-optimized Neon-based
> implementation. A single thread is used for evaluation.
([ShuffleNet V2: Practical Guidelines for Efficient
CNN Architecture Design](https://arxiv.org/pdf/1807.11164.pdf) p.3)  

> 324~388.8GFLOPS  
(https://gpuflops.blogspot.com/2015/02/gpu-flops-list.html?m=1)  

my environment([source](https://www.raspberrypi.org/products/raspberry-pi-2-model-b/))　:
>  A 900MHz quad-core ARM Cortex-A7 CPU  
>  1GB RAM

> Raspberry Pi 2 	Cortex-A7 	7.2 GFLOPS 	0.9GHz 	4 	8 	NEON: 2(mad) x1(simd) x4(core) x0.9(clock) = 7.2 GFLOPS  
(https://dench.flatlib.jp/opengl/cpuflops)  

24.4x(7.2GFLOPS/324GFLOPS)=0.54  

Therefore, the estimated FPS is 0.54.  
This is just a half of actual FPS(1.09).  
I will continue to investigate to know the reason.  

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
 
## Requirements

 Raspberry Pi (I used Pi 2 Model B for this repo)  
 Rasbian stretch (32bit)  
 Python 2.7  

## Installation
Please install following things into your Pi.  

PyTorch-0.2.0(499MB) - Follow [my guide](https://github.com/ba-san/MobilePose-Pi/blob/master/PyTorch_Installation_Guide.md).  
torchvision-0.2.1(2.7MB)  - Please install it from **source**. Repo is [here](https://github.com/pytorch/vision).  
OpenCV-3.4.0(2.5GB) - You can refer to the installation guide matching your pi model from [this page](https://www.pyimagesearch.com/opencv-tutorials-resources-guides/).   

Also, don't forget to install libraries.
```shell
pip install -r requirements.txt
```
 
## Execution
First of all, please put 'mobilepose-pi' directory on your Pi.
Please note that this directory's size is around 80MB.

For mobilenet:   
 ```shell
python eval.py --model mobilenet
```
For resnet:  
```shell
python eval.py --model resnet
```
For shufflenet:  
```shell
python eval.py --model shufflenet
```
 
 *I just reused the same models MobilePose-pytorch author provided. For shufflenet I used my original model.  
 Of course, you can use your own models also.
 
**Note**: I use 20 images picked up from MPII randomly for test dataset.
 
## Training
You can train three models (shufflenet/mobilenet/resnet) at your **PC**.  
For instllation, please follow instructions written in there.  
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
2.Visualize results  
3.Add my detailed experiment information    
4.Deploy PyTorch model  
5.Convert PyTorch to Caffe2 via ONNX  
6.Scripts to run by Caffe2 (C++)  
7.Add better instruction--**Done**  

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
