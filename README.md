# MobilePose-Pi

 This is a deployment of [MobilePose-pytorch](https://github.com/YuliangXiu/MobilePose-pytorch) for Raspberry Pi.  
 You can download this repo into PC using ```git clone https://github.com/ba-san/MobilePose-Pi```.  
 Please note that this repo's size is around 80MB.
## Results
*FPS is execution time of forward pass per image.  
**Note**:As you can see, each model has room to be improved. I'd appreciated if there are any ideas or opinions!  

1.0 ShufflenetV2: FPS is 1.09 and Model size is 5.3MB  
From [paper](https://arxiv.org/pdf/1807.11164.pdf), FPS is estimated around 1.8

Author's environment:
>ARM.
>A Qualcomm Snapdragon 810. We use a highly-optimized Neon-based
>implementation. A single thread is used for evaluation.
([ShuffleNet V2: Practical Guidelines for Efficient
CNN Architecture Design](https://arxiv.org/pdf/1807.11164.pdf) p.3)  

my environment:


0.66*(24.4/8.9)=1.8
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
 
## Things To Be Done  
1.Add shufflenet result&training scripts--**Done**  
2.Visualize results  
3.Add my detailed experiment information    
4.Deploy PyTorch model  
5.Convert PyTorch to Caffe2 via ONNX  
6.Scripts to run by Caffe2 (C++)  
7.Add better instruction--**Done**  
 
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
