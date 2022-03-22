# YOLO5Face: Why Reinventing a Face Detector
## 简介：
使用yolov5作为backbone去做face detector，其有个前提那就是认为人脸识别可以直接套用通用识别器的backbone。同时文章中还实验了在比较小的flops的情况下使用shuffleNet。

## 五点人脸关键点 five-point landmark regression head
通常的目标检测识别器没有包含关键点检测，所以本文加入了landmark head。通常的关键点识别使用L1，smooth-L1或L2回归。但是都有各自的问题，本文采用了Wing-Loss来回归。
$${wing(x)} = w \cdot ln(1 + |x| / e),if\,x<w$$
$$wing(x) = |x| - C,otherwise$$
$w$一定大于0，设置了在回归方程中非线性部分。  
$e$限制了非线性区域的曲率程度。  
$C=w-wln(1+w/e)$是一个常数，可以平滑化回归方程中线性部分和非线性部分。  
实际中我们是五点的特征点,$s_i$是识别的，$s_i^`$是ground truth。用如下的方程  
$$loss_L(s) = \sum_{i=1}^{5}{wing(s_i - s_i^`)}$$
总的YOLO5Face的损失函数
$$loss(s) = loss_O + \lambda_L \cdot loss_L$$
  
    

## 别的信息
这篇文章涉及到很多别的文章中的信息，但是又有很多没有细讲。基本上是大杂烩然后做实验。这里列出
* Yolo系列的信息，anchor，cbs等等
* stem block structure
* ShuffleNetV2 V1
* FPN和PAN

## 结论
最后效果很好 巴拉巴拉巴拉， 但是不如SCRFD。这表示手动设计网路，真的不如算法算出来的。