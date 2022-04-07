
# 编写目的
本文档是郑州大学秃头宝贝队3D识别和工业测量参赛项目的软件说明手册，用于介绍软件使用方法。
# 环境依赖
Jetson Nano Jetpack v6.1 
TensorRT v5.0
YOLOv5 v5.0
Pytorch-gpu v1.7
Pyrealsense2 2.41.0

# 目录结构描述

├── best.engine
├── best.wts
├── build
│   ├── CMakeCache.txt
│   ├── CMakeFiles
│   │   ├── 3.15.1
│   │   │   ├── CMakeCCompiler.cmake
│   │   │   ├── CMakeCXXCompiler.cmake
│   │   │   ├── CMakeDetermineCompilerABI_C.bin
│   │   │   ├── CMakeDetermineCompilerABI_CXX.bin
│   │   │   ├── CMakeSystem.cmake
│   │   │   ├── CompilerIdC
│   │   │   │   ├── a.out
│   │   │   │   ├── CMakeCCompilerId.c
│   │   │   │   └── tmp
│   │   │   └── CompilerIdCXX
│   │   │       ├── a.out
│   │   │       ├── CMakeCXXCompilerId.cpp
│   │   │       └── tmp
│   │   ├── cmake.check_cache
│   │   ├── CMakeDirectoryInformation.cmake
│   │   ├── CMakeOutput.log
│   │   ├── CMakeRuleHashes.txt
│   │   ├── CMakeTmp
│   │   ├── Makefile2
│   │   ├── Makefile.cmake
│   │   ├── myplugins.dir
│   │   │   ├── build.make
│   │   │   ├── cmake_clean.cmake
│   │   │   ├── DependInfo.cmake
│   │   │   ├── depend.internal
│   │   │   ├── depend.make
│   │   │   ├── flags.make
│   │   │   ├── link.txt
│   │   │   ├── myplugins_generated_yololayer.cu.o
│   │   │   ├── myplugins_generated_yololayer.cu.o.cmake.pre-gen
│   │   │   ├── myplugins_generated_yololayer.cu.o.Debug.cmake
│   │   │   ├── myplugins_generated_yololayer.cu.o.depend
│   │   │   └── progress.make
│   │   ├── progress.marks
│   │   ├── TargetDirectories.txt
│   │   └── yolov5.dir
│   │       ├── build.make
│   │       ├── calibrator.cpp.o
│   │       ├── cmake_clean.cmake
│   │       ├── CXX.includecache
│   │       ├── DependInfo.cmake
│   │       ├── depend.internal
│   │       ├── depend.make
│   │       ├── flags.make
│   │       ├── link.txt
│   │       ├── progress.make
│   │       └── yolov5.cpp.o
│   ├── cmake_install.cmake
│   ├── libmyplugins.so
│   ├── Makefile
│   └── yolov5
├── calibrator.cpp
├── calibrator.h
├── CMakeLists.txt
├── common.hpp
├── cuda_utils.h
├── datasets.py
├── filte.py
├── gen_wts.py
├── g.png
├── Lines_check.py
├── logging.h
├── macros.h
├── main.py
├── __pycache__
│   ├── datasets.cpython-36.pyc
│   ├── filte.cpython-36.pyc
│   ├── Lines_check.cpython-36.pyc
│   ├── save_crops.cpython-36.pyc
│   ├── tcp.cpython-36.pyc
│   ├── Texture_luoshuan.cpython-36.pyc
│   └── yolov5_trt_pipeline.cpython-36.pyc
├── README.md
├── save_crops.py
├── tcp.py
├── Texture_luoshuan.py
├── utils.h
├── yololayer.cu
├── yololayer.h
├── yolov5.cpp
├── yolov5_trt_pipeline.py
└── yolov5_trt.py

# 部署步骤

## 注意： Jetson Nano密码为: `1`

## 1.1 启动桌面sh脚本
![在这里插入图片描述](https://img-blog.csdnimg.cn/dd9ddbfcfc7f43788a46ef1d1caba0d1.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAR2VlayBM,size_11,color_FFFFFF,t_70,g_se,x_16)
##  1.2 bash脚本内容解读
在Downloads/yolov5_measure目录下有一个main.py文件，运行脚本将自动执行此文件：

![在这里插入图片描述](https://img-blog.csdnimg.cn/ef3a13e1957644a59013bd0f1a6318c3.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAR2VlayBM,size_20,color_FFFFFF,t_70,g_se,x_16)
![在这里插入图片描述](https://img-blog.csdnimg.cn/00c14993feff4d97a93729c919ddc212.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAR2VlayBM,size_20,color_FFFFFF,t_70,g_se,x_16)
## 1.3 启动软件界面
![在这里插入图片描述](https://img-blog.csdnimg.cn/535b347153c84d3e8f3a6277f7cb8917.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAR2VlayBM,size_20,color_FFFFFF,t_70,g_se,x_16)
## 1.4 项目工程文件
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








