The author collect a large-scale dataset, PIDray, which covers various cases in real-world scenarios for prohibited item detection.
The author design the selective dense attention network(SDANet) to construct a strong baseline, which consists of the dense attention module and the dependency refinement module.
# PIDray
It Contian labels of  Classification, Object Detection, and Instance Segmentation.
It Contian images from Subway, Airport and Railway station.
It Contian Easy, Hard, Hidden three split label to indicate their occluded degree.
# Selective Dense Attention Network
The author's goal is to learn the importance of multi-scale feature maps based on top-down feature pyramid stucture. The network consists two steps:
1. Fusing information from different layers by two selective attention modules. 
2. Enhancing the fused features by the dependency refinement module.
The author speculate the mechanic behind this network is:
1. Two selective attention modules can aggregate semantic information across multi-layers densely.
2. The dependency refinement module can further capture long-range dependencies among different feature maps.
