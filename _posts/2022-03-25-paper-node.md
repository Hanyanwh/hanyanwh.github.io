---
layout:     post
title:      "OUR-GAN 16K大尺寸图像超分辨率"
subtitle:   "Arxiv Donghwee Yoon"
date:       2022-03-25
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
  - 超分辨率
  - 图像翻译
---

# OUR-GAN: One-shot Ultra-high-Resolution Generative Adversarial Networks
![网络结构](/img/OUR_GAN/2022-OUR_GAN.jpg)

[https://arxiv.org/....](https://arxiv.org/pdf/2202.13799.pdf)
---

该工作实现了4k-16k的极端高清超分辨率，文中将超分任务分为三个阶段。
1. 以4K图片为基准生成全局结构图，采用**HP-VAE-GAN**的构架生成具有多样性的全局结构图

2. 在**HP-VAE-GAN**的基础上加以改进，增加了纵向卷积层，使得网络可以保持基于坐标的纵向结构(该工作认为对于自然照片纵向的混乱非常容易被察觉，而横向的混乱则没有太大影响)
![](/img/OUR_GAN/2022-OUR_GAN1.jpg)

3. 将生成的全局结构图分成等尺寸的区块，使用预训练的ESRGAN对全局结构图逐区块的进行超分，补充细节。
![](/img/OUR_GAN/2022-OUR_GAN2.jpg)

4. 拼接的边缘差异大通常是由于卷积操作时的0填充padding导致的，扩大输入子区域，重叠部分宽度采用有效感受野可以消除拼接边缘
![](/img/OUR_GAN/2022-OUR_GAN3.jpg)