# U-Net: Convolutional Networks for Biomedical Image Segmentation
U-Net 一个小样本细胞分类比赛中 最优的结果，远优于滑动窗口的CNN。

# 最重要的创新
在FCN的文章中，作者并没有对‘skip’架构给与足够的重视，本文中重点介绍了他们自己的‘skip’结构。他们在上采样阶段使用了大量的特征通道融合，这使得网络可以把深层的语义信息传播到最高分辨率，最浅层的输出。同时U-Net和FCN一样没有任何的全连接层。事实上，相对于FCN-8s，U-Net把所有的特征图全部融合起来，这是其效果优秀（同时计算量巨大）的特点。U-Net由此也获得的卷积+池化和上卷积部分完全对称的U型网路结构，这也给与了它的名字。


## Notes
CSDN上都是什么妖魔鬼怪，介绍U-nets的文章全他妈扯蛋的，看原论文，还有原作者的讲解视频比什么都靠谱。

# 为什么效果好?其实不是网路结构的创新
根据我自己复现的结果，U-Net的效果很差。看原论文后得出结论，这篇论文效果之所以好，主要是其训练数据处理和损失函数选择十分优秀。如果不采用其采用的数据增强方式or损失函数。效果会下降很多。

## 数据增强——elastic deformations
在生物语义分割中，细胞常常被扭曲。所以在训练集中加入这种随机的扭曲十分重要和有效。具体实现方式是通过using random displacement vectors on a coarse 3 by 3 grid. 当然旋转，平移缩放。此次训练中也使用了。

## 数据增强——预测边界上细胞
To predict the pixels in the border region of the image, the missing context is extrapolated by mirroring the input image.

## 损失函数——细胞边界损失函数
因为细胞会聚集在一起，边界很难分离开来，作者提出了一种weighted loss。The separating background labels between touching sells obtain a large weight in the loss function.作者在训练之前就计算了ground truth来得到这些数据，这些数据加上损失函数会逼迫网络去学习细胞之间细小的分界线。

## 输出层的softmax
The energy function is computed by a pixel-wise soft-max over the finalfeature map combined with the cross entropy loss function. The soft-max is defined as 
$$p_k(x) = exp(a_k(x))/(\sum_{k^`=1}^Kexp(a_{k^`}(x)))$$ 
K是有多少类，$a_k(x)$代表的是输出像素。

## 损失函数——像素级别交叉熵损失函数
$$ E = \sum_{X \in \Omega} w(x) log(p_{l(x)}(x))$$
这会对每一个位置的像素计算损失。$\Omega$里面是所有的识别类别。



