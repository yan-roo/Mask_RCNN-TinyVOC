# Tiny Pascal VOC Instance Segmentation

To read the detailed , please, refer to [CS_IOC5008_HW4](https://github.com/NCTU-VRDL/CS_IOC5008/tree/master/HW4)
Based on https://github.com/matterport/Mask_RCNN

## Hardware
The following specs were used to create the original solution.
- Ubuntu 16.04 LTS
- Intel(R) Core(TM) i7-6700 CPU @ 3.40GHz
- 1x NVIDIA TitanXp 


## Installation
All requirements should be detailed in [requirements.txt](https://github.com/yan-roo/Mask_RCNN-TinyVOC/blob/master/requirements.txt). Using Anaconda is strongly recommended.
```
conda create -n mrnn python=3.6
source activate mrnn
pip install -r requirements.txt
```

## Dataset Preparation
Following the Jupyter Notebook [data loader](https://github.com/yan-roo/Mask_RCNN-TinyVOC/blob/master/samples/VOC/data_loader.ipynb) in samples/VOC.
And you have to create val.txt as validation images by your own.(Choose labels from train.txt)

### Prepare Images
After execution of data loader, the data directory is structured as:
```
VOC
  +- VOCdevkit_Tiny
  |  +- VOC2012
  	|  +- Annotation
  	|  +- SegmentationClass
  	|  +- SegmentationObject
  	|  +- train_images
  	|  +- train.txt
  	|  +- val.txt
  +- data_loader.ipynb
  +- pascal_train.json
  +- voc.py
```






## Training
You can set the config in voc.py (class VocConfig)
The config template is in mrcnn/config.py

### Model architecture(Callbacks, Optimizer, Regularizer)
You can set them in [voc.py](https://github.com/yan-roo/Mask_RCNN-TinyVOC/blob/master/samples/VOC/voc.py) or [model.py](https://github.com/yan-roo/Mask_RCNN-TinyVOC/blob/master/mrcnn/model.py)(recommend)


### Train models
To train models, run following commands.
```
$ python voc.py train --dataset VOCdevkit_Tiny/ --model imagenet
```


The expected training times are:

Model | GPUs  | Training Epochs | Training Time
------------ | ------------- | ------------- | -------------
ResNet50 | 1x TitanXp | 160 | 11 hours
ResNet101 | 1x TitanXp | 1024 | 14 hours



### Pretrained models
We only can use ImageNet pretrained model for the fairness. 

### Training weights
The training weights are saved in logs directory.


## Make Submission

### Download the Test Image & json
[Dataset GoogleDrive](https://drive.google.com/drive/u/0/folders/1fGg03EdBAxjFumGHHNhMrz2sMLLH04FK)

At the directory samples/VOC/
```
$ wget https://drive.google.com/open?id=1VAhbaxLH7mjoPcJpoji5WijEoJy87wkk
$ wget https://drive.google.com/file/d/1s7OTV0rGW3AijyqSS6Tfl5IsDNGkiZWM/view?usp=sharing
$ tar xvf test_images.tar
```
Afterward, use [demo.py](https://github.com/yan-roo/Mask_RCNN-TinyVOC/blob/master/samples/demo.ipynb) to generate a json file.
