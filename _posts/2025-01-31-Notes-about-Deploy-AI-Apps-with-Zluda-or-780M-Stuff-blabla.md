---
layout: post
title: 有关ZLUDA和780M等情况部署AI应用的记录
date: 2025-01-31 16:35:50 +0800
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: 2025-01-31/2025-01-31-quote-from-喵喵hmkai.png # Add image post (optional)
tags: [ZLUDA, 780M, AMD, Stable Diffusion, So-VITS] # add tag

---

### 一、秋叶一键包

1 安装ROCM

请下；载5.7版本

说明：多版本安装亦可，笔者先安装5.7，再安装6.2.4版本，在系统环境变量中会出现多版本的HIP PATH，实测正常工作

2 下载并解压秋叶一键包

3 下载780M所需单独编译的rocblas库等文件（By 喵喵hmkai UID: 2082155）

 780m_20240321_163205.7z 文件： https://pan.baidu.com/s/1kun1meOadjTJniETpO39AQ?pwd=sy59

解压后的文件放入，整合包启动器相同路径下

4 打开启动器，自动更新启动器及各组件，此时在高级选项-生成引擎中，应出现ZLUDA相关选项

5 在高级选项-环境维护-安装pytorch中，选择一项CUDA11.8版本的GPU选项，进行安装

这里我选择了	Torch 2.3.1(CUDA 11.8+xFormers 0.0.27) 进行实测

6 一键启动，首次启动ZLUDA编译时间较久，约20-30min（此步骤占用算力性能较低，内存性能较多

~~补充说明

1 实际跑图中关闭了高级选项中的VAE半精度优化，曾因在迷你主机的780M设备上测试时，遇到部分报错，检索后部分网友反馈可能是相关能力受限导致

2 因AMD尚未正式对780M (gfx1103)进行ROCM的支持，故需通过编译文件处理rocblas.dll和library文件夹的兼容问题。（若不补充相关文件，报错信息检索可得知类似的结论）

该库可在ROCM的bin文件夹下查看到，其他尝试780M提供算力给3D、LLM等应用的网友亦编译了相关文件，但在结合一键包进行尝试时遇到了报错（揣测一键包集成的ZLUDA调用可能是根据自己的路径、命名进行了调整）



Ref:

https://www.bilibili.com/opus/911274356655521814 (适用于绘世启动器的 AMD Radeon 780M 的 ZLUDA 教程)

https://github.com/ggerganov/llama.cpp/issues/6509 (HIP SDK with AMD iGPU rocBLAS error)

https://rocm.docs.amd.com/projects/install-on-windows/en/latest/reference/system-requirements.html (Windows-supported GPUs)

https://www.amd.com/en/developer/resources/rocm-hub/hip-sdk.html#sdk (AMD HIP SDK for Windows)

https://github.com/likelovewant/ROCmLibs-for-gfx1103-AMD780M-APU (ROCmLibs-for-gfx1103-AMD780M-APU)

https://www.bilibili.com/opus/906747525555290131 (让 AMD 780M 核显也用上 zluda 加速 AI)

https://www.bilibili.com/opus/929830372020060160 (在780M显卡笔记本上安装并运行Stable Diffusion：我的安装流程)

https://github.com/vosen/ZLUDA/issues/59 (Does it work on AMD Radeon 780M? #59)

https://bbs.deepin.org.cn/post/272254?_gl=1*9b5l9i*_ga*MTQwNDUwODcyOC4xNzM4MjU1OTMw*_ga_QHZ7DPPD2D*MTczODI1NTkzMC4xLjAuMTczODI1NTkzMC4wLjAuMA..( Deepin: R7 7840HS 780m核显成功运行Stable Diffusion生成图片)

https://github.com/vosen/ZLUDA/issues/64 (ZLUDA for llama.cpp)