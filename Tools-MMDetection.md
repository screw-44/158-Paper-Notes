# MMDetection: Open MMLab Detection Toolbox and Benchmark

MMDetection是一个工具包，里面有很多种类的识别和分割的工具还有相关组件和框架。其特点有1. 模块化设计；2. 支持多种框架；3. 都是STOA算法. 具体支持的网络等信息可以在官网查看。

## Arthitrecture 框架
### 网路框架
__1. Backbone__   
   Backbone is the part that transforms an image to feature maps, Eg: 分类的卷积网路去除最后的全连接层。  
   总结：图像特征提取。  
__2. Neck__  
   Neck is the part that connects the backbone and heads. It performs some refinements or reconfigurations on the raw feature maps produced by the backbone. Eg: Feature Pyramid Network(FPN)  
   总结：特征图融合。   
__3. DenseHead(AnchorHead/AnchorFreeHead)__  
    DenseHead is the part that operates on dense locations of feature maps, including AnchorHead and AnchorFreeHead. Eg: RPN-Head, RetinaHead, FCOSHead.  
    总结：用于one-stage直接提取识别结果。有Anchor和AnchorFree两种算法。  
__4. RoIHeadExtractor （没有使用过）__  
   RoIExtractor is the part that extracts RoI-wise features from a single or multiple feature maps with RoIPooling-like operators.  
   总结：模型中可以多处应用的，roi提取器。  
__5. RoIHead(BBoxHead/MaskHead)__  
   RoIHead is the part that takes RoI features as input and make RoI-wise task-specific predictions, such as bounding box classification/regression, mask prediction.  
   总结：two-stage中前一个stage提取候选框的Head。


### Traning Pipeline
   使用hooking mechanism。具体得用这个框架复现过代码后再记录。hooking mechanism，作者设计了一些timepoints 用户可以在里面注册(register)可执行操作（hook). 这些hook会在不同的触发条件和时间下触发。

## 实验部分
比较了不同框架下在不同gpu上面的推理速度。测试了不同的正则化对于最后结果的影响，BN层的设定，etc。这一部分也是等复现完成后，才能比较全面的记录。