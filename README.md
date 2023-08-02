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

## Unet architecture
![ex_screenshot](img/Unet.png)

## ResUnet architecture
![ex_screenshot](img/Res_Unet.png)


## Result

### Unet_grayscale
We can see that Unet_grayscale is overfitting from the traning history. The same is true for RGB. Below is the data for Unet_grayscale. 

##### Training History
Epoch : 100 , Batch : 4, Optimizer : Adam, lr = 1e-4, Augmentation : random_flip

![ex_screenshot](./img/IoU_Unet_grayscale.png)|![ex_screenshot](./img/Loss_Unet_grayscale.png)
---|---|

##### Test img
![ex_screenshot](./img/Unet_grayscale_output2.png)|![ex_screenshot](./img/Unet_grayscale_output5.png)
---|---|

![ex_screenshot](./img/Unet_grayscale_output7.png)|![ex_screenshot](./img/Unet_grayscale_output9.png)
---|---|

### ResUnet_grayscale
To prevent overfitting, we tried a more complex model, ResUnet. Looking at the loss rate, we concluded that ResUnet prevented overfitting. However, we noticed an increase in the loss value at certain epochs. We decided that the learning rate was too high to reach a local minimum.

And we can see the performance decrease when we look at test_img. But overfitting has been avoided. Experiment by adding a way to stably reduce the loss value.

##### Training History
Epoch : 100 , Batch : 4, Optimizer : Adam, lr = 1e-4, Augmentation : random_flip

![ex_screenshot](./img/IoU_ResUnet_grayscale.png)|![ex_screenshot](./img/Loss_ResUnet_grayscale.png)
---|---|

##### Test img
![ex_screenshot](./img/ResUnet_grayscale_output2.png)|![ex_screenshot](./img/ResUnet_grayscale_output5.png)
---|---|

![ex_screenshot](./img/ResUnet_grayscale_output7.png)|![ex_screenshot](./img/ResUnet_grayscale_output9.png)
---|---|

### ResUnet_grayscale + Early stoping + Learning rate scheduler 
Epoch : 100 , Batch : 4, Optimizer : Adam, lr = 1e-4, Augmentation : random_flip

![ex_screenshot](./img/IoU_ResUnet_scheduler.png)|![ex_screenshot](./img/Loss_ResUnet_scheduler.png)
---|---|

##### Test img
![ex_screenshot](./img/ResUnet_grayscale_scheduler_output2.png)|![ex_screenshot](./img/ResUnet_grayscale_scheduler_output5.png)
---|---|

![ex_screenshot](./img/ResUnet_grayscale_scheduler_output7.png)|![ex_screenshot](./img/ResUnet_grayscale_scheduler_output9.png)
---|---|

## References
[1] Olaf Ronneberger, Philipp Fischer, Thomas Brox. U-Net: Convolutional Networks for Biomedical Image Segmentation. arXiv, 2015. https://arxiv.org/abs/1505.04597v1


[2] Estibaliz Gómez de Mariscal, Martin Maška, Anna Kotrbová, Vendula Pospichalova, Pavel Matula & Arrate Muñoz-Barrutia. Deep-Learning-Based Segmentation of Small Extracellular Vesicles in Transmission Electron Microscopy Images. Scientific Reports, 2019. https://www.researchgate.net/publication/335802605_Deep-Learning-Based_Segmentation_of_Small_Extracellular_Vesicles_in_Transmission_Electron_Microscopy_Images


[3] JEET B. LAHIRI. "Blood Cell Segmentation Dataset." Kaggle. July 10, 2023. https://www.kaggle.com/datasets/jeetblahiri/bccd-dataset-with-mask

## License
Distributed under the MIT License.



