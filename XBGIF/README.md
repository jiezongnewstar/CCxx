### 使用 android 系统原生库加载 gif

1. 了解 GIF 文件格式

2. 了解 LZW 算法

3. 使用 libgif 库实现 gif 文件播放

- 参考 [What's In A GIF](http://giflib.sourceforge.net/whatsinagif/bits_and_bytes.html "gif是什么")

---

#### 思考 1，android 已有 gif 图片加载框架（如 glide），为什么我们还要去写原生 native 代码？

#### 思考 2，java 层代码如何实现加载 gif？

好了，这两个问题一起来回答，无论是第三方图片加载框架，亦或者是 java 层代码实现，
避不开的一个问题就是内存占用问题，也就是性能问题，如果 gif 过大，则会出现 OOM。

---

### GIF 数据结构

    gif最多支持8位，及256色，前6个字节通常为“47 49 46 38 39 61” 或者 “47 49 46 37 61”对应的ASCII码为“GIF89a”或者“GIF87a”，表示GIF头（签名（前三位）+版本（后三位））

   ![Image gifdata](https://github.com/jiezongnewstar/CCxx/blob/master/XBGIF/gifdatasource.jpg)

   上图表示的是头部后面的位数各自表示的部分，包括宽度、高度等等，对应的文档在上面的参考部分已经讲的很详细，如果有兴趣的可以进行研究（属实我是没什么兴趣去研究，会用就好了）。

    我后悔了，列出这个标题，这部分不要去看我写的了，我想直接撸码，这种东西写好工具类就好了。。。Sorry，i am not a good writer.