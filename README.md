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
* Dataset is highly imbalanced: to deal with this issue I set up the experiments in two modes, sub_sampling and data augmentation
* Image resolution : Images are provided in different sizes, the avarage image size is (3000x2000) pixels 
* Image orientation : Images are from both left and right eyes and they are not registered
* Image quality: Images have different brightness and illuminations and they all come with black background, some images have camera artifacts, Since images rae taken with different cameras and different zooming levels we can see a lot of variety in images

## Pre-processing :
The ideas that I tried for pre-processing are: 
* Histogram equalization
* Background removal
* Brightness adjustment
* Contrast adjustment

## Inital models :

## More experiments using AlexNet+Weights: 

## Results: 
<p align="center"><img src="https://github.com/monasharifi/Deep_Learning_project/blob/master/Results.png" width="650"></p>

## Localization: 

## Future Plan: 





