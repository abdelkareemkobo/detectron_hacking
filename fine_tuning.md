Detectorn2 utilizes the concpets of anchors to improve its object detection accuracy by allowing object detection models to predict from a set of anchors instead of from scratch. 

The set of anchors having a set of  various sizes and ratios to reflect the shapes of the objects to be detected. 
Detectron2 uses two sets of hyperparameters called sizes and ratios to generate the initial set of anchors. 

input image pixels' means and standard deviations are crucial in training Detectron2 models
# Preprocessing input images
We need to know the sizes and ratios of the ground-truth boxes in the training dataset to find appropriate intial values for them. However,input images may have different sizes and go through various augmentations before feeding to the backbone network to extract features. The configuration values for these hyperparameters are set as if the input images have a standard input size.
#  Generating sizes and ratios hyperparameters
the algorithm to get the best set of sizes and ratios for training has the following steps:
1. Quantify how well each ground truth box matches a set of anchors (compute best ratios)
2. Quantify the fitness between the set of ground-truth boxes,as a whole,and the set of anchors (compute a fitness score)
3. Perform clustering algorithms on the ground-truth sizes and ratios and get the initializations for these two sets of parameters
4. Use a genetic algorithm to randomly evolve and get a good set of sizes and ratios for the training process. 

