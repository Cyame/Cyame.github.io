# Aegisub Override Tags | AEG标签

## General 综述

### What is "Override"? 何为"重载"?

### Break 空白

### Line Autobreaking Style 自动换行模式

### Interpretation 名词解释

#### Color Notation 颜色注记

A color notation is used to present a RGB color, and in Aegisub, it should be written as `&H<6-digits_color_code>&`. For the 6-digit's code, it is a standard code to discribe any of the RGB color, which is widely used in web, Photoshop and etc. It is in a format of `RRGGBB` which has **a hexical number used for a 8-bit color discription**.

In most case, color notation is capital insensitive, which means `FFACDB`and`ffacdb`are actually the same.

> Note: Though unstandard color code still work, such as `&HFF0000&`(Red) could be written as `&FF0000&`,`FF0000`,`Hff`and even`ff`. 
>
> A pattern for Aegisub's interpretor is that:
>
> - **Left-Association**
>
>   In another word, it will read from left to right, so left code share higher priority than the right. So that's why `FF` equals to `FF0000` instead of `0000FF`. It's the same for inline key words and override tags.
>
> - **1-Parameter Inclusity**
>
>   Although it's hard for those programming freshman to comprehend, it's neccessary to tell somthing about [parameter](#Parameter) so that it will be easier for amateurs to remember those **format**. The law is that every tag has only one parameter, or parameter tuple(list). So for those tags that need multi-variables, we need a `()` to make them together as a tuple, otherwise without it.

#### Library 库

#### Fx Scope 效果作用域

#### Parameter 参数

#### Notation 注记形式


## Elements 元素

### Size 大小

#### Font Size 字体大小

| Code               | \fs<font_size>                                               |
| ------------------ | ------------------------------------------------------------ |
| Discription        | Inline modifier of font's dot size.                          |
| Fx Scope           | Syn                                                          |
| Library Affiliated | VSFilter                                                     |
| Note               | The dot size contributes to the frame size. For instance, a font in size of 80 in 1080P video script could be as large as the one in size of 60 whose script is in 720P size. Besides, the size is limited which means it could not be extremely large. |

#### Element Size 元素大小

- code: `\fsc<size(%)>`

### Color

If you forget about `color_notation`, you can return to paragraph [Color Notation](#Color Notation) before read.

#### Simple Color 单色

- code: `\<scope>c<color_notation>`
- discription:
- note:

#### Various Color 渐变色

- code: `\<scope>vc(LT,RT,LB,LT)`
- discription:
- note:

### Font Style 字体样式

#### Border Width 描边宽度

- code: `\bord<width>`

#### Shadow Distance 阴影距离

- code: `\shad<distance>`

#### Blur Edge 模糊边缘
##### Simple Blur 简单模糊
- code: `\b`
##### Gaussian Blur 高斯模糊
- code: `\be`

#### Spacing 字符间距

-code: ``

#### Font Family 字体

-code: `\fn<font-family name>`

## Shape(AssDraw) 形状(绘图)

### Draw Activation 开启绘图
- code: `\p<0/1>`
### ASSDraw Code 绘图代码



## Attribute 属性

### Alpha 不透明度

### Line Alignment 对齐方式
- code: `\an<align>`
### Rotation 旋转
#### Common Rotation (Z-axis Rotation) 平面旋转(Z轴旋转)
- code: `\frz<angle>`

#### X-axis Rotation (Fake 3D) X轴旋转(伪3D)
- code: `\frx<angle>`

#### Y-axis Rotation (Fake 3D) Y轴旋转(伪3D)
- code: `\fry<angle>`

### Mask 遮罩

#### Clip 矩形遮罩

#### Bezier Clip 贝塞尔遮罩

### Position 位置

### Style Reset 重置样式

## Motion 动画

### Keyframe Animation 关键帧动画

### Fade(Fade-in&out) 渐变(淡入淡出)

#### Simple Fade 简单渐变
- code: `\fad(intime_range,outtime_range)`

#### Complex Fade 复杂渐变
- code: `\fade(alpha_at_first, alpha_in_the_middle, alpha_before_end, timestamp_at_the_tail_of_*first*,time_at_the_head_of_the_*middle*,time_at_the_tail_of_the_*middle*,time_at_the_head_of_*end*)`
### Movement 移动

## Karaoke 卡拉OK

### Key Time

### Key with Fade

### Conclusion