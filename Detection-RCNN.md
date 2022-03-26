# Region proposals with CNN
原论文标题：Rich feature hierarchies for accurate object detection and semantic segmentation  

#### 概括：本文全篇就是两个论文的结合+实验，1. Selective search for object recognition 2. Alexnet。综合来说就是二阶段识别。先找出框，再在框里面找到相对于框的偏移量和属于什么类别。本文重点是在于是开山之作。 
  
#### 作者认为的两个重点：
1.  one can apply high-capacity convolutional neural networks(CNNs) to bottom-up region proposals in order to localize and segment objects
2.  when labeled training data is scarce, supervised pre-training for an auxiliary task, followed by domain-specific fine-tuning, yields a significant performance boost.（现在来看，pre-train没啥用，fine-tuning很重要，事实上二阶段的detection算法，fine-tuning可以说是最重要的东西）

***
## Selective search for object recognition
输入图像，经过算法提出2k多个候选框。之前的方法要么是划窗（计算量大），要么是把这个看成是一个回归问题（在本文写的之前效果不好，但是很快这个方式证明效果很好）。注：下面的内容是来自于Selective Search for Object Recognition的原论文。R_CNN论文中我认为说的不清楚。  
提出候选框的过程就是一个迭代优化过程。其实我理解下来和k-means聚类方法类似。把所有近似于自身的图像融合在一起，然后就可以实现segementation或者画框了。下面给出算法过程。  

__Algorithm 1:__ Hierarchical Grouping Algorithm  
__Input:__ (colour)image  
__Output:__ Set of object location hypotheses $L$  
Obtain initial regions $R={r_1, ..., r_n}  
Initialise similarity set $S=\emptyset$  
__foreach__ *Neighbouring region pair* $(r_i, r_j) __do__  
&emsp; Calculate similarty $s(r_i, r_j)$  
&emsp; $S = S \cup s(r_i, r_j)$  
__While__ $S \neq \emptyset$ __do__  
&emsp; Get highest similarity $s(r_i, r_j) = max(S)$  
&emsp; Merge corresponding regions $r_t = r_i \cup r_j$  
&emsp; Remove similarities regarding $r_i:S = S / s(r_i, r_*)$  
&emsp; Remove similarties regarding $r_j:S = S / s(r_*, r_j)$  
&emsp; Calculate similarity set $S_t$ between $r_t$ and its neighbours   
&emsp; $S= S\cup S_t$  
&emsp; $R=R\cup r_t$  
Extract object location boxes $L$ from all regions in $R$  
注：R-CNN这个论文引用的这个论文其实也做了识别，只是在提取出候选框后，用手动设计的特征识别器，加上SVM去做识别。
***
## CNN识别
这一块就很简单。实际上就是分类器。这里介绍下独特的在后面识别任务中会出现的算法。
### 非极大值抑制
Given all scored regions in an image, we appy a greedy non-maximum suppression(for each class independently) that refects a region if it has an intersection-over-uion(IoU) overlap with a higher scoring selected region lager than a learned threshold.
### Domain-sepecific fine-tuning
就是切出来框，框有个IoU重叠阈值（0.5），然后就去训练分类器。效果提升很明显，算法也很简单。