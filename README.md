# Detecting Diabetic Retinopathy grading in Retinal Fundus Photographs
This is the report of my progress on a classification problem based on a Kaggle competition launched in 2015(https://www.kaggle.com/c/diabetic-retinopathy-detection). 
## Introduction: 
Diabetic retinopathy (DR) is the leading cause of blindness in the working-age population of the developed world and is estimated to affect over 93 million people. (From the competition website.)

The grading process consists of recognising very fine details, such as microaneurysms, to some bigger features, such as exudates, and sometimes their position relative to each other on images of the eye(more detail information can be found at https://www.gov.uk/government/uploads/system/uploads/attachment_data/file/582710/Grading_definitions_for_referrable_disease_2017_new_110117.pdf . An annotated image is shown below showing different pathologies related to DR.

<p align="center"><img src="https://github.com/monasharifi/Deep_Learning_project/blob/master/biomarkers_1.png" width="550"></p>
Based on the severity of disease, DR can be categorized as Mild NPDR, Moderate NPDR, Severe NPDR and PDR. Some examples of images in different categories are shown below: 
<p align="center"><img src="https://github.com/monasharifi/Deep_Learning_project/blob/master/DR_overview.png" width="450"></p>

## Dataset:
For the classification phase of this project, I used training set of dataset provided by kaggle. The detail information of sample distribution among classes provided in the following table: 
<p align="center"><img src="https://github.com/monasharifi/Deep_Learning_project/blob/master/dataset.png" width="350"></p>
In Kaggle competition, competitors were asked to predict the class label (one of the 5 categories) for each of the 53576 test images and the predictions were scored on the quadratic weighted kappa metric. Since the labesl of test dataset is not available at the time of this project, I splitted the 35126 images in trainig dataset to train and test sets for my experiments.  some example of images in the dataset are as shown below: 
<p align="center"><img src="https://github.com/monasharifi/Deep_Learning_project/blob/master/montage.png" width="450"></p>

## Dataset analysis:
The summary of initail analysis of dataset is as below mentioned: 
* <b>Dataset is highly imbalanced:</b> to deal with this issue I set up the experiments in two modes, sub_sampling and data augmentation
* <b>Image resolution :</b> Images are provided in different sizes, the avarage image size is (3000x2000) pixels 
* <b>Image orientation :</b> Images are from both left and right eyes and they are not registered
* <b>Image quality:</b> Images have different brightness and illuminations and they all come with black background, some images have camera artifacts, Since images rae taken with different cameras and different zooming levels we can see a lot of variety in images

## Pre-processing :
The ideas that I tried for pre-processing are: 
* <b>Histogram equalization : </b>Our original input images are 2D color images and I tried image enhancement by histogram equalization in two settings : color image enhancement, G channel Enhancement
* <b>Brightness and Contrast adjustment:</b> Since Images taken with different cameras, they come with different illuminations and requires some brightness and contract adjustment
* <b>Cropping by centering at Optic nerve:</b> Images in dataset are from both left and right eyes and they come in different orientation, scale and zoom level. Based on this, I tried to put the center of cropping at optic nerve and crop proportinal with respect to image scale. The code for finding the optic nerve actually didn't work very well on all images and this approach was tried but not used in our final experimental results. 
* <b>Cropping with respect to image scale:</b> To remove some background region, I just removed some boundry pixels by cropping with some ratio which is proportianl to image size. 

## Inital models :
The purpose of initial models is to get more familiar with data and try some quick and tiny experiments to get some ideads about the proper and effective settings mainly for image pre-processing approaches. For this purpose, I just got a tiny subsampled version of two classes and run some experiments using a network with a few convolutial layers. The details can be found as below mentioned: 
* <b>Base Model Architecture: </b> 
* <b> Base model Evaluation and conclusion: </b>

## More experiments using AlexNet+Weights: 
Most of our evaulations and results are based on pre-trained Alexnet Model. We used all the pre-trained weights except for the last FC layer('fc8') and finetune Alexnet by feeding our Fundus images for the binary classification setting. Our evaluation metric for each experiment is simply Accuracy of test set which was seperated from the train set at the first stage and non of these images were shown to the Model at training time. 
Experiments are set up in binary classification mode between Healthy group( mentioned with label 0) and different stages of diseased group(mentioned by class 1 to 4). The last experiment is between Healthy group and all diseased group merged together. 

## Results: 
<p align="center"><img src="https://github.com/monasharifi/Deep_Learning_project/blob/master/Results.png" width="650"></p>

## Localization: 

## Future Plan: 





