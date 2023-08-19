---
title: Incremental Learning
categories: Machine Learning
tags:
  - 2022年06月24日
---

Incremental Learning's Survey,挺长时间没有进行总结了，现在花点时间总结一下近期在做的方向，这段时间主要进行的是对增量学习的研究。


### **学习资源**

___

* [全集论文合集](https://github.com/xialeiliu/Awesome-Incremental-Learning)
* [代码合集](https://github.com/G-U-N/PyCIL)

### **目标**

---

* 借用一篇论文中话" Incremental Learning aims to develop artificially intelligent systems that can continuously learn to address new tasks from new data while preserving knowledge learned from previously learned tasks.
* 我的理解呢？简单的说就是 给你n个不同的任务（n个不同的数据集，disjoint），输入呢？ 就是这一个个的任务Ti，送入模型（第一个随机化的模型或者上一个任务得到的模型）进行训练，输出呢？就是经过当前任务训练完成的模型。测试就是用最后得到的模型在当前见过的所有的任务上的准确率。

### **难点**

---

* Catastrophic Forgetting

### **目前主流方法**

---

* 主要分为三大类：Replay methods、Regularization-based methods、Parameter isolation methods

#### **Replay Methods**

* 这种方法又可以分为Rehearsal、Pseudo Rehearsal、Constrained,其中Rehearsal methods包括了ICarl、ER、SER、TEM、CoPE；Pseudo Rehearsal包括了DGR、PR、CCLUGM、LGM；Constrained包括了GEM、A-GEM、GSS。
 
#### **Regularization-based methods**

* 这种方法又可以分为Prior focused、Data focused,其中Prior focused包括了EWC、IMM、SI、R-EWC、MAS、Riemannian、Walk；Data focused包括了LWF、LFL、EBLL、DMC。

#### **Parameter isolation methods**

* 这种方法又可以分为Fixed Network、Dynamic Architectures，其中Fixed Network包括了PackNet、PathNet、Piggyback、HAT；Dynamic Architectures包括了PNN、Expert Gate、RCL、DAN。


### **常用的数据集**

---

* CIFAR100数据集，100个类，每个类有600张图片，一般500张用来训练，100张用来测试；
* Tiny Imagenet数据集，200个类，每个类总共有600张图片，500张用来训练，50张验证，50张测试；
* Imagenet 1k数据集，1000个类，1281167张用来训练，50000张用来验证，100000用与测试。

### **Low & High level**

---

* Low level, 普通的SGD优化
* High Level, 将所有Task的数据集放在一起进行训练

### **目前效果对比**


### 暂时写到这，有空了再来补充