# Yolov1

相比于本文前的两阶段式的检测算法，yolo十分简单，把识别问题综合看成一个回归问题。

## Unified Detection 
yolov1的主要特点，后面yolov2换成了anchor的算法，这个算法效果不是很好，看原文，此处不赘述。

## loss
本文的loss是主要的创新点：使用了sum-squared error，目的是最小化MAP。
1. 原本的loss，对于分类的loss和框定位的loss权重的相同的，显然这个是不合理的。通过给与对应0.5和5的权重。避免了空的框中，confidence趋向0而导致的梯度消失。
2. 大框小位移往往loss会压过小框大位移。这个问题作者没有完全解决，通过预测 w,h的平方来减缓这个问题。
3. 和unified detection相关的loss优化。

## 注意点：
1. yolo的一个特点是其具有很大的泛化性，所以作者为了更快的拟合，往往会先在imageNet上先进行训练，提取通用特征。
2. yolov1的loss在不同大小的box之间的loss分配是手动分配的，有根本性缺陷。yolov2加入anchor，yolov3微调，根本上是优化loss。
3. yolov1强处在于分类准，同时误检率低。R-CNN的框定准确。两两结合效果优秀。
