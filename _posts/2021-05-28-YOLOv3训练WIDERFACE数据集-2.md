---
title:  YOLOv3训练WIDERFACE数据集
categories:  YOLOv3
tags:
  - 2021年05月28日
---

本文主要是基于上一篇YOLOv3训练WIDERFACE数据集而补充的知识，上一篇中使用了YOLOv3的官网代码进行训练的，本文中将说明使用Tensorflow和keras进行训练,主要是基于Lilnux下，在Windows下也可以运行，只不过对于路径的问题，需要修改一下，详见文章底部。

### 参考资源

-----
[Tensorflow代码资源](https://github.com/YunYang1994/tensorflow-yolov3)

[Keras+Tensorflow代码资源](https://github.com/qqwweee/keras-yolo3)


### 代码下载

----
参考上面代码链接，下载相关代码，可以直接使用git下载，也可以下载到本地后上传到服务器上。

### 环境要求

--------
* 服务器上使用的python版本为3.6，Tensorflow版本为1.14.1，记得1.14之前版本的是下载不成功的，Keras版本为2.1.5，numpy版本为1.19.2，其他环境根据自己的需求下载即可，上面的环境是部署在服务器上的，运行代码没有问题。

> Tensorflow不推荐使用2.0版本以上的，之前使用过2.0版本以上的，报错是很难解决的，网上的解决方法特别少，过一段时间可能就好了。

* Windows10下的python版本为3.7，Tensorflow-GPU版本为1.14.1，Keras版本也是2.1.5

#### 由于代码中有详细的使用步骤，在此就不赘述了，下面记录一下运行过程中的问题。

### 权重文件

----
* YunYang大佬的代码中，对你下载的.weights文件（可能是yolov3.weights、darknet53.weights、darknet53.conv.74），首先进行convert_weights(或者是from_darknet_weights_to_cpkt)操作，转换成Tensorflow样式的权重文件，转换之后，你可以进行相应的操作，但是如果你想检测图片，不管是使用原先的Tensorflow样式的权重文件还是你训练出来的权重文件，都得经过freeze_graph（或者from_darknet_weights_to_pb）操作，生成pb文件，因为检测代码中使用的正是pb文件。

* qqwwee大佬的代码中，对权重文件进行convert操作后转换成了h5文件，进行相应的操作。

### 保存检测结果

----
服务器中无法直接显示图片，你可以保存下检测结果进行查看，修改代码如下：

* YunYang大佬中的，在image_demo中修改，文档中的最后处
```
image = Image.fromarray(image)
image.save('./picture/output.jpg')
#image.show()
```
* qqwwee大佬中的，在yolo_video中第16行处
```
 r_image = yolo.detect_image(image)
            r_image.show()
            r_image.save('./picture/output.jpg')
```

### 遇到的问题

----
1. 在运行qqwwee大佬检测视频的时候，输入一段视频，会报一个错误，具体忘了是什么错误了，需要修改的地方是视频输出路径中必须有数字，如下：
```
def detect_video(yolo, video_path, output_path="./output001.mp4"):
```

#### 目前想到的问题就这么多，后续继续补充。

#### 如有问题，欢迎交流！