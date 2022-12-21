Introduce a high-quality dataset.
Introduce the Lateral Inhibition Module(LIM) inspired by the fact that humans recognize these ignoring irrelevant information and focusing on identifiable characteristics, especially when objects are overlapped with each other.
The LIM suppresses the noisy information flowing maximumly by the Bidirectional Propagation(BP) module and activates the most identifiable charismatic, boundary, from four directions by Boundary Activation(BA) module.
The LIM improve the mAP of SSD/FCOS/YOLOv5 by roughly 2.5%.
# Work
## HiXray dataset
The High-quality X-ray dataset(HiXray dataset) is the largest high-quality dataset for prohibited items detection in X-ray images. (102,928 labeled instance)
| 102,928 labeled instance| 8 category  | 45,364 pictures | Detection Task |
| ------ | ------ | ------ | ------ |
## The Lateral Inhibition Module (LIM)
![[Pasted image 20221216111522.png]]

### The Bidirectional Propagation (BP)  module
To summerize, it is just a PAN, FPN like neck module.
### The Boundary Activation (BA) module
![[Pasted image 20221216111612.png]]
The process of perceiving the left boundary can be formulated as Eq.(4)
![[Pasted image 20221216111921.png]]
# 创新点
The BA module is interesting, provides a novel way of intensifying boundary information.
# Summary
The author or this gourp of researcher focus more on the edge information of the X-ray. This solution improve the mAP on occluded items, but worsen the score on not occluded items.
The article is published on ICCV, which really improve the writing!