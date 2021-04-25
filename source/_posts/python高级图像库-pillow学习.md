---
title: python高级图像库 Pillow学习
tags: [python,pillow]
id: '635'
categories:
  - - 计算机编程
abbrlink: f4ebfb31
date: 2019-04-22 15:18:18
---

频段 一个图片允许包含一个或多个频段. Python Imaging Library 允许你在单个图像中存储多个频段. 包括原图像的尺寸和大小. 举个例子, 一个PNG图片可能包含 ‘R’, ‘G’, ‘B’, 和 ‘A’ 频段来表示红, 绿, 蓝和 alpha 透明值. 有许多对应频段的操作. 例如: histograms. 它常常用来处理不同像素的每个频段的值. 要想获得图像的频段的数量和名称, 使用 getbands() 方法. 模式 图像的 mode 定义了这个图像每一个像素点的大小. 目前版本支持以下标准模式: 1 (1-bit 像素点, 黑白, 一个像素点占用一个byte) L (8-bit 像素点, 黑白) P (8-bit 像素点, 使用调色板来映射其他模式) RGB (3x8-bit 像素点, 真彩) RGBA (4x8-bit 像素点, 带有透明标记的真彩) CMYK (4x8-bit 像素点, 分色) YCbCr (3x8-bit 像素点, 图像视频格式) 值得注意的是这个属于 JPEG, 而并不是 ITU-R BT.2020, standard LAB (3x8-bit 像素点, L\*a\*b 色彩空间) HSV (3x8-bit 像素点, Hue, Saturation, Value 色彩空间) I (32-bit 有符号整数像素) F (32-bit 浮点像素)     **打开和查看一个文件** from PIL import Image >>>im = Image.open("lena.ppm") >>> from \_\_future\_\_ import print\_function >>> print(im.format, im.size, im.mode) PPM (512, 512) RGB #os.path.splitext()可以用来分离文件名和文件格式 #im.format 如果图片打开失败，则为None #im.size返回元祖（宽，高） #im.mode 这个属性代表图片的band属性, 一般情况(黑白)下为 “L”, 当图片是彩色的时候是 “RGB”, 如果图片经过压缩,则是 “CMYK”.   **根据图片生成缩略图** im.thumbnail(size)    可以设置缩略图的大小

from \_\_future\_\_ import print\_function
import os, sys
from PIL import Image

size \= (128, 128)

for infile in sys.argv\[1:\]:
    outfile \= os.path.splitext(infile)\[0\] + ".thumbnail"
    if infile != outfile:
        try:
            im \= Image.open(infile)
            im.thumbnail(size)
            im.save(outfile, "JPEG")
        except IOError:
            print("cannot create thumbnail for", infile)

  **截取图片的某个区域的矩形** 尺寸排序为 (左, 上, 右, 下)，截取的部分就是一个坐标系 ![](https://gitee.com/wittzhang/pic332b/raw/master/wp-content/uploads/2019/04/20190422163547.png)  

box \= (100, 100, 400, 400)
region \= im.crop(box)
region.show() 

  **将某个图片复制到另外一张** ![](https://gitee.com/wittzhang/pic332b/raw/master/wp-content/uploads/2019/04/113214214124.jpg)     **将截图的某个图片进行平铺**

from PIL import Image
im = Image.open('xej.jpg')
box = (100, 100, 400, 400)
region = im.crop(box)
# region.show()
region = region.transpose(Image.ROTATE\_180)   #旋转180度
im.paste(region, box)
im.show()

![](https://gitee.com/wittzhang/pic332b/raw/master/wp-content/uploads/2019/04/20190422163027.png)     **图片旋转** 图片围绕着自身旋转，默认是自身为中心点旋转，当是正数是则为逆时针旋转

out = im.rotate(-45)
out.show()

  图片镜像

out = im.transpose(Image.FLIP\_LEFT\_RIGHT)
out.show()

![](https://gitee.com/wittzhang/pic332b/raw/master/wp-content/uploads/2019/04/20190422165246.png)   图片翻转

out = im.transpose(Image.FLIP\_TOP\_BOTTOM)
out.show()

![](https://gitee.com/wittzhang/pic332b/raw/master/wp-content/uploads/2019/04/20190422165724.png)   它也可以根据度数来旋转，不过只有三个固定的度数90、180和270度

out = im.transpose(Image.ROTATE\_90)

  它的旋转和im.rotate()是右区别的，让他们都旋转90度，左为im.rotate()，不会改变图片的尺寸但不能完全显示；右边为im.transpose(Image.ROTATE\_90)，会改变图片尺寸能完全显示 ![](https://gitee.com/wittzhang/pic332b/raw/master/wp-content/uploads/2019/04/20190422170521.png) **图片模式转换** 在L模式下图片色彩会变成黑白的

im = im.convert("L")

  **图片滤镜**

out = im.filter(ImageFilter.DETAIL)

  **创建一个空白图像** 图片模式，图片大小，图片颜色

im = Image.new('1',(100,100),'white')

  **在一个图像写入一个线条** 前面参数是坐标（左上右下），后面是颜色

draw = ImageDraw.Draw(im)
draw.line((0, 0,255,255), fill=(255,255,255))

  文本使用指定字体写入图像 1.设置字体和字体大小 2.定义文字的左上角坐标，文本，字体，字体颜色

fnt = ImageFont.truetype('msyh.ttf', 40)

d = ImageDraw.Draw(image)

d.text((10,10), "Hello", font=fnt, fill=(255,255,255,128))