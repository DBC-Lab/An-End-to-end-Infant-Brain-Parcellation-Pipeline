# An-End-to-end-Infant-Brain-Parcellation-Pipeline# An-End-to-end-Infant-Brain-Parcellation-Pipeline

## Model Overview

![](https://github.com/limeiwang5050/An-End-to-end-Infant-Brain-Parcellation-Pipeline/blob/main/Picture-3.png)

This repository contains the code for an end-to-end infant brain parcellation pipeline.

The code is composed of two network folders: (1) Global_ROIs_localization_network, and (2) Local_ROIs_Refinement_network, and their respective pretrained models are placed in ```./model/``` files in their respective folders.

The Global_ROIs_localization_network is used for 2-channel MR images inputs (T1w+T2w MRIs) and for 146-regions probability maps outputs. The Local_ROIs_Refinement_network uses the 146-regions probability maps produced by Global_ROIs_localization_network, together with 2-channel raw MR images inputs, as 148-channel inputs, and then produces final 146-regions parcellation results.

We provided a ```pipeline.csh``` file for merging the testing procedure of two networks to achieve an end-to-end segmentation process.



## Installing Dependencies

```
pip install -r requirements.txt
```

## testing 
You can use the pre-trained model or test it on demo Infant brain MR images from Infant Brain Imaging Study(IBIS) network we provided or on your own data.

If you would like to test on the demo images in ```./Demo_Images/```, you can directly run the following command:

```
./ pipeline.csh
```

If you would like to test on your own data, you need to follow the following steps:

#### 1. Data preprocessing

The testing data should contain T1w and T2w MRIs, and they have been aligned to each other. The image resolution is uniformly resampled to (1, 1, 1) with the size of (192, 192, 192), and the conduct correction of intensity inhomogeneity.

#### 2. Update testing data name and file address

You need to change the *.json file in ```./Global_ROIs_localization_network/dataset/``` and ```./Local_ROIs_Refinement_network/dataset/``` to indicate your own testing data, and then provide the location of your dataset directory by using --data_dir.

Then you can run the ```./ pipeline.csh``` command to carry out testing.
