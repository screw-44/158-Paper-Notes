# 目标检测中的Anchor
Anchor似乎没有直接的论文来讲解，如下内容是从论文和网络上的博客中整理。  
## Anchor是什么？
Anchor的直接翻译是锚，船锚。在backbone当中不同的特征图上，设置anchor，把图像划分为不同的**固定参考框**。算法接下来在这个固定参考框中，识别**有无认识的目标，相对于固定参考框的偏移是多少**。可以参考yolov1的无anchor，yolov2加入anchor，SSD的anchor算法。
## Anchor的优点和局限性
相对于死遍历，Anchor减少了很多的计算量。但是对于不同的数据集和应用场景，Anchor的大小都需要分别调整，十分不便。  
如果需要检测大量的小目标，那就需要在底层加入anchor，底层的分辨率又很大，这会导致巨大的性能损失。
## Anchor对于网路的发展
Anchor是对于detection这个任务所出现的技术。因为detection有不同大小的，所以需要在低层，中层，高层都实现Anchor。然后融合这些不同层级的信息来去处理。无意之中完成了现在常见的backbone+neck+head的架构。
## 总结
Anchor需要全面覆盖。Anchor使用好了可以又快又好。