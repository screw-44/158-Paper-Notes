# FCN网路

## 一、相对于前人优秀的结果
 * 输入输出对应的图像大小相同，同时没有限制
 * 效果比前人做的更好，同时也避免使用了复杂的多级计算，是端到端的网络

## 二、创新点
 * 把全链接层换成卷积层，加速了前向推理和反向梯度传播
 * 介绍了下跳采样来做up-sampling，最后选择反卷积做上采样, 别的论文采用的跳采方式（shift-and-stitch）差值，这个是不如上卷积的效果好。
 * 如果只是反卷积，最后的一层再反卷积上去会导致高频细节丢失，所以提出深层的反卷积上去再和中层相加，再去反卷积上去（可以做重复）从而改进。最初级的是FCN-32 层级融合的有FCN-16s 和 FCN-8s

## 三、有意思的点
 * 输入训练集的旋转和裁切对于效果影响不大，图像全图输入训练效果最好。
 * 采用了overlap的的卷积，实验下来比不overlap的要好很多。  
 * 减低pooling层的stride能获得更加精细的效果。

## 四、英语单词总结
space -> spatial -> spatially  空间上的 \
coarse 粗糙的 coarsen （使）变粗糙 \
arbitary-sized 任意的-大小 \
feedforward computation 前馈计算 \
backpropagation 反向传播算法 \
asymptotically 渐进的 \
ostensible 表面上的 \
nonspatial 非空间上的 \
yields 产出，提供 \
Input shifting 输入移位，输入改变 \
output interlacing n. 隔行，间行 v.使交错，使交织 \
interpolation 插值 \
stochastic 随机的 

## 重点：定义了一个'skip'架构
这个十分重要，skip架构把深层，粗糙的特征和浅层，细致的特征融合在一起。实验展现了出来，这种skip架构用的越多，效果越好。Eg:FCN-8s, FCN-16s, FCN-32s。

## 总结
重点是能用卷积实现了语义分割。个人感觉和U-net没有本质区别。但是他是这个领域的开山之作。