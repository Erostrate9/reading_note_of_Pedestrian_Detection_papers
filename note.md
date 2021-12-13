# A Shape Transformation-based Dataset Augmentation Framework for Pedestrian Detection

## Abstract

## Introduction

* deep convolutional neural networks (DCNNs) 深度卷积神经网络在行人识别中表现良好，但DCNNs识别器在遇到负背景比正前景突出的情况时可能会不够鲁棒。用有限前景样本训练的DCNN识别器面对未学习过的复杂测试物体会非常脆弱。

  * positive foreground or positive space 是图像中我们期望观察的主体，如行人。

  * negative background or negative space 是图像中主体以外的背景，如街道。

* 为了改善识别器的鲁棒性，数据增强是除设计新机器学习算法外的另一个解决方案。例如：

  * 像Stephan R. Richter等人用3D游戏GTA5识别生成图像数据集那样，Huang等人用一个3D游戏引擎生成行人，调整后加入训练集中。

  * 还有些研究使用了GANs，通过改变行人的姿势来扩充人重识别数据集。

* 但是上述的这些方法想要直接应用到行人识别是很困难的，因为：

1. 使用3D游戏引擎等外部平台合成行人可能会引入与真实行人间显著的域差距domain gap，总体上对鲁棒性的收益可能不大。
2. 关于利用GANs渲染行人的方法，这往往需要训练图像丰富的外观细节，以便于确定生成网络的期望输出，但真实的行人数据集（Caltech, CityPersons）往往图像质量低 （比如重度重叠，外观模糊，低分辨率），这些数据集只能提供非常少的能用于训练生成网络的外观细节，作者通过实验证明，在这些数据集中，现有的基于GAN的方法只能生成很少的真实行人，甚至产生了反作用。

* 为了解决上述问题，作者建议通过根据不同形状（研究中的提到的segmentation mask）将来自同一数据集的真实行人转换成不同姿势，而不是渲染新的行人。这基于以下观察：
  1. 