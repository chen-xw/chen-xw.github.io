---
title:  YOLOv3在WIDERFACE数据集测试自己的模型
categories:  YOLOv3
tags:
  - 2021年05月30日
---

本文主要是在WIDERFACE数据集上评估自己的模型（利用官网代码生成的模型），包括图片的检测、损失函数的绘制、验证集上准确率和召回率的计算以及P-R曲线的绘制。

 <head>
     <meta name="referrer" content="no-referrer">
 </head>



### 参考资源

----
[绘制损失函数、IOU](https://blog.csdn.net/qq_34806812/article/details/81459982?utm_source=blogxgwz3)

[绘制p-r曲线](https://blog.csdn.net/tzwsg/article/details/107677231?utm_medium=distribute.pc_aggpage_search_result.none-task-blog-2~aggregatepage~first_rank_v2~rank_aggregation-6-107677231.pc_agg_rank_aggregation&utm_term=yolov3%E7%BB%98%E5%88%B6pr%E6%9B%B2%E7%BA%BF&spm=1000.2123.3001.4430)

[计算recall值](https://blog.csdn.net/cgt19910923/article/details/80524173)

[reval_voc_py.py代码](https://blog.csdn.net/xue_csdn/article/details/95519585)

[voc_eval.py代码](https://blog.csdn.net/qq_32473523/article/details/107493849)

[计算准确率、召回率等](https://blog.csdn.net/qq_33193309/article/details/108453810)

### 图片的检测

----
单图片检测部分是比较简单的一个步骤，忘记了源代码中是否有保存检测结果的代码，如果没有自己添加即可。

```
./darknet detect cfg/yolov3.cfg yolov3.weights data/dog.jpg
```

### 损失函数的绘制

----
这部分的前提应该是你有每次迭代过程的记录文件，可以是nohup命令得出的nohup.out文件，也可以是其他形式的文件。

* 首先利用extract_log.py文件对nohup.out文件进行处理，取出每次迭代过程的记录文件，去除其他没有用的信息，代码借鉴了参考资源中的代码。运行成功后，会得到下图中的两个文件（我生成了多次）。

![](http://chen-xiuwei.github.io/image/YOLO/损失函数.png)

```
# coding=utf-8
# 该文件用来提取训练log，去除不可解析的log后使log文件格式化，生成新的log文件供可视化工具绘图
 
import inspect
import os
import random
import sys
def extract_log(log_file,new_log_file,key_word):
    with open(log_file, 'r') as f:
      with open(new_log_file, 'w') as train_log:
  #f = open(log_file)
    #train_log = open(new_log_file, 'w')
        for line in f:
    # 去除多gpu的同步log
          if 'Syncing' in line:
            continue
    # 去除除零错误的log
          if 'nan' in line:
            continue
          if key_word in line:
            train_log.write(line)
    f.close()
    train_log.close()
 
extract_log('train_yolov3.log','train_log_loss.txt','images')
extract_log('train_yolov3.log','train_log_iou.txt','IOU')
```

* 运行train_loss_visualization.py文件，绘制loss函数图像，代码也是参考资源中的，此时就会出现你所需要的图像。

```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
#%matplotlib inline
 
lines =50000    #改为自己生成的train_log_loss.txt中的行数
result = pd.read_csv('train_log_loss.txt', skiprows=[x for x in range(lines) if ((x%10!=9) |(x<1000))] ,error_bad_lines=False, names=['loss', 'avg', 'rate', 'seconds', 'images'])
result.head()
 
result['loss']=result['loss'].str.split(' ').str.get(1)
result['avg']=result['avg'].str.split(' ').str.get(1)
result['rate']=result['rate'].str.split(' ').str.get(1)
result['seconds']=result['seconds'].str.split(' ').str.get(1)
result['images']=result['images'].str.split(' ').str.get(1)
result.head()
result.tail()
 
# print(result.head())
# print(result.tail())
# print(result.dtypes)
 
print(result['loss'])
print(result['avg'])
print(result['rate'])
print(result['seconds'])
print(result['images'])
 
result['loss']=pd.to_numeric(result['loss'])
result['avg']=pd.to_numeric(result['avg'])
result['rate']=pd.to_numeric(result['rate'])
result['seconds']=pd.to_numeric(result['seconds'])
result['images']=pd.to_numeric(result['images'])
result.dtypes
 
 
fig = plt.figure()
ax = fig.add_subplot(1, 1, 1)
ax.plot(result['avg'].values,label='avg_loss')
# ax.plot(result['loss'].values,label='loss')
ax.legend(loc='best')  #图列自适应位置
ax.set_title('The loss curves')
ax.set_xlabel('batches')
fig.savefig('avg_loss')
# fig.savefig('loss')

```

#### 绘制损失函数的图像就上述两个操作，同理，绘制IOU图像也是类似的，只需要运行参考链接中的train_IOU_visualization.py文件即可。

### 使用Fast R-CNN代码中的方法计算准确率

----
这是我第一个使用的计算准确率的方法，虽然处理预测文件的时候，我去除了非人脸信息的检测结果，也设置了相应的阈值，但是很奇怪的是计算出的准确率离奇的低。

* 从上述参考资源处下载voc_eval.py和reval_voc_py3.py文件

* 利用官网代码对验证集的图片进行检测，默认生成comp4_det_test_face.txt(在results文件夹下)

```
./darknet detector valid cfg/voc.data cfg/yolov3-voc.cfg backup/yolov3-voc_final.weights -out car.txt -gpu 0 -thresh .5
```

* 运行reval_voc_py3.py代码，会得到各个类别的AP值，以及mAP值。

> 每次检测后都会在voc2007数据集文件夹下生成一个annotation的文件，需要再次检测时，得把它删除，不然报错。

```
python3.6 reval_voc_py3.py  --voc_dir /home/amax/cxw/darknet-master/voc/VOCdevkit --year 2007 --image_set test --classes data/voc-my.names  Testforpr
```

### 绘制p-r曲线

----
上一步骤中，已经求得了准确率和召回率的值，并保存在了pkl文件中，绘制p-r曲线时，只需要加载上这个文件即可。

```
# coding=utf-8
import _pickle as cPickle
import matplotlib.pyplot as plt

plt.rcParams['font.sans-serif'] = [u'NSimSun']
plt.rcParams['axes.unicode_minus'] = False
fr = open('tower_pr.pkl', 'rb')  # 这里open中第一个参数需要修改成自己生产的pkl文件
inf = cPickle.load(fr)
fr.close()

# fbad = open('tower_pr.pkl','rb')#这里open中第一个参数需要修改成自己生产的pkl文件
# inf_bad = cPickle.load(fbad)
# fbad.close()


x = inf['rec']
y = inf['prec']
plt.figure()
plt.xlabel('召回率', size=15)
plt.ylabel('精确率', size=15)
plt.xticks(fontproperties='Times New Roman', size=14)
plt.yticks(fontproperties='Times New Roman', size=14)

plt.plot(x, y)

plt.savefig("PR曲线.svg", bbox_inches='tight')  # plt保存需要在show之前
plt.show()

print('AP：', inf['ap'])

```

### 利用一个更直观的方法计算AP值

----
AP值的计算无非就是将验证集的检测结果同原数据进行对比，设置相应的阈值，计算数据即可。

* 首先是要对验证集上的检测结果进行处理，将每幅图片检出的人脸保存到每一个txt文件中，有多少张图片就会有多少txt文件。代码如下：

![](http://chen-xiuwei.github.io/image/YOLO/test结果.png)

```
import os
 
# txt_file为配置文件.data中的valid
txt_file = '/home/amax/cxw/darknet-master/scripts/2007_val.txt'
f = open(txt_file)
lines = f.readlines()
for line in lines:
    line = line.split('/')[-1][0:-5]
    # test_out_file 为转换后保存的结果地址
    test_out_file = '/home/amax/cxw/darknet-master/testresults'
    # 下面3个with需要自己的修改，修改成自己对应的类别
    with open(os.path.join(test_out_file , line + '.txt'), "a") as new_f:
        f1 = open('/home/amax/cxw/darknet-master/results/comp4_det_test_face.txt', 'r')
        f1_lines = f1.readlines()
        for f1_line in f1_lines:
            f1_line = f1_line.split()
            if line == f1_line[0]:
                new_f.write("%s %s %s %s %s %s\n" % ('smoke', f1_line[1], f1_line[2], f1_line[3], f1_line[4], f1_line[5]))
```

* 同理对你原先的标注数据集进行相应的处理，也处理成上述的格式，便于比较，注意其中的Labels文件是经过归一化处理之后的文件了，要进行相应的复原操作。

```
import os
from PIL import Image
import numpy as np
# label_img为数据集的labels地址，img_path为数据集images的地址
label_img = '/home/amax/cxw/darknet-master/voc/VOCdevkit/VOC2007/labels'
img_path = '/home/amax/cxw/darknet-master/voc/VOCdevkit/VOC2007/JPEGImages'
classes = {
    0:'smoke',
    1:'white',
    2:'red'
}
for line in lines:
    line = line.split('/')[-1][0:-5] + '.txt'
    txt = label_img + line
    img = np.array(Image.open(img_path + line.split('/')[-1][0:-4] + '.jpg'))
    sh, sw = img.shape[0], img.shape[1]
    # gt_out_file为转换后的地址
    gt_out_file = '/home/amax/cxw/darknet-master/yoloresults'
    with open(os.path.join(gt_out_file , line ), "a") as new_f:
        f1 = open(txt)
        f1_lines = f1.readlines()
        for f1_line in f1_lines:
            f1_line = f1_line.split()
            x = float(f1_line[1]) * sw
            y = float(f1_line[2]) * sh
            w = float(f1_line[3]) * sw
            h = float(f1_line[4]) * sh
            xmin = x+1-w/2
            ymin = y+1-h/2
            xmax = x+1+w/2
            ymax = y+1+h/2
            new_f.write("%s %s %s %s %s\n" % (classes[int(f1_line[0])], xmin ,ymin,xmax,ymax))

```

* 执行如下代码，可以计算出标注人脸框、检测出的总人脸框、检测正确的人脸框和检测错误的人脸框，可以根据自己的需要设置相应的阈值，所谓的阈值就是利用交并比判定是否是人脸框的标准，大于阈值的判定为人脸框，否则不是人脸框。

```
import os
 
 
def compute_IOU(rec1, rec2):
    """
    计算两个矩形框的交并比。
    :param rec1: (x0,y0,x1,y1)      (x0,y0)代表矩形左上的顶点，（x1,y1）代表矩形右下的顶点。下同。
    :param rec2: (x0,y0,x1,y1)
    :return: 交并比IOU.
    """
    left_column_max = max(rec1[0], rec2[0])
    right_column_min = min(rec1[2], rec2[2])
    up_row_max = max(rec1[1], rec2[1])
    down_row_min = min(rec1[3], rec2[3])
    # 两矩形无相交区域的情况
    if left_column_max >= right_column_min or down_row_min <= up_row_max:
        return 0
    # 两矩形有相交区域的情况
    else:
        S1 = (rec1[2] - rec1[0]) * (rec1[3] - rec1[1])
        S2 = (rec2[2] - rec2[0]) * (rec2[3] - rec2[1])
        S_cross = (down_row_min - up_row_max) * (right_column_min - left_column_max)
        return S_cross / (S1 + S2 - S_cross)
 
# gt为yolo数据转换后的地址
gt = '/home/amax/cxw/darknet-master/yoloresults/'
# test为检测结果转换后的地址
test = '/home/amax/cxw/darknet-master/testresults/'
# count_gt为标注的所有数据框
count_gt = {
 
}
# count_test为检测的所有数据框
count_test = {
 
}
# count_yes_test为检测正确的数据框
count_yes_test = {
 
}
# count_no_test为检测错误的数据框
count_no_test = {
 
}
# 计数
for gt_ in os.listdir(gt):
    txt = gt + gt_
    f = open(txt)
    lines = f.readlines()
    for line in lines:
        line = line.split()
        name = line[0]
        if name not in count_gt:
            count_gt[name] = 0
        count_gt[name] += 1
for test_ in os.listdir(test):
    txt = test + test_
    f = open(txt)
    lines = f.readlines()
    for line in lines:
        line = line.split()
        name = line[0]
        if name not in count_test:
            count_test[name] = 0
        count_test[name] += 1
# 下面主要思想：遍历test结果，再遍历对应gt的结果，如果两个框的iou大于一定的阙址并且类别相同，视为正确
for test_ in os.listdir(test):
    f_test_txt = test + test_
    f_test = open(f_test_txt)
    f_test_lines = f_test.readlines()
    for f_test_line in f_test_lines:
        f_test_line = f_test_line.split()
        f_gt_txt = gt + test_
        f_gt = open(f_gt_txt)
        f_gt_lines = f_gt.readlines()
        flag = 1
        for f_gt_line in f_gt_lines:
            f_gt_line = f_gt_line.split()
            IOU = compute_IOU([float(f_gt_line[1]), float(f_gt_line[2]), float(f_gt_line[3]), float(f_gt_line[4])],
                              [float(f_test_line[2]), float(f_test_line[3]), float(f_test_line[4]), float(f_test_line[5])])
            if f_gt_line[0] == f_test_line[0] and IOU >= 0.5 and float(f_test_line[1]) >= 0.3:
                flag = 0
                if f_test_line[0] not in count_yes_test:
                    count_yes_test[f_test_line[0]] = 0
                count_yes_test[f_test_line[0]] += 1
 
        if flag == 1:
            if f_test_line[0] not in count_no_test:
                count_no_test[f_test_line[0]] = 0
            count_no_test[f_test_line[0]] += 1
# 有以下4个结果，就可以计算相关指标了
print(count_gt)
print(count_test)
print(count_yes_test)
print(count_no_test)

```

#### 注意修改文件的路径，第三部分介绍的计算准确率的方法比利用Fast R-CNN的方法简单，没有详细的研究第二部分的方法，有时间再去补充。

#### 如有问题，欢迎交流！

