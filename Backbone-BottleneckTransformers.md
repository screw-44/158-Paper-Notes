# Bottleneck Transformers for Visual Recognition
#### 概括：论文很简单，在resnet最后一层的resnet block中替换成了多头注意力机制。效果提升明显。

# *注：有空了可以把里面的那个分析不同transformer在cv的应用的图拿出来放笔记里面*

现在有两种方式应用transformer在视觉识别任务中。第一种是替换掉ResNet中的空间卷积，通过使用不同的注意力机制。第二种是（ViT），通过叠加Transformer块来实现纯注意力识别。论文中指出这两种方式是一样的。把ResNet中的空间卷积换成MHSA模块，可以看成一个Bottleneck Transformer,加上一些小的变化。（没咋说明为啥，但是就说了）。  

## BotNet
论文中设计了BotNet, 思路是Transfomer计算量很大，那就先用空间卷积从一个很大的图片中学习到一个低分斌率，抽象的特征图。再用全局的自注意力机制（注意和ViT的区别），来去提取，推理这个特征图。最终结果就是只是替换掉了ResNet中最后三层的bottleneck层，用BoT block（就是把最后三层里面的卷积换成了MHSA）。效果很好，训练epoch很少 巴拉巴拉巴拉。

### 视觉中Transformer和NLP中的Transformer的不同
Transformer用的是laer normalization（显然），我们用了Batch Normalization（这个在CV的Transformer里面每家都不太一样）。

### 和Detectioin Transformer(DETR)的区别
DETR使用Transformer在backbone之外，来规避region proposal和非极大值抑制。BotNet是直接作为Backbone了。

## 结论：
这篇文章说明了在相同层的情况下，transformer一定是比卷积要好的。但是并不是很有启发性，也没有和ViT这种全部注意力的网路做比较。本文论文中主要是介绍了Transformer在CV的应用，同时花了很多时间去做实验。没有多少突出的想法在里面。
