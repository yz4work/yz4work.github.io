---
layout: work
title: 论文阅读整理
slug: /paper
# items:
#   - title: [Spatial Transformer Networks](https://proceedings.neurips.cc/paper/2015/file/33ceb07bf4eeb3da587e268d663aba1a-Paper.pdf) 
#     image:
#       src: /assets/img/work/water.png
#       alt: water
#     description: 可以自动学到空间变换。
#   - title: [CBAM, Convolutional Block Attention Module](https://openaccess.thecvf.com/content_ECCV_2018/papers/Sanghyun_Woo_Convolutional_Block_Attention_ECCV_2018_paper.pdf)
#     image:
#       src: /assets/img/work/sand.png
#       alt: sand
#     description: 空间和通道的注意力机制。
---

1. Spatial Transformer Networks. [原文](https://proceedings.neurips.cc/paper/2015/file/33ceb07bf4eeb3da587e268d663aba1a-Paper.pdf)  
可学习的空间变换，也可以理解为空间注意力。想象一下你最近刚拍的一张照片，端端正正的放在你面前，你可以旋转、拉近、离远地从不同角度欣赏它。但是不论你从哪个角度看，它其实都是从端端正正的那个方位转换过来的。这就是文章的思想：对于任意的输入（图片），文中通过一个网络学习到一个变换，利用该变换尝试将现在的输入变回到最开始那个端端正正的角度。  

2. Squeeze-and-Excitation Networks. [原文](https://openaccess.thecvf.com/content_cvpr_2018/papers/Hu_Squeeze-and-Excitation_Networks_CVPR_2018_paper.pdf)  
学习不同通道之间的关系，也可以理解为对通道的注意力。对某一输出，文中先对每个通道计算一个数值（文中使用average-pooling，AvePool）作为对应通道的一个表示，再利用神经网络（MLP）进一步学习到对应通道的权重，最后将权重赋予对应通道（点乘），以这样的方式重构了输出。  

3. CBAM, Convolutional Block Attention Module. [原文](https://openaccess.thecvf.com/content_ECCV_2018/papers/Sanghyun_Woo_Convolutional_Block_Attention_ECCV_2018_paper.pdf)  
通道注意力和空间注意力。通道注意力和上文2类似，不同的是，文中同时使用了AvePool和max-pooling（MaxPool）提取每个通道的表示。空间注意力是空间的重要性。对某一输出，文中先在通道方向利用AvePool和MaxPool计算了所有通道的空间表示（这样保持了长宽尺寸不变），接下来用卷积网络在空间表示上学习到空间注意力，最后利用通道注意力和空间注意力重构输出。  
