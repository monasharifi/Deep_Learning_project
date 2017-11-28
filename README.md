# Detecting Diabetic Retinopathy grading in Retinal Fundus Photographs
This is the report of my progress on a classification problem based on a Kaggle competition launched in 2015(https://www.kaggle.com/c/diabetic-retinopathy-detection). 
## Introduction and Motivation: 
Diabetic retinopathy (DR) is the leading cause of blindness in the working-age population of the developed world and is estimated to affect over 93 million people. (From the competition website.)

The grading process consists of recognising very fine details, such as microaneurysms, to some bigger features, such as exudates, and sometimes their position relative to each other on images of the eye(more detail information can be found at https://www.gov.uk/government/uploads/system/uploads/attachment_data/file/582710/Grading_definitions_for_referrable_disease_2017_new_110117.pdf . An annotated image is shown below showing different signitures of pathologies related to DR.

<p align="center"><img src="https://github.com/monasharifi/Deep_Learning_project/blob/master/biomarkers_1.png" width="550"></p>
Based on the severity of disease, DR can be categorized as Mild NPDR, Moderate NPDR, Severe NPDR and PDR. Some examples of images in different categories are shown below: 
<p align="center"><img src="https://github.com/monasharifi/Deep_Learning_project/blob/master/DR_overview.png" width="450"></p>
</br> 
The problem of DR classification task using Fundus images has been already adressed in previous works with the goal of providing an automatic system for disease prediction. The altimate goal of this project is improving this prediction by adding another image modality to the analysis which is called OCTA(OCT angiography). OCTA is a new image modality that could give us a better view of vascular system in the deep retina and especially in the early stage of the disease this image could help more in early diagnosis of the disease. </br> 
The initial step of the project is to find out the power of Fundus image in different stages of DR which is mainly covered in this report. Altimately we will add OCTA analysis and extract features of OCTA images in order to improve the Fundus based model. 

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

## Initial models :
The purpose of initial models is to get more familiar with data and try some quick and tiny experiments to get some ideads about the proper and effective settings mainly for image pre-processing approaches. For this purpose, I just got a tiny subsampled version of two classes and run some experiments using a network with a few convolutial layers. The details can be found as below mentioned: 
* <b>Base Model Architecture: </b> 32, 3*3 Conv/Relu/pool -32, 3*3 Conv/Relu/pool - 64, 3*3 Conv/Relu/ pool - FC1,128 , FC2, 128
* <b> Base model Evaluation and conclusion: </b> 
This simple model is used for some experiments on a tiny subset of only two classes. I used only 300 samples of class 0,1 and could improved the classification result on test set by almost 11% using proper pre-processing and data augmentation.
</t>* The preprocessings that I found useful could be summarized as cropping(back ground removal), Image enhancement, using only Enhanced Green channel. 
* For Image augmentation, I tried different methods like rotation by random angle, flipping both horizontally and vertically, zoom in by cropping and I found out that flipping and rotation are more useful in this application. Rotation by random angle and also zoom in by cropping could cause the problem of removing some informative regions. 

## More experiments using AlexNet+Weights: 
Most of our evaulations and results are based on pre-trained Alexnet Model. We used all the pre-trained weights except for the last FC layer('fc8') and finetune Alexnet by feeding our Fundus images for the binary classification setting. Our evaluation metric for each experiment is simply Accuracy of test set which was seperated from the train set at the first stage and non of these images were shown to the Model at training time. </br>
Experiments are set up in binary classification mode between Healthy group( mentioned with label 0) and different stages of diseased group(mentioned by class 1 to 4). The last experiment is between Healthy group and all diseased group merged together. </br> 
Since the dataset is highly imbalanced, we tried our experiments by subsampling the major class to the number of minor class and also tried some experiments with data augmentation. </br> 
The other idead that we tried for improving the results is using only Enhanced G channel of image as input instead of original color image. </br> 

## Results: 
* <b>Binary classification:</b></br>
For the experimental results listed in the following table we used the same training parameters for fair comparison. 
<p align="center"><img src="https://github.com/monasharifi/Deep_Learning_project/blob/master/Results.png" width="650"></p>

## Future Plan: 
## Localization: 

## Related pevious work: 
* <b> State of the art method: </b>The state of the art method for DR classification task has been published by Google and their collaborators in JAMA 2015. The results is based on a dataset of 128K subject which is not the same as the datatset we used and the best performed model is Inception V3. The finding of this paper is :</br> 
 In 2 validation sets of 9963 images and 1748 images, at the operating point selected for high specificity, the algorithm had 90.3% and 87.0% sensitivity and 98.1% and 98.5% specificity for detecting referable diabetic retinopathy, defined as moderate or worse diabetic retinopathy or referable macular edema by the majority decision of a panel of at least 7 US board-certified ophthalmologists. At the operating point selected for high sensitivity, the algorithm had 97.5% and 96.1% sensitivity and 93.4% and 93.9% specificity in the 2 validation sets.more details can be found at https://jamanetwork.com/journals/jama/fullarticle/2588763
* <b> Top deep learning winner in kaggle competition</b> The winning method of Diabetic retinopathy competition was not Deep Learning based but there are some proposed Deep learning approaches whith the highest rank of 5th in leader board. They proposed their own architecture and also benefit from data augmentation. The evaulation metric for their performance is Kappa metric which is not the one I used in this project and that makes comparison difficult. The details of the top deep learning proposed method can be found in this repo: http://jeffreydf.github.io/diabetic-retinopathy-detection/#code-models-and-example-activations
 * 





