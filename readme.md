# Thematic Map Generator for Land Cover

There are total 3 modles, asjusted standard model, many branch model, and many stage model.

Each model requres different configuration and parameters.

## Configurations
Model configurations are stored in this repository as follows.
1. **_trial_0_**: Adjusted Standard Model
2. **_trial_1_**: Many Branch Model
3. **_trial_2_**: Many Stage Model


## Parameters to adjust
Please refer to the report pdf file for details.
1. **_batch_size_** 
2. **_init_lr_**
3. **_final_lr_**
4. **_epochs_**

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
