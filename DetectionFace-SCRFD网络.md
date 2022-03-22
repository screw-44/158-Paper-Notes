# Sample and Computation Redistribution for Efficient Face Detection
正如题目所说，Sample Redistribution 和 Computation Redistribudtion 是这篇文章的重点。  


## Sample Redistribution 样本重分配
&emsp;SampleRedistribution会根据benchmark datasets的信息，来提炼出最需要信息的stage是那一个，然后去优化样本去着重训练这个stage。从逻辑上有点类似于根据benchmark datasets去调整anchor大小。

### 具体步骤
&emsp;首先分析benchmark datasets中 face scale distribution，根据distribution和自己网络中不同stage之间的stride大小来决定那一层重要。本文中 the feature map of stride 8最重要。用这个去返回来决定训练集怎么分布。

### 训练集处理阶段别的操作
&emsp;1. 随机裁切 2. 随机放大**缩小** 

### 特别特别小的脸不会影响训练，因为unsuccessful anchor matching
Moreover, even though there will be more extermely tiny faces under the large cropping strategy, these ground-truth face will be neglected during training due to unsuccessful anchor matching.  
  

## Computation Redistribution 算力重分配
&emsp;在给定Flops的情况下，分配在backbone，neck，head的算力。提出了两段式的分配方式。第一阶段先固定neck和head，去搜索backbone。第二阶段backbone,neck和head一起去搜索。这里与Facebook的Designing Network Design Space这篇论文有很大联系。具体细节可以参考这篇论文。

### 具体步骤 这里可以直接去看Facebook的论文
Face detector structure
1. backbone stem. Three 3*3 conv layers with $w_0$ 输出通道数。
2. backbone body. Four stages, stages里面有n个block。
3. neck. A multi-scale feature aggregation module by a top-down path and a bottom-up path with $n_i$ channels.
4. head. Has $h_i$ channels of $m$ blocks to predict face scores and regress face boxes.  
由于stem的输出层和第一个stage的输入width相同，可以继续减少自由度  
实际优化的时候，neck和head减少自由度到三个维度
1. output channel number n for neck.
2. output channel number h for head.
3. block中3*3卷积层的个数。
backbone减少到8个自由度。4个stage，每个stage中有2个参数，block的数量和block的宽度。  
随机采样，采样320个，训练80个epochs。然后去画图寻找最好的。原文中说使用了empirical bootstrap去估计模型的成功程度，不太理解，还没有读过这个论文。

## 结论
1. 主要的计算在backbone,其次在neck，head基本没有。
2. 更多的资源重分配在更大的模型flops，是因为WIDER FACE的关系（不太理解）
3. 对于更大的flops，更深比更广更常见。这点和Facebook的论文结论相同。
4. 对于很小的flops，把算力分配在更深的网络中可以帮助优化较浅深度的识别。可能和neck中特征融合有关，同时在很小的flops中，浅层不可能分配足够的算力。