# 安装opencv

<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=6 orderedList=false} -->

<!-- code_chunk_output -->

- [安装opencv](#安装opencv)
  - [什么是 OpenCV](#什么是-opencv)
  - [安装 OpenCV](#安装-opencv)
  - [测试 OpenCV 安装](#测试-opencv-安装)
  - [opencv架构](#opencv架构)
  - [OpenCV 图像读取与显示](#opencv-图像读取与显示)
    - [读取图像](#读取图像)
    - [显示图像](#显示图像)
    - [保存图像](#保存图像)

<!-- /code_chunk_output -->

python的opencv安装比较简单，一句命令行`pip install opencv-python`就可以了，不过前提是python环境要配好，我没有按教程一样安装特定版本......甚至python版本都是最新的 ~~（已经做好踩坑的准备了）~~。

我使用的环境是WSL2+VSCode，目前没有感觉什么不适，同普通的linux区别不大，甚至更方便 ~~（什么是最好的linux发行版啊！）~~，如果有想体验的可以参考这个[Dev on Windows with WSL](https://dowww.spencerwoo.com/1-preparations/1-0-intro.html)文档，我在配置的参考了这个教程。

## 什么是 OpenCV

OpenCV（Open Computer Vision）是一个开源的计算机视觉库，提供了各种丰富的图像处理工具和算法。它支持多种编程语言，如 C++、Python 等，并且可以在多种平台上使用，包括 Windows、Linux 和 MacOS。

OpenCV 最初是由 Intel 公司在 1999 年开发的，现在已经成为计算机视觉领域的一个行业标准。它提供了大量的基础图像处理功能，如图像缩放、旋转、裁剪等，也提供了各种高级图像处理功能，如目标检测、边缘检测、图像分类等。

## 安装 OpenCV

要使用 OpenCV，首先需要在计算机上安装它。这里介绍在 Python 环境中安装 OpenCV 的方法。
首先，确保你的计算机上已经安装了 Python 和 pip（Python 的包管理工具）。
在终端中运行以下命令：

```sh
pip install opencv-python
```

就可以安装opencv-python

## 测试 OpenCV 安装

可以在 Python 中导入 OpenCV 库来查看是否可以正常使用：

```py
import cv2
print(cv2.__version__)
```

还可以使用 OpenCV 的命令行工具来测试一下：

```sh
# 显示帮助信息
opencv_version -h

# 显示版本信息
opencv_version
```

## opencv架构

OpenCV的架构由两个部分组成：内核（Kernel）和接口（Interfaces）。

内核部分由若干个模块组成，每个模块都是一组相关的函数和类，用于实现某种特定的功能。这些模块包括：

- 基础模块（Core）：提供基本的数据类型、图像处理函数、线性代数运算等功能。
- 图像处理模块（Imgproc）：提供图像的转换、滤波、形态学处理、边缘检测等功能。
- 图像分析模块（Imgcodecs）：提供图像的读取、写入、压缩等功能。
- 图像特征检测模块（Features2d）：提供图像的特征检测、匹配、描述等功能。
- 目标检测模块（Objdetect）：提供目标检测、跟踪等功能。

接口部分提供了多种方式来调用OpenCV的内核函数。这些接口包括：

- C接口（C API）：使用C语言编写的接口，提供了一组C语言风格的函数来调用OpenCV的内核函数。
- C++接口（C++ API）：使用C++语言编写的接口，提供了一组C++类来封装OpenCV的内核函数。
- Python接口（Python API）：使用Python语言编写的接口，提供了一组Python模块来调用OpenCV的内核函数。
OpenCV还提供了许多其他的功能，如视频处理、机器学习、3D重建等。

## OpenCV 图像读取与显示

### 读取图像

使用 OpenCV 读取图像非常简单，只需要使用 cv2.imread() 函数即可。该函数的第一个参数是图像的路径，第二个参数是图像的读取模式。有两种读取模式：

`cv2.IMREAD_COLOR`：该模式会忽略图像的 alpha 通道，并将图像转换为 BGR 格式。
`cv2.IMREAD_GRAYSCALE`：该模式会将图像转换为灰度图。
下面是一个示例，展示了如何使用 OpenCV 读取图像：

```py
import cv2

# 读取彩色图像
image = cv2.imread('image.jpg', cv2.IMREAD_COLOR)

# 读取灰度图像
gray_image = cv2.imread('image.jpg', cv2.IMREAD_GRAYSCALE)
```

### 显示图像

使用 OpenCV 显示图像也非常简单，只需要使用 cv2.imshow() 函数即可。该函数接受两个参数：窗口的名称和要显示的图像。

下面是一个示例，展示了如何使用 OpenCV 显示图像：

```py
import cv2

# 读取图像
image = cv2.imread('image.jpg', cv2.IMREAD_COLOR)

# 显示图像
cv2.imshow('Image', image)

# 等待按键按下
cv2.waitKey(0)

# 关闭所有窗口
cv2.destroyAllWindows()
```

在上面的代码中，我们先使用 `cv2.imshow()` 函数显示图像，然后使用 `cv2.waitKey()` 函数等待按键按下。最后，使用 `cv2.destroyAllWindows()` 关闭所有窗口。

### 保存图像

如果你想保存图像，可以使用 `cv2.imwrite()` 函数。该函数接受两个参数：图像的路径和要保存的图像。

下面是一个示例，展示了如何使用 OpenCV 保存图像：

```py
import cv2

# 读取图像
image = cv2.imread('image.jpg', cv2.IMREAD_COLOR)

# 保存图像
cv2.imwrite('image_copy.jpg', image)
```

在上面的代码中，我们使用 `cv2.imwrite()` 函数将图像保存到了 `image_copy.jpg` 文件中。
