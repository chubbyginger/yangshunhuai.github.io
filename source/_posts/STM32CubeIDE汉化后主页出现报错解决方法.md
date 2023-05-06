---
title: STM32CubeIDE汉化后主页出现报错解决方法
date: 2022-09-11 22:54:15
categories: 嵌入式开发
tags: stm32
---

STM32CubeIDE是基于eclipse二次开发的IDE，汉化步骤基本与eclipse相同，但是如果直接照搬会导致主页出现故障无法打开，可能会出现`class org.eclipse.ui.internal.ViewIntroAdapterPart cannot be cast to class org.eclipse.ui.IViewPart`的故障。

解决方法是，如果主页出故障了，就把STM32CubeIDE重新安装一遍，然后按照下面步骤来一遍：

## 正确的汉化方法
1. 打开Install New Software界面
   ![安装新软件](安装新软件.png)
2. 在顶部点击Add
   ![添加软件源](添加软件源.png)
3. 输入清华大学的`babel`软件源，名字随便取
   > https://mirrors.tuna.tsinghua.edu.cn/eclipse/technology/babel/update-site/latest
   ![填写软件源](填写地址.png)
4. 加载完之后就会有这样一些项目出现，务必要按照下面的指示选择，不能多选，因为有一些选项选上了就会导致主页崩溃
   ![选择1](eclipse.png)
   ![选择2](cdt.png)
5. 然后点击next即可按照正常步骤汉化操作。汉化过后主页是这样的：
   ![汉化后](汉化后.png)