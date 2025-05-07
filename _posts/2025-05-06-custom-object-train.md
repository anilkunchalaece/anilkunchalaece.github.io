---
layout: post
title: "Fine-tuning Custom Object Detector Using Pytorch"
categories:
  - Blog
  - Computer-Vision
# tags:
#   - Machine Learning
excerpt: Fine-Tuning Custom Object Detector using Pytorch
comments: false
category:
  - Blog
---

In this post, I will describe how to fine-tune and pretrained object detector model using pytorch.

#### Data Requirements
For Object Detection Training and Test line, you Need
- Images
- No of Classes you want to detect in the images [One image may contain multiple classes]
- Bounding Boxes of Each Object with in Image [These may have different formats based on annotation tool]

#### What You need to do
Most of the work you do can be split into 3 stages
1. Custom Dataset Class for your data 
2. Model Modification  
3. Train and Test Scripts 

#### Custom Dataset Class
- Create an custom dataset class (lets call it CustomDatasetClass) **inherited** from `torch.utils.data.dataset` class.
- In the custom class create the following methods. These will be replaced in parent `torch.utils.data.datset` class
    - `__getitem(self,idx)__`
        - This is used to get the each item for training and testing
        - Include the code to do any preprocessing for data - for ex, converting image and class labels to tensors
        - **For Object Detection**
            - `__getitem__` should return following
                - **image :** should be a tensor of shape [Channels, Height, Width]
                - **targets :** list of dictionary containing
                    - *boxes :* ground truth bounding boxes in ``[x1,y1,x2,y2]`` format
                    - *labels :* class label for each bounding box

    - `__len(self)__`
        - This is used to get the total number of samples in the dataset

Once you create these two methods, we can use this class to load the dataset suitable for pytorch dataloader for both training and testing

References
- [https://docs.pytorch.org/tutorials/intermediate/torchvision_tutorial.html](https://docs.pytorch.org/tutorials/intermediate/torchvision_tutorial.html)
- [https://docs.pytorch.org/vision/stable/_modules/torchvision/models/detection/faster_rcnn.html#FasterRCNN_ResNet50_FPN_V2_Weights](https://docs.pytorch.org/vision/stable/_modules/torchvision/models/detection/faster_rcnn.html#FasterRCNN_ResNet50_FPN_V2_Weights)


#### Model Modifications
Instead of creating model from scratch, We can use one of the pretrained models from pytorch and modify the number of classes in the classifier head to match our use case.

Following is the comparision of easy to use pytorch models

| Model Name | Backbone | Type |  Speed | Accuracy |
| ---------- | --------- | ----- | ------ | -------- |
| fasterrcnn_resnet50_fpn | ResNet50 + FPN | Two Stage | Medium | High |
| fasterrcnn_mobilenet_v3_large_fpn | MobileNet + FPN | Two Stage | Fast | Medium |
| retinanet_resnet50_fpn | ResNet50 + FPN | One Stage | Fasterthan FastRCNN | Decent |

**Faster RCNN** 
```python
from torchvision.models.detection.faster_rcnn import FastRCNNPredictor

model = torchvision.models.detection.fasterrcnn_resnet50_fpn(pretrained=True)
in_features = model.roi_heads.box_predictor.cls_score.in_features
model.roi_heads.box_predictor = FastRCNNPredictor(in_features, num_classes)
```

**MobileNet**
```python
from torchvision.models.detection.faster_rcnn import FastRCNNPredictor

model = torchvision.models.detection.fasterrcnn_mobilenet_v3_large_fpn(pretrained=True)
in_features = model.roi_heads.box_predictor.cls_score.in_features
model.roi_heads.box_predictor = FastRCNNPredictor(in_features, num_classes)
```

**RetinaNet**
```python
from torchvision.models.detection.retinanet import RetinaNetClassificationHead

model = torchvision.models.detection.retinanet_resnet50_fpn(pretrained=True)
in_channels = model.head.classification_head.conv[0].in_channels  # usually 256
num_anchors = model.head.classification_head.num_anchors  # usually 9

model.head.classification_head = RetinaNetClassificationHead(in_channels, num_anchors, num_classes)
```



