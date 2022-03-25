# MMDetection: Open MMLab Detection Toolbox and Benchmark

MMDetection是一个工具包，里面有很多种类的识别和分割的工具还有相关组件和框架。其特点有1. 模块化设计；2. 支持多种框架；3. 都是STOA算法. 具体支持的网络等信息可以在官网查看。

## Arthitrecture 框架
### 网路框架
1. Backbone 
   Backbone is the part that transforms an image to feature maps, Eg: 分类的卷积网路去除最后的全连接层。
   总结：图像特征提取。
2. Neck
   Neck is the part that connects the backbone and heads. It performs some refinements or reconfigurations on the raw feature maps produced by the backbone. Eg: Feature Pyramid Network(FPN)
   总结：特征图融合。
3. DenseHead(AnchorHead/AnchorFreeHead)
    DenseHead is the part that operates on dense locations of feature maps, including AnchorHead and AnchorFreeHead. Eg: RPN-Head, RetinaHead, FCOSHead.
    总结：用于one-stage直接提取识别结果。有Anchor和AnchorFree两种算法。
4. RoIHeadExtractor 
   RoIExtractor is the part that extracts RoI-wise features from a single or multiple feature maps with RoIPooling-like operators.
   总结：Two-stage中