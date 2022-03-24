# Attention is all you need

注：没有全部搞懂

## Abstarct:
在主流的序列转录模型主要依赖于复杂的循环或者是卷积神经网络，而其包含encoder和decoder的架构。Transformer只依赖于注意力机制，不需要循环或者卷积。

## Introduction
Multi-Head Attention机制，参考了卷积层能够输出多通道，表现为多个特征的特点。

## Conclusion
Transformer是第一个在序列转述的模型里面完全使用注意力机制的。把所有的循环层换成了multi-headed self-attention

## 注意力机制
注意力机制（Attention Mechanism）是机器学习中的一种数据处理方法。通常来说，人们在观察外界事物的时候，首先会比较关注比较倾向于观察事物某些重要的局部信息，然后再把不同区域的信息组合起来，从而形成一个对被观察事物的整体印象。
注意力机制可以分为两种：软注意力机制和硬注意力机制。