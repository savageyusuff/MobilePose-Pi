# MobilePose-Pi

 this is an deployment of [MobilePose-pytorch](https://github.com/YuliangXiu/MobilePose-pytorch) for Raspberry Pi.
 
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
 models - download from [original repo](https://github.com/YuliangXiu/MobilePose-pytorch)

## installation


PyTorch 
torchvision
OpenCV

```shell
pip install -r requirements.txt
```
 
## how to run
 
## Citation

Original Repo:
https://github.com/YuliangXiu/MobilePose-pytorch

PyTorch installation:
https://www.pyimagesearch.com/2017/09/04/raspbian-stretch-install-opencv-3-python-on-your-raspberry-pi/
https://wormtooth.com/20180617-pytorch-on-raspberrypi/
