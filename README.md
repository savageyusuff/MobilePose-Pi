# MobilePose-Pi

 This is a deployment of [MobilePose-pytorch](https://github.com/YuliangXiu/MobilePose-pytorch) for Raspberry Pi.  
 You can download this repo into Pi using ```git clone https://github.com/ba-san/MobilePose-Pi```.  
 Please note that this repo's size is around 80MB.
## Results
  
MobilenetV2: FPS is 0.66
```shell
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
 
 Resnet: FPS is 0.39
 ```shell
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
 Rasbian stretch  
 Python 2.7  

## Installation
Please install following things into your Pi.

PyTorch-0.2.0(499MB) - Please refer to [this website](https://wormtooth.com/20180617-pytorch-on-raspberrypi/).  
torchvision-0.2.1(2.7MB)  - Please install it from **source**. Repo is [here](https://github.com/pytorch/vision).  
OpenCV-3.4.0(2.5GB) - You can follow the installation guide matching your pi model from [this page](https://www.pyimagesearch.com/opencv-tutorials-resources-guides/).   

Also, don't forget to install libraries.
```shell
pip install -r requirements.txt
```
 
## Execution
For mobilenet:   
 ```shell
python eval.py --model mobilenet
```
For resnet:  
```shell
python eval.py --model resnet
```
 
 *I just reused the same models MobilePose-pytorch author provided, but you can use your own models.
 
**Note**: I use 20 images picked up from MPII randomly for test dataset.
 
## Citation

Original Repo:  
https://github.com/YuliangXiu/MobilePose-pytorch  

PyTorch installation:  
https://wormtooth.com/20180617-pytorch-on-raspberrypi/

torchvision installation:  
https://github.com/pytorch/vision  

OpenCV installation:  
https://www.pyimagesearch.com/2017/09/04/raspbian-stretch-install-opencv-3-python-on-your-raspberry-pi/  

## License

You can use it freely for non-commercial use.  
