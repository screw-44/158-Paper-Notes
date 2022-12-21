A data augmentation method for prohibited item X-ray pseudocolor images in X-ray security inspection is proposed.
# 工作
1. a framwork of our method to achieve the dataset augmentation using the dataset with and without prohibited items.
2. A spatial-and-channel attention block and a new base block to compose our X-ray Wasserstein generative adversarial network model with gradient penalty.
3. A composite strategy to **composite the generated and real dual-energy X-ray data with background data into a new X-ray pseudocolor image**, which can simulate the real overlapping relationship among items.
# 思路分析
1. X-ray dataset has low quality
2. Introduce GAN to artificially generate dataset
3. Occulated Items can be hard to detect
4. Introduce a composite strategy to generate occulated item image dataset.
# 创新点
1. Using gan and this composite strategy generated more realistic image data, which gramatically improved the mAP of different models.(Up average at 10% using yolov4-tiny) 
# 未来可以做的方向
1. We can use more up to date GAN model to replace the Wasserstein Generative Adversarial Network
	* Need to follow the trend in GAN
1. We can optimize the model all the way from data composition to detection together, need to search whether it has been done before or not.
	* Need to have a solid understanding of GAN, Lose Function and modelling ingeneral.

# Questions
1. The SCAB-XWGAN-GP model(just a gan modle) using dual-energy X-ray data instead  of X-ray pseudocolor images. The author indicate that it allow the composited strategy in the next step to composite more realistic and higher-quality X-ray pseudocolor images. My questions is that transforming from dual-energy X-ray data to pseudocolor  data is by the use of LUT(look Up Table), which should be a easy thing to learn for our network. So my conjecture is that either the transformation is done not by LUT, or  the model is easier to learn in dual-energy data.


