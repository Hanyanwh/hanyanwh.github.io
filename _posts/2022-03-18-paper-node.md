---
layout:     post
title:      "U-GAT-IT 真实人脸转动漫人脸"
subtitle:   "ICLR 2020, Junho Kim"
date:       2022-03-18
author:     "WHGuo"
catalog: true
header-style: text
# header-mask: 0.4
# lang: en
# hidden: true
# header-img: "img/post-bg-kuaidi.jpg"
tags:
  - GAN
  - 论文笔记
  - 风格迁移
  - 图像翻译
---

# U-GAT-IT: UNSUPERVISED GENERATIVE ATTENTIONAL NETWORKS WITH ADAPTIVE LAYERINSTANCE NORMALIZATION FOR IMAGE-TO-IMAGE TRANSLATION

![网络结构](/img/U_GAT_IT/Snipaste_2022-03-20_22-34-34.jpg)

[https://arxiv.org/....](https://arxiv.org/pdf/1907.10830.pdf)
---

<font color='gay' font-weight='bolder'> 主要贡献点本质上是一种给风格迁移网络中给生成器增加约束的方式。对输入图像进行Encode编码, 得到多个特征层，将每个特征层的全局pooling作为全连接分类器的输入，根据CAM的思想，可以学习到各特征层的权重，将权重作为各特征层的注意力，该网络的全连接分类器loss为 </font>
![CAM](/img/U_GAT_IT/Snipaste_2022-03-26_20-09-40.jpg)
其优化目标为让网络更关注两种domain相似的特征。
### 贡献点
**1. 将注意力机制引如风格转移生成模型** 

**2. 提出一种新的归一化层AdaLIN，将LN和IN结合起来，实验证明这样做对风格迁移是有效的**

###### 注意力机制
从CAM得到的启发，CAM是一个CNN的可视化工具。使用CAM，我们可以清楚的观察到，网络关注图片的哪块区域。
![CAM](/img/U_GAT_IT/v2-a0a76e2d3fa0475c39a990ae26844bee_b.jpg)
![CAM](/img/U_GAT_IT/v2-a2b7d9ca5ab237a674ec8ebb808350ed_b.jpg)

将输入图像通过EnCode得到多个特征图，使用辅助分类器$\eta_s$进行分类判别该图像属于原域或特征域，使用判定得到的权重以及特征图结合得到 attention map
###### AdaLIN
![AdaLIN](/img/U_GAT_IT/Snipaste_2022-03-21_09-52-52.jpg)

通过实验发现，IN可以有效地保留原始图片的边缘信和特征保留的很好，但是风格样式转移的不够，而LN可以充分的转移风格样式，但是在残差块中使用LN细节特征得不到很好的保留,于是作者通过一个可学习的参数$\rho$融合了两种归一化方式
![AdaLIN](/img/U_GAT_IT/Snipaste_2022-03-21_09-55-09.jpg)
