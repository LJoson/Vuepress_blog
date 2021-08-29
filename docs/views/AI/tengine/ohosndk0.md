---
title: 基于tengine+ohos的ndk开发-环境准备
date: 2021-03-27 22:00:12
sidebar: true
sidebarDepth: 5
tags: 
- 模型部署及加速
categories:
- "AI及大数据类"
isShowComments: true
---
[[toc]]

# 引言

[Tengine](https://github.com/OAID/Tengine)


## 安装 DevEco Studio 和 OHOS NDK
下载安装[DevEco Studio](https://developer.harmonyos.com/cn/develop/deveco-studio#download)，若没有华为开发者账号，需到[HarmonyOS应用开发门户](https://developer.harmonyos.com/cn/home)注册。

打开 DevEco Studio，Configure（或File）-> Settings -> Appearance & Behavior -> System Settings -> HarmonyOS SDK，勾选并下载 Native，完成 OHOS NDK 下载。
## 准备 OHOS NDK cmake toolchain 文件
ohos.toolchain.cmake 这个文件可以从 $OHOS_NDK/build/cmake 找到，例如C:/Users/mycomputer/AppData/Local/Huawei/Sdk/native/2.1.0.13/build/cmake/ohos.toolchain.cmake

(可选) 删除debug编译参数，缩小二进制体积，方法和 android ndk相同 android-ndk issue
```
# 用编辑器打开 $ANDROID_NDK/build/cmake/android.toolchain.cmake
# 删除 "-g" 这行
list(APPEND ANDROID_COMPILER_FLAGS
 -g
 -DANDROID

```
## 下载 Tengine Lite 源码
```
git clone -b tengine-lite https://github.com/OAID/Tengine.git Tengine-Lite
```
## 编译 Tengine Lite
Arm64 OHOS 编译（主要是Windows平台,DevEco Studio还没有Linux）
- 新建一个build文件夹
- 在build文件夹里新建一个ohos-arm64-v8a.bat.bat脚本

```

@ECHO OFF
@SETLOCAL

:: Set OHOS native toolchain root
@SET OHOS_NDK=<your-ndk-root_path, such as C:/Users/mycomputer/AppData/Local/Huawei/Sdk/native/2.1.0.13>


:: Set ninja.exe and cmake.exe
@SET NINJA_EXE=%OHOS_NDK%/build-tools/cmake/bin/ninja.exe
@SET CMAKE_EXE=%OHOS_NDK%/build-tools/cmake/bin/cmake.exe
@SET PATH=%OHOS_NDK%/llvm/bin;%OHOS_NDK%/build-tools/cmake/bin;%PATH%


::下面部分脚本有点问题
::mkdir build-ohos-armeabi-v7a
::pushd build-ohos-armeabi-v7a
::%CMAKE_EXE% ../.. -G Ninja -DCMAKE_TOOLCHAIN_FILE="%OHOS_NDK%/build/cmake/ohos.toolchain.cmake"  ::-DCMAKE_MAKE_PROGRAM=%NINJA_EXE%  -DOHOS_ARCH="armeabi-v7a" -DCMAKE_BUILD_WITH_INSTALL_RPATH=ON 
::%CMAKE_EXE% --build . --parallel %NUMBER_OF_PROCESSORS%
::%CMAKE_EXE% --build . --target install
::popd

mkdir build-ohos-arm64-v8a
pushd build-ohos-arm64-v8a
%CMAKE_EXE% ../.. -G Ninja -DCMAKE_TOOLCHAIN_FILE="%OHOS_NDK%/build/cmake/ohos.toolchain.cmake"  -DCMAKE_MAKE_PROGRAM=%NINJA_EXE%  -DOHOS_ARCH="arm64-v8a" -DCMAKE_BUILD_WITH_INSTALL_RPATH=ON  
%CMAKE_EXE% --build . --parallel %NUMBER_OF_PROCESSORS%
%CMAKE_EXE% --build . --target install
popd


@ENDLOCAL


```

运行即可。
ps:可能需要安装ninja:

下载[ninja](https://github.com/ninja-build/ninja/releases)中的exe(win平台)，解压在任意一个文件夹，并在系统环境变量中加入此路径路径，重启。运行
```
ninja -V
```
可以验证是否成功安装。但是如果想自己编译安装，需要准备好环境，之后可参考这篇博客[https://github.com/ninja-build/ninja/wiki](https://github.com/ninja-build/ninja/wiki)

## issues

期间遇到很多llvm,clang,openmp等有关的bug，不少是跟cmakelists编写有关。（这些还需要更加深入学习以及了解）


::: tip 更多

[llvm](https://llvm.org/)

[openmp](https://www.openmp.org/)

[simd](https://wiki.mozilla.org/SIMD/Overview)
:::