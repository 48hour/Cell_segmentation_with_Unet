# Cell_segmentation_with_Unet

## Overview
For some types of cancer, a cytology test is essential, such as a fine needle aspiration cytology or an exclusion cytology test. Cancer is diagnosed by observing cells. Adding artificial intelligence to this process can make diagnosis easier and faster. In addition, cell segmentation is important for detection and classification in pathology. Segmentation of cancerous tissue helps in the development of cancer diagnosis and treatment.

To increase the reliability of our diagnostic model, we identified the distribution and number of cancer cells. For this purpose, we tried cell segmentation with different architectures based on Unet. After creating a mask, we used OpenCV's Contour function to determine the number and distribution of cancer cells.

Our purpose is to segment thyroid cancer data. However, our data does not have annotated images. Therefore, we utilize similar data to develop a mask generation model for our data. Also, the thyroid cancer data is limited data belonging to our project and is not available to the public. We replace it with images from the paper "Medullary Thyroid Cancer" [6], which is most similar to our data.

## Dataset source
### 1) JEET B. LAHIRI. "Blood Cell Segmentation Dataset." Kaggle. 2023.
A total of 2656 images are available. 1328 Original blood cell images with 1328 corresponding ground truths. Out of that, Jeet B Lahiri separated the training and testing sets with 1169 images and 159 images respectively.
Data gernerate by Deponker, Sarker Depto, Shazidur Rahman, Md. Mekayel Hosen, Mst Shapna Akter, Tamanna Rahman Reme, Aimon Rahman, Hasib Zunai, M. Sohel Rahman and M.R.C.Mahdy

#### Short Description
With the advent of deep learing algorithms in medial domain, there is a need for quality and large datasets. In this work, we introduced the largest microscopic blood cell segmentation dataset and benchmark different state-of-the-art algorithms on it. Our findings and contributions are particularly helpful for researchers working in deep learning with applications in medial domain.
![ex_screenshot](./image/Dataset_img.png)

Distributed under the MIT License.

### 2) Larxel. "Cancer Instance Segmentation and Classification 1,2,3" Kaggle. 2022.
This dataset, also known as PanNuke, contains semi automatically generated nuclei instance segmentation and classification images with exhaustive nuclei labels across 19 different tissue types. The dataset consists of 481 visual fields, of which 312 are randomly sampled from more than 20K whole slide images at different magnifications, from multiple data sources.
In total the dataset contains 205,343 labeled nuclei, each with an instance segmentation mask. Models trained on PanNuke can aid in whole slide image tissue type segmentation, and generalize to new tissues.

![ex_screenshot](./image/Dataset_img2.png)

Distributed under the CC BY NC SA 4.0

The second data is instance segment, so the annotation is different. I loaded the npy data using the dataset processing.ipynb code to load the original images and annotation labels and preprocessed them into a binary mask.

## Result

### Unet_grayscale & ResUnet_grayscale

##### Training History
Epoch : 100 , Batch : 4, Optimizer : Adam, lr = 1e-4, Augmentation : random_flip

Unet|ResUnet|
---|---|
![ex_screenshot](./image/Unet_gray.png)|![ex_screenshot](./image/ResUnet_gray.png)|

We can see in the traning history that Unet_grayscale is being overfitted. The same is true for RGB.

For ResUnet, we noticed an exploding gradient in the loss value at certain epochs. We determined that the learning rate was too high to reach a local minimum.

So we experimented by adding different models, schedulers, and early stopping.

### ResUnet, VGG11Unet, VGG16Unet, AttentionUnet + Early stoping & Learning rate scheduler 

##### Training History
Epoch : 100 , Batch : 4, Optimizer : Adam, lr = 1e-4, Augmentation : random_flip, patience = 10

scheduler = ReduceLROnPlateau(optim, mode='min', factor=0.5, patience=5, min_lr=1e-6)

ResUnet|UnetVGG11|
---|---|
![ex_screenshot](./image/ResUnet_sch.png)|![ex_screenshot](./image/UnetVGG11.png)|

UnetAttention|UnetVGG11|
---|---|
![ex_screenshot](./image/UnetAttention.png)|![ex_screenshot](./image/UnetVGG16.png)|

Overfitting occurred in all models. After adding L2-Regularization and drop out, I tried reducing the number of hidden units and layers, but the results were the same.

So we add more data. Since our task is lightweight sementic segmentation, we need to preprocess the data for instance segmentation.

The preprocessed mask is shown below.

![ex_screenshot](./image/Process_mask.png)
---|

### Additional data Unet, ResUnet, VGG11Unet, VGG16Unet, AttentionUnet + Learning rate scheduler 

##### Training History
Epoch : 50 , Batch : 4, Optimizer : Adam, lr = 1e-4, Augmentation : random_flip, patience = 10

scheduler = ReduceLROnPlateau(optim, mode='min', factor=0.5, patience=5, min_lr=1e-6)

Unet|ResUnet|
---|---|
![ex_screenshot](./image/Add_data_Unet.png)|![ex_screenshot](./image/Add_data_ResUnet.png)|

UnetVGG11|UnetVGG16|
---|---|
![ex_screenshot](./image/Add_data_VGG11.png)|![ex_screenshot](./image/Add_data_VGG16.png)|

UnetAttention| |
---|---|
![ex_screenshot](./image/Add_data_Attention.png)|![ex_screenshot](./image/Blank.png)|


We excluded early stopping to see the overall performance. Unet is overfitting. ResUnet suffers from gradient exploding. VGG11, VGG16, and Attention models showed ideal traning history.

RGB
Attention|VGG11|VGG16
---|---|---|
![ex_screenshot](./image/Att_RGB.png)|![ex_screenshot](./image/VGG11_RGB.png)|![ex_screenshot](./image/VGG16_RGB.png)

Grayscale
Attention|VGG11|VGG16
---|---|---|
![ex_screenshot](./image/Att_gray.png)|![ex_screenshot](./image/VGG11_gray.png)|![ex_screenshot](./image/VGG16_gray.png)

We trained VGG11, VGG16, and Attention on RGB and Grayscale with early-starting and tested them on our data.

They all performed poorly on things that are difficult to distinguish with the eye.

Based on the effectiveness in removing impurities, lines and fluids, and good cell separation, attention-Unet was the best. attention-Unet performed the best.

Below is the inference of thyroid images in the paper with Attention_Unet_gray.

### Inference images
_|_ 
---|---|
![ex_screenshot](./image/Inference_iamges1.png)|![ex_screenshot](./image/Inference_iamges2.png)

Runtime & Memory with SAM for 1000 images

![ex_screenshot](./image/Runtim&gpu,cpu.png)

Additionally, we tried Meta's Segment Anything Model and it performed well, but we couldn't adopt it due to its long run time and high memory usage.

## References
[1] JEET B. LAHIRI. "Blood Cell Segmentation Dataset." Kaggle. 2023. https://www.kaggle.com/datasets/jeetblahiri/bccd-dataset-with-mask


[2] Olaf Ronneberger, Philipp Fischer, Thomas Brox. U-Net: Convolutional Networks for Biomedical Image Segmentation. arXiv, 2015. https://arxiv.org/abs/1505.04597v1


[3] Estibaliz Gómez de Mariscal, Martin Maška, Anna Kotrbová, Vendula Pospichalova, Pavel Matula & Arrate Muñoz-Barrutia. Deep-Learning-Based Segmentation of Small Extracellular Vesicles in Transmission Electron Microscopy Images. Scientific Reports, 2019. https://www.researchgate.net/publication/335802605_Deep-Learning-Based_Segmentation_of_Small_Extracellular_Vesicles_in_Transmission_Electron_Microscopy_Images


[4] Ozan Oktay, Jo Schlemper, Loic Le Folgoc, Matthew Lee, Mattias Heinrich, Kazunari Misawa, Kensaku Mori, Steven McDonagh, Nils Y Hammerla, Bernhard Kainz, Ben Glocker, Daniel Rueckert. Attention U-Net: Learning Where to Look for the Pancreas. arXiv, 2018. https://arxiv.org/abs/1804.03999

[5] Vladimir Iglovikov, Alexey Shvets. TernausNet: U-Net with VGG11 Encoder Pre-Trained on ImageNet for Image Segmentation. arXiv, 2018. https://arxiv.org/abs/1801.05746

[6] Michiya Nishino, Marc Philippe Pusztaszeri, Martha B. Pitman. Medullary Thyroid Carcinoma, In book: The Bethesda System for Reporting Thyroid Cytopathology (pp.157-175). ResearchGate, 2018. 
https://www.researchgate.net/publication/319449480_Medullary_Thyroid_Carcinoma

[7] Larxel. "Cancer Instance Segmentation and Classification 1,2,3" Kaggle. 2022. https://www.kaggle.com/datasets/andrewmvd/cancer-inst-segmentation-and-classification

[8] Gamper, Jevgenij and Koohbanani, Navid Alemi and Graham, Simon and Jahanifar, Mostafa and Benet, Ksenija and Khurram, Syed Ali and Azam, Ayesha and Hewitt, Katherine and Rajpoot, Nasir. PanNuke Dataset Extension, Insights and Baselines. arXiv, 2020.
https://arxiv.org/abs/2003.10778


## License
Distributed under the MIT License.
