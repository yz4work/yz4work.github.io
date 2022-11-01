---
layout: blog
title: 风格迁移
slug: /main/blog
---

1. Neural style transfer: A review. [原文](https://arxiv.org/pdf/1705.04058.pdf%20http://arxiv.org/abs/1705.04058.pdf)  

2. Image Style Transfer Using Convolutional Neural Networks. [原文](https://www.cv-foundation.org/openaccess/content_cvpr_2016/papers/Gatys_Image_Style_Transfer_CVPR_2016_paper.pdf)  
这是我特别喜欢的一篇风格迁移的文章。学过深度学习的知道，当输入图片让深度学习网络去识别图片的内容时（车/猫/狗），不同的网络层提取出了不同的特征，例如浅层网络可能提取了边缘信息，深层网络可能提取了高阶的信息（无法用现有术语描述）。文中的图1很好的描述了这一点：利用不同网络层提取的特征去重构原图时会得到什么样的结果。既然如此，给定一张照片和一张艺术画，我们可不可以生成一张图片，保持和照片中的内容但是照片的风格像艺术画呢？如果我们定义了什么是内容，什么是风格，那么我们的问题就解决了。文中把内容定义成深层网络提取到的特征（而不是像素点），把风格定义成不同网络层提取到的特征的Gram矩阵。其实文中的图1就解释了为什么要这样定义。因此，在生成新的图片时，我们只需要最小化风格损失和内容损失就行了，见文中图2。  

3. Perceptual losses for real-time style transfer and super-resolution. [原文](https://cs.stanford.edu/people/jcjohns/papers/eccv16/JohnsonECCV16.pdf)  
这又是一篇特别有意思的风格迁移论文。文章写的特别的清晰，读下来十分享受。上文2的方法缺点非常显而易见，即每次我们想要要转换一种风格，我们都必须重新训练模型。我们可以不可以专门设计一个生成模型呢？对于任意输入的照片，我们都可以通过这个训练好的模型直接输出具有某个风格的结果。文中图2概括了主要的过程，即先通过一个生成模型生成一个照片，这张照片内容必须和输入是一致的，而且这张照片的风格还要和我们想要的风格一致。内容和风格的定义和上文2一致。