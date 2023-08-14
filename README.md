# Blood_cell_segmentation_with_Unet

## Overview
Cell segmentation plays an important role in the detection and classification of tumor or disease cells in the context of pathological tissue examination. The segmentation of cancerous tissue help in the development of cancer diagnosis and treatment. 

To create a diagnostic model, we need to understand how cancer cells are distributed and how many there are. For this purpose, we tried cell segmentation with uninet and resunet architecture. Then we used OpenCV Water shade function to understand the distribution and number.

In order to diagnose with AI and convince users, it is essential to explain fine needle aspiration cytology, cell exclusion test, etc. used in various tests.

## Dataset source
A total of 2656 images are available. 1328 Original blood cell images with 1328 corresponding ground truths. Out of that, Jeet B Lahiri separated the training and testing sets with 1169 images and 159 images respectively.
Data gernerate by Deponker, Sarker Depto, Shazidur Rahman, Md. Mekayel Hosen, Mst Shapna Akter, Tamanna Rahman Reme, Aimon Rahman, Hasib Zunai, M. Sohel Rahman and M.R.C.Mahdy

#### Short Description
With the advent of deep learing algorithms in medial domain, there is a need for quality and large datasets. In this work, we introduced the largest microscopic blood cell segmentation dataset and benchmark different state-of-the-art algorithms on it. Our findings and contributions are particularly helpful for researchers working in deep learning with applications in medial domain.
![ex_screenshot](./img/Dataset_img.png)

Distributed under the MIT License.

## Result

### Unet_grayscale & ResUnet_grayscale
You can see in the traning history that Unet_grayscale is being overfitted. The same is true for RGB.

For ResUnet, we noticed an exploding gradient in the loss value at certain epochs. We determined that the learning rate was too high to reach a local minimum.

So we experimented by adding different models, schedulers, and early stopping.

##### Training History
Epoch : 100 , Batch : 4, Optimizer : Adam, lr = 1e-4, Augmentation : random_flip

![ex_screenshot](./image/Unet_gray.png)|![ex_screenshot](./image/ResUnet_gray.png)
---|---|


### ResUnet_grayscale + Early stoping + Learning rate scheduler 

##### Training History
Epoch : 100 , Batch : 4, Optimizer : Adam, lr = 1e-4, Augmentation : random_flip, patience = 10

scheduler = StepLR(optim, step_size=1, gamma=0.95)

Early stop : 42epochs

![ex_screenshot](./img/IoU_ResUnet_scheduler.png)|![ex_screenshot](./img/Loss_ResUnet_scheduler.png)
---|---|

### VGG11Unet + Early stoping + Learning rate scheduler 

##### Training History
Epoch : 100 , Batch : 4, Optimizer : Adam, lr = 1e-4, Augmentation : random_flip, patience = 10

scheduler = ReduceLROnPlateau(optim, mode='min', factor=0.5, patience=5, min_lr=1e-6)

Early stop : 36epochs

![ex_screenshot](./img/IoU_VGG11Unet.png)|![ex_screenshot](./img/Loss_VGG11Unet.png)
---|---|

### VGG16Unet + Early stoping + Learning rate scheduler 

##### Training History
Epoch : 100 , Batch : 4, Optimizer : Adam, lr = 1e-4, Augmentation : random_flip, patience = 10

scheduler = ReduceLROnPlateau(optim, mode='min', factor=0.5, patience=5, min_lr=1e-6)

Early stop : 39epochs

![ex_screenshot](./img/IoU_VGG16Unet.png)|![ex_screenshot](./img/Loss_VGG16Unet.png)
---|---|

### AttentionUnet + Early stoping + Learning rate scheduler 

##### Training History
Epoch : 100 , Batch : 4, Optimizer : Adam, lr = 1e-4, Augmentation : random_flip, patience = 10

scheduler = ReduceLROnPlateau(optim, mode='min', factor=0.5, patience=5, min_lr=1e-6)

Early stop : 52epochs

![ex_screenshot](./img/IoU_AttentionUnet.png)|![ex_screenshot](./img/Loss_AttentionUnet.png)
---|---|

## References
[1] JEET B. LAHIRI. "Blood Cell Segmentation Dataset." Kaggle. July 10, 2023. https://www.kaggle.com/datasets/jeetblahiri/bccd-dataset-with-mask


[2] Olaf Ronneberger, Philipp Fischer, Thomas Brox. U-Net: Convolutional Networks for Biomedical Image Segmentation. arXiv, 2015. https://arxiv.org/abs/1505.04597v1


[3] Estibaliz Gómez de Mariscal, Martin Maška, Anna Kotrbová, Vendula Pospichalova, Pavel Matula & Arrate Muñoz-Barrutia. Deep-Learning-Based Segmentation of Small Extracellular Vesicles in Transmission Electron Microscopy Images. Scientific Reports, 2019. https://www.researchgate.net/publication/335802605_Deep-Learning-Based_Segmentation_of_Small_Extracellular_Vesicles_in_Transmission_Electron_Microscopy_Images


[4] Ozan Oktay, Jo Schlemper, Loic Le Folgoc, Matthew Lee, Mattias Heinrich, Kazunari Misawa, Kensaku Mori, Steven McDonagh, Nils Y Hammerla, Bernhard Kainz, Ben Glocker, Daniel Rueckert. Attention U-Net: Learning Where to Look for the Pancreas. arXiv, 2018. https://arxiv.org/abs/1804.03999

[5] Vladimir Iglovikov, Alexey Shvets. TernausNet: U-Net with VGG11 Encoder Pre-Trained on ImageNet for Image Segmentation. arXiv, 2018.https://arxiv.org/abs/1801.05746



## License
Distributed under the MIT License.



