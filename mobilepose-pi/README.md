# Running Code for evaluating model on raspberry pi

## Dependencies

Install libraries.  
```shell
pip3 install tqdm
sudo apt-get install libatlas-base-dev
pip3 install scikit-image
pip3 install scipy matplotlib
pip3 install opencv-python
sudo apt-get install libjpeg-dev libtiff5-dev libjasper-dev libpng12-dev ## Depedencies for opencv
sudo apt-get install libatlas3-base libsz2 libharfbuzz0b libtiff5 libjasper1 libilmbase12 libopenexr22 libilmbase12 libgstreamer1.0-0 libavcodec57 libavformat57 libavutil55 libswscale4 libqtgui4 libqt4-test libqtcore4 ## Depedencies for opencv
sudo apt-get install libgeos-dev
pip3 install imgaug
pip3 install torchvision-raspi
pip3 install pycocotools
```

## Error Encountered currently.  
```shell
0
Loading testing dataset, wait...
100%|█████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████| 1/1 [00:07<00:00,  7.43s/it]
==> write./results/resnet/result-gt-json.txt
  0%|                                                                                                                                 | 0/1 [00:00<?, ?it/s]Traceback (most recent call last):
  File "eval.py", line 158, in <module>
    eval_coco(full_name, os.path.join(PATH_PREFIX, 'result-gt-json.txt'), os.path.join(PATH_PREFIX, 'result-pred-json.txt'))
  File "eval.py", line 138, in eval_coco
    output = net(Variable(sample_data['image'],volatile=True))
  File "/home/pi/.virtualenvs/torch/lib/python3.5/site-packages/torch/nn/modules/module.py", line 491, in __call__
    result = self.forward(*input, **kwargs)
  File "/home/pi/mobilepose-pi/networks.py", line 49, in forward
    pose_out = self.resnet(x)
  File "/home/pi/.virtualenvs/torch/lib/python3.5/site-packages/torch/nn/modules/module.py", line 491, in __call__
    result = self.forward(*input, **kwargs)
  File "/home/pi/.virtualenvs/torch/lib/python3.5/site-packages/torchvision/models/resnet.py", line 145, in forward
    x = self.layer3(x)
  File "/home/pi/.virtualenvs/torch/lib/python3.5/site-packages/torch/nn/modules/module.py", line 491, in __call__
    result = self.forward(*input, **kwargs)
  File "/home/pi/.virtualenvs/torch/lib/python3.5/site-packages/torch/nn/modules/container.py", line 91, in forward
    input = module(input)
  File "/home/pi/.virtualenvs/torch/lib/python3.5/site-packages/torch/nn/modules/module.py", line 491, in __call__
    result = self.forward(*input, **kwargs)
  File "/home/pi/.virtualenvs/torch/lib/python3.5/site-packages/torchvision/models/resnet.py", line 41, in forward
    out = self.conv1(x)
  File "/home/pi/.virtualenvs/torch/lib/python3.5/site-packages/torch/nn/modules/module.py", line 491, in __call__
    result = self.forward(*input, **kwargs)
  File "/home/pi/.virtualenvs/torch/lib/python3.5/site-packages/torch/nn/modules/conv.py", line 301, in forward
    self.padding, self.dilation, self.groups)
RuntimeError: $ Torch: not enough memory: you tried to allocate 0GB. Buy new RAM! at /home/cyrilhsu/Downloads/pytorch/aten/src/TH/THGeneral.c:218

Exception ignored in: <function WeakValueDictionary.__init__.<locals>.remove at 0x6f0911e0>
Traceback (most recent call last):
  File "/home/pi/.virtualenvs/torch/lib/python3.5/weakref.py", line 117, in remove
TypeError: 'NoneType' object is not callable
```


