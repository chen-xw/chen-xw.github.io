---
title:  YOLOv3训练WIDERFACE数据集
categories:  YOLOv3
tags:
  - 2021年05月
---

本文主要描写了使用官网给出的YOLOv3目标检测模型（也就是使用darknet)，在Linux下对WIDERFACE数据集进行训练，以此来实现人脸检测的任务。


 <head>
     <meta name="referrer" content="no-referrer">
 </head>



### 参考链接

-------

[https://www.cnblogs.com/Assist/p/11091501.html](https://www.cnblogs.com/Assist/p/11091501.html)

[https://blog.csdn.net/lilai619/article/details/79695109](https://blog.csdn.net/lilai619/article/details/79695109)

[https://blog.csdn.net/sunqiande88/article/details/102414883](https://blog.csdn.net/sunqiande88/article/details/102414883)

### 其他资源


------

[YOLOv3官网](https://pjreddie.com/darknet/yolo/)

[YOLOv3源码](https://github.com/pjreddie/darknet)

[YOLOv3论文](https://pjreddie.com/media/files/papers/YOLOv3.pdf)

### 算法下载及使用

----
YOLOv3源码既可以在Linux下使用，也可以在Windows下使用，Windows的使用可以参考链接中的使用方法，本文是基于Linux下使用的。
* 首先从YOLOv3源码处，下载源码，参考上面其他资源处，可以使用git下载，也可以在本地下载后，上传到服务器中。下载后会出现下面的各个文件：

![](https://chen-xiuwei.github.io/image/YOLO/代码源文件.png)

*  下载后，需要进行make操作，修改Makefile文件,如下图：

![](https://chen-xiuwei.github.io/image/YOLO/makefile1.png)

> 首先修改第一处，如上图，可以修改GPU=1，表示使用GPU，CUDNN=1，表示使用CUDN加速，下面的同理，我在运行时，只使用了GPU=1，速度已经可以达到我的要求。

> 修改第二处，NVCC的位置，将后面的nvcc修改成自己nvcc在服务器上的位置,如下图

![](https://chen-xiuwei.github.io/image/YOLO/makefile2.png)

#### 目前为止，算法已经可以在本地运行，可以输入./darknet，观察输出结果，如果输出为下图，证明此部分工作已经完成。

![](https://chen-xiuwei.github.io/image/YOLO/检验darknet运行是否成功.png)

### 数据集进行处理，生成训练和验证的图片路径

----
下载的YOLOv3代码中包含了voc_label.py文件，这个文件就是用于生成训练图片路径的代码，我修改后的代码如下，修改的地方主要就是数据集的路径，总共修改了8处，最后一行代码也可以根据自己的需求进行修改。
```
import xml.etree.ElementTree as ET
import pickle
import os
from os import listdir, getcwd
from os.path import join

sets=[ ('2007', 'train'), ('2007', 'val')]   #修改处1

classes = ["face"]                           #修改处2


def convert(size, box):
    dw = 1./(size[0])
    dh = 1./(size[1])
    x = (box[0] + box[1])/2.0 - 1
    y = (box[2] + box[3])/2.0 - 1
    w = box[1] - box[0]
    h = box[3] - box[2]
    x = x*dw
    w = w*dw
    y = y*dh
    h = h*dh
    return (x,y,w,h)

def convert_annotation(year, image_id):
    in_file = open('/home/amax/cxw/tensorflow-yolov3-master/voc/train/VOCdevkit/VOC%s/Annotations/%s.xml'%(year, image_id))   #修改处3
    out_file = open('/home/amax/cxw/tensorflow-yolov3-master/voc/train/VOCdevkit/VOC%s/labels/%s.txt'%(year, image_id), 'w')  #修改处4
    tree=ET.parse(in_file)
    root = tree.getroot()
    size = root.find('size')
    w = int(size.find('width').text)
    h = int(size.find('height').text)

    for obj in root.iter('object'):
        difficult = obj.find('difficult').text
        cls = obj.find('name').text
        if cls not in classes or int(difficult)==1:
            continue
        cls_id = classes.index(cls)
        xmlbox = obj.find('bndbox')
        b = (float(xmlbox.find('xmin').text), float(xmlbox.find('xmax').text), float(xmlbox.find('ymin').text), float(xmlbox.find('ymax').text))
        bb = convert((w,h), b)
        out_file.write(str(cls_id) + " " + " ".join([str(a) for a in bb]) + '\n')

wd = "/home/amax/cxw/tensorflow-yolov3-master/voc/train"        #修改处5

for year, image_set in sets:
    if not os.path.exists('/home/amax/cxw/tensorflow-yolov3-master/voc/train/VOCdevkit/VOC%s/labels/'%(year)):                      #修改处6
        os.makedirs('/home/amax/cxw/tensorflow-yolov3-master/voc/train/VOCdevkit/VOC%s/labels/'%(year))                             #修改处7
    image_ids = open('/home/amax/cxw/tensorflow-yolov3-master/voc/train/VOCdevkit/VOC%s/ImageSets/Main/%s.txt'%(year, image_set)).read().strip().split()    #修改处8
    list_file = open('%s_%s.txt'%(year, image_set), 'w')
    for image_id in image_ids:
        list_file.write('%s/VOCdevkit/VOC%s/JPEGImages/%s.jpg\n'%(wd, year, image_id))
        convert_annotation(year, image_id)
    list_file.close()

os.system("cat 2007_train.txt 2007_val.txt > train.txt")

```
* 执行成功之后，可以看到生成了如下图的三个文件。

![](https://chen-xiuwei.github.io/image/YOLO/数据集的处理1.png)
![](https://chen-xiuwei.github.io/image/YOLO/数据集的处理2.png)

### 使用K均值聚类算法得到自己的anchors

----
这一部分你可能觉得很突兀，但这是为了下一章节修改anchors需要的工作，这个部分你可以先跳过，当需要的时候再回到这。
* 下载k-means算法或者k-means++算法对WIDERFACE数据集进行聚类，由于时间的关系，忘记是从哪下载的代码了，应该是下面的代码，记得有一个代码是不成功的（但愿不是这一个）。

```

import numpy as np

class YOLO_Kmeans:

    def __init__(self, cluster_number, filename):
        self.cluster_number = cluster_number
        self.filename = "voc_train.txt"

    def iou(self, boxes, clusters):  # 1 box -> k clusters
        n = boxes.shape[0]
        k = self.cluster_number

        box_area = boxes[:, 0] * boxes[:, 1]
        box_area = box_area.repeat(k)
        box_area = np.reshape(box_area, (n, k))

        cluster_area = clusters[:, 0] * clusters[:, 1]
        cluster_area = np.tile(cluster_area, [1, n])
        cluster_area = np.reshape(cluster_area, (n, k))

        box_w_matrix = np.reshape(boxes[:, 0].repeat(k), (n, k))
        cluster_w_matrix = np.reshape(np.tile(clusters[:, 0], (1, n)), (n, k))
        min_w_matrix = np.minimum(cluster_w_matrix, box_w_matrix)

        box_h_matrix = np.reshape(boxes[:, 1].repeat(k), (n, k))
        cluster_h_matrix = np.reshape(np.tile(clusters[:, 1], (1, n)), (n, k))
        min_h_matrix = np.minimum(cluster_h_matrix, box_h_matrix)
        inter_area = np.multiply(min_w_matrix, min_h_matrix)

        result = inter_area / (box_area + cluster_area - inter_area)
        return result

    def avg_iou(self, boxes, clusters):
        accuracy = np.mean([np.max(self.iou(boxes, clusters), axis=1)])
        return accuracy

    def kmeans(self, boxes, k, dist=np.median):
        box_number = boxes.shape[0]
        distances = np.empty((box_number, k))
        last_nearest = np.zeros((box_number,))
        np.random.seed()
        clusters = boxes[np.random.choice(
            box_number, k, replace=False)]  # init k clusters
        while True:

            distances = 1 - self.iou(boxes, clusters)

            current_nearest = np.argmin(distances, axis=1)
            if (last_nearest == current_nearest).all():
                break  # clusters won't change
            for cluster in range(k):
                clusters[cluster] = dist(  # update clusters
                    boxes[current_nearest == cluster], axis=0)

            last_nearest = current_nearest

        return clusters

    def result2txt(self, data):
        f = open("yolo_anchors.txt", 'w')
        row = np.shape(data)[0]
        for i in range(row):
            if i == 0:
                x_y = "%d,%d" % (data[i][0], data[i][1])
            else:
                x_y = ", %d,%d" % (data[i][0], data[i][1])
            f.write(x_y)
        f.close()

    def txt2boxes(self):
        f = open(self.filename, 'r')
        dataSet = []
        for line in f:
            infos = line.split(" ")
            length = len(infos)
            for i in range(1, length):
                width = int(infos[i].split(",")[2]) - \
                    int(infos[i].split(",")[0])
                height = int(infos[i].split(",")[3]) - \
                    int(infos[i].split(",")[1])
                dataSet.append([width, height])
        result = np.array(dataSet)
        f.close()
        return result

    def txt2clusters(self):
        all_boxes = self.txt2boxes()
        result = self.kmeans(all_boxes, k=self.cluster_number)
        result = result[np.lexsort(result.T[0, None])]
        self.result2txt(result)
        print("K anchors:\n {}".format(result))
        print("Accuracy: {:.2f}%".format(
            self.avg_iou(all_boxes, result) * 100))


if __name__ == "__main__":
    cluster_number = 9
    filename = "voc_train.txt"
    kmeans = YOLO_Kmeans(cluster_number, filename)
    kmeans.txt2clusters()
```

* 需要修改一下自己的filename，改成自己的路径，结果会输出九组anchors，同时还会输出一个概率，一般是70%左右（记得）。

### 修改配置文件

----
此部分需要修改.data、.names、.cfg等文件，修改成适合单目标检测（face），文件中的random属性可以设置为0（显存比较小的时候，此部分位于三个[yolo]处，下文）

1. 修改names文件
   - names文件处于data文件夹下，可以新建一个names文件，里面内容只写入face一个属性，如下图：

![](https://chen-xiuwei.github.io/image/YOLO/names文件.png)

2. 修改data文件
    - data文件处于cfg文件下，可以新建一个data文件，打开后如下图：

![](https://chen-xiuwei.github.io/image/YOLO/修改data文件.png)
    
    - 修改classes=1，只进行人脸检测
    - 修改train和valid路径，本文上一步生成的三个文件中的前两个的路径
    - 修改names路径，本章节第一小步修改的names文件路径
    - backup属性可以不用修改，它的用途忘记了，健忘


3. 修改cfg文件
* 修改batch、subdivisions属性，分为test和train两部分，由于是进行训练，因此修改如下：

![](https://chen-xiuwei.github.io/image/YOLO/cfg文件.png)
    
    > 其中batch需要根据自己电脑的配置进行修改，服务器一般可以使用64，32，自己的电脑可能要低一些，16，32都可，根据自己的需求,subdivisions也得根据自己的电脑修改，如果太高，会严重消耗CPU资源。


* 修改learning_rate,学习率可以使用多种策略，（可以上网百度，查看各种策略的区别），如下图

![](https://chen-xiuwei.github.io/image/YOLO/学习率.png)

    > 此部分使用了step策略，初始学习率设置为0.001，40000步后学习率降低为0.0001，45000步后学习率降低为0.00001，可以根据自己的需求进行调整，
    
* 修改anchors，classes和filters属性，此部分总共需要修改三处，每处三个属性，从文件的最后面向前，三部分[yolo]处，如下图
    
![](https://chen-xiuwei.github.io/image/YOLO/最后三处.png)
    
    > 前面K均值聚类算法得到的九组anchors就是用于此部分的，修改成先前得到的九组anchors；修改classes为1，filters为18（（1+5）*3）。
    


#### 前面的准备工作已经结束，下一步进行数据集的训练。

### 下载预训练权重

----
预训练权重可以使用darknet53的权重，此权重已经包含了最主要的网络结构，便于模型的扩展，并且文件还小。

[下载链接](https://pjreddie.com/media/files/darknet53.conv.74)


### 进行数据集的训练

-----
对数据集进行训练，可以在后台执行，使用nohup等命令。
* 使用官网命令如下,我使用的服务器上有两块GPU，因此为0，1
```
./darknet detector train cfg/voc.data cfg/yolov3-voc.cfg darknet53.conv.74 -gpus 0,1
```
* 查看nohup.out文件，查看中间过程，如下图：

![](https://chen-xiuwei.github.io/image/YOLO/nohup.png)

* 如果训练到中间，因其他原因导致服务器意外关闭，可以加载上已经训练出的模型权重，重新训练，如下代码
```
./darknet detector train cfg/voc-my.data cfg/yolov3-voc-my.cfg backup/yolov3-voc-100000.weights -gpus 0,1
```     
> 其中，训练出的模型权重保存在backup文件夹下。
* 使用nohup命令如下
```
nohup ./darknet detector train cfg/voc.data cfg/yolov3-voc.cfg darknet53.conv.74 -gpus 0,1 &
```                                                                   
> 如果出现没有权限，把错误百度，有解决方法。

#### 到目前为止，训练的过程已经结束，当你理解YOLOv3模型和训练过程的参数的含义后，下一步就是常说的“炼药”的过程了，修改自己的学习率，batch等参数让自己的模型更精确。

### 可能遇到的错误

-----
其他错误，一般都能在网上百度到，博客的连接中也写明了大部分的错误，如果make阶段出现错误，建议只开GPU=1，我使用过程中，由于是老师的服务器，没有大部分的权限，报了很多错误，因此只使用了GPU=1.
* 你可能出现./darknet: error while loading shared libraries: libcudart.so.10.0: cannot open shared object file: No such file or directory这个错误，解决方法如下：
```
export LD_LIBRARY_PATH=/usr/local/cuda/lib64 && sudo ldconfig
```
> 通过输入密码后，成功解决了上述错误。


#### 如有问题，欢迎交流！
