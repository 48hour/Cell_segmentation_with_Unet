# Blood_cell_segmentation_with_Unet

## Overview
Cell segmentation is an important part of the detection and classification of tumor or disease cells in the context of pathological tissue examination. The segmentation of cancerous tissue is of great help in the development of cancer diagnosis and treatment. We believe that it is essential to explain fine needle aspiration cytology and exclusion cytology, which are used in various tests, in order to diagnose with AI and convince users. In addition to the diagnostic model, we need to understand how cancer cells are distributed and how many there are. We tried to perform cell segmentation, which is the basis for this, with Unet and ResUnet architecture.

## Dataset source
https://www.kaggle.com/datasets/jeetblahiri/bccd-dataset-with-mask

A total of 2656 images are available. 1328 Original blood cell images with 1328 corresponding ground truths. Out of that, Jeet B Lahiri separated the training and testing sets with 1169 images and 159 images respectively.
Data gernerate by Deponker, Sarker Depto, Shazidur Rahman, Md. Mekayel Hosen, Mst Shapna Akter, Tamanna Rahman Reme, Aimon Rahman, Hasib Zunai, M. Sohel Rahman and M.R.C.Mahdy

### Short Description
With the advent of deep learing algorithms in medial domain, there is a need for quality and large datasets. In this work, we introduced the largest microscopic blood cell segmentation dataset and benchmark different state-of-the-art algorithms on it. Our findings and contributions are particularly helpful for researchers working in deep learning with applications in medial domain.
![ex_screenshot](./img/Dataset_img.png)

Distributed under the MIT License.

## Unet architecture
![ex_screenshot](img/Unet.png)
https://arxiv.org/abs/1505.04597v1

## ResUnet architecture
![ex_screenshot](img/Res_Unet.png)
https://www.researchgate.net/figure/Fully-Residual-U-Net-architecture-Input-size-is-written-on-the-side-of-each-box-The_fig2_335802605

## Training History
Epoch : 100 , Batch : 4, Optimizer : Adam, lr = 1e-4, Augmentation : random_flip

## Result



## References





## License
Distributed under the MIT License.



