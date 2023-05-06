---
title: 给硬盘创建raw镜像，并挂载尝试修复
date: 2023-05-06 17:08:17
tags:
---

## 所需资源
* Bochs bximage
  > [下载地址](https://wwmf.lanzout.com/i5KiC0uu12uj)
* Forensics OSFMount
  > [官网](https://www.osforensics.com/tools/mount-disk-images.html)
  > 
  > [备用](https://wwmf.lanzout.com/iGV320uu17rg)
* MSYS2
  > [官网](https://www.msys2.org/)，点击"Download the installer：msys2 xxxxx.exe"
  >
  > [备用](https://wwmf.lanzout.com/ifIx30uu270f)密码:ctk5
* GNU ddrescue
  > [本人编译版本](https://wwmf.lanzout.com/iLqA10uu2cvg)


## 正文
1. 硬盘多大，raw镜像就要多大，例如2T的硬盘，镜像也必须是2T大小。但是很多硬盘后半部分是没有数据的，全部是0，可以利用这个特性在不到2T的硬盘上存放2T的镜像。
   接下来创建这样的镜像：
   1. 用资源管理器打开bximage所在文件夹，在顶部地址栏输入`powershell`，按下Enter键。
      ![](打开bximage.png)
   2. 在控制台依次键入：`1`，然后按下Enter
   3. 按下三次Enter键，当询问`Enter the hard disk size in megabytes`时，输入`2097152`，该数值对应2T硬盘
   4. 询问`What should be the name of the image?`时，输入一个方便的地方，如：`D:\c.img`
   5. 完成后如图：
      ![](bximage完成.png)
2. 安装MSYS
   
   很简单，步骤略，建议网上找个教程

3. 制作镜像
   1. 进入MSYS环境。在开始菜单中打开"MSYS2 MSYS"
   2. 出现终端。这个终端字体默认较小，可以右键点击终端，打开`Options`，点击左边`Text`栏，然后点击Select按钮，修改字体。
   3. 首先进入放了ddrescue的文件夹。msys2环境使用bash，输入路径时注意用正斜杠（/）替换反斜杠(\\)。
      ```bash
      cd /d/ddrescue-1.27-install
      ```
    4. 输入以下命令，查看硬盘情况：
       ```bash
       ls /dev/sd*
       ```
    5. 找到你的硬盘。先进入diskmgmt.msc，然后查看你的硬盘对应哪个号（磁盘0还是磁盘1之类），如果是磁盘1，则对应的设备号码为`/dev/sdb`，请记住，后面要用到。
    6. 在MSYS终端输入下面命令：
       ```bash
       ./ddrescue -n -f <刚才的设备号码> <镜像文件的位置（**以msys形式填入**）> ddrescue.log
       ```
    7. 保持电脑开机，直到完成操作
4. 挂载
   1. 打开OSFMount软件，点击Mount New
   2. 出现对话框，打开刚才镜像文件：
      ![](osfmount1.png)
   3. 如下设置：
      ![](osfmount2.png)
      ![](osfmount4.png)
      ![](osfmountfinish.png)

## 完成了
接下来可以用任何方法修理这块虚拟硬盘。所有对镜像的更改都不会保存在源文件中，而是在delta文件中，所以如果改坏了，就删除delta和index文件，然后重新修理即可。