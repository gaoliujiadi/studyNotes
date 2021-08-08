# Python-Pandas学习

Pandas是Python第三方库，提供高性能易用数据类型和分析工具

Pandas基于NumPy实现，常与NumPy和Matplotlib一同使用

---

`import pandas as pd`

| Numpy              | Pandas             |
| :----------------- | ------------------ |
| 基础数据类型       | 扩展数据类型       |
| 关注数据的结构表达 | 关注数据的应用表达 |
| 维度：数据间关系   | 数据与索引间关系   |

## Series类型（一维）

Series类型由一组数据及与之相关的数据索引组成

```
index_0 --> data_a
index_1 --> data_b
index_2 --> data_c
index_3 --> data_d
索引			数据
```

如：

```python
In [2]: a = pd.Series([9, 8, 7, 6])

In [3]: a
Out[3]:
0    9# 0 => 自动检索；9 => 数据
1    8
2    7
3    6
dtype: int64# 数据类型
```

Series类型可以由如下类型创建：

- Python列表，index与列表元素个数一致

- 标量值，index表达Series类型的尺寸

  ```python
  In [4]: s = pd.Series(25, index=['a', 'b', 'c'])
  
  In [5]: s
  Out[5]:
  a    25
  b    25
  c    25
  dtype: int64
  ```

- Python字典，键值对中的“键”是索引，index从字典中进行选择操作

  ```python
  In [11]: e = pd.Series({'a':9, 'b':8, 'c':7}, index=['c', 'a', 'b', 'd'])# index从字典中进行选择操作
  
  In [12]: e
  Out[12]:
  c    7.0
  a    9.0
  b    8.0
  d    NaN
  dtype: float64
  ```

- ndarray，索引和数据都可以通过ndarray类型创建

  ```python
  In [16]: n = pd.Series(np.arange(5), index=np.arange(9,4,-1))
  
  In [17]: n
  Out[17]:
  9    0
  8    1
  7    2
  6    3
  5    4
  dtype: int32
  ```

- 其他函数，range()函数等

### Series类型的基本操作

- Series类型包括index和values两部分

  ```python
  In [18]: b = pd.Series([9, 8, 7, 6], ['a', 'b', 'c', 'd'])
  
  In [19]: b
  Out[19]:
  a    9
  b    8
  c    7
  d    6
  dtype: int64
  
  In [20]: b.index# 获得索引
  Out[20]: Index(['a', 'b', 'c', 'd'], dtype='object')
  
  In [21]: b.values# 获得数据
  Out[21]: array([9, 8, 7, 6], dtype=int64)
  
  In [27]: b['b']
  Out[27]: 8
  
  In [28]: b[1]# 自动索引和自定义索引并存
  Out[28]: 8
  
  In [29]: b[['c', 'd', 'a']]
  Out[29]:
  c    7
  d    6
  a    9
  dtype: int64
  
  In [30]: b[['c', 'd', 1]]# 不能混用
  ```

- Series类型的操作类似ndarray类型

  - 索引方法相同，采用`[]`
  - NumPy中运算和操作可用于Series类型
  - 可以通过自定义索引的列表进行切片
  - 可以通过自动索引进行切片，如果存在自定义索引，则一同被切片
  ```python
  In [32]: b[3]
  Out[32]: 6
  
  In [33]: b[:3]
  Out[33]:
  a    9
  b    8
  c    7
  dtype: int64
  
  In [34]: b[b>b.median()]
  Out[34]:
  a    9
  b    8
  dtype: int64
  
  In [35]: np.exp(b)
  Out[35]:
  a    8103.083928
  b    2980.957987
  c    1096.633158
  d     403.428793
  dtype: float64
  ```
  
- Series类型的操作类似Python字典类型

  - 通过自定义索引访问

    ```python
    In [36]: b['b']
    Out[36]: 8
    ```

  - 保留字in操作

    ```python
    In [37]: 'c' in b
    Out[37]: True
    
    In [38]: 0 in b
    Out[38]: False
    ```

  - 使用`.get()`方法

    ```python
    In [39]: b.get('f', 100)
    Out[39]: 100
    ```

### Series类型对齐操作

`Series + Series`

 ```python
In [40]: a = pd.Series([1, 2, 3], ['c', 'd', 'e'])

In [41]: b = pd.Series([9, 8, 7, 6], ['a', 'b', 'c', 'd'])

In [42]: a + b
Out[42]:
a    NaN
b    NaN
c    8.0
d    8.0
e    NaN
dtype: float64
 ```

Series类型在运算中会自动对齐不同索引的数据

### Series类型的name属性

Series对象和索引都可以有一个名字，存储在属性.name中

```python
In [43]: b = pd.Series([9, 8, 7, 6], ['a', 'b', 'c', 'd'])

In [44]: b.name

In [45]: b.name = 'Series对象'

In [46]: b.index.name = '索引列'

In [47]: b
Out[47]:
索引列
a    9
b    8
c    7
d    6
Name: Series对象, dtype: int64
```

## DataFrame类型

DataFrame是一个表格型的数据类型，每列值类型可以不同

DataFrame既有行索引、也有列索引

DataFrame常用于表达二维数据，但可以表达多维数

```
		column		axis=1
index	index_0 --> data_a data_1 ... data_w
		index_1 --> data_b data_2 ... data_x
		index_2 --> data_c data_3 ... data_y
anis=0	index_3 --> data_d data_4 ... data_z
```

DataFrame类型可以由如下类型创建：

- 二维ndarray对象

  ```python
  In [54]: d = pd.DataFrame(np.arange(10).reshape(2,5))
  
  In [55]: d
  Out[55]:
     0  1  2  3  4
  0  0  1  2  3  4
  1  5  6  7  8  9
  ```

- 由一维ndarray、列表、字典、元组或Series构成的字典

  - 一维ndarry

  ```python
  In [58]: dt = {'one':pd.Series([1, 2, 3], index=['a', 'b', 'c']),
      ...:       'two':pd.Series([9, 8, 7, 6], index=['a', 'b', 'c', 'd'])}
  
  In [59]: d = pd.DataFrame(dt)
  
  In [60]: d
  Out[60]:
     one  two # 自定义索引
  a  1.0    9
  b  2.0    8
  c  3.0    7
  d  NaN    6
  # 自定义行索引
  In [61]: pd.DataFrame(dt, index=['b', 'c', 'd'], columns=['two', 'three'])
  Out[61]:
     two three
  b    8   NaN # 数据根据行索引自动补齐
  c    7   NaN
  d    6   NaN
  ```

  - 列表类型的字典

    ```python
    In [62]: dl = {'one':[1, 2, 3, 4], 'two':[9, 8, 7, 6]}
    
  In [63]: d = pd.DataFrame(dl, index = ['a', 'b', 'c', 'd'])
    
    In [64]: d
    Out[64]:
       one  two
    a    1    9
    b    2    8
    c    3    7
    d    4    6
    
    In [67]: dl = {'城市':['北京', '上海', '广州', '深圳'],
        ...:       '环比':[101.5, 101.2, 101.3, 102.0],
        ...:       '同比':[120.7, 127.3, 119.4, 140.9],
        ...:       '定基':[121.4, 127.8, 120.0, 145.5,]}
    
    In [68]: d = pd.DataFrame(dl, index=['c1', 'c2', 'c3', 'c4'])
    
    In [69]: d
    Out[69]:
        城市     环比     同比     定基
    c1  北京  101.5  120.7  121.4
    c2  上海  101.2  127.3  127.8
    c3  广州  101.3  119.4  120.0
    c4  深圳  102.0  140.9  145.5
    
    In [70]: d.index
    Out[70]: Index(['c1', 'c2', 'c3', 'c4'], dtype='object')
    
    In [71]: d.columns
    Out[71]: Index(['城市', '环比', '同比', '定基'], dtype='object')
    
    In [72]: d.values
    Out[72]:
    array([['北京', 101.5, 120.7, 121.4],
           ['上海', 101.2, 127.3, 127.8],
           ['广州', 101.3, 119.4, 120.0],
           ['深圳', 102.0, 140.9, 145.5]], dtype=object)
    ```
    

- Series类型

- 其他的DataFrame类型

DataFrame是二维带“标签”数组

DataFrame基本操作类似Series，依据行列索引

```
		   column_0	column_1  column_i
index_0 --> data_a	data_1	data_w
```

## Pandas库的数据类型操作

### 重新索引

`.reindex(index=None, columns=None, ...)`

| 参数            | 说明                                            |
| --------------- | ----------------------------------------------- |
| `ndex, columns` | 新的行列自定义索引                              |
| `fill_value`    | 重新索引中，用于填充缺失位置的值                |
| `method`        | 填充方法, ffill当前值向前填充，bfill向后填充    |
| `limit`         | 最大填充量                                      |
| `copy`          | 默认True，生成新的对象，False时，新旧相等不复制 |

*Series和DataFrame的索引是I ndex类型 Index对象是不可修改类型*

### 索引类型的常用方法

| 方法                 | 说明                                   |
| -------------------- | -------------------------------------- |
| `.append(idx)`       | 连接另一个Index对象，产生新的Index对象 |
| `.diff(idx)`         | 连接另一个Index对象，产生新的Index对象 |
| `.intersection(idx)` | 计算交集                               |
| `.union(idx)`        | 计算并集                               |
| `.delete(loc)`       | 删除loc位置处的元素                    |
| `.insert(loc,e)`     | 在loc位置增加一个元素e                 |

### 删除指定索引对象

`.drop()`能够删除Series和DataFrame指定行或列索引

## Pandas库的数据类型运算

### 算术运算

算术运算根据行列索引，补齐后运算，运算默认产生浮点数，补齐时缺项填充NaN (空值 )，二维和一维、一维和零维间为广播运算，采用 + ‐ * /符号进行的二元运算产生新的对象。

| 方法               | 说明                     |
| ------------------ | ------------------------ |
| `.add(d, **argws)` | 类型间加法运算，可选参数 |
| `.sub(d, **argws)` | 类型间减法运算，可选参数 |
| `.mul(d, **argws)` | 类型间乘法运算，可选参数 |
| `.div(d, **argws)` | 类型间除法运算，可选参数 |

### 比较运算

比较运算只能比较相同索引的元素，不进行补齐，二维和一维、一维和零维间为广播运算，采用` > < >= <= == !=`等符号进行的二元运算产生布尔对象。

## Pandas数据特征分析简述

**一组数据的摘要**

| 特征         | 函数                              |
| ------------ | --------------------------------- |
| 排序         | `.sort_index()`  `.sort_values()` |
| 基本统计函数 | `.describe()`                     |
| 累计统计函数 | `.cum*()`  `.rolling().*()`       |
| 相关性分析   | `.corr()`  `.cov()`               |

