# 一文让你理解NumPy中的Broadcasting广播机制

# 前言

在吴恩达老师的深度学习专项课程中，老师有提到NumPy中的广播机制，同时那一周的测验也有涉及到广播机制的题目。那么，到底什么是NumPy中的广播机制？

# 官方文档

接下来到了看官方文档的时间。

[Array Broadcasting in Numpy](https://numpy.org/devdocs/user/theory.broadcasting.html)

## 广播机制概述

让我们探索numpy中一个更高级的概念，这个概念被称为广播。 广播展现了NumPy在算术运算期间是如何处理具有不同形状的数组的。 受到某些约束，较小的阵列将在较大的阵列上“广播”，以使它们具有兼容的x相同形状。 广播提供了一种数组矢量化操作，从而使得循环在C而不是Python中发生。 它无需复制不必要的数据即可完成，并且通常算法的效率还挺高。 当然在某些情况下，广播并不是一个好办法，因为它会导致内存使用效率低，从而减慢计算速度。 本文通过示例，对广播进行了详尽的介绍。 它还提供何时使用广播的提示。 



numpy操作通常是逐个元素完成的，这就需要两个数组具有完全相同的形状

Example 1

```python
>>> from numpy import array
>>> a = array([1.0, 2.0, 3.0])
>>> b = array([2.0, 2.0, 2.0])
>>> a * b
array([ 2.,  4.,  6.])
```



当数组的形状满足某些条件时，numpy的广播规则将放宽这种数组限制。 **将数组和标量值在一起运算时，会出现最简单的广播示例**： 

Example 2

```python
>>> from numpy import array
>>> a = array([1.0,2.0,3.0])
>>> b = 2.0
>>> a * b
array([ 2.,  4.,  6.])
```

尽管只有一个变量是数组，但是结果和之前的一个代码例子是一样的。 我们可以认为其中的标量在算术运算中被拓展成与数组`a`变量形状相同的数组。 例如下图中显示的中拓展的新元素只是原始标量的副本。这种拓展只是概念上的。 **numpy的明智之处在于使用原始标量值而不必要创建副本，从而使广播操作尽可能地节省内存提高计算效率**。 由于上面的代码例子中，乘法过程中标量移动的内存较少，所以在具有一百万个元素数组的Windows 2000上，广播机制与之前的两个数组相加相比大概快10%。 

![Vector-Scalar multiplication](https://numpy.org/devdocs/_images/theory.broadcast_1.gif)



在最简单的广播示例中，标量`b`被拉伸为与`a`相同形状的数组，使得这些形状适用于逐元素乘法。 

下面的规则决定了两个具有兼容形状的数组是否可以在单个代码段中进行广播。  

## 广播机制规则

广播规则 

**为了广播，操作中两个阵列的尾轴的大小必须相同，或者其中一个必须是一个。**

问题来了，尾轴是什么？

为此我找到了[python - numpy broadcasting - explanation of trailing axes - Stack Overflow](https://stackoverflow.com/questions/65435712/numpy-broadcasting-explanation-of-trailing-axes)这篇解答。

---



> If you have two arrays with different dimensions number, say one 1x2x3 and other 2x3, then you compare only the trailing common dimensions, in this case 2x3. But **if both your arrays are two-dimensional, then their corresponding sizes have to be either equal or one of them has to be 1**.
>
> In your case you have a 2x2 and 4x2 and 4 != 2 and neither 4 or 2 equals 1, so this doesn't work.

假设你有两个不同维度的数组。一个是1x2x3，另一个是2x3，那么只需要比较后面的公共尺寸，在这种情况下为2x3。 但是，**如果两个数组都是二维的，则它们的对应大小必须相等或其中之一必须为1 **。 

在两个二维数组中2x2和4x2，4！= 2，并且4或2都不等于1，所以广播行不通的。

这个解释应该比较清楚了。



----

如果不满足此条件，则会引发异常，提示数组的形状不兼容。 广播操作创建的结果数组的大小是两个数组中每个维度的最大大小。 请注意，该规则并未说明需要具有相同维数的两个数组。 如果有一个256 x 256 x 3的RGB值数组，想要按不同的值缩放图像中的每种颜色，则可以将图像乘以具有3个值的一维数组。

| Image  | (3d array) | 256 x | 256 x | 3    |
| ------ | ---------- | ----- | ----- | ---- |
| Scale  | (1d array) |       |       | 3    |
| Result | (3d array) | 256 x | 256 x | 3    |

在下面的示例中，两个数组都具有长度为1的轴，这些轴在广播操作中被扩展为更大的大小。 

| A      | (4d array) | 8 x  | 1 x  | 6 x  | 1    |
| ------ | ---------- | ---- | ---- | ---- | ---- |
| B      | (3d array) |      | 7 x  | 1 x  | 5    |
| Result | (4d array) | 8 x  | 7 x  | 6 x  | 5    |

下面，是几个代码例子和图形表示，有助于使广播规则直观明了。例3将一个一维数组添加到一个二维数组。

Example 3

```python
>>> from numpy import array
>>> a = array([[ 0.0,  0.0,  0.0],
...            [10.0, 10.0, 10.0],
...            [20.0, 20.0, 20.0],
...            [30.0, 30.0, 30.0]])
>>> b = array([1.0, 2.0, 3.0])
>>> a + b
array([[  1.,   2.,   3.],
       [ 11.,  12.,  13.],
       [ 21.,  22.,  23.],
       [ 31.,  32.,  33.]])
```

如下图2所示，b将拓展维度大小和`a`一样。在图3中，当`b`的列维度大于`a`的时，由于形状不兼容而引发异常。

![Matrix-Vector](https://numpy.org/devdocs/_images/theory.broadcast_2.gif)

*Figure 2*

如果一维数组元素的数量与二维数组列的数量匹配，则将二维数组乘以一维数组将导致广播。 

当数组的尾部不相等时，广播将失败，因为无法将第一个数组的行中的值与第二个数组的元素对齐进行逐元素加法。

![Matrix-Vector-with-error](https://numpy.org/devdocs/_images/theory.broadcast_3.gif)

*Figure 3*

广播提供了一种获取两个数组的外部乘积（或任何其他外部操作）的便捷方法。 下面的示例显示两个1维数组的外部加法运算，其结果与示例3相同。 

Example 4

```python
>>> from numpy import array, newaxis
>>> a = array([0.0, 10.0, 20.0, 30.0])
>>> b = array([1.0, 2.0, 3.0])
>>> a[:,newaxis] + b
array([[  1.,   2.,   3.],
       [ 11.,  12.,  13.],
       [ 21.,  22.,  23.],
       [ 31.,  32.,  33.]])
```

在这里，newaxis索引运算符将一个新轴插入，使其成为二维4x1数组。 图4说明了两个阵列的拉伸以产生所需的4x3输出阵列。 

在这里例子里是`b = array([1.0, 2.0, 3.0])`,但是下图中是`0,1,2`，emmmm.....尊重原文吧！

![vector-vector with newaxis](https://numpy.org/devdocs/_images/theory.broadcast_4.gif)

*Figure 4*.

在某些情况下，广播会拉伸两个阵列以形成一个比任何一个初始阵列都大的输出阵列。



# 总结

以上是对官方文档的翻译，总的来说广播机制主要是以下几点：

- 效率较快，性能较好
- 广播时，操作中两个数组的尾轴的大小必须相同，或者其中之一必须是1
- 如果两个数组都是二维的，则它们的对应大小必须相等或其中之一必须为1

通过这篇文章，你是否了解了NumPy的广播机制呢？如果了解了请点赞加关注，若有疑惑不解欢迎留言。每一个评论都会认真看的