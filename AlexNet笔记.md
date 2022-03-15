# AlexNet 网络 -- ImageNet Classification with Deep Convolutional Neural Networks
 *注:按照b站上面李沐学AI记下来的笔记*

### 重要结果：
 * 深度卷积网络训练出来的最后一个向量在语义空间里面表示的特别好（相似的图片可以合到一起）  
 * 第一个端到端的网络，当时别的工作都是输入比如说sift这样的特征，他是RGB输入。

### 两个贡献：
  1. 网络的架构  
  2. 怎么防止过拟合

## 网络架构上的创新
1. **激活函数 Relu**：relu比tanh和sigmod要效果更好，rulu相对于tanh训练拟合更快。*李老师：现在来看比不一定比别人好很多，但是因为他简单所以大家都在用。*
2. **Local Response Normalization** 现在看来没有什么必要，没有多少人用到他。现在有更好的技术（没有读，因为现在不需要了）
3. **Overlap Pooling**, 如果pool的stride小于size那就会出现重叠，使用重叠的会轻微的效果提升，轻微的防止过拟合
4. **Overall Architecture** 模型切割放到两个gpu上训练，后来不常见，但是最近由于新的模型出现，由流行起来了

## 防止过拟合上的创新
1. **数据增强** 为了减少过拟合：输入是在256 * 256的图，然后随机切224 * 224来数据增强。
2. **Dropout** 使用了Dropout，Dropout随机把一些隐藏层的输出用50%的概率设置为0。*李老师：dropout后来认为是一个L2的正则项。*论文中把dropout放在了最前面的两个全连接层上，没有dropout的话模型会很容易过拟合，同时dropout大概增加了两倍所需要的迭代次数去训练。*李：现在不需要那么大的4096的全连接*

## 拟合方式
本文章采用**SGD（随机梯度下降）（stochastic gradient desent)**去训练。*李：人们发现SGD里面的噪声对于模型的泛化是有好处的。*每当validation error没有继续提升，手动把学习率下降十倍（开始时0.01）

