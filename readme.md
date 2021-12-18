# Thematic Map Generator for Land Cover

There are total 3 modles, Adsjusted Standard Model, Many Branch Model, and Many Stage Model.

**_ASM_** is the transformation of HRNet18. The number of channels, blocks and modules are adjusted while keeping the origianl relationships between each parameters.

**_MBM_** is a custom model. It utilizes many branches and focuses on a new born branch. The new born branch takes the most blocks and channels while old banches take them as least as possible.

**_MSM_** is a custom model. It utilizes more stage than ASM. Like MBM, it focuses on a new born branch. But unlike MBM, it also gives more resources to the old branches than MBM.

Each model requres different configuration and parameters.

## Configurations
Model configurations are stored in this repository as follows.
1. **_trial_0_**: Adjusted Standard Model
2. **_trial_1_**: Many Branch Model
3. **_trial_2_**: Many Stage Model

If you want to change the configuration, use **_cfg_** Python Dictionary variable.

**_cfg_** format is as follow.

**_cfg['INIT_CHANNEL']_**: The number of channel of **_stem_net_**. **_stem_net_** is the first module of HRNet, consisting of two 2X2 Convolutions, two Batch Normalization, and a ReLU function.

**_cfg['STAGEX']['NUM_MODULES']_**: The number of HighResolution modules of Stage X.

**_cfg['STAGEX']['NUM_BRANCHES']_**: The number of branches of Stage X.

**_cfg['STAGEX']['NUM_BLOCKS']_**: A Python List containing the number of blocks of each branch. The length of this list must be same as the number of branches.

**_cfg['STAGEX']['NUM_CHANNELS']_**: A Python List containing the number of channels of each branch. The length of this list must be same as the number of branches. 

**_cfg['STAGEX']['BLOCK']_**: The type of block which consists a branch. It can be **_'BASIC'_**, or **_'BOTTLENECK'_**.

Finally, the **_'X'_** in **_'STAGEX'_** must be an positive integer, starting from 1 and increasing sequentially.

## Parameters to adjust
Please refer to the report pdf file for details.
1. **_batch_size_** 
   
   
   ![image](https://user-images.githubusercontent.com/53179332/146635250-7a4c6f75-5136-43b8-bb40-26feb5529021.png)

3. **_init_lr_**
4. **_final_lr_**
5. **_epochs_**

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
