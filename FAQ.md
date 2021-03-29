# ncnn 小白常见问题整理

## 常见问题1. rtti/exceptions冲突

在Android NDK（JNI）代码中遇到报错`error: use of typeid requires -frtti`

原因：ncnn的android预编译包的编译选项中，禁用了`rtti`（同时还禁用了`exceptions`），而OpenCV的android预编译包开启了`rtti`和`exceptions`（这是在NDK的toolchains.cmake中默认开启的）；当两个（或多个）库的rtti、exceptions编译选项设定不同时，会导致冲突，需要统一。

P.S.为什么ncnn预编译包要关掉rtti和exceptions：大概是为了减小包的大小

P.S.怎样统一ncnn和opencv的android库里头的rtti和exceptions？提供几种方案，任选其一，难度从低到高：

**方法1：用opencv-mobile库替代opencv anroid库**

不用opencv官方的预编译android库，用 https://github.com/nihui/opencv-mobile/releases

**方法2：重编ncnn，编译时开启rtti、exceptions**

基于cmake和ninja，自行编译ncnn的android库，编译时注意：
- 去掉`-g`参数以减小库体积：打开`$ANDROID_NDK/build/cmake/android.toolchain.cmake`
```
# 删除 "-g" 这行
list(APPEND ANDROID_COMPILER_FLAGS
  -g
  -DANDROID
```

- 在命令行（或CMake-GUI）里，用cmake构建，构建时传入`-DNCNN_DISABLE_EXCEPTION=OFF -DNCNN_DISABLE_RTTI=OFF`；如果先前构建过，请清理build/CMakeCache.txt；不要在Android Studio里构建ncnn库，因为很可能你的rtti和exceptions还是弄错

- 如果你不会cmake，请去学习，这非常基础

**方法3：不用opencv**

## 常见问题2. 编ncnn时protobuf报错/版本错？

当编译 ncnn 时，我们从 cmake 构建的角度去看，ncnn 这个开源项目有多个构建目标，包括：
- ncnn 库本身；它不依赖protobuf，也不依赖opencv
- ncnn 转换工具，例如 caffe2ncnn, mxnet2ncnn, darknet2ncnn, onnx2ncnn, keras2ncnn, mlir2ncnn等；其中 caffe2ncnn 和 onnx2ncnn 依赖 protobuf 库
- ncnn 例子，包括 squeezenet，yolov5, nanodet 等，都依赖opencv

如果你遇到 protobuf 找不到或版本错误等问题，可以考虑跳过，因为 https://convertmodel.com 这个网站提供了一站式的各种常见CNN推理库的模型转换工具的本地在线版，直接使用即可。

简单解释下什么是“本地在线版”：它是基于WebAssembly（wasm）实现的一个网页，当你上传模型文件时，实际上是在本地执行的转换；或者说，当你访问 https://convertmodel.com 后，断网，然后用这个网页，依然是能转换的；因此不必担心模型被上传到外网的风险。


P.S. 如果用 https://convertmodel.com 这个网站转换，发现报错，请在 ncnn卷卷群里 @大缺弦 ，他是这个网站的作者；或 @nihui ，他是 ncnn 作者。

