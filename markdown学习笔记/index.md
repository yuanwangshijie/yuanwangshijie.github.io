# MarkDown学习笔记


## 一、标题

```
# 一级标题
## 二级标题
### 三级标题
#### 四级标题
##### 五级标题
###### 六级标题
```

> ## 二级标题
>
> ### 三级标题
>
> #### 四级标题
>
> ##### 五级标题
>
> ###### 六级标题

## 二、字体

```
*斜体文本*
_斜体文本_
**粗体文本**
__粗体文本__
***粗斜体文本***
___粗斜体文本___
```

*斜体文本*

_斜体文本_

**粗体文本**

__粗体文本__

***粗斜体文本***

___粗斜体文本___

## 三、分割线

```
***
* * *
*****
- - -
----------
```

---

---

---

---

---

## 四、删除线

```
~~BAIDU.COM~~
```

~~BAIDU.COM~~

## 五、脚注

```
创建脚注格式类似这样 [^RUNOOB]。

[^RUNOOB]: 菜鸟教程 -- 学的不仅是技术，更是梦想！！！
```

创建脚注格式类似这样 [^RUNOOB]。

## 六、列表

### 1.无序列表

```
* 第一项
* 第二项
+ 第一项
+ 第二项
- 第一项
- 第二项
```

* 第一项
* 第二项

+ 第一项
+ 第二项

- 第一项
- 第二项

### 2.有序列表

```
1. 第一项
2. 第二项
```

1. 第一项
2. 第二项

### 3.列表嵌套

```
1. 第一项：
    - 第一项嵌套的第一个元素
    - 第一项嵌套的第二个元素
2. 第二项：
    - 第二项嵌套的第一个元素
    - 第二项嵌套的第二个元素
```

1. 第一项：
   - 第一项嵌套的第一个元素
   - 第一项嵌套的第二个元素
2. 第二项：
   - 第二项嵌套的第一个元素
   - 第二项嵌套的第二个元素

## 七、区块

```
> 最外层
> > 第一层嵌套
> > > 第二层嵌套
```

> 最外层
>
>> 第一层嵌套
>>
>>> 第二层嵌套
>>>
>>

### 1.区块中使用列表

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
> 1. 第一项
> 2. 第二项
>
> + 第一项
> + 第二项

### 2.列表中使用区块

```
* 第一项
    > 菜鸟教程
    > 学的不仅是技术更是梦想
* 第二项
```

* 第一项

  > 菜鸟教程
  > 学的不仅是技术更是梦想
  >
* 第二项

## 八、代码块

```
`printf()` 函数
```

`printf()` 函数

````javascript
```javascript
$(document).ready(function () {
    alert('RUNOOB');
});
```
````

```javascript
$(document).ready(function () {
    alert('RUNOOB');
});
```

## 九、链接

```
这是一个链接 [菜鸟教程](https://www.runoob.com)
```

这是一个链接 [菜鸟教程](https://www.runoob.com)

### 1.高级链接

```
这个链接用 1 作为网址变量 [Google][1]
这个链接用 runoob 作为网址变量 [Runoob][runoob]

[1]: http://www.google.com/
[runoob]: http://www.runoob.com/
```

这个链接用 1 作为网址变量 [Google][1]

这个链接用 runoob 作为网址变量 [Runoob]

## 十、图片

```
![alt 属性文本](图片地址)

![alt 属性文本](图片地址 "可选标题")

![RUNOOB 图标](http://static.runoob.com/images/runoob-logo.png)

![RUNOOB 图标](http://static.runoob.com/images/runoob-logo.png "RUNOOB")
```

![RUNOOB 图标](http://static.runoob.com/images/runoob-logo.png)

![RUNOOB 图标](http://static.runoob.com/images/runoob-logo.png "RUNOOB")

```
这个链接用 1 作为网址变量 [RUNOOB][1].
然后在文档的结尾为变量赋值（网址）

[1]: http://static.runoob.com/images/runoob-logo.png
```

这个链接用 1 作为网址变量 [RUNOOB][1].
然后在文档的结尾为变量赋值（网址）

```
<img src="http://static.runoob.com/images/runoob-logo.png" width="50%">
```

<img src="http://static.runoob.com/images/runoob-logo.png" width="50%">

## 十一、表格

```
|  表头   |  表头  |
|  ----  | ----  |
| 单元格  | 单元格 |
| 单元格  | 单元格 |
```


| 表头   | 表头   |
| ------ | ------ |
| 单元格 | 单元格 |
| 单元格 | 单元格 |

```
| 左对齐 | 右对齐 | 居中对齐 |
| :-----| ----: | :----: |
| 单元格 | 单元格 | 单元格 |
| 单元格 | 单元格 | 单元格 |
```


| 左对齐列 | 右对齐列 | 居中对齐 |
| :------- | -------: | :------: |
| 单元格   |   单元格 |  单元格  |
| 单元格   |   单元格 |  单元格  |

## 十二、高级技巧

### 1.支持的 HTML 元素

```
使用 <kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>Del</kbd> 重启电脑
```

使用 <kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>Del</kbd> 重启电脑

### 2.转义

```
**文本加粗** 
\*\*正常显示星号\*\*
```

**文本加粗**

\*\*正常显示星号\*\*

[1]: http://www.google.com/
[runoob]: http://www.runoob.com/
[1]: http://static.runoob.com/images/runoob-logo.png
[^RUNOOB]: 菜鸟教程 -- 学的不仅是技术，更是梦想！！！

