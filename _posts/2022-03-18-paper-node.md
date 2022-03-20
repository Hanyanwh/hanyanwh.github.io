---
layout:     post
title:      "U-GAT-IT 真实人脸转动漫人脸"
subtitle:   "SIGGRAPH 2018, YANG ZHOU , Shenzhen University and Huazhong University of Science & Technology"
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
![网络结构](/img/U_GAT_IT/Snipaste_2022-03-20_22-34-34.jpg)

#### 贡献点
**1. 将注意力机制引如风格转移生成模型**

**2. 提出一种新的归一化层AdaLIN，将LN和IN结合起来，实验证明这样做对风格迁移是有效的**

###### 注意力机制
从CAM得到的启发，CAM是一个CNN的可视化工具。使用CAM，我们可以清楚的观察到，网络关注图片的哪块区域。
![网络结构](/img/U_GAT_IT/v2-a0a76e2d3fa0475c39a990ae26844bee_b.jpg)
![网络结构](/img/U_GAT_IT/v2-a2b7d9ca5ab237a674ec8ebb808350ed_b.jpg)

将输入图像通过EnCode得到多个特征图，使用辅助分类器$\eta_s$进行分类判别该图像属于原域或特征域，使用判定得到的权重以及特征图结合得到 attention map
###### AdaLIN

