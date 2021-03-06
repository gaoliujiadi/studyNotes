# Python-Numpy 学习

## 入门

**`import numpy as np`**

### NumPy的数组对象：ndarray

| 属性        | 说明                                         |
| ----------- | -------------------------------------------- |
| `.ndim`     | 秩，即轴的数量或维度的数量                   |
| `.shape`    | ndarray对象的尺度，对于juzhen，n行m列        |
| `.size`     | naarray对象元素的个数，相当于.shape中n*m的值 |
| `.dtype`    | ndarray对象的元素类型                        |
| `.itemsize` | ndarray对象中每个元素的大小，以字节为单位    |

#### ndarray的元素类型

| 数据类型     | 说明                                               |
| ------------ | -------------------------------------------------- |
| `bool`       | 布尔类型，True或False                              |
| `intc`       | 与C语言中int类型一致，一般是int32或int64           |
| `intp`       | 用于索引的整数，与C语言中ssize_t一致，int32或int64 |
| `int8`       | 字节长度的整数，取值：$[-128, 127]$                |
| `int16`      | 16位长度的整数，取值：$[-32768, 32767]$            |
| `int32`      | 32位长度的整数，取值：$[-2^{31}, 2^{31}-1]$        |
| `int64`      | 64位长度的整数，取值：$[-2^{63}, 2^{63}-1]$        |
| `uint8`      | 8位无符号整数，取值：$[0, 255]$                    |
| `uint16`     | 16位无符号整数，取值：$[0, 65535]$                 |
| `uint32`     | 32位无符号整数，取值：$[0, 2^{32}-1]$              |
| `uint64`     | 64位无符号整数，取值：$[0, 2^{64}-1]$              |
| `float16`    | 16位半精度浮数点：1位符号位，5位指数，10位尾数     |
| `float32`    | 32位半精度浮数点：1位符号位，8位指数，23位尾数     |
| `float64`    | 64位半精度浮数点：1位符号位，11位指数，52位尾数    |
| `complex64`  | 复数类型，实部和虚部都是32位浮数点                 |
| `complex128` | 复数类型，实部和虚部都是64位浮数点                 |

*实部(.real) + j虚部(.imag) *



### ndarray数组的创建

- 从python中列表、元组等类型创建ndarray数组

  `x = np.array(list/tuple)`

  `x = np.array(list/tuple, dtype=np.float32)`

  ```python
  In [2]: x = np.array([0, 1, 2, 3])
  
  In [3]: print(x)
  [0 1 2 3]
  
  In [4]: x = np.array([[1, 2], [9, 8], (0.1, 0.2)])
      
  In [5]: print(x)
  [[1.  2. ]
   [9.  8. ]
   [0.1 0.2]]
  ```

- 使用NumPy中函数创建ndarray数组，如：arange，ones，zeros等

  | 函数                   | 说明                                           |
  | ---------------------- | ---------------------------------------------- |
  | `np.arange(n)`         | 类似range()函数，返回ndarray类型，元素从0到n-1 |
  | `np.ones(shape)`       | 根据shape生成一个全1数组，shape是元组类型      |
  | `np.zeros(shape)`      | 根据shape生成一个全0数组，shape是元组类型      |
  | `np.full(shape, val)`  | 根据shape生成一个数组，每个元素值都是val       |
  | `np.eye(n)`            | 创建一个正方的n*n单位矩阵，对角线为1，其余为0  |
  | `np.ones_like(a)`      | 根据数组a的形状生成一个全1数组                 |
  | `np.zeros_like(a)`     | 根据数组a的形状生成一个全0数组                 |
  | `np.full_like(a, val)` | 根据数组a的形状生成一个数组，每个元素值都是val |

- 使用NumPy中其他函数创建ndarray数组

  | 函数               | 说明                                   |
  | ------------------ | -------------------------------------- |
  | `np.linspace()`    | 根据起止数据等间距地填充数据，形成数组 |
  | `np.concatenate()` | 将两个或多个数组合并成一个新的数组     |

  ```python
  In [8]: a = np.linspace(1, 10, 4)
  
  In [9]: a
  Out[9]: array([ 1.,  4.,  7., 10.])
  
  In [10]: b = np.linspace(1, 10, 4, endpoint=False)
  
  In [11]: b
  Out[11]: array([1.  , 3.25, 5.5 , 7.75])
  
  In [12]: c = np.concatenate((a, b))
  
  In [13]: c
  Out[13]: array([ 1.  ,  4.  ,  7.  , 10.  ,  1.  ,  3.25,  5.5 ,  7.75])
  ```
  
  

### ndarray数组的变换

#### 维度的变换

| 方法                  | 说明                                                |
| --------------------- | --------------------------------------------------- |
| `.reshape(shape)`     | 不改变数组元素，返回一个shape形状的数组，原数组不变 |
| `.resize(shape)`      | 与`.reshape()`功能一致，但修改原数组                |
| `.swapaxes(ax1, ax2)` | 将数组n个维度中两个维度进行调换                     |
| `.flatten()`          | 对数组进行降维，返回折叠后的一维数据，原数组 不变   |

```python
In [17]: a = np.ones((2, 3, 4), dtype=np.int32)

In [18]: a
Out[18]:
array([[[1, 1, 1, 1],
        [1, 1, 1, 1],
        [1, 1, 1, 1]],

       [[1, 1, 1, 1],
        [1, 1, 1, 1],
        [1, 1, 1, 1]]])

In [19]: a.reshape((3, 8))
Out[19]:
array([[1, 1, 1, 1, 1, 1, 1, 1],
       [1, 1, 1, 1, 1, 1, 1, 1],
       [1, 1, 1, 1, 1, 1, 1, 1]])

In [20]: a
Out[20]:
array([[[1, 1, 1, 1],
        [1, 1, 1, 1],
        [1, 1, 1, 1]],

       [[1, 1, 1, 1],
        [1, 1, 1, 1],
        [1, 1, 1, 1]]])

In [21]: a.resize((3, 8))

In [22]: a
Out[22]:
array([[1, 1, 1, 1, 1, 1, 1, 1],
       [1, 1, 1, 1, 1, 1, 1, 1],
       [1, 1, 1, 1, 1, 1, 1, 1]])
In [23]: a = np.ones((2, 3, 4), dtype=np.int32)

In [24]: a.flatten()
Out[24]:
array([1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1,
       1, 1])

In [25]: a
Out[25]:
array([[[1, 1, 1, 1],
        [1, 1, 1, 1],
        [1, 1, 1, 1]],

       [[1, 1, 1, 1],
        [1, 1, 1, 1],
        [1, 1, 1, 1]]])

In [26]: b = a.flatten()

In [27]: b
Out[27]:
array([1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1,
       1, 1])
```

#### 类型变换

- `new_a = a.astype(new_type)`

  ```python
  In [32]: a = np.ones((2, 3, 4), dtype=np.int)
  
  In [33]: a
  Out[33]:
  array([[[1, 1, 1, 1],
          [1, 1, 1, 1],
          [1, 1, 1, 1]],
  
         [[1, 1, 1, 1],
          [1, 1, 1, 1],
          [1, 1, 1, 1]]])
  
  In [34]: b = a.astype(np.float)
  
  In [35]: b
  Out[35]:
  array([[[1., 1., 1., 1.],
          [1., 1., 1., 1.],
          [1., 1., 1., 1.]],
  
         [[1., 1., 1., 1.],
          [1., 1., 1., 1.],
          [1., 1., 1., 1.]]])
  ```

  `astype()`方法一定会创建新的数组（原始数据的拷贝），即使两个类型一致

- ndarray数组向列表的转换

  `ls = a.tolist()`

  ```python
  In [37]: a = np.full((2, 3, 4), 25, dtype=np.int32)
  
  In [38]: a
  Out[38]:
  array([[[25, 25, 25, 25],
          [25, 25, 25, 25],
          [25, 25, 25, 25]],
  
         [[25, 25, 25, 25],
          [25, 25, 25, 25],
          [25, 25, 25, 25]]])
  
  In [39]: a.tolist()
  Out[39]:
  [[[25, 25, 25, 25], [25, 25, 25, 25], [25, 25, 25, 25]],
   [[25, 25, 25, 25], [25, 25, 25, 25], [25, 25, 25, 25]]]
  ```

### ndarray数组的操作

#### 数组的索引

索引：获取数组中特定位置元素的过程

- 一维数组的索引和切片：与Python的列表类似

  ```python
  In [40]: a = np.array([9, 8, 7, 6, 5])
  
  In [41]: a[2]
  Out[41]: 7
  
  In [42]: a[1:4:2]#起始编号:终止编号（不含）:步长
  Out[42]: array([8, 6])
  ```

- 多维数组的索引

  ```python
  In [43]: a = np.arange(24).reshape((2,3,4))
  
  In [44]: a
  Out[44]:
  array([[[ 0,  1,  2,  3],
          [ 4,  5,  6,  7],
          [ 8,  9, 10, 11]],
  
         [[12, 13, 14, 15],
          [16, 17, 18, 19],
          [20, 21, 22, 23]]])
  
  In [45]: a[1,2,3]
  Out[45]: 23
  
  In [46]: a[0,1,2]
  Out[46]: 6
  
  In [47]: a[-1,-2,-3]#编号0开始从左递增，或-1开始从右递减
  Out[47]: 17
  ```

#### 数组的切片

```python
In [48]: a = np.arange(24).reshape((2,3,4))

In [49]: a
Out[49]:
array([[[ 0,  1,  2,  3],
        [ 4,  5,  6,  7],
        [ 8,  9, 10, 11]],

       [[12, 13, 14, 15],
        [16, 17, 18, 19],
        [20, 21, 22, 23]]])

In [50]: a[:,1,-3]#第一个维度覆盖，第二个维度1，第三个维度-3
Out[50]: array([ 5, 17])

In [51]: a[:, 1:3,:]#每个维度切片方法与一维数组相同
Out[51]:
array([[[ 4,  5,  6,  7],
        [ 8,  9, 10, 11]],

       [[16, 17, 18, 19],
        [20, 21, 22, 23]]])

In [52]: a[:, :, ::2]#每个维度可以使用步长跳跃切片
Out[52]:
array([[[ 0,  2],
        [ 4,  6],
        [ 8, 10]],

       [[12, 14],
        [16, 18],
        [20, 22]]])
```

![numpy数组切片工作原理](https://www.numpy.org.cn/static/images/article/numpy_2D_slicing_diagram-1.jpg)

### ndarray数组的运算

#### 数组与标量间运算

*作用于数组每个元素*

```python
In [53]: a = np.arange(24).reshape((2,3,4))

In [54]: a
Out[54]:
array([[[ 0,  1,  2,  3],
        [ 4,  5,  6,  7],
        [ 8,  9, 10, 11]],

       [[12, 13, 14, 15],
        [16, 17, 18, 19],
        [20, 21, 22, 23]]])

In [55]: a.mean()#计算a与元素平均值的商
Out[55]: 11.5

In [56]: a = a / a.mean()

In [57]: a
Out[57]:
array([[[0.        , 0.08695652, 0.17391304, 0.26086957],
        [0.34782609, 0.43478261, 0.52173913, 0.60869565],
        [0.69565217, 0.7826087 , 0.86956522, 0.95652174]],

       [[1.04347826, 1.13043478, 1.2173913 , 1.30434783],
        [1.39130435, 1.47826087, 1.56521739, 1.65217391],
        [1.73913043, 1.82608696, 1.91304348, 2.        ]]])
```

#### NumPy一元函数

*对ndarray中的数据执行元素级运算的函数*

| 函数                                                         | 说明                                               |
| ------------------------------------------------------------ | -------------------------------------------------- |
| `np.abs(x)` `np.fabs(x)`                                     | 计算数组各元素值的绝对值                           |
| `np.sqrt(x)`                                                 | 计算数组各元素值的平方根                           |
| `np.square(x)`                                               | 计算数组各元素值的平方                             |
| `np.log(x)` `np.log10(x)` `np.log2(x)`                       | 计算数组各元素值的自然对数、10底对数和2底对数      |
| `np.ceil(x)` `np.floor(x)`                                   | 计算数组各元素值的ceiling值 或 floor值             |
| `np.rint(x)`                                                 | 计算数组各元素值的四舍五入值                       |
| `np.modf(x)`                                                 | 将数组各元素的小数和整数部分以两个独立数组形式返回 |
| `np.cos(x)` `np.cosh(x)` `np.sin(x)` `np.sinh(x)` `np.tan(x)` `np.tanh(x)` | 计算数组各元素值的普通型和双曲型三角函数           |
| `np.exp(x)`                                                  | 计算数组各元素值的指数值                           |
| `np.sign(x)`                                                 | 计算数组各元素值的符号值，`1(+), 0, -1(-)`         |

```python
In [58]: a = np.arange(24).reshape((2,3,4))

In [59]: np.square(a)#数组未被真实改变
Out[59]:
array([[[  0,   1,   4,   9],
        [ 16,  25,  36,  49],
        [ 64,  81, 100, 121]],

       [[144, 169, 196, 225],
        [256, 289, 324, 361],
        [400, 441, 484, 529]]], dtype=int32)

In [60]: a = np.sqrt(a)

In [61]: a
Out[61]:
array([[[0.        , 1.        , 1.41421356, 1.73205081],
        [2.        , 2.23606798, 2.44948974, 2.64575131],
        [2.82842712, 3.        , 3.16227766, 3.31662479]],

       [[3.46410162, 3.60555128, 3.74165739, 3.87298335],
        [4.        , 4.12310563, 4.24264069, 4.35889894],
        [4.47213595, 4.58257569, 4.69041576, 4.79583152]]])

In [62]: np.modf(a)
Out[62]:
(array([[[0.        , 0.        , 0.41421356, 0.73205081],
         [0.        , 0.23606798, 0.44948974, 0.64575131],
         [0.82842712, 0.        , 0.16227766, 0.31662479]],

        [[0.46410162, 0.60555128, 0.74165739, 0.87298335],
         [0.        , 0.12310563, 0.24264069, 0.35889894],
         [0.47213595, 0.58257569, 0.69041576, 0.79583152]]]),
 array([[[0., 1., 1., 1.],
         [2., 2., 2., 2.],
         [2., 3., 3., 3.]],

        [[3., 3., 3., 3.],
         [4., 4., 4., 4.],
         [4., 4., 4., 4.]]]))
```

#### NumPy二元函数

| 函数                                                         | 说明                                       |
| ------------------------------------------------------------ | ------------------------------------------ |
| `+` `-` `*` `/` `**`                                         | 两个数组各元素进行对应运算                 |
| `np.maximum(x, y)` `np.fmax()`<br> `np.minimum(x, y)` `np.fmin()` | 元素级的最大值/最小值计算                  |
| `np.mod(x, y)`                                               | 元素级的模运算                             |
| `np.copysign(x, y)`                                          | 将数组y中各元素值的符号赋值给数组x对应元素 |
| `>` `<` `>=` `<=` `==` `!=`                                  | 算术比较，产生布尔型数组                   |

```python
In [63]: a = np.arange(24).reshape((2,3,4))

In [64]: b = np.sqrt(a)

In [65]: a
Out[65]:
array([[[ 0,  1,  2,  3],
        [ 4,  5,  6,  7],
        [ 8,  9, 10, 11]],

       [[12, 13, 14, 15],
        [16, 17, 18, 19],
        [20, 21, 22, 23]]])

In [66]: b
Out[66]:
array([[[0.        , 1.        , 1.41421356, 1.73205081],
        [2.        , 2.23606798, 2.44948974, 2.64575131],
        [2.82842712, 3.        , 3.16227766, 3.31662479]],

       [[3.46410162, 3.60555128, 3.74165739, 3.87298335],
        [4.        , 4.12310563, 4.24264069, 4.35889894],
        [4.47213595, 4.58257569, 4.69041576, 4.79583152]]])

In [67]: np.maximum(a, b)
Out[67]:
array([[[ 0.,  1.,  2.,  3.],
        [ 4.,  5.,  6.,  7.],
        [ 8.,  9., 10., 11.]],

       [[12., 13., 14., 15.],
        [16., 17., 18., 19.],
        [20., 21., 22., 23.]]])#运算结果为浮数点

In [68]: a > b
Out[68]:
array([[[False, False,  True,  True],
        [ True,  True,  True,  True],
        [ True,  True,  True,  True]],

       [[ True,  True,  True,  True],
        [ True,  True,  True,  True],
        [ True,  True,  True,  True]]])
```

## 数据存储

### CSV文件存取

**`np.savetxt(frame, array, fmt='%.18e', delimiter=None)`**

- `freame`：文件、字符串或产生器，可以是.gz或.bz2的压缩文件
- `array`：存入文件的数组
- `fmt`：写入文件的格式，例如：`%d %.2f %.18e`
- `delimiter`：分割字符串，默认是任何空格

```python
In [2]: a = np.arange(100).reshape(5, 20)

In [3]: np.savetxt('a.csv', a, fmt='%.1f', delimiter=',')
```

**`np.loadtxt(frame, dtype=np.float, delimiter=None,  unpack=False`**

- `frame`：文件、字符串或产生器，可以是.gz或.bz2的压缩文件
- `dtype`：数据类型，可选
- `delimiter`：分割字符串，默认是任何空格
- `unpack`：如果`True`，读入属性将分别写入不同变量

```python
In [4]: b = np.loadtxt('a.csv', delimiter=',')

In [5]: b
Out[5]:
array([[ 0.,  1.,  2.,  3.,  4.,  5.,  6.,  7.,  8.,  9., 10., 11., 12.,
        13., 14., 15., 16., 17., 18., 19.],
       [20., 21., 22., 23., 24., 25., 26., 27., 28., 29., 30., 31., 32.,
        33., 34., 35., 36., 37., 38., 39.],
       [40., 41., 42., 43., 44., 45., 46., 47., 48., 49., 50., 51., 52.,
        53., 54., 55., 56., 57., 58., 59.],
       [60., 61., 62., 63., 64., 65., 66., 67., 68., 69., 70., 71., 72.,
        73., 74., 75., 76., 77., 78., 79.],
       [80., 81., 82., 83., 84., 85., 86., 87., 88., 89., 90., 91., 92.,
        93., 94., 95., 96., 97., 98., 99.]])

In [6]: b = np.loadtxt('a.csv', dtype=np.int, delimiter=',')

In [7]: b
Out[7]:
array([[ 0,  1,  2,  3,  4,  5,  6,  7,  8,  9, 10, 11, 12, 13, 14, 15,
        16, 17, 18, 19],
       [20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33, 34, 35,
        36, 37, 38, 39],
       [40, 41, 42, 43, 44, 45, 46, 47, 48, 49, 50, 51, 52, 53, 54, 55,
        56, 57, 58, 59],
       [60, 61, 62, 63, 64, 65, 66, 67, 68, 69, 70, 71, 72, 73, 74, 75,
        76, 77, 78, 79],
       [80, 81, 82, 83, 84, 85, 86, 87, 88, 89, 90, 91, 92, 93, 94, 95,
        96, 97, 98, 99]])
```

*局限性：只能有效存储一维和二维数组* 

### 多维数据的存取

**`a.tofile(frame, sep='', format'%s'`**

- `frame`文件、字符串
- `sep`数据分割字符串，如果是空串，写入文件为二进制
- `format`：写入数据的格式

```python
In [8]: a = np.arange(100).reshape(5, 10, 2)

In [9]: a.tofile('b.dat', sep=',', format='%d')
```

**`np.fromfile(frame, dtype=float, count=-1, sep=''`**`**

- `frame`文件、字符串
- `dtpye`：读取的数据类型
- `count`：读入元素个数，-1表示读入整个文件
- `sep`数据分割字符串，如果是空串，写入文件为二进制

```python
In [13]: c = np.fromfile('b.dat', dtype=np.int, sep=',')

In [14]: c
Out[14]:
array([ 0,  1,  2,  3,  4,  5,  6,  7,  8,  9, 10, 11, 12, 13, 14, 15, 16,
       17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33,
       34, 35, 36, 37, 38, 39, 40, 41, 42, 43, 44, 45, 46, 47, 48, 49, 50,
       51, 52, 53, 54, 55, 56, 57, 58, 59, 60, 61, 62, 63, 64, 65, 66, 67,
       68, 69, 70, 71, 72, 73, 74, 75, 76, 77, 78, 79, 80, 81, 82, 83, 84,
       85, 86, 87, 88, 89, 90, 91, 92, 93, 94, 95, 96, 97, 98, 99])

In [15]: c = np.fromfile('b.dat', dtype=np.int, sep=',').reshape(5, 10, 2)

In [16]: c
Out[16]:
array([[[ 0,  1],
        [ 2,  3],
        [ 4,  5],
        [ 6,  7],
        [ 8,  9],
        [10, 11],
        [12, 13],
        [14, 15],
        [16, 17],
        [18, 19]],

       [[20, 21],
        [22, 23],
        [24, 25],
        [26, 27],
        [28, 29],
        [30, 31],
        [32, 33],
        [34, 35],
        [36, 37],
        [38, 39]],

       [[40, 41],
        [42, 43],
        [44, 45],
        [46, 47],
        [48, 49],
        [50, 51],
        [52, 53],
        [54, 55],
        [56, 57],
        [58, 59]],

       [[60, 61],
        [62, 63],
        [64, 65],
        [66, 67],
        [68, 69],
        [70, 71],
        [72, 73],
        [74, 75],
        [76, 77],
        [78, 79]],

       [[80, 81],
        [82, 83],
        [84, 85],
        [86, 87],
        [88, 89],
        [90, 91],
        [92, 93],
        [94, 95],
        [96, 97],
        [98, 99]]])
```

#### 便携文件存取

**`np.save(fname, array)`** 或 **`np.savez(fname, array)`**

- `fname`：文件名，以.npy为扩展名，压缩扩展名为.npz
- `array`：数组变量

**`np.load(fname)`**

- `fname`：文件名，以.npy为扩展名，压缩扩展名为.npz

## 函数

#### 随机数函数

- `np.random`的随机数函数

  | 函数                          | 说明                                              |
  | ----------------------------- | ------------------------------------------------- |
  | `rand(d0, d1, ..., dn)`       | 根据d0‐dn创建随机数数组，浮点数，[0,1)，均匀分布  |
  | `randn(do, d1, ..., dn)`      | 根据d0‐dn创建随机数数组，标准正态分布             |
  | `randint(low[, high, shape])` | 根据shape创建随机整数或整数数组，范围是[low, high |
  | `seed(s)`                     | 随机数种子，s是给定的种子值                       |

  ```python
  In [17]: a = np.random.rand(3, 4, 5)
  
  In [18]: a
  Out[18]:
  array([[[0.28456296, 0.57297647, 0.16379908, 0.16875091, 0.94947769],
          [0.98968264, 0.11221193, 0.37058908, 0.83361386, 0.68230262],
          [0.35134076, 0.47139436, 0.91832987, 0.5261529 , 0.23496556],
          [0.15739841, 0.32665968, 0.78843293, 0.71016085, 0.20462567]],
  
         [[0.53900756, 0.19413748, 0.14917924, 0.94800407, 0.47807917],
          [0.31373816, 0.76993117, 0.84375788, 0.68478222, 0.82777768],
          [0.39075001, 0.82948522, 0.52698984, 0.23253831, 0.22418133],
          [0.39450561, 0.66635006, 0.11688929, 0.47847531, 0.87352249]],
  
         [[0.03698468, 0.77379447, 0.23188117, 0.42336785, 0.3880457 ],
          [0.40791392, 0.61488804, 0.43527748, 0.27386942, 0.42960129],
          [0.26605846, 0.53707489, 0.9872779 , 0.93178179, 0.2630792 ],
          [0.10643995, 0.89796764, 0.02040815, 0.17687156, 0.72119773]]])
  
  In [19]: sn = np.random.randn(3, 4, 5)
  
  In [20]: sn
  Out[20]:
  array([[[-0.8525443 ,  0.86982285,  1.03694475,  0.59835155,
            1.00543305],
          [-0.48587878, -0.02835018, -0.13764559,  0.93942635,
           -0.56297613],
          [ 0.30777055,  0.30388093,  1.00377136,  1.36880841,
           -1.15389071],
          [ 0.62984272, -0.0318629 ,  0.2750638 , -1.15108662,
            0.58068166]],
  
         [[ 0.46451064,  1.41176632,  0.21872987, -0.0727752 ,
            2.48571047],
          [ 1.53161066, -1.32659946,  0.15721524, -2.06338447,
           -0.48668684],
          [-0.07184072,  0.93544985,  0.94721884, -0.99617068,
            1.62134945],
          [ 0.28437938,  0.09509007, -0.04152597, -0.21455104,
            0.58300975]],
  
         [[-1.92880387, -0.59232266,  0.65520443,  2.17787463,
           -0.20859337],
          [-1.92451517,  1.62817647, -0.27914219,  0.10487522,
           -0.30725874],
          [-0.0094378 ,  0.26938796, -1.77361648,  1.2648457 ,
            0.51825572],
          [ 0.83707755, -0.72390048,  0.30032902, -0.02587365,
            0.33571255]]])
  
  In [22]: b = np.random.randint(100, 200, (3, 4))
  
  In [23]: b
  Out[23]:
  array([[154, 128, 160, 125],
         [141, 171, 103, 156],
         [182, 195, 195, 163]])
  
  In [26]: np.random.seed(10)
  
  In [27]: np.random.randint(100, 200, (3, 4))
  Out[27]:
  array([[109, 115, 164, 128],
         [189, 193, 129, 108],
         [173, 100, 140, 136]])
  ```

  | 函数                            | 说明                                                         |
  | ------------------------------- | ------------------------------------------------------------ |
  | `shuffle(a)`                    | 根据数组a的第1轴进行随排列，改变数组x                        |
  | `permutation(a)`                | 根据数组a的第1轴产生一个新的乱序数组，不改变数组x            |
  | `choice(a[, size, replace, p])` | 从一维数组a中以概率p抽取元素，形成size形状新数组 replace表示是否可以重用元素，默认为False |
  | `uniform(low, high, size)`      | 产生具有均匀分布的数组,low起始值,high结束值,size形状         |
  | `normal(loc, scale, size)`      | 产生具有正态分布的数组,loc均值,scale标准差,size形状          |
  | `poisson(lam, size)`            | 产生具有泊松分布的数组，lam随机事件发生率，size形状          |

  ```python
  In [31]: a = np.random.randint(100, 200, (3, 4))
  
  In [32]: a
  Out[32]:
  array([[169, 113, 125, 113],
         [192, 186, 130, 130],
         [189, 112, 165, 131]])
  
  In [33]: np.random.shuffle(a)# a有变化
  
  In [34]: a
  Out[34]:
  array([[189, 112, 165, 131],
         [169, 113, 125, 113],
         [192, 186, 130, 130]])
  
  In [35]: a = np.random.randint(100, 200, (3, 4))
  
  In [36]: a
  Out[36]:
  array([[127, 118, 193, 177],
         [122, 123, 194, 111],
         [128, 174, 188, 109]])
  
  In [37]: np.random.permutation(a)# a无变化
  Out[37]:
  array([[122, 123, 194, 111],
         [127, 118, 193, 177],
         [128, 174, 188, 109]])
  
  In [38]: a
  Out[38]:
  array([[127, 118, 193, 177],
         [122, 123, 194, 111],
         [128, 174, 188, 109]])
  
  In [39]: b = np.random.randint(100, 200, (8,))
  
  In [40]: b
  Out[40]: array([171, 188, 111, 117, 146, 107, 175, 128])
  
  In [41]: np.random.choice(b, (3, 2))
  Out[41]:
  array([[188, 146],
         [111, 171],
         [171, 146]])
  
  In [42]: np.random.choice(b, (3, 2), replace=False)
  Out[42]:
  array([[188, 117],
         [175, 111],
         [128, 171]])
  
  In [44]: np.random.choice(b, (3, 2), p=b/np.sum(b))
  Out[44]:
  array([[175, 111],
         [188, 111],
         [171, 175]])
  
  In [45]: u = np.random.uniform(0, 10, (3, 4))
  
  In [46]: u
  Out[46]:
  array([[1.5115202 , 3.84114449, 9.44260712, 9.87625475],
         [4.56304547, 8.26122844, 2.51374134, 5.97371648],
         [9.0283176 , 5.34557949, 5.90201363, 0.39281767]])
  
  In [48]: n = np.random.normal(10, 5, (3, 4))
  
  In [49]: n
  Out[49]:
  array([[ 6.73620032,  8.89118781,  4.65856717,  3.86153973],
         [ 1.00713488,  6.5739633 ,  2.95065566, 16.26199297],
         [12.34781381, 11.63460824, 19.04271603,  2.93466001]])
  ```

#### 统计函数

*`axis=None`是统计函数的标配参数*

| 函数                                  | 说明                                                  |
| ------------------------------------- | ----------------------------------------------------- |
| `sum(a, axis=None)`                   | 根据给定轴axis计算数组a相关元素之和，axis整数或元组   |
| `mean(a, axis=None)`                  | 根据给定轴axis计算数组a相关元素的期望，axis整数或元组 |
| `average(a, axis=None, weights=None)` | 根据给定轴axis计算数组a相关元素的加权平均值           |
| `std(a, axis=None)`                   | 根据给定轴axis计算数组a相关元素的标准差               |
| `var(a, axis=None)`                   | 根据给定轴axis计算数组a相关元素的方差                 |

```python
In [50]: a = np.arange(15).reshape(3, 5)

In [51]: a
Out[51]:
array([[ 0,  1,  2,  3,  4],
       [ 5,  6,  7,  8,  9],
       [10, 11, 12, 13, 14]])

In [52]: np.sum(a)
Out[52]: 105

In [53]: np.mean(a, axis=1)
Out[53]: array([ 2.,  7., 12.])

In [54]: np.mean(a, axis=0)
Out[54]: array([5., 6., 7., 8., 9.])

In [55]: np.average(a, axis=0, weights=[10, 5, 1])
Out[55]: array([2.1875, 3.1875, 4.1875, 5.1875, 6.1875])

In [56]: np.std(a)
Out[56]: 4.320493798938574

In [57]: np.var(a)
Out[57]: 18.666666666666668
```

| 函数                          | 说明                                        |
| ----------------------------- | ------------------------------------------- |
| `min(a)` `max(a)`             | 计算数组a中元素的最小值、最大值             |
| `argmin(a)` ` argmax(a)`      | 计算数组a中元素最小值、最大值的降一维后下标 |
| `unravel_index(index, shape)` | 根据shape将一维下标index转换成多维下标      |
| `ptp(a)`                      | 计算数组a中元素最大值与最小值的差           |
| `median(a)`                   | 计算数组a中元素的中位数（中值）             |

```python
In [58]: b = np.arange(15, 0, -1).reshape(3, 5)

In [59]: b
Out[59]:
array([[15, 14, 13, 12, 11],
       [10,  9,  8,  7,  6],
       [ 5,  4,  3,  2,  1]])

In [60]: np.max(b)
Out[60]: 15

In [61]: np.argmax(b)#扁平化后的下标
Out[61]: 0

In [62]: np.unravel_index(np.argmax(b), b.shape)#重塑成多维下标
Out[62]: (0, 0)

In [63]: np.ptp(b)
Out[63]: 14

In [64]: np.median(b)
Out[64]: 8.0
```

#### 梯度函数

*梯度：连续值之间的变化率*

| 函数             | 说明                                                 |
| ---------------- | ---------------------------------------------------- |
| `np.gradient(f)` | 计算数组f中元素的梯度，当f为多维时，返回每个维度梯度 |

XY坐标轴连续三个X坐标对应的Y轴值：a, b, c，其中，b的梯度是： (c‐a)/2

```python
In [65]: a = np.random.randint(0, 20, (5))

In [66]: a
Out[66]: array([16,  0,  5,  9,  0])

In [67]: np.gradient(a)
Out[67]: array([-16. ,  -5.5,   4.5,  -2.5,  -9. ])

In [68]: b = np.random.randint(0, 20, (5))

In [69]: b
Out[69]: array([6, 0, 2, 3, 3])

In [71]: np.gradient(b)
Out[71]: array([-6. , -2. ,  1.5,  0.5,  0. ])
    
    In [74]: c = np.random.randint(0, 50, (3, 5))

In [75]: c
Out[75]:
array([[43, 24, 32, 37,  9],
       [40, 37, 43, 43, 26],
       [ 7,  8, 21,  8, 28]])

In [76]: np.gradient(c)
Out[76]:
[array([[ -3. ,  13. ,  11. ,   6. ,  17. ],
        [-18. ,  -8. ,  -5.5, -14.5,   9.5],
        [-33. , -29. , -22. , -35. ,   2. ]]),
 array([[-19. ,  -5.5,   6.5, -11.5, -28. ],
        [ -3. ,   1.5,   3. ,  -8.5, -17. ],
        [  1. ,   7. ,   0. ,   3.5,  20. ]])]
```

