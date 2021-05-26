---
title:  WIDERFACE数据集转化为VOC格式
categories:  YOLOv3
tags:
  - 2021年05月26日
---

本文是对WIDERFACE数据集进行预处理，生成YOLOv3代码输入要求的COCO或者VOC格式，在此将其转化成了VOC格式，总体来说，此部分比较简单。

##参考链接

----

https://blog.csdn.net/sunqiande88/article/details/102414883

##下载WIDERFACE数据集

------

[数据集官网下载](http://shuoyang1213.me/WIDERFACE/)

* 下载数据集可以从上述官网中下载，也可以直接在网上搜索，可以找到许多百度网盘分享的，下载后可以看到如下内容：


* 其中WIDER_train为训练集，WIDER_test为测试集，WIDER_val为验证集，wider_face_split包含了人脸框等信息。

## 训练集、验证集转换为VOC格式

-----
借鉴网上的代码将WIDERFACE数据集转换为VOC格式

```
# -*- coding: utf-8 -*-

import shutil
import random
import os
import string
from skimage import io

headstr = """\
<annotation>
    <folder>VOC2012</folder>
    <filename>%06d.jpg</filename>
    <source>
        <database>My Database</database>
        <annotation>PASCAL VOC2012</annotation>
        <image>flickr</image>
        <flickrid>NULL</flickrid>
    </source>
    <owner>
        <flickrid>NULL</flickrid>
        <name>company</name>
    </owner>
    <size>
        <width>%d</width>
        <height>%d</height>
        <depth>%d</depth>
    </size>
    <segmented>0</segmented>
"""
objstr = """\
    <object>
        <name>%s</name>
        <pose>Unspecified</pose>
        <truncated>0</truncated>
        <difficult>0</difficult>
        <bndbox>
            <xmin>%d</xmin>
            <ymin>%d</ymin>
            <xmax>%d</xmax>
            <ymax>%d</ymax>
        </bndbox>
    </object>
"""

tailstr = '''\
</annotation>
'''


def writexml(idx, head, bbxes, tail):
    filename = ("Annotations/%06d.xml" % (idx))
    f = open(filename, "w")
    f.write(head)
    for bbx in bbxes:
        f.write(objstr % ('face', bbx[0], bbx[1], bbx[0] + bbx[2], bbx[1] + bbx[3]))
    f.write(tail)
    f.close()


def clear_dir():
    if shutil.os.path.exists(('Annotations')):
        shutil.rmtree(('Annotations'))
    if shutil.os.path.exists(('ImageSets')):
        shutil.rmtree(('ImageSets'))
    if shutil.os.path.exists(('JPEGImages')):
        shutil.rmtree(('JPEGImages'))

    shutil.os.mkdir(('Annotations'))
    shutil.os.makedirs(('ImageSets/Main'))
    shutil.os.mkdir(('JPEGImages'))


def excute_datasets(idx, datatype):

    f = open(('ImageSets/Main/' + datatype + '.txt'), 'a')
    f_bbx = open(('wider_face_split/wider_face_' + datatype + '_bbx_gt.txt'), 'r')

    while True:
        filename = f_bbx.readline().strip('\n')

        if not filename:
            break
        im = io.imread(('WIDER_' + datatype + '/images/' + filename))
        head = headstr % (idx, im.shape[1], im.shape[0], im.shape[2])
        nums = f_bbx.readline().strip('\n')
        bbxes = []
        if nums=='0':
            bbx_info= f_bbx.readline()
            continue
        for ind in range(int(nums)):
            bbx_info = f_bbx.readline().strip(' \n').split(' ')
            bbx = [int(bbx_info[i]) for i in range(len(bbx_info))]
            # x1, y1, w, h, blur, expression, illumination, invalid, occlusion, pose
            if bbx[7] == 0:
                bbxes.append(bbx)
        writexml(idx, head, bbxes, tailstr)
        shutil.copyfile(('WIDER_' + datatype + '/images/' + filename), ('JPEGImages/%06d.jpg' % (idx)))
        f.write('%06d\n' % (idx))
        idx += 1
    f.close()
    f_bbx.close()
    return idx


if __name__ == '__main__':
    clear_dir()
    idx = 1
    idx = excute_datasets(idx, 'val')
    idx = excute_datasets(idx, 'train')
    print('Complete...')

```
* 其中main函数中，可以修改val和train来改成自己需要的，前者为验证集，后者为训练集，这部分代码执行是与下载的数据集同一个文件中的。
* 运行代码，输出Complete...后，查看原来的文件可以看到多了三个文件，如下图，各个文件表示的含义就是VOC格式的文件。

## 测试集转换为VOC格式

-----

* 网上搜了很长时间没有找到转换测试集的代码，自己认真分析了上述代码，测试集没有人脸框的标注，原来可以修改上述代码，是自己菜了，代码如下：
```
# -*- coding: utf-8 -*-

import shutil
import random
import os
import string
from skimage import io

headstr = """\
<annotation>
    <folder>VOC2012</folder>
    <filename>%06d.jpg</filename>
    <source>
        <database>My Database</database>
        <annotation>PASCAL VOC2012</annotation>
        <image>flickr</image>
        <flickrid>NULL</flickrid>
    </source>
    <owner>
        <flickrid>NULL</flickrid>
        <name>company</name>
    </owner>
    <size>
        <width>%d</width>
        <height>%d</height>
        <depth>%d</depth>
    </size>
    <segmented>0</segmented>
"""
objstr = """\
    <object>
        <name>%s</name>
        <pose>Unspecified</pose>
        <truncated>0</truncated>
        <difficult>0</difficult>
        <bndbox>
            <xmin>%d</xmin>
            <ymin>%d</ymin>
            <xmax>%d</xmax>
            <ymax>%d</ymax>
        </bndbox>
    </object>
"""

tailstr = '''\
</annotation>
'''




def writexml(idx, head, bbxes, tail):
    filename = ("Annotations/%06d.xml" % (idx))
    f = open(filename, "w")
    f.write(head)
    for bbx in bbxes:
        f.write(objstr % ('face', bbx[0], bbx[1], bbx[0] + bbx[2], bbx[1] + bbx[3]))
    f.write(tail)
    f.close()


def clear_dir():
    if shutil.os.path.exists(('Annotations')):
        shutil.rmtree(('Annotations'))
    if shutil.os.path.exists(('ImageSets')):
        shutil.rmtree(('ImageSets'))
    if shutil.os.path.exists(('JPEGImages')):
        shutil.rmtree(('JPEGImages'))

    shutil.os.mkdir(('Annotations'))
    shutil.os.makedirs(('ImageSets/Main'))
    shutil.os.mkdir(('JPEGImages'))


def excute_datasets(idx, datatype):

    f = open(('ImageSets/Main/' + datatype + '.txt'), 'a')
    f_bbx = open(('wider_face_split/wider_face_' + datatype + '_filelist.txt'), 'r')

    while True:
        filename = f_bbx.readline().strip('\n')

        if not filename:
            break

        shutil.copyfile(('WIDER_' + datatype + '/images/' + filename), ('JPEGImages/%06d.jpg' % (idx)))
        f.write('%06d\n' % (idx))
        idx += 1
    f.close()
    f_bbx.close()
    return idx


if __name__ == '__main__':
    clear_dir()
    idx = 1
    idx = excute_datasets(idx, 'test')
    print('Complete...')

```
* 之前转换的代码删了，这部分是自己写博客的时候，凭记忆修改的，如果有问题，可以自己读一下代码。
* 代码运行提示成功后，可以看到输出了两个文件，如下图，之所以没有以前的几个文件是因为测试集没有人脸框的标注。

####  总体来说，上述已经完成了WIDERFACE数据集转换为VOC数据集，但是后续代码评估时，你可能需要（有可能，看你的评估模型）labels文件，因此下面是用于生成labels文件的代码。 

## 生成labels文件

----
下面的代码，就是生成labels文件的代码，实在是忘记从哪下载的了，因此没有在开始处复制链接。
````
"""
 @Usage: generate custom voc-format-dataset labels, convert .xml to .txt for each image
 @author: sun qian
 @date: 2019/9/25
 @note: dataset file structure must be modified as:
 --VOCdevkit
   --VOC2012
     --Annotations
     --ImageSets
        --Main (include train.txt, test.txt, val.txt)
     --JPEGImages
     --labels
 @ merge val and test: Run command: type 2012_test.txt 2012_val.txt  > test.txt
"
import xml.etree.ElementTree as ET
import os
from os import getcwd

# file list - train.txt, test.txt, val.txt
sets = [('2012', 'train'), ('2012', 'val')]

# class name
classes = ["face"]


def convert(size, box):
    dw = 1. / size[0]
    dh = 1. / size[1]
    x = (box[0] + box[1]) / 2.0
    y = (box[2] + box[3]) / 2.0
    w = box[1] - box[0]
    h = box[3] - box[2]
    x = x * dw
    w = w * dw
    y = y * dh
    h = h * dh
    return (x, y, w, h)


def convert_annotation(year, image_id):
    in_file = open('VOCdevkit/VOC%s/Annotations/%s.xml' % (year, image_id))
    out_file = open('VOCdevkit/VOC%s/labels/%s.txt' % (year, image_id), 'w')
    tree = ET.parse(in_file)
    root = tree.getroot()
    size = root.find('size')
    w = int(size.find('width').text)
    h = int(size.find('height').text)

    for obj in root.iter('object'):
        difficult = obj.find('difficult').text
        cls = obj.find('name').text
        if cls not in classes or int(difficult) == 1:
            continue
        cls_id = classes.index(cls)
        xmlbox = obj.find('bndbox')
        b = (float(xmlbox.find('xmin').text), float(xmlbox.find('xmax').text), float(xmlbox.find('ymin').text),
             float(xmlbox.find('ymax').text))
        bb = convert((w, h), b)
        out_file.write(str(cls_id) + " " + " ".join([str(a) for a in bb]) + '\n')


if __name__ == '__main__':
    wd = getcwd()
    for year, image_set in sets:
        if not os.path.exists('VOCdevkit/VOC%s/labels/' % (year)):
            os.makedirs('VOCdevkit/VOC%s/labels/' % (year))
        image_ids = open('VOCdevkit/VOC%s/ImageSets/Main/%s.txt' % (year, image_set)).read().strip().split()
        list_file = open('%s_%s.txt' % (year, image_set), 'w')
        for image_id in image_ids:
            line = '%s/VOCdevkit/VOC%s/JPEGImages/%s.jpg\n' % (wd, year, image_id)
            list_file.write(line.replace("\\", '/'))
            convert_annotation(year, image_id)
        list_file.close()

````
* 运行上述代码之后，可以看到文件夹下多了一个labels文件，里面的信息是归一化后的坐标信息和类别。

#### 到目前为止，转换的工作已经全部完成，下一步就行进行自己的训练了。

#### 如有问题，欢迎交流！
