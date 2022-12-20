# Land Cover Map Generator

<img width="835" alt="스크린샷 2022-12-20 오후 10 40 00" src="https://user-images.githubusercontent.com/53179332/208680519-8acae39a-544c-4aab-8295-31a6b3ad7569.png">


## Models

There are total 3 modles, Adsjusted Standard Model, Many Branch Model, and Many Stage Model.

**_ASM_** is the transformation of HRNet18. The number of channels, blocks and modules are adjusted while keeping the origianl relationships between each parameters.

**_MBM_** is a custom model. It utilizes many branches and focuses on a new born branch. The new born branch takes the most blocks and channels while old banches take them as least as possible.

**_MSM_** is a custom model. It utilizes more stage than ASM. Like MBM, it focuses on a new born branch. But unlike MBM, it also gives more resources to the old branches than MBM.

Each model requres different configuration and parameters.

The pretrained models are large so it is not able to upload in this repository.
They are available via Google Drive share link:
https://drive.google.com/drive/folders/1deOm_1dN0xHuT_la3mmgviO9E-L2A4Jj?usp=sharing

There are three files in **_results_** folder.
1. **_trial_0_**: Adjusted Standard Model
2. **_trial_1_**: Many Branch Model
3. **_trial_2_**: Many Stage Model

For each **_trial_x_** folder, there are two files.
1. **_model.pt_**: Trained model.
2. **_best.pt_**: Trained model which shows the best performance on validatoin mIoU. Please use this model.

The root is setted as '/gdrive/My Drive/Colab Notebooks/final'.

Please put **_final.py_** and **_results_** folder in **_final_** folder.


## Configurations

**_cfg_** format is as follow.

**_cfg['INIT_CHANNEL']_**: The number of channel of **_stem_net_**. **_stem_net_** is the first module of HRNet, consisting of two 2X2 Convolutions, two Batch Normalization, and a ReLU function.

**_cfg['STAGEX']['NUM_MODULES']_**: The number of HighResolution modules of Stage X.

**_cfg['STAGEX']['NUM_BRANCHES']_**: The number of branches of Stage X.

**_cfg['STAGEX']['NUM_BLOCKS']_**: A Python List containing the number of blocks of each branch. The length of this list must be same as the number of branches.

**_cfg['STAGEX']['NUM_CHANNELS']_**: A Python List containing the number of channels of each branch. The length of this list must be same as the number of branches. 

**_cfg['STAGEX']['BLOCK']_**: The type of block which consists a branch. It can be **_'BASIC'_**, or **_'BOTTLENECK'_**.

Finally, the **_'X'_** in **_'STAGEX'_** must be an positive integer, starting from 1 and increasing sequentially.

Model configurations are stored in this repository as follows.
1. **_trial_0_**: Adjusted Standard Model
2. **_trial_1_**: Many Branch Model
3. **_trial_2_**: Many Stage Model


## Parameters to adjust
1. **_batch_size_** at line 177
2. **_init_lr_** at line 818
3. **_final_lr_** at line 819
4. **_epochs_** at line 973 in **_train_net_** function

||ASM|MBM|MSM|
|:---:|:---:|:---:|:---:|
|batch_size|16|16|12|
|init_lr1|0.005(~100 epoch)|0.01(~100 epoch)|0.002(~147 epoch)|
|final_lr1|0.001(~100 epoch)|0.001(~100 epoch)|0.0005(~147 epoch)|
|epochs1|100|100|200|
|init_lr2|0.001(~140 epoch)|0.001(~130epoch)|
|final_lr2|0.0002(~140 epoch)|0.0001(~130 epoch)|
|epochs2|200|200|
|init_lr3|0.001(~156 epoch)|
|final_lr3|0.001(~156 epoch)|
|epochs3|200|

**_X_** in **_init_lr(~X epoch)_** and **_final_lr(~X epoch)_** is the epoch when stop training.

**When you change the epochs, you also have to change poly learning rate equation at line 861. Subtract previous epochs for both nominator and denominator. For example, if you change the epochs from 100 to 200 like above table, subtract 100 so (1- (epoch-100)/(epochs-100))^0.9 can be mutiplied.



## Data and DataLoader
There is a porper dataset at AIHub. Follow the link https://aihub.or.kr/aidata/30737

The dataset contains 512X512 images and 1024X1024 images.

There are three dataloaders: train dataloader, validation dataloader, and test dataloader.

For train and validation set, the dataloaders crop 512X512 and 1024X1024 to 216X216.

However, for test set, the dataloader use 512X512 images to minimize randomness of cropping. So it crops only 1024X1024 to 512X512.

Also, for train and validation set, the dataloaders use random horizontal and vertical flip augmentation.

But for test set, there is no augementation at all.

For image preprocessing, there is a dataloader which is used for calculating average and standard deviation of train images.

It uses 512X512 images, and the results are written in the code.

## Citation
### HRNet Citation

@inproceedings{SunXLW19,
  title={Deep High-Resolution Representation Learning for Human Pose Estimation},
  author={Ke Sun and Bin Xiao and Dong Liu and Jingdong Wang},
  booktitle={CVPR},
  year={2019}
}

@article{WangSCJDZLMTWLX19,
  title={Deep High-Resolution Representation Learning for Visual Recognition},
  author={Jingdong Wang and Ke Sun and Tianheng Cheng and 
          Borui Jiang and Chaorui Deng and Yang Zhao and Dong Liu and Yadong Mu and 
          Mingkui Tan and Xinggang Wang and Wenyu Liu and Bin Xiao},
  journal={TPAMI},
  year={2019}
}

@article{YuanCW19,
  title={Object-Contextual Representations for Semantic Segmentation},
  author={Yuhui Yuan and Xilin Chen and Jingdong Wang},
  booktitle={ECCV},
  year={2020}
}

There are some changes in the code. 
The main changes are as below

1.   Now one can configure the number of stage easily by just writing configure variables.
2.   Now one can congigure the initial number of channels easily by just writing configure variables.
3.   The first layer in HRNet is changed as first stage.
4.   Down sample checking code is moved into Basic Block and Bottleneck Block.


### Function Citation

From CS492(I) Assignment #2: Image Segmentation using Fully Convolutional Network (FCN)

TA : Jinwoo Kim (jinwoo-kim@kaist.ac.kr), Jaehoon Yoo (wogns98@kaist.ac.kr)

1. train_net()
2. test_net()
3. _fast_hist()
4. label_accuracy_score()

There are minor changes in the code to fit into this model.
