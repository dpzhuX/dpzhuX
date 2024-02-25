---
title: Build VTK 8.1.0 with Qt on a Mac
date: 2018-03-25 13:50:12
categories:
- Tutorial
tags:
- General
---

This marks my second attempt at compiling VTK on a Mac. A month ago, I invested considerable time figuring out how to compile it using CMake and eventually succeeded. However, it's surprisingly easy to forget the steps involved. To prevent that from happening again, I'm documenting the entire compilation process here.

<!-- more -->

First step is to download the VTK from the [VTK official website](https://vtk.org/download/). Then, unzip the package to a folder. Here I put it into the folder called "VTK-8.1.0". By the way, you should also install CMake from the [CMake website](https://cmake.org/download/) (Please ensure that the Qt and Xcode are installed in your Mac). Now, create another folder called "VTK_Build". This is the target folder to save the files generated by CMake. Open CMake and set the "source code" and "binaries" folder,

![CMake](/uploads/images/2018/BuildVtkForQt1.png)

Click "Configure" button, and set the generator for the source code, I just use the default selection. This means we will use make and make install to compile the code,

![CMake](/uploads/images/2018/BuildVtkForQt2.png)

After clicking "Done", CMake will configure the code,

![CMake](/uploads/images/2018/BuildVtkForQt3.png)

Now, we create another folder called "VTK_Bin" which is used to install VTK libraries. In CMake, we need change two options,

CMAKE_INSTALL_PREFIX: /User/zhudongping/Documents/Code/VTK_Bin
VTK_Group_Qt: ON

![CMake](/uploads/images/2018/BuildVtkForQt4.png)

Click "Configure" again, and CMake will tell you it cannot found the Qt5_DIR,

![CMake](/uploads/images/2018/BuildVtkForQt5.png)

Set the Qt5_DIR: /Applications/Qt/5.10.0/clang_64/lib/cmake/Qt5 and click "Configure" again. you will see,

![CMake](/uploads/images/2018/BuildVtkForQt6.png)

Now, you to need click "Configure" again, CMake will finish the final configuration. 

![CMake](/uploads/images/2018/BuildVtkForQt7.png)

Then, Click "Generate" in the panel to generate the binaries into "VTK_Build". Use Mac terminal to find this folder and type make command. If you want to use multithreading, type make -j8 command. Mac will compile the files generated by CMake,

![CMake](/uploads/images/2018/BuildVtkForQt8.png)

After the make command, you just need to type make install command to install the VTK libraries into "VTK_Bin" folder:

![CMake](/uploads/images/2018/BuildVtkForQt9.png)

Now, we successfully build the source code of VTK 8.1.0,

![CMake](/uploads/images/2018/BuildVtkForQt10.png)

For using VTK in Qt 5.10.0, remember to put the following code into main function,

```
QSurfaceFormat::setDefaultFormat(QVTKOpenGLWidget::defaultFormat());
```
