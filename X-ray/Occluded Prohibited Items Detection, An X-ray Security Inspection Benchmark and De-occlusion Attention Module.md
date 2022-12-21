This paper shared lots of information with Over-sampling De-occlusion Attention Network for Prohibited Items Detection in Noisy X-ray Images.
# Summary
The edge information is more important than it's content when the object is occlated with one and another. So We using a data argument like model to exaggerate the importance of edge information. Improve the mAP of SSD by 5%, but the mAP droped on less occluded scenario.
1. 方法效果不是特别好
2. 文章的语法和行文较差，读起来费力
# Work
1. The first high-quality object detection dataset for security inspection (OPIXray)
2. The De-occlusion Attention Module (DOAM), a plug-and-play module that can be easily inserted into and thus promote most popular detector.
	X-ray imaging preserves the shape appearance in the heavy occluded part and assigns various colors to different materials in the visual part. 
	The DOAM simultaneously lays particular emphasis on edge information and material information of the prohibited item by utilizing *Edge Guidancestors(EG)* module and *Material Awareness(MA)* module.  
	Then DOAM leverages the two information to generate an attention distribution map as a high-quality mask for each input sample to generate high-quality feature mask for each input sample to generate high-quality feature maps, serving identifiable information for next step.(General detector)
3. Over-sampling Strategy
	Using the over-sampling strategy to retrain hard samples, the model reduced the performance decrease caused by hard samples in the training set significantly and enhanced the ability of generalization highly, just as that human learns a lot from the difficulties they felt hard to solve.
	This part of work is questionable, and is deleted in the final release(I think). But it shows that the author trying to optimize the learning part of the model.
# 未来可以跟进的点
1. In this article, the author indicated that the occlusion in X-ray is different to normal pictures in the wild. In different scenarios, such as person re-identification, face recognition, the occlusion is INTRA-CLASS（一堆脸堆在一块）, but in X-ray, the occlusion is INTER-CLASS.（一个刀和别的叠在一块）. In a normal scenario, a loss function can be designed by annotation information to decrease the impact of occlusion. So, We can introduce a loss function that will emphasize the loss from occulated items.
	* Need a deeper understanding of loss function
	* Need a larger and more diversified dataset.