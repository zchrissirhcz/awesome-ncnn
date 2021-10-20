# Awesome-NCNN

[![Awesome](https://cdn.rawgit.com/sindresorhus/awesome/d7305f38d29fed78fa85652e3a63e154dd8e8829/media/badge.svg)](https://github.com/sindresorhus/awesome)

[ncnn](https://github.com/tencent/ncnn) is a high-performance neural network inference framework optimized for the mobile platform. [This repo](https://github.com/zchrissirhcz/awesome-ncnn) lists some awesome ncnn-based projects. Welcome Star & Fork & Pull Requests!

[ncnn](https://github.com/tencent/ncnn) 是一个为手机端极致优化的高性能神经网络前向计算框架。[本仓库](https://github.com/zchrissirhcz/awesome-ncnn) 收集了基于ncnn的很棒的项目。欢迎 Star & Fork & Pull Request 一键三连！

## Contents
- [Awesome-NCNN](#awesome-ncnn)
    - [Application projects](#application-projects)
        - [Detection](#detection)
        - [Super Resolution](#super-resolution)
        - [Video Frame Interpolation](#video-frame-interpolation)
        - [Pose Estimation](#pose-estimation)
        - [Segmentation](#segmentation)
        - [Wasm](#wasm)
        - [Other](#other)
    - [Tools](#tools)
    - [Wrappers](#wrappers)
    - [Optimization](#optimization)
    - [Training](#training)
    - [Source Analysis](#source-analysis)
## Application projects
### Detection

General object detection, face detection (and landmark) projects on Android platform.

- [ncnn-android-yolox](https://github.com/FeiGeChuanShu/ncnn-android-yolox) YOLOX detection android demo based on NCNN.

- [ncnn-android-nanodet](https://github.com/nihui/ncnn-android-nanodet) NanoDet object detection android project with Android ndk camera for best efficiency. Tutorial: [android camera nanodet 实时物体检测的高效实现总结](https://zhuanlan.zhihu.com/p/356991989)

- [thundernet_ncnn](https://github.com/DayBreak-u/thundernet_ncnn) The C++ version of thundernet with ncnn.

- [ncnn_nanodet_hand](https://github.com/FeiGeChuanShu/ncnn_nanodet_hand) Hand detection on android platform with ncnn (安卓平台人手检测)

- [RobotVision2](https://github.com/hzq-zjm/RobotVision2) Real-time fatigue driving detection on the mobile platform (移动端实时疲劳驾驶检测)

- [hayoou_safe_driving_android](https://github.com/youkpan/hayoou_safe_driving_android) Lane detection (with FCW and LDW) android demo based on Yolov4 and Ultra fast lane detection, runs at 8 fps on HONOR 20PRO Kirin 980 phone.

- [nanodet](https://github.com/RangiLyu/nanodet) NanoDet, a Super fast and lightweight anchor-free object detection model. 🔥Only 1.8mb and run 97FPS on cellphone, with training and NCNN based inference inside.

- [YOLOv5_NCNN by WZTENG](https://github.com/WZTENG/YOLOv5_NCNN) Android/iOS camera preview with YOLOv5 (移动端目标检测，当前项目使用的是YOLOv5的5s模型，摄像头实时捕获视频流进行检测)

- [Face-Mask-Detection-Raspberry-Pi-64-bits](https://github.com/Qengineering/Face-Mask-Detection-Raspberry-Pi-64-bits) Face mask detection on Rasberry Pi (树莓派上的口罩检测)

- [YOLOV5_NCNN_Android by sunnyden](https://github.com/sunnyden/YOLOV5_NCNN_Android) YOLOv5 NCNN implementation on Android platform.

- [PFLD-pytorch](https://github.com/polarisZhao/PFLD-pytorch) Practical Facial Landmark Detector with PyTorch and NCNN implementation. (PFLD pytorch Implementation ，自带 ncnn 推理实现)

- [LFFD-with-ncnn](https://github.com/SyGoing/LFFD-with-ncnn) LFFD ( A Light and Fast Face Detector for Edge Devices )'s implementation in NCNN.

- [Iris_Landmarks_PyTorch](https://github.com/ItchyHiker/Iris_Landmarks_PyTorch) Iris landmarks localization 瞳孔定位，有转ncnn模型脚本

- [ncnn-android-ultraface](https://github.com/oaup/ncnn-android-ultraface) ultraface android project

- [DBface_ncnn_demo](https://github.com/yuanluw/DBface_ncnn_demo) dbface ncnn 人脸检测

- [darknet_face_with_landmark](https://github.com/ouyanghuiyu/darknet_face_with_landmark)  借鉴AlexeyAB大神的 darknet 做适量修改，用于人脸检测以及关键点检测,支持ncnn推理

- [ncnn_android_face_vehicle](https://github.com/791136190/ncnn_android_face_vehicle) ncnn在Android的一个测试,包含了人脸检测(face detection),人脸属性(face attributes),人脸识别(face recognition);车辆检测(Vehicle detection),车牌检测(plate detection),车牌识别(plate recognition);人头检测(head detection)的流程

- [centernet_ncnn](https://github.com/wanglaotou/centernet_ncnn) Objects as Points, ncnn implementation

- [centerface-ncnn](https://github.com/JuZiSYJ/centerface-ncnn) centerface android project

- [PCN-ncnn](https://github.com/HandsomeHans/PCN-ncnn) Progressive Calibration Networks (PCN) is an accurate rotation-invariant face detector running at real-time speed on CPU (CVPR 2018), with ncnn based inference.

- [Ultra-Light-Fast-Generic-Face-Detector-1MB](https://github.com/Linzaer/Ultra-Light-Fast-Generic-Face-Detector-1MB) 1MB lightweight face detection model (1MB轻量级人脸检测模型)

### Super Resolution

- [realsr-ncnn-vulkan](https://github.com/nihui/realsr-ncnn-vulkan) ncnn implementation of Real-World Super-Resolution via Kernel Estimation and Noise Injection super resolution.

- [srmd-ncnn-vulkan](https://github.com/nihui/srmd-ncnn-vulkan) ncnn implementation of SRMD super resolution.

- [waifu2x-ncnn-vulkan](https://github.com/nihui/waifu2x-ncnn-vulkan) waifu2x converter ncnn version, runs fast on intel / amd / nvidia GPU with vulkan

- [vapoursynth-waifu2x-ncnn-vulkan](https://github.com/Nlzy/vapoursynth-waifu2x-ncnn-vulkan) Waifu2x filter for VapourSynth

- [VapourSynth-SRMD-ncnn-Vulkan](https://github.com/Kiyamou/VapourSynth-SRMD-ncnn-Vulkan) SRMD super resolution for VapourSynth

- [Waifu2x-Extension-GUI](https://github.com/AaronFeng753/Waifu2x-Extension-GUI) Photo/Video/GIF enlargement and Video frame interpolation using machine learning (使用NCNN的图像超分辨率及视频插帧软件)

- [waifu2x-ncnn-vulkan-python](https://github.com/tonquer/waifu2x-ncnn-vulkan-python) Exporting pyd for python based on waifu2x-ncnn-vulkan (修改waifu2x-ncnn-vulkan项目，导出pyd给python使用)

### Video Frame Interpolation

- [flowframes](https://github.com/n00mkrad/flowframes) Flowframes Windows GUI for video interpolation - Supports DAIN NCNN as well as RIFE Pytorch and NCNN implementations.

- [rife-ncnn-vulkan](https://github.com/nihui/rife-ncnn-vulkan) ncnn implementation of RIFE, Real-Time Intermediate Flow Estimation for Video Frame Interpolation.

- [cain-ncnn-vulkan](https://github.com/nihui/cain-ncnn-vulkan) ncnn implementation of CAIN, Channel Attention Is All You Need for Video Frame Interpolation.

- [dain-ncnn-vulkan](https://github.com/nihui/dain-ncnn-vulkan) ncnn implementation of DAIN, Depth-Aware Video Frame Interpolation.

### Pose Estimation

- [NCNN_Android_SinglePoseEstimation](https://github.com/ZtoYtoQ/NCNN_Android_SinglePoseEstimation) 单人人体姿态定位 android 工程

- [NCNN-PoseEstimation](https://github.com/ZtoYtoQ/NCNN-PoseEstimation) Realtime Pose Estimation NCNN ONNX 

- [ncnn_Android_MoveNet](https://github.com/FeiGeChuanShu/ncnn_Android_MoveNet) Android MoveNet pose estimation by ncnn

- [deep-head-pose-ncnn](https://github.com/docongminh/deep-head-pose-ncnn) Simple inference deep head pose ncnn version.

### Segmentation

- [RobustVideoMatting](https://github.com/FeiGeChuanShu/ncnn_Android_RobustVideoMatting) Android human segmentation by ncnn.

- [ncnn_Android_hair](https://github.com/FeiGeChuanShu/ncnn_Android_hair) Android hair segmentation demo by ncnn (基于 ncnn 的头发分割 android demo app)

- [ncnn-portrait-segmentation](https://github.com/leeys888/ncnn-portrait-segmentation) Real-time human segmentation on CPU

- [ncnn-android-deeplabv3plus](https://github.com/runrunrun1994/ncnn-android-deeplabv3plus) The deeplabv3+ person segmentation android example.

- [SOLOV2_ncnn](https://github.com/DayBreak-u/SOLOV2_ncnn) The C++ version of solov2 with ncnn 

- [Sky-Segmentation-and-Post-processing](https://github.com/xiongzhu666/Sky-Segmentation-and-Post-processing) C++ implementation for Sky segmentation and post-processing for the paper [https://arxiv.org/abs/2006.10172](https://arxiv.org/abs/2006.10172) with ncnn.

### Wasm

- [ncnn-webassembly-scrfd](https://github.com/nihui/ncnn-webassembly-scrfd) Deploy SCRFD, an efficient high accuracy face detection approach, in your web browser with ncnn and webassembly

- [ncnn-webassembly-ocrlite](https://github.com/Sg4Dylan/ncnn-webassembly-ocrlite) Deploy OcrLite in your web browser with ncnn and webassembly

- [ncnn-webassembly-portrait-segmentation](https://github.com/nihui/ncnn-webassembly-portrait-segmentation) Portrait segmentation in your browser with ncnn and webassembly

- [ncnn-webassembly-nanodet](https://github.com/nihui/ncnn-webassembly-nanodet) Deploy nanodet, the super fast and lightweight object detection, in your web browser with ncnn and webassembly

- [ncnnRay++](https://github.com/QuantScientist/ncnnRay) A CMake / WASM integration of rayib UI and the Tencent ncnn C++ AI platform

- [ncnn-webassembly-yolov5](https://github.com/nihui/ncnn-webassembly-yolov5) Run NCNN based YoloV5 detector in your browser!

- [ncnn-webassembly-blazeface](https://github.com/zineos/ncnn-webassembly-blazeface) Run blazeface detector in browser.

### Other

- [YOLOP-NCNN](https://github.com/EdVince/YOLOP-NCNN) _You Only Look Once for Panopitic Driving Perception_, Android app by ncnn (车辆检测+路面分割+车道线分割 三合一的网络, Android Demo).

- [SID-NCNN](https://github.com/EdVince/SID-NCNN) _Learning to See in the Dark_ running in Android by ncnn with Raw Camera (CVPR2018'Learning to See in the Dark, 暗光成像，用ncnn在安卓上进行简单的部署实现)

- [monodepth-NCNN](https://github.com/EdVince/monodepth-NCNN) Deploy wavelet-monodepth ([CVPR 2021  Monocular depth estimation using wavelets for efficiency](https://github.com/nianticlabs/wavelet-monodepth) ) model on Android with ncnn (将wavelet-monodepth的模型搬运到NCNN上，工程里面给了安卓的工程以及以及生成好的app安装包).

- [PiDiNet-NCNN](https://github.com/EdVince/PiDiNet-NCNN) Deploy PiDINet([Pixel Difference Networks for Efficient Edge Detection](https://github.com/zhuoinoulu/pidinet)) on Android with ncnn (使用NCNN在安卓上实现PiDiNet这个边缘检测网络)

- [OpenSitUp](https://github.com/DL-Practise/OpenSitUp) OpenSitUp是一个基于姿态估计的开源项目，基于 ncnn 搭建了一个在android手机上运行的仰卧起坐计数APP

- [SeqSeq ncnn](https://github.com/DayBreak-u/seq2seq_ncnn) The C++ version of SeqSeq with ncnn

- [ncnn_paddleocr](https://github.com/FeiGeChuanShu/ncnn_paddleocr) convert paddleocr light model to ncnn,you can use it by ncnn.

- [ncnn-swift](https://github.com/zhuzilin/ncnn-swift) A project of using ncnn in Swift for modern iOS development, with image classification & object detection (yolov5) examples.

- [ncnn-picture-enhancement](https://github.com/JuZiSYJ/ncnn-picture-enhancement) A simple demo to run dehaze / underwater model in Android (照片去雾和水下增强).

- [enet-as-linux](https://github.com/watersink/enet-as-linux) 基于ncnn的android端的enet分割

- [mobile-lpr](https://github.com/xiangweizeng/mobile-lpr) 一个面向移动端的准商业级车牌识别库

- [demo_deepsort](https://github.com/ProLing1994/demo_deepsort) deepsort tracking demo

- [chineseocr_lite](https://github.com/ouyanghuiyu/chineseocr_lite) Super lightweight OCR for Chinese characters, supporting horizontal recognition, support ncnn inference (超轻量级中文ocr，支持竖排文字识别, 支持ncnn推理)

- [ncnn-android-styletransfer](https://github.com/nihui/ncnn-android-styletransfer)  ncnn style transfer android example

- [ncnn_example by MirrorYuChen](https://github.com/MirrorYuChen/ncnn_example) A collection of ncnn examples: face/mask detection, tracking, recognition...

## Tools 

Model convert tools and wrapper/bindings of ncnn (模型转换工具、对ncnn封装等相关项目)

- [keras2ncnn](https://github.com/MarsTechHAN/keras2ncnn): A keras h5df to ncnn model converter

- [darknet-ncnn-android](https://github.com/paleomoon/darknet-ncnn-android)  darknet ncnn android project

- [caffe-int8-convert-tools](https://github.com/BUG1989/caffe-int8-convert-tools) Caffe INT8 Quantization convert tool

## Wrappers

- [ros_ncnn](https://github.com/nilseuropa/ros_ncnn) ROS wrapper for NCNN neural inference framework

- [pyncnn](https://github.com/caishanli/pyncnn) python wrapper of ncnn with pybind11 (Note: now updated in [ncnn official](https://github.com/tencent/ncnn) repo's python directory)

- [ncnn-lite](https://github.com/nullptr-leo/ncnn-lite) NCNN lite without C++ support (Note: There is [ncnn C API](https://github.com/Tencent/ncnn/blob/master/src/c_api.h) now)

- [NcnnDotNet](https://github.com/takuya-takeuchi/NcnnDotNet) ncnn .NET wrapper written in C++ and C# for Windows, MacOS and Linux

## Optimization

- [ncnn-with-cuda](https://github.com/atanmarko/ncnn-with-cuda) Tencent NCNN with added CUDA support

## Training

- [ncnnqat](https://github.com/ChenShisen/ncnnqat) quantize aware training package for NCNN on pytorch.

## Source Analysis

- [ncnn_breakdown - by All Star](https://github.com/Zhengtq/ncnn_breakdown) A breakdown of NCNN (学习ncnn的过程的一个记录)

- [ncnn初探 - by OFShare](https://www.zhihu.com/column/c_1320446932913762304) ncnn源码解析, 带你进入底层实现的点点滴滴.

- [如何阅读一个前向推理框架？以NCNN为例 - by BBuf](https://blog.csdn.net/just_sort/article/details/111403398) 如何阅读NCNN框架

- [ncnn源码分析 - by MirrorYuChen](https://blog.csdn.net/sinat_31425585/category_9312419.html)
