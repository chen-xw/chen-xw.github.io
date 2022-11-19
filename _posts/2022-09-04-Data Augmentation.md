---
title: Data Augmentation
categories: Machine-Learning
tags:
  - 2022年09月04日
---

合适的数据增广方法对于最后模型的精度具有重要的影响，本文总结了常用的数据增广方法。


### **学习资源**

___

* [总结](https://zhuanlan.zhihu.com/p/61759947)
* [AutoAugment 总结](https://zhuanlan.zhihu.com/p/439206910)
* [AutoAugment Paper](https://openaccess.thecvf.com/content_CVPR_2019/papers/Cubuk_AutoAugment_Learning_Augmentation_Strategies_From_Data_CVPR_2019_paper.pdf)
* [RandAugment Paper](https://arxiv.org/abs/1909.13719)
* [SMOTE](https://arxiv.org/abs/1106.1813)
* [SamplePairing](https://arxiv.org/abs/1801.02929)
* [mixup](https://arxiv.org/abs/1710.09412)

### **分类**

——————

* 有监督的数据增强（采用预设的数据变换规则，在已有数据的基础上进行数据的扩增，包含单样本数据增强和多样本数据增强，其中单样本又包括几何操作类，颜色变换类）多样本数据增强中，利用多个样本来产生新的样本（SMOTE，Samplepairing,mixup等）
* 无监督的数据增强，包括两类（1）通过模型学习数据的分布，随机生成与训练数据集分布一致的图像（GAN代表方法）（2）通过模型学习出适合当前任务的数据增强方法（AutoAugment代表方法）

### **Autoaugment常用基础方法**

---

* ShearX(Y)是沿着x/y轴，固定另外一轴进行放射变换的过程
* TranslateX(Y)就是在水平/竖直两个方向平移图像，
* Rotate 旋转也是一种放射变换，围绕着旋转中心旋转一定角度
* AutoContrast，Contrast 图像的对比度是指图像明亮的地方与灰暗地方的像素的差别。可以认为扩大差别或者减少。自动增加对比度是指让图像中最大的灰度变为255，最小的灰度变为0，然后依次成比率改变图像的像素。
* Invert 是指对图像的像素值全部变成255
* Equalize 是指把图像的密度直方图给规则化一下。图像本质上是一组采样数据，我们可以以像素值为划分，观察在每一个像素值上有多少个像素，这就是所谓的图像直方图。可以根据直方图做出F的分布函数，Equalize操作本质上是希望这个分布函数是线性均匀上升到1的，这就是均衡化操作。
* Solarize 是指给定一个阈值，对像素值大于阈值的所有像素点做invert操作。
* Posterize 把原来每个像素用8比特表示的图像压缩到更少的比特（一个更好的压缩方法是Vector Quantization）
* Color 将颜色从RGB空间向HSV空间进行转移，其中V表示明度，S表示饱和度，H表示色调。
* Brightness 就是图像的亮度，他是HSV空间的V部分，V为0的时候表示非常暗，越高代表视觉上的越亮
* Sharpness 代表图像的锐度。锐度计算是通过图像的梯度进行计算的，即对图像的像素空间进行差分，一般差分值大的部分代表图像变化剧烈，这也就是所谓的边缘部分，增大这些边缘就会显得锐度变大。


### **其他**

————

* Cutout,与randomerasing类似，也是通过填充区域，从而将填充区域的图像信息遮挡，有利于提高模型的泛化能力。与RandomErasing不同的是，Cutout使用固定大小的正方形区域，采用全0填充，而且允许正方形区域在图片外。
