- [编写目的](#----)
- [环境依赖](#----)
- [目录结构描述](#------)
- [部署步骤](#----)
  * [注意： Jetson Nano密码为: `1`](#----jetson-nano------1-)
  * [1.1 启动桌面sh脚本](#11-----sh--)
  * [1.2 bash脚本内容解读](#12-bash------)
  * [1.3 启动软件界面](#13-------)
  * [1.4 项目工程文件](#14-------)
  * [1.5 开始识别](#15-----)
  * [1.5 切换比赛轮次](#15-------)
  * [1.6 结果文件生成](#16-------)
  * [1.7 软件退出](#17-----)




# 编写目的
本文档是郑州大学秃头宝贝队3D识别和工业测量参赛项目的软件说明手册，用于介绍软件使用方法。
# 环境依赖
Jetson Nano Jetpack v6.1 
TensorRT v5.0
YOLOv5 v5.0
Pytorch-gpu v1.7
Pyrealsense2 2.41.0

# 目录结构描述
.

yolov5-recog  
├─ CMakeLists.txt  
├─ README.md  
├─ __pycache__  
│    ├─ datasets.cpython-36.pyc  
│    ├─ filte.cpython-36.pyc  
│    ├─ tcp.cpython-36.pyc  
│    ├─ yolov5_trt_pipeline.cpython-36.pyc  
│    └─ yolov5_trt_test.cpython-36.pyc  
├─ build  
│    ├─ CMakeCache.txt  
│    ├─ CMakeFiles  
│    │    ├─ 3.15.1  
│    │    ├─ CMakeDirectoryInformation.cmake  
│    │    ├─ CMakeOutput.log  
│    │    ├─ CMakeRuleHashes.txt  
│    │    ├─ CMakeTmp  
│    │    ├─ Makefile.cmake  
│    │    ├─ Makefile2  
│    │    ├─ TargetDirectories.txt  
│    │    ├─ cmake.check_cache  
│    │    ├─ myplugins.dir  
│    │    ├─ progress.marks  
│    │    └─ yolov5.dir  
│    ├─ Makefile  
│    ├─ cmake_install.cmake  
│    ├─ last_4_3.engine  
│    ├─ libmyplugins.so  
│    └─ yolov5  
├─ calibrator.cpp  
├─ calibrator.h  
├─ common.hpp  
├─ cuda_utils.h  
├─ datasets.py  
├─ filte.py  
├─ g.png  
├─ gen_wts.py  
├─ last_4_3.engine  
├─ last_4_3.wts  
├─ logging.h  
├─ macros.h  
├─ main.py  
├─ main_withoutfilter.py  
├─ myvoc.yaml  
├─ tcp.py  
├─ utils.h  
├─ yololayer.cu  
├─ yololayer.h  
├─ yolov5.cpp  
├─ yolov5_trt.py  
├─ yolov5_trt_pipeline.py  
├─ yolov5_trt_test.py  
└─ zzu-tutoubaby-R1.txt  

# 部署步骤

## 注意： Jetson Nano密码为: `1`

## 1.1 启动桌面sh脚本
![在这里插入图片描述](https://img-blog.csdnimg.cn/dd9ddbfcfc7f43788a46ef1d1caba0d1.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAR2VlayBM,size_11,color_FFFFFF,t_70,g_se,x_16)
##  1.2 bash脚本内容解读
在Downloads/yolov5_measure目录下有一个main.py文件，运行脚本将自动执行此文件：  


![在这里插入图片描述](https://img-blog.csdnimg.cn/ef3a13e1957644a59013bd0f1a6318c3.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAR2VlayBM,size_20,color_FFFFFF,t_70,g_se,x_16)
启动后软件界面需要打开相机，点击后将持续打开相机直至用户点击右下角`退出`按钮。  

![在这里插入图片描述](https://img-blog.csdnimg.cn/00c14993feff4d97a93729c919ddc212.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAR2VlayBM,size_20,color_FFFFFF,t_70,g_se,x_16)
## 1.3 启动软件界面
运行桌面的start.sh脚本后将自动运行软件，软件启动后将呈现如下的界面：  

![在这里插入图片描述](https://img-blog.csdnimg.cn/535b347153c84d3e8f3a6277f7cb8917.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAR2VlayBM,size_20,color_FFFFFF,t_70,g_se,x_16)
## 1.4 项目工程文件
所运行的main.py文件及其相关联的模块均在同一个项目工程目录下，如果是识别组，目录名为`yolov5-recog`，如果为测量组，目录名为`yolov5-measure`。  

![在这里插入图片描述](https://img-blog.csdnimg.cn/d08ab08fd335426db1df1a5785cb113c.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAR2VlayBM,size_20,color_FFFFFF,t_70,g_se,x_16)
## 1.5 开始识别

比赛开始后，点击软件界面上`开始识别`按钮启动识别，程序开始自动运行，开始后立即与裁判软件通信并发送数据。  

![在这里插入图片描述](https://img-blog.csdnimg.cn/fe81c4e4b2784f8981069a19478d5916.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAR2VlayBM,size_20,color_FFFFFF,t_70,g_se,x_16)
## 1.5 切换比赛轮次
第一轮比赛结束后点击软件右上方导航栏，选择轮次，不同轮次设置的运行时间不同，注意切换轮次。  

![在这里插入图片描述](https://img-blog.csdnimg.cn/31fd12e3ba93470883ab1a8abc7e72e6.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAR2VlayBM,size_20,color_FFFFFF,t_70,g_se,x_16)
## 1.6 结果文件生成
每轮运行结束后会自动在`~/Desktop/result` 目录下生成结果文件。  


![在这里插入图片描述](https://img-blog.csdnimg.cn/2af8f81b46c4413b85959cbaa18bee62.png)
## 1.7 软件退出
程序运行后会自动结束，最后点击右下方`退出`按钮即可安全退出界面。  


![在这里插入图片描述](https://img-blog.csdnimg.cn/329f4f021f7d49f3bd7cf31499997533.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAR2VlayBM,size_20,color_FFFFFF,t_70,g_se,x_16)








