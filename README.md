# Detecting Diabetic Retinopathy grading in Retinal Fundus Photographs
This is the report of my progress on a classification problem based on a Kaggle competition launched in 2015(https://www.kaggle.com/c/diabetic-retinopathy-detection). 
## Introduction: 
Diabetic retinopathy (DR) is the leading cause of blindness in the working-age population of the developed world and is estimated to affect over 93 million people. (From the competition website.)

The grading process consists of recognising very fine details, such as microaneurysms, to some bigger features, such as exudates, and sometimes their position relative to each other on images of the eye(more detail information can be found at https://www.gov.uk/government/uploads/system/uploads/attachment_data/file/582710/Grading_definitions_for_referrable_disease_2017_new_110117.pdf . An annotated image is shown below showing different pathologies related to DR.

<p align="center"><img src="https://github.com/monasharifi/Deep_Learning_project/blob/master/biomarkers_1.png" width="550"></p>
Based on the severity of disease, DR can be categorized as Mild NPDR, Moderate NPDR, Severe NPDR and PDR. Some examples of images in different categories are shown below: 
<p align="center"><img src="https://github.com/monasharifi/Deep_Learning_project/blob/master/DR_overview.png" width="450"></p>

## Dataset:
For this 
Class	Name	Number of images	Percentage
0	Normal	25810	73.48%
1	Mild NPDR	2443	6.96%
2	Moderate NPDR	5292	15.07%
3	Severe NPDR	873	2.48%
4	PDR	708	2.01%
