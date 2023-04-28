# What is the best way to do augmentations TorchVision ,Detectron2 or albumentations ??? 
# Is there any fitness function to choose and improve data augmentation techniques with Genetic algorithms! or invent now augmentations ? 
# Photometric distortions 
1. hue -> making them look more blue or green and produces more images
2. saturation -> changes how colorful the color channel of the input images is-> makes blue less blue by adding some white colors 
3. birghtness ->shedding some amount of light 
4. exposure -> biased to highlight tones,while brightness changes all tones equally 
5. grayscale -> if it retains three channels,all channels have the same value per pixel location 
6. blur -> help the model to be more robust to camera focse. 
7. noise -> makes the training models more robust to camera artifact and tackles adversarial attacks 
# Geometric distortions 
These techniques change input images to different contexts related to the location and perspectives where the images are collected. These differences in perspectives help provide the vision models with training data containing different views. These techniques change the images geometrically; thus, they also change image annotations such as bounding boxes
1. flip -> model more robust to object orientation changes 
2. crop  -> helps simulate changes in camera position and/or object movements 
3. rotation  -> add images such as take with different camera rolls. more robust to cameras and objects that are not perfectly aligned
4. shear  -> add more pictures as if they were taken from different pitches and yaws of the camera 
# Image occlusions 
This category of image augmentations includes techniques such as Cutout, MixUp, CutMix, and Mosaic.
These techniques help the model learn an object as a whole and not just focus on a particular part of
it so that when we see that part of an object is occluded, the model can still recognize it. Additionally,
it places the object in other contexts (for example, different backgrounds or surrounding objects) so
that the model focuses on the features of the object itself instead of the contexts:
1. Cutout -> makes the training model more robust to the cases where some other object may cover part of the object. This technique forces the model to learn features from an object as a whole and doesn't focus on a particular part of it.it may or may not change the annotations of the input image,depending on the cutout regions 
2. Mixup -> It allows us to train models on convex combinations of pairs of input images and their labels.These convex combinations regularize the training model to favor simple linear behavior across training examples 
3. CutMix -> This technique replaces one region of an input image with a part of another image based on a defined ratio and produces new versions. This technique may remove annotations from the input image and include annotations from the other image. This technique works well by leveraging the advantages of both the cutout and the mixup approaches.
4. Mosaic :This technique combines four images (versus two in CutMix) based on some defined ratios and produces new versions. This technique leverages the advantages of the other image occlusion techniques listed previously. Additionally, it is useful if the mini-batch size is small due to having limited computation resources because one image is similar to four in this case
# Detectron2's Image augmentation system 
The Transform adn Augmentation classes are the bases for all the classes in their respective groups
the data format for boxes is in XYXY_ABS mode, which indicated the boxes to be in (x_min,y_min,x_max,y_max) specified in absolute pixels. 
- Subclasses of the Transform base class perform the deterministic changes of the input data, 
- subclasses of the Augmentation base class define the policy with some randomness and generate objects of the Transform subclasse. 
- The AugInput class is used to encapsulate input  data for Augmentation classes,and it can be used independently(via the transform method) or as the input for the Augmentation classes. 
### Typical usage of this system 
1. Create an input using the AugInput class (input)
2. Declare one or more instances of the Augmentation  class (augs)
3. Apply the augmentations to the input(in place) and return an object of the Transform class : transform = augs(input)
4. Use the returned transform object to perform augmentations on extra data if needed 
# Transformation classes 
1. the Transform class 
2. The NoOpTransform class 
3. The ResizeTransform 
4. The ExtentTransform class 
5. The RotationTransform class 
6. The PILColorTransform and ColorTransform classes 
7. The VFlipTransform adn HFlip Transform classes 
8. The CropTransform class
9. The BlendTransform class 
10. The PadTransform class 
11. The TransformList class 
# The Augmentation classes 
1. The Augmentation class 
2. The FixedSizeCrop class 
3. The RandomApply class 
4. The RandomCrop class 
5. The RadnomExtent class 
6. The RandomFlip class 
7. The RandomRotation class 
8. The Resize class 
9. The RandomResize class 
10. The ResizeScale class 
11. The ResizeShortestEdge class 
12. The RandomCrop and CategoryAreaConstraint classes 
13. The MinIoURandomCrop class 
14. The RandomContrast class
15. The RandomSaturation class
16. The RandomLightning class 
17. The AugmentationList class















