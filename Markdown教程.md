## 一、Markdown与Typora介绍

### 1.1 Markdown介绍

> Markdown 是一种轻量级标记语言，它允许人们使用易读易写的纯文本格式编写文档。       
> Markdown 语言在 2004 由约翰·格鲁伯（英语：John Gruber）创建。  
> Markdown 编写的文档可以导出 HTML 、Word、图像、PDF、Epub 等多种格式的文档。  
> Markdown 编写的文档后缀为 **.md**, **.markdown**。

### 1.2 Typora介绍与下载

Typora编辑器让人们能更简单地用Markdown语言书写文字，解决了使用传统的Markdown编辑器写文的痛点，并且界面简洁优美，实现了实时预览等功能。

Typora官网： https://typora.io/  
windos版本下载地址：https://typora.io/#windows   

### 1.3Markdown应用

Markdown 能被使用来撰写电子书，如：Gitbook。

当前许多网站都广泛使用 Markdown 来撰写帮助文档或是用于论坛上发表消息。例如：GitHub、简书、reddit、Diaspora、Stack Exchange、OpenStreetMap 、SourceForge等。

## 二、Markdown语法

### 2.1标题

Markdown 标题有两种格式。  
1）使用 = 和- 标记一级和二级标题

```
我展示的是一级标题
=================

我展示的是二级标题
-----------------
```

2）使用 # 号标记

```html
# 一级标题
## 二级标题
### 三级标题
#### 四级标题
##### 五级标题
###### 六级标题
```

### 2.2段落格式

- **空格**
  在输入连续的空格后，Typora 会在编辑器视图里保留空格，但当你打印或导出时，这些空格会被省略成一个。你可以在源代码模式下，为每个空格前加一个转义符，或者直接使用 HTML 风格的来保持连续的空格。

- **软换行**
  采用shift+enter来完成软换行，只在编辑界面可见，导出时换行被省略。
  比如Jekyll 使用 kramdown 作为默认 Markdown 解释器。kramdown 可以通过 ALDs来设置块级元素或行内元素的属性，使用软换行才能显示属性效果。

- **硬换行**
  使用space+space+shift+enter完成，硬换行在文档被导出时保留，且没有换段的段后距

- **换段**
  直接enter

  

- **字体**

  ```
  *斜体文本*
  _斜体文本_
  **粗体文本**
  __粗体文本__
  ***粗斜体文本***
  ___粗斜体文本___
  ```

- **分隔线**

  你可以在一行中用三个以上的星号、减号、底线来建立一个分隔线，行内不能有其他东西。你也可以在星号或是减号中间插入空格。下面每种写法都可以建立分隔线：

  ```
  ***
  
  * * *
  
  *****
  
  - - -
  
  ----------
  ```

  显示效果如下所示

  ![](https://www.runoob.com/wp-content/uploads/2019/03/3F46EAA9-DADE-48FD-99AA-DF7BEBFAA4FA.jpg)

- **删除线**

  如果段落上的文字要添加删除线，只需要在文字的两端加上两个波浪线 **~~** 即可，实例如下：

  ```
  ~~bilibili.COM~~
  ```

         ~~bilibili.com~~

  

- 下划线

  下划线可以通过HTML的标签来实现

  ```
  <u>带下划线的文本</u>
  ```

  <u>带下划线的文本</u>



- 脚注

  ```
  [^要注明的文本]
  ```

  以下实例演示了脚注的用法：

  ```
  创建脚注格式类似这样 [^hello world]。
  
  [^hello world]: 你好 世界！
  ```

  创建脚注格式类似这样 [^hello world]。

  [^hello world]: 你好 世界！

  

### 2.3列表

Markdown 支持有序列表和无序列表。

无序列表使用星号(*****)、加号(**+**)或是减号(**-**)作为列表标记，这些标记后面要添加一个空格，然后再填写内容：

```
* 第一项
* 第二项
* 第三项

+ 第一项
+ 第二项
+ 第三项


- 第一项
- 第二项
- 第三项
```

> * 第一项
>   + 第二项
>     - 第三项



有序列表使用数字并加上 **.** 号来表示，如：

```
1. 第一项
2. 第二项
3. 第三项
```

> 1. 第一项
> 2. 第二项
> 3. 第三项



列表嵌套  
列表嵌套只需在子列表的选项前面添加四个空格即可：

```
1. 第一项：
    - 第一项嵌套的第一个元素
    - 第一项嵌套的第二个元素
2. 第二项：
    - 第二项嵌套的第一个元素
    - 第二项嵌套的第二个元素
```

> 1.第一项
>
>    - 第一项嵌套的第一个元素
>         - 第一项嵌套的第一个元素嵌套中再嵌套的第一个元素
>
> 2.第二项
>
>    - 第二项嵌套的第一个元素
>          + 第二项嵌套的第一个元素嵌套中再嵌套的第一个元素



### 2.4区块

Markdown 区块引用是在段落开头使用 **>** 符号 ，然后后面紧跟一个**空格**符号：

```
> 区块引用
> hello world！
> 你好，世界！
```

> 区块应用
>
> hello world！
>
> 你好，世界！



另外区块是可以嵌套的，一个 **>** 符号是最外层，两个 **>** 符号是第一层嵌套，以此类推：

```
> 最外层
> > 第一层嵌套
> > > 第二层嵌套
```

> 最外层
>
> > 第一层
> >
> > > 第二层嵌套



区块中使用列表  

```
> 区块中使用列表
> 1. 第一项
> 2. 第二项
> + 第一项
> + 第二项
> + 第三项
```

> 区块中使用列表
>
> 1.第一项
>
> 2.第二项
>
> + 第一项
> + 第二项



列表中的区块  如果要在列表项目内放进区块，那么就需要在 **>** 前添加四个空格的缩进。

```
* 第一项
    > 菜鸟教程
    > 学的不仅是技术更是梦想
* 第二项
```

* 第一项

  > hello world!
  >
  > 你好，世界！

* 第二项

  

### 2.5代码

如果是段落上的一个函数或片段的代码可以用反引号把它包起来（**`**）  **~**键就是反引号

```
`println()` 函数
```

`println`函数



代码区块使用 **4 个空格**或者一个**制表符（Tab 键）**。

![](https://www.runoob.com/wp-content/uploads/2019/03/55EDFE05-5F27-458E-AFE0-7B96685C9603.jpg)

```java
public class helloworld {
    public static void main(String[] args) {
        System.out.println("hello world");
    }
}

```

也可以用 **```** 包裹一段代码，并指定一种语言（也可以不指定）：

```
​```javascript
$(document).ready(function () {
    alert('RUNOOB');
});
​```
```

```javascript
$(document).ready(function () {
    alert('RUNOOB');
});
```



### 2.6链接

链接使用方法

```
[链接名称](链接地址)

或者

<链接地址>
```

```
这是一个链接 [bilibili](https://bilibili.com/)
```

这是一个链接 [bilibili](https://search.bilibili.com/)

```
<https://bilibili.com/>
```

<https://bilibili.com/>



高级链接  
我们可以通过变量来设置一个链接，变量赋值在文档末尾进行：

```
这个链接用 1 作为网址变量 [Google][1]
这个链接用 bilibili 作为网址变量 [Bilibili][bilibili]
然后在文档的结尾为变量赋值（网址）

  [1]: http://www.google.com/
  [bilibili]: https://bilibili.com/
```

这个链接用 1 作为网址变量 [Google][1]
这个链接用 bilibili 作为网址变量 [Bilibili][bilibili]
然后在文档的结尾为变量赋值（网址）

[1]: http://www.google.com/
[bilibili]: https://bilibili.com/



### 2.7图片

Markdown 图片语法格式  

```
![alt 属性文本](图片地址)

![alt 属性文本](图片地址 "可选标题")
```

- 开头一个感叹号 !
- 接着一个方括号，里面放上图片的替代文字
- 接着一个普通括号，里面放上图片的网址，最后还可以用引号包住并加上选择性的 'title' 属性的文字。

使用实例：

```
![RUNOOB 图标](http://static.runoob.com/images/runoob-logo.png)

![RUNOOB 图标](http://static.runoob.com/images/runoob-logo.png "RUNOOB")
```

![RUNOOB 图标](http://static.runoob.com/images/runoob-logo.png)

![RUNOOB 图标](http://static.runoob.com/images/runoob-logo.png "RUNOOB")

也可以像网址那样对图片网址使用变量:

```
这个链接用 1 作为网址变量 [RUNOOB][1].
然后在文档的结尾为变量赋值（网址）

[1]: http://static.runoob.com/images/runoob-logo.png
```

这个链接用 1 作为网址变量 [RUNOOB][1].
然后在文档的结尾为变量赋值（网址）

[1]: http://static.runoob.com/images/runoob-logo.png

Markdown 还没有办法指定图片的高度与宽度，还可以使用普通的 <img> 标签。

```
<img src="http://static.runoob.com/images/runoob-logo.png" width="50%">
```

<img src="http://static.runoob.com/images/runoob-logo.png" width="50%">

### 2.8表格

制作表格使用 **|** 来分隔不同的单元格，使用 **-** 来分隔表头和其他行。  
语法格式如下：

```
|  表头   | 表头  |
|  ----  | ----  |
| 单元格  | 单元格 |
| 单元格  | 单元格 |
```

| 表头   | 表头   |
| ------ | ------ |
| 单元格 | 单元格 |
| 单元格 | 单元格 |



**设置表格的对齐方式：**

- **-:** 设置内容和标题栏居右对齐。
- **:-** 设置内容和标题栏居左对齐。
- **:-:** 设置内容和标题栏居中对齐。

实例如下：

```
| 左对齐 | 右对齐 | 居中对齐 |
| :-----| ----: | :----: |
| 单元格 | 单元格 | 单元格 |
| 单元格 | 单元格 | 单元格 |
```

| 左对齐 | 右对齐 | 居中对齐 |
| :----- | -----: | :------: |
| 单元格 | 单元格 |  单元格  |
| 单元格 | 单元格 |  单元格  |



## 三、高级技巧



### 3.1支持HTML元素

不在 Markdown 涵盖范围之内的标签，都可以直接在文档里面用 HTML 撰写。

目前支持的 HTML 元素有：`<kbd> <b> <i> <em> <sup> <sub> <br>`等 ，如：

```
使用 <kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>Del</kbd> 重启电脑
```

使用 <kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>Del</kbd> 重启电脑



### 3.2让字体变颜色

```
<font color=red size=10>yes</font>  #yes代表你想改变颜色的字体，10代表字体大小，red是字体的颜色，也可以设置成blue或者其他颜色#
```

<font color=red size=10>yes</font>  *#yes代表你想改变颜色的字体，10代表字体大小，red是字体的颜色，也可以设置成blue或者其他颜色#*
