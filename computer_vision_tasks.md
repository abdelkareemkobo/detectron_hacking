# Object detection 
Includes object localization and classification by applying the bounding boxes around theses objects 
# Instance Segmentation 
Models for this task localize teh detected object at the pixel level. it identifies all the pixels of each detected object. 
#  Keypoint detection 
indicated important parts of the detected objects. These keypoints describe the detected objects' essentail trait.this trait is often invariant to image rotation,shrinkage,translation,or distortion. 
keypoint detection is important for applications such as action estimation,pose detection of face detection 
# Semantic segmentation 
doesn't detect specific instances of objects but classifies each pixel in an image into some classes of interest 
# Panoptic segmentation 
panoptics literally means "everything visible in the image". In other words,it can be viewed as combining common CV tasks such as instance segmentation and semantic segmenation. Generally, it classifies objects in an image into foreground objects(that have proper geometries) and background objects(that don't have appropriate geometries but are textures or materials)
-> Different from semantic segmentation,panoptic segmentation doesn't group consecutive individual objects of the same class into one region 

# Main Components of Detectron2 
Input data->BackBone->Region proposal->Region of interest Heads
## The Input data Module
The input data module is designed to load data in large batches from hard drives with optimization techniques such as caching and multi-workers. Furthermore, it is relatively easy to plug data augmentation techniques into a data loader for this module. Additionally, it is designed to be customizable so that users can register their custom datasets. The following is the typical syntax for assigning a custom dataset to train a Detectron2 model using this module:
`python 
DatasetRegistery.register("my_dataset",load_my_dataset)
`
## The backbone module
this module often uses a cutting-edge CNN network such as ResNet or ResNeXt. it also has a great deal of knowledge about transfer learning 
`python 
@BACKBONE_REGISTRY.register()
class CustomBackbone(Backbone):
    pass
`
## The region proposal module
The next module is the region proposal module (Region Proposal). This module accepts the extracted
features from the backbone and predicts or proposes image regions (with location specifications) and
scores to indicate whether the regions contain objects (with objectness scores). The objectness score
of a proposed region may be 0 (for not having an object or being background) or 1 (for being sure
that there is an object of interest in the predicted region). Notably, this object score is not about the
probability of being a class of interest but simply whether the region contains an object (of any class)
or not (background).
This module is set with a default Region Proposal Network (RPN). However, replacing this network
with a custom one is relatively easy. The following is the typical syntax for registering a custom RPN
to train the Detectron2 model using this module:
`python
@ROI_BOX_HEAD_REGISTRY.register()
class CustomBoxHead(nn.Module):
    pass
`
## Region of interset module 
For instance, the detection heads accept the region proposals
and the input features of the proposed regions and pass them through a fully connected network, with
two separate heads for prediction and classification. Specifically, one head is used to predict bounding
boxes for objects, and another is for classifying the detected bounding boxes into corresponding classes.
On the other hand, semantic segmentation heads also use convolutional neural network heads to
classify each pixel into one of the classes of interest. The following is the typical syntax for registering
custom region of interest heads to train the Detectron2 model using this module:
`python 
@ROI_HEAD_REGISTRY.register()
class CustomHeads(StandardROIHeads):
    pass
`
