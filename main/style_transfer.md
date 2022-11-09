---
layout: blog
title: 风格迁移
slug: /main/blog
---

1. Neural style transfer: A review. [原文](https://arxiv.org/pdf/1705.04058.pdf%20http://arxiv.org/abs/1705.04058.pdf)|[源码]()|[复现](https://yz4work.github.io/style_transfer/test.ipynb)  

2. Image Style Transfer Using Convolutional Neural Networks. [原文](https://www.cv-foundation.org/openaccess/content_cvpr_2016/papers/Gatys_Image_Style_Transfer_CVPR_2016_paper.pdf)  
这是我特别喜欢的一篇风格迁移的文章。学过深度学习的知道，当输入图片让深度学习网络去识别图片的内容时（车/猫/狗），不同的网络层提取出了不同的特征，例如浅层网络可能提取了边缘信息，深层网络可能提取了高阶的信息（无法用现有术语描述）。文中的图1很好的描述了这一点：利用不同网络层提取的特征去重构原图时会得到什么样的结果。既然如此，给定一张照片和一张艺术画，我们可不可以生成一张图片，保持和照片中的内容但是照片的风格像艺术画呢？如果我们定义了什么是内容，什么是风格，那么我们的问题就解决了。文中把内容定义成深层网络提取到的特征（而不是像素点），把风格定义成不同网络层提取到的特征的Gram矩阵。其实文中的图1就解释了为什么要这样定义。因此，在生成新的图片时，我们只需要最小化风格损失和内容损失就行了，见文中图2。  

3. Perceptual losses for real-time style transfer and super-resolution. [原文](https://cs.stanford.edu/people/jcjohns/papers/eccv16/JohnsonECCV16.pdf)  
这又是一篇特别有意思的风格迁移论文。文章写的特别的清晰，读下来十分享受。上文2的方法缺点非常显而易见，即每次我们想要要转换一种风格，我们都必须重新训练模型。我们可以不可以专门设计一个生成模型呢？对于任意输入的照片，我们都可以通过这个训练好的模型直接输出具有某个风格的结果。文中图2概括了主要的过程，即先通过一个生成模型生成一个照片，这张照片内容必须和输入是一致的，而且这张照片的风格还要和我们想要的风格一致。内容和风格的定义和上文2一致。  

4. Unpaired Image-to-Image Translation
using Cycle-Consistent Adversarial Networks. [原文](https://openaccess.thecvf.com/content_ICCV_2017/papers/Zhu_Unpaired_Image-To-Image_Translation_ICCV_2017_paper.pdf)  
经典的CycleGAN。就如题目所说，它是一个循环的结构，或者就像文中提到的可以理解为自编码器。对于输入图片x，文中先用模型G将其转换成具有某种风格的图片y（可以将y理解为自编码器的隐空间），再利用模型F将y还原成原图x。因此，对于模型G和F都可以引入对抗损失（实际中，对抗损失可以选表现较好的一种）。与此同时，模型G和F生成图片后可以基于像素点引入损失（文中称为cycle consistency loss）。以上的过程在文中的图3描述的非常清晰。  

5. Arbitrary Style Transfer in Real-time with Adaptive Instance Normalization. [原文](https://openaccess.thecvf.com/content_ICCV_2017/papers/Huang_Arbitrary_Style_Transfer_ICCV_2017_paper.pdf)  
该文想把一张照片转换成具有任意风格的照片。同样，因为上文2每次转换时必须要重新训练模型，所以该文想训练好一个生成模型，给定照片和参考的风格，该生成模型可以直接输出转换结果。文中图2描述了主要框架，对于输入的照片c和风格s，文中先用VGG网络对它们分别提取特征，然后根据文中提出的方法AdaIN计算出一个特征表示t，并利用基于该特征表示t去生成所想要的转换风格后的照片g(t)，最后文中利用VGG网络去分别评判该生成的照片g(t)与照片c和风格s的差异。  

6. Fast Patch-based Style Transfer of Arbitrary Style. [原文](https://arxiv.org/pdf/1612.04337.pdf)  
从论文的结果看来，我觉得这个风格转换的挺符合我的审美的。从文中的描述（见图2）看来，作者主要是用卷积网络计算了内容和风格的一个表示，然后利用生成网络将这个表示转换成期望的风格。文中首先将风格画切成尺寸一样的很多小块，然后将这些小块作为卷积核对内容画计算卷积结果。所以，有多少个小块，输出就会有多少个通道。接着，文中对每个通道都计算了一个one-hot向量，然后还是基于风格画的小块作为卷积核去计算这些one-hot向量的反卷积结果。这个反卷积结果集成了内容和风格。所以，在训练时，文中输入反卷积结果到生成网络，然后提取（如利用VGG网络）生成图片的特征，最后计算该特征和反卷积结果的相似性。  

7. A Learned Representation for Artistic Style. [原文](https://arxiv.org/pdf/1610.07629.pdf)  
待细读。感觉就是加了归一化。  

8. Universal Style Transfer via Feature Transforms [原文](#)  
方法见文中图1。文中用VGG当作特征提取器，提取内容和风格的特征，然后将内容和风格的特征混合在一起。混合的方式是白噪化的方式。然后把混合后的特征输入解码器进行解码。

9. Multimodal Transfer: A Hierarchical Deep Convolutional Neural Network for Fast Artistic Style Transfer. [原文](https://openaccess.thecvf.com/content_cvpr_2017/papers/Wang_Multimodal_Transfer_A_CVPR_2017_paper.pdf)  
文中的方法见图2.该文一次只能训练一种风格。输入图片，该文也是通过编码解码的方式生成想要的风格照片。该文生成了不同尺寸风格照片（是不是可以理解为先生成小尺寸风格照片，然后把小尺寸进行了超分辨率？），然后对不同尺寸的风格照片和风格进行特征比对。

10. Stable and Controllable Neural Texture Synthesis and Style Transfer Using Histogram Losses[原文](https://arxiv.org/pdf/1701.08893.pdf)  
在上文2的基础上加入了直方图loss。文章有分析为什么上文2会有一些不好的结果，待细看。

11. A Style-Aware Content Loss for Real-time HD Style Transfer [原文](#)  
方法见文中图3.作者想迁移一种风格，而不是某张照片的风格，所以作者用到了GAN和一批艺术画（而不是单张）。对于输入的一张照片，先用编码器得到特征，再将该特征解码成风格照片，而解码出来效果是否真实就用辨别器和真实的风格做对比。为了保持解码出来的内容，把解码出来的风格照片再放回编码器，得到风格照片的特征，将其与原先照片的特征做对比。同时，还将原先照片和风格照片通过卷积网络进行变换后再对比。  

12. Artistic Style Transfer with Internal-external Learning and Contrastive Learning. [原文](#)  
发展太快了，连对比学习都用上了。方法见文中图2.作者也是通过编码解码再加上GAN网络来生成风格照片的。也是先通过解码器解码风格图片，并对比风格图片和内容以及风格中间的相似度（VGG的中间层信息），然后用辨别器区别是不是具有某种风格。除此之外，作者还加入了对比损失，不同的照片迁移了相同的风格，那么它们的风格就是相似的，但是它们的内容是不相似的，与此同时，相同的照片迁移了不同的风格，它们的内容是相似的而风格是不相似的。  

13. Arbitrary Style Transfer with Style-Attentional Networks. [原文](https://openaccess.thecvf.com/content_CVPR_2019/papers/Park_Arbitrary_Style_Transfer_With_Style-Attentional_Networks_CVPR_2019_paper.pdf)  
只要看到任意风格转换的标题，都会立刻想作者是这怎么把内容和风格糅合到一起的。作者通过加入注意力机制，将风格和内容的特征合并到一起。文章的框架是编码和解码，把内容和风格先编码，再通过注意力机制合并到一起，然后解码出风格照片。作者加入了内容（对比隐藏层特征相似度）、风格（对比隐藏层特征的均值和方差相似度）损失。除此之外，作者认为内容和内容解码出来应该是内容，风格和风格解码出来也是风格，所以加了这一个损失函数。  

14. Avatar-Net: Multi-scale Zero-shot Style Transfer by Feature Decoration. [原文](https://openaccess.thecvf.com/content_cvpr_2018/papers/Sheng_Avatar-Net_Multi-Scale_Zero-Shot_CVPR_2018_paper.pdf)  
可以理解为作者结合了AdaIN和StyleSwap的方式。作者先通过编码器提取内容和风格的特征，然后以类似AdaIN的方式对这些特征进行归一化，接着在特征层面上进行Swap（StyleSwap是在原始输出层面上），就是将风格特征切分成小块当作不同的卷积核对内容特征进行卷积，最后对卷积的结果进行解码，输出想要的风格照片。  

15. Content and Style Disentanglement for Artistic Style Transfer. [原文](#)  
这篇论文的结果我也觉得挺满意的。作者的框架就是编码器提取特征，解码器生成风格图片，辨别器区别风格的真伪。除了风格损失、内容损失和GAN损失以外，作者还提出了两个损失，一是不同风格渲染的同一张图片它们在风格上应该存在差异，二是用相同风格渲染的不同内容它们在风格上应该相似。  

