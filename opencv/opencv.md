# opencv学习记录

|日期|任务|
|--|--|
|2022/12/12|[安装opencv](#安装opencv)|
|2022/12/14|[图像基本操作](#图像基本操作)|
|2022/12/16|[滚动条/键盘响应/颜色表/通道操作](#滚动条键盘响应颜色表通道操作)|
|2022/12/18|[图像统计信息图像几何形状绘制/随机数与随机颜色/多边形填充与绘制](#图像统计信息图像几何形状绘制随机数与随机颜色多边形填充与绘制)|
|2022/12/20|[鼠标操作与响应图像像素类型转换与归一化图像几何变换视频读写处理](#鼠标操作与响应图像像素类型转换与归一化图像几何变换视频读写处理)|

## 安装opencv

python的opencv安装比较简单，一句命令行`pip install opencv-python`就可以了，不过前提是python环境要配好，我没有按教程一样安装特定版本......甚至python版本都是最新的 ~~（已经做好踩坑的准备了）~~。

我使用的环境是WSL2+VSCode，目前没有感觉什么不适，同普通的linux区别不大，甚至更方便 ~~（什么是最好的linux发行版啊！）~~，如果有想体验的可以参考这个[Dev on Windows with WSL](https://dowww.spencerwoo.com/1-preparations/1-0-intro.html)文档，我在配置的参考了这个教程。

另外在那个测试界面好像对缩放不是支持的很好，我的浏览器缩放是120%，右边那个作答情况就有一半看不见了。

## 图像基本操作

最近考试有点多，只能抽时间来学opencv了。

这次学习加强了对图像编码的认识：图像本质是一个大数组，至于解码就交给渲染了。使用opencv对图像操作也就是对数组进行操作。以一个简单的例子如一个灰度图，~~（用灰度图是因为他结构比较简单）~~要对它某个像素进行改动，那么其实就是对应的数组值进行变动，图形的加减乘除就是也是同样的道理，感觉有点像PS的原理，不知道PS底层是不是这样实现的。

## 滚动条/键盘响应/颜色表/通道操作

滚动条是一种用于控制变量值的小部件。它通常用于图像处理程序，可以调整图像的对比度、亮度等参数。可以使用 OpenCV 中的 cv2.createTrackbar() 函数创建一个滚动条。该函数需要指定滚动条的名称、窗口名称、初始值和最大值，并返回一个整数值，该值表示当前滚动条的位置。可以使用 cv2.getTrackbarPos() 函数获取当前滚动条的位置。

可以使用 cv2.setMouseCallback() 函数响应鼠标事件。该函数需要指定窗口名称、回调函数名称和一个可选的额外参数。回调函数将在鼠标事件发生时调用，并接收四个参数：鼠标事件、鼠标指针的 x 坐标、鼠标指针的 y 坐标和额外参数。可以在回调函数内部编写代码来响应鼠标事件，例如绘制图形或打印坐标。

自带颜色表是一种预定义的颜色集合，可以用于图像处理。例如，可以使用自带颜色表来绘制彩色的直方图或标记图像中的不同部分。OpenCV 中提供了多种自带颜色表，可以使用 cv2.applyColorMap() 函数将自带颜色表应用到图像上。该函数需要指定输入图像和自带颜色表的类型，并返回一个转换后的图像。

通道分离与合并是指将图像的颜色信息拆分成单独的通道（例如红色通道、绿色通道、蓝色通道）或将多个通道合并成单个图像的过程。可以使用 cv2.split() 函数将图像的通道分离成多个单独的数组，并使用 cv2.merge() 函数将多个数组合并成单个图像。还可以使用 cv2.extractChannel() 函数提取图像的单个通道，或使用 cv2.insertChannel() 函数将单个通道插入图像中。

## 图像统计信息图像/几何形状绘制/随机数与随机颜色/多边形填充与绘制

考试终于快结束了，接下来可以安心投入各种感兴趣的学习之中了。

这次的学习还是挺简单的，图形信息统计实际上是对数组的进行操作，不过没想到opencv也可以作图，不过想想也是，作图也是对图形的操作，要不然在深度学习中的标记是怎么画的，另外随机数与随机颜色，我记得那个绘图的AI就是通过扩散模型来实现的，而一开始就是生成的初始图案就是一堆噪点，然后通过扩散模型降噪。

## 鼠标操作与响应/图像像素类型转换与归一化/图像几何变换/视频读写处理

### 鼠标操作与响应

在 OpenCV 中，可以使用 `setMouseCallback()` 函数来设置鼠标回调函数:

```python
import cv2

# 定义鼠标回调函数
def mouse_callback(event, x, y, flags, params):
    if event == cv2.EVENT_LBUTTONDOWN:
        print("左键按下，坐标为：(%d, %d)" % (x, y))
    elif event == cv2.EVENT_RBUTTONDOWN:
        print("右键按下，坐标为：(%d, %d)" % (x, y))

# 创建图像窗口，并设置鼠标回调函数
cv2.namedWindow("image")
cv2.setMouseCallback("image", mouse_callback)

# 加载图像并在窗口中显示
image = cv2.imread("image.jpg")
cv2.imshow("image", image)
cv2.waitKey(0)
```

在这个示例中，我们定义了一个名为 `mouse_callback` 的鼠标回调函数，该函数接收五个参数：

* `event`：表示鼠标事件的常量，可以是如下之一：
  * `cv2.EVENT_LBUTTONDOWN`：左键按下
  * `cv2.EVENT_RBUTTONDOWN`：右键按下
  * `cv2.EVENT_MBUTTONDOWN`：中键按下
  * `cv2.EVENT_LBUTTONUP`：左键弹起
  * `cv2.EVENT_RBUTTONUP`：右键弹起
  * `cv2.EVENT_MBUTTONUP`：中键弹起
  * `cv2.EVENT_MOUSEMOVE`：鼠标移动
* `x`：鼠标指针在图像上的横坐标（以像素为单位）
* `y`：鼠标指针在图像上的纵坐标（以像素为单位）

* `flags`：鼠标事件的标志位，可以是如下之一：
  * `cv2.EVENT_FLAG_LBUTTON`：左键按下
  * `cv2.EVENT_FLAG_RBUTTON`：右键按下
  * `cv2.EVENT_FLAG_MBUTTON`：中键按下
  * `cv2.EVENT_FLAG_CTRLKEY`：CTRL 键按下
  * `cv2.EVENT_FLAG_SHIFTKEY`：SHIFT 键按下
  * `cv2.EVENT_FLAG_ALTKEY`：ALT 键按下
  * `params`：额外参数，可以是任意值（在这个示例中未使用）

在程序中，我们先使用 `cv2.namedWindow()` 函数创建一个图像窗口，然后使用 `cv2.setMouseCallback()` 函数将鼠标回调函数设置为 `mouse_callback`。接着，使用 `cv2.imread()` 函数加载图像，并使用 `cv2.imshow()` 函数在窗口中显示图像。最后，使用 `cv2.waitKey()` 函数等待键盘输入，使窗口保持打开状态。

### 图像像素类型转换与归一化

在 OpenCV 中，可以使用`cv2.normalize()` 函数来对图像进行归一化。此函数的第一个参数是输入图像，第二个参数是输出图像，第三个参数是归一化的最小值，第四个参数是归一化的最大值，第五个参数是归一化类型，第六个参数是归一化后图像的数据类型。

例如，以下代码对输入图像进行归一化，并将结果保存到输出图像中：

```py
import cv2

# 读取图像
img = cv2.imread("input.jpg")

# 归一化图像
normalized_img = cv2.normalize(img, None, 0, 255, cv2.NORM_MINMAX, cv2.CV_8U)

# 保存归一化后的图像
cv2.imwrite("normalized.jpg", normalized_img)
```

另外，在 OpenCV 中，也可以使用 `cv2.convertScaleAbs()` 函数来对图像进行像素类型转换和归一化。此函数的第一个参数是输入图像，第二个参数是输出图像，第三个参数是缩放因子，第四个参数是偏移量。

例如，以下代码将输入图像的像素类型转换为 8 位无符号整型，并将结果保存到输出图像中：

```py
import cv2

# 读取图像
img = cv2.imread("input.jpg")

# 像素类型转换和归一化
converted_img = cv2.convertScaleAbs(img, alpha=1.0, beta=0)
# 保存像素类型转换和归一化后的图像
cv2.imwrite("converted.jpg", converted_img)
```

### 图像几何变换

在 OpenCV 中，可以使用 `cv2.warpAffine()` 函数来进行仿射变换。此函数的第一个参数是输入图像，第二个参数是仿射变换矩阵，第三个参数是输出图像的大小。

例如，以下代码对输入图像进行仿射变换，并将结果保存到输出图像中：

```py
import cv2
import numpy as np

# 读取图像
img = cv2.imread("input.jpg")

# 计算仿射变换矩阵
rows, cols = img.shape[:2]
M = np.float32([[1, 0, 100], [0, 1, 50]])

# 仿射变换
warped_img = cv2.warpAffine(img, M, (cols, rows))

# 保存仿射变换后的图像
cv2.imwrite("warped.jpg", warped_img)
```

另外，在 OpenCV 中，也可以使用 `cv2.resize()` 函数来对图像进行缩放。此函数的第一个参数是输入图像，第二个参数是输出图像的大小，第三个参数是缩放比例（可以为 0），第四个参数是缩放插值方法。

例如，以下代码对输入图像进行缩放，并将结果保存到输出图像中：

```py
import cv2

# 读取图像
img = cv2.imread("input.jpg")

# 缩放图像
resized_img = cv2.resize(img, (600, 400), interpolation=cv2.INTER_LINEAR)

# 保存缩放后的图像
cv2.imwrite("resize.jpg")
```

此外，在 OpenCV 中，也可以使用 `cv2.getRotationMatrix2D()` 函数来计算旋转矩阵。此函数的第一个参数是旋转中心的坐标，第二个参数是旋转角度，第三个参数是旋转缩放因子。

例如，以下代码计算旋转矩阵：

```py
import cv2
import numpy as np

# 计算旋转矩阵
rows, cols = img.shape[:2]
M = cv2.getRotationMatrix2D((cols / 2, rows / 2), 45, 1)
```

然后，可以使用 `cv2.warpAffine()` 函数将旋转矩阵应用到图像上，从而实现图像旋转。

例如，以下代码对输入图像进行旋转，并将结果保存到输出图像中：

```py
import cv2
import numpy as np

# 读取图像
img = cv2.imread("input.jpg")

# 计算旋转矩阵
rows, cols = img.shape[:2]
M = cv2.getRotationMatrix2D((cols / 2, rows / 2), 45, 1)

# 旋转图像
rotated_img = cv2.warpAffine(img, M, (cols, rows))

# 保存旋转后的图像
cv2.imwrite("rotated.jpg", rotated_img)
```

### 视频读写处理

在 OpenCV 中，可以使用 `cv2.VideoCapture()` 函数来读取视频文件,例如，以下代码读取视频文件 "input.mp4"：

```py
import cv2

# 读取视频文件
cap = cv2.VideoCapture("input.mp4")
```

接下来，可以使用 `cv2.VideoCapture.read()` 方法来读取视频帧。此方法返回两个值：一个布尔值表示是否读取成功，以及当前帧的图像。

例如，以下代码读取视频的每一帧，并在窗口中显示：

```py
import cv2

# 读取视频文件
cap = cv2.VideoCapture("input.mp4")

# 循环读取视频帧
while True:
    # 读取帧
    ret, frame = cap.read()

    # 如果读取失败，退出循环
    if not ret:
        break

    # 显示帧
    cv2.imshow("Frame", frame)

    # 等待按键操作
    key = cv2.waitKey(30)
    if key == 27:  # 按下 Esc 键退出
        break

# 释放视频文件
cap.release()

# 销毁窗口
cv2.destroyAllWindows()
```

另外，在 OpenCV 中，也可以使用 `cv2.VideoWriter()` 函数来创建视频写入器。此函数的第一个参数是视频文件的路径，第二个参数是视频编码器，第三个参数是帧率,第四个参数是帧的大小，第五个参数是是否是彩色视频。

例如，以下代码创建视频写入器，并将视频帧写入文件 "output.mp4" 中：

```py
import cv2

# 创建视频写入器
fourcc = cv2.VideoWriter_fourcc(*"mp4v")
writer = cv2.VideoWriter("output.mp4", fourcc, 30, (640, 480), True)

# 循环读取视频帧
while True:
    # 读取帧
    ret, frame = cap.read()

    # 如果读取失败，退出循环
    if not ret:
        break

    # 写入帧
    writer.write(frame)

# 释放视频写入器
writer.release()
```
