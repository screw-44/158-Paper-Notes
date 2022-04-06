# Feature Pyramid Networks for Object Detection
注：本文没有看实验部分，只是看了网路

参考网址：[【论文笔记】FPN —— 特征金字塔 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/92005927)

总结：
特征金字塔网络，用来融合不同特征之间的特征。论文最终点出了neck的作用：“Finally, our study suggests that despite the strong representational power of deep ConvNets and their implicit robustness to scale variation, it is still critical to explicitly address multi-scale problems using pyramid representations.
![[FPN四种特征融合.png]]
#### 四种不同的方法
(a) 单纯的不同图像金字塔去做预测（注意是图像金字塔，不是特征图）
(b) 用最深级别的特征图去做预测 Eg:AlexNet分类任务
(c) 使用卷积的不同层级特征图分别去做预测 Eg:SSD等识别任务
(d) FPN 所有的预测都融合了所有层级的特征信息（虽然底层是卷积来融合，高层是上采样）
![[FPN和类似结构的不同.jpg]]
和最新的成果，比如说和FCN之间的特征增强不同的是，FPN每一层特征图都进行了预测。

FPN具体的实现方式，如图所示
![[FPN特征融合结构.png]]
分为两块：bottom-up pathway; Top-down pathway；分别对应上图左右两侧。bottom-up就是常见的backbone部分。Top-down使用了skip架构和上采样来融合**深层信息进入浅层信息。**

实验部分没有看，因为感觉不是重点。































