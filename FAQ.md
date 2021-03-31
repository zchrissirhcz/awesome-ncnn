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


## 常见问题3. 怎样添加ncnn库到项目中？cmake方式怎么用？

基于cmake，在CMakeLists.txt里写这几句：
```cmake
set(ncnn_DIR "<ncnn_install_dir>/lib/cmake/ncnn" CACHE PATH "Directory that contains ncnnConfig.cmake")
find_package(ncnn REQUIRED)
target_link_libraries(my_target ncnn)
```
其中 `ncnn_DIR`是包含`ncnnConfig.cmake`的目录；如果你的ncnn是手动编译的，在Linux/Mac下请先执行make install，`ncnn_install_dir`此时对应 `build/install` 目录。

## 常见问题4. 找不到OpenCV？OpenCV_DIR设成什么？

在自己的项目中使用到 opencv；或者是在ncnn的项目中希望跑通example例子，需要正确的找到opencv。cmake方式，是设定`OpenCV_DIR`，它的指，是包含`OpenCVConfig.cmake`的目录：注意请自行检查这个目录，而不是草率的设定为“OpenCV安装的根目录”，因为在Linux/Windows/Mac/Android下，这个目录不一样。

例如本人的常用设定模板：
```cmake
if (CMAKE_HOST_SYSTEM_NAME MATCHES "Linux")
    if (CMAKE_SYSTEM_NAME MATCHES "Linux")
        #set(OpenCV_DIR "/home/zz/soft/opencv-4.5.1/lib/cmake/opencv4" CACHE PATH "") # shared
        set(OpenCV_DIR "/home/zz/soft/opencv-4.5.1-static/lib/cmake/opencv4" CACHE PATH "") # static
    elseif (ANDROID)
        set(OpenCV_DIR "/home/zz/soft/opencv-4.5.1-android/sdk/native/jni" CACHE PATH "")
    endif()
elseif (CMAKE_HOST_SYSTEM_NAME MATCHES "Windows")
    if (CMAKE_SYSTEM_NAME MATCHES "Windows")
        #set(OpenCV_DIR "E:/lib/opencv/4.5.0" CACHE PATH "")
        set(OpenCV_DIR "E:/lib/opencv/4.5.2-pre" CACHE PATH "")
    elseif (ANDROID)
        set(OpenCV_DIR "E:/soft/Android/opencv-4.5.0-android-sdk/sdk/native/jni" CACHE PATH "")
    endif()
elseif (CMAKE_HOST_SYSTEM_NAME MATCHES "Darwin")
    if (CMAKE_SYSTEM_NAME MATCHES "Darwin")
        set(OpenCV_DIR "/usr/local/opencv-4.2/lib/cmake/opencv4" CACHE PATH "")
    elseif (ANDROID)
        set(OpenCV_DIR "/Users/chris/soft/opencv-4.5.0-android-sdk/sdk/native/jni" CACHE PATH "")
    endif()
endif()
find_package(OpenCV REQUIRED)
target_link_libraries(testbed ${OpenCV_LIBS})
```

## 常见问题5. 为啥自己编译的ncnn android库特别大？

很可能是没有去掉`-g`导致的。

基于cmake和ninja，自行编译ncnn的android库，编译时注意：
- 去掉`-g`参数以减小库体积：打开`$ANDROID_NDK/build/cmake/android.toolchain.cmake`
```
# 删除 "-g" 这行
list(APPEND ANDROID_COMPILER_FLAGS
  -g
  -DANDROID
```

## 常见问题6. undefined reference to `glslang::FinalizeProcess()'
使用ncnn vulkan库时遇到报错例如：
```
/hone/inxsuno/inx-yocto-bsp/inx6qp/task/ncnn_inx8_build/install/lib/Libncnn.a(gpu.cpp.o): In function 'ncn::destroy
_gpu_instance() ':
gpu.cpp:(.text+0xfb8): undefined reference to 'glslang::FinalizeProcess() '
/hone/inxsuno/inx-yocto-bsp/inx6qp/task/ncnn_imx8 butid/instal/ltb/l.tbncn .a(gpu.cpp.o): In function 'ncm:create gpu_instance() pu.cpp:(.text+0x39a0): undefined reference to 'glslang::InitializeProcess()'
/hone/inxsuno/inx -ycto-bsp/in;oqp/task /ncm inmv8 buildjinstal/Lib/litncm.a(gpu.pp.o): In fucion ‘ncnm:comple spitv ole(char cost,in , nmn1 .oprto coste,cator<unsigned int> >&) ':
gpu.cpp:(.text+Ox78b4): undefined reference to 'glslang::TShader : :TShader(EShLanguage)'
gpu.cpp:(.text+×78c8): undefined reference to glslang::TShader:.setstringswithLengths(char const* const*,int const*,int)"
Spu.cpp;(.text-+8x7B8dc): undefined reference to 'glslang Tshader :.dProcsses(std:.vectorsty:_co1:basic string chr ,tti.xchar_traitschar ,.sthallacatorcharpic_string<char, std::char_traits<char>, std::allocator<char> > > > const&)'
gpu.cpp:(.text+0x78ec): undefined reference to 'glslang:: TShader ::setEntryPoint(char const*)'
gpu.cpp:( . text+0x78f8): undefined reference to 'glslang::TShader::setSourceEntryPoint(char const*)'
gpu.cpp:(.text+0x7a8c): undefined reference to ‘glslang::TShader ::.parse( TBuiltInResource const*，int，EProfile， boo
, bool，EShMessages, glslang : : TShader : : Includer&)'
gpu.cpp:(.text+0x7ad4): undefined reference to `glslang:: TShader ::getInfoLog()'
pu.cpp:(.text+Ox7afc): undefined reference to 'glslang::TShader ::getInfoDebugLog()'gpu.cpp:(.text+0x7b20): undefined reference to `glslang::TShader::~TShader() '
Jpu.gp:(.text+6x84f4): undefined reference to ‘glslang;clslangTosp(glslng.e TIntenediate cost& lstt.wecoransigned nt, stir:alloctoransigned int >, glslag:gpu.cpp:(.text+0x8500): undefined reference to 'glslang:: TShader :~TShader()'
pu.cpp:(.text+0x9618): undefined reference to 'glslang::TShader : :~TShader()'collect2 : error : ld returned 1.exit status
nake[2]:***[TEST_PIPLINE]错误1
ake[1j:***[CMakeFiles /TEST_PIPLINE.dir/all]错误﹖
```

错误的写法：
```cmake
set(NCC_INCLUDE_DIRS /home/imxsumo/imx-yocto-bsp/imx6qp/task/ncnn_imx8_build/install/include/ncnn)

target_link_libraries(TEST_PIPLINE glslang MachineIndependent SPIRV ncnn ${OpenCV_LIBS} ${FT_LIBS} pthread g2d gomp vulkan)
```


原因：CMakeLists.txt中，自行手动指定的ncnn静态库，以及vulkan相关的glslang库等，但顺序没弄对。

解决方法：`find_package(ncnn)`，它会自动设定正确的链接库及其顺序
```
set(ncnn_DIR "<ncnn_install_dir>/lib/cmake/ncnn" CACHE PATH "Directory that contains ncnnConfig.cmake")
find_package(ncnn REQUIRED)
target_link_libraries(my_target ncnn)
```