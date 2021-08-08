# os库初学

- os库是Python标准库，包含几百个函数
- 常用路径操作、进程管理、环境参数等几类

## 路径操作

- os.path子库，处理文件路径及信息

  `import os.path`或`import os.path as op`

  |            函数             | 描述                                                         |
  | :-------------------------: | ------------------------------------------------------------ |
  |   `os.path.abspath(path)`   | 返回path在当前系统中的绝对路径<br/>`>>>os.path.abspath("file.txt")`<br/>`'C:\\Users\\Tian Song\\Python36-32\\file.txt'` |
  |  `os.path.normpath(path)`   | 归一化path的表示形式，统一用\\分隔路径<br/>`>>>os.path.normpath("D://PYE//file.txt")`<br/>`'D:\\PYE\\file.txt'` |
  |   `os.path.relpath(path)`   | 返回当前程序与文件之间的相对路径(relativepath)<br/>`>>>os.path.relpath("C://PYE//file.txt")`<br/>`'..\\..\\..\\..\\..\\..\\..\\PYE\\file.txt'` |
  |   `os.path.dirname(path)`   | 返回path中的目录名称<br/>`>>>os.path.dirname("D://PYE//file.txt")`<br/>`'D://PYE'` |
  |  `os.path.basename(path)`   | 返回path中最后的文件名称<br/>`>>>os.path.basename("D://PYE//file.txt")`<br/>`'file.txt'` |
  | `os.path.join(path,*paths)` | 组合path与paths，返回一个路径字符串<br/>`>>>os.path.join("D:/","PYE/file.txt")`<br/>`'D:/PYE/file.txt'` |
  |   `os.path.exists(path)`    | 判断path对应文件或目录是否存在，返回True或False<br/>`>>>os.path.exists("D://PYE//file.txt")`<br/>`False` |
  |   `os.path.isfile(path)`    | 判断path所对应是否为已存在的文件，返回True或False<br/>`>>>os.path.isfile("D://PYE//file.txt")`<br/>`True` |
  |    `os.path.isdir(path)`    | 判断path所对应是否为已存在的目录，返回True或False<br/>`>>>os.path.isdir("D://PYE//file.txt")`<br/>`False` |
  |  `os.path.getatime(path)`   | 返回path对应文件或目录上一次的访问时间<br/>`>>>os.path.getatime("D:/PYE/file.txt")`<br/>`1518356633.7551725` |
  |  `os.path.getmtime(path)`   | 返回path对应文件或目录最近一次的修改时间<br/>`>>>os.path.getmtime("D:/PYE/file.txt")`<br/>`1518356633.7551725` |
  |  `os.path.getctime(path)`   | 返回path对应文件或目录的创建时间<br/>`>>time.ctime(os.path.getctime("D:/PYE/file.txt"))`<br/>`'Sun Feb 11 21:43:53 2018'` |
  |   `os.path.getsize(path)`   | 返回path对应文件的大小，以字节为单位<br/>`>>>os.path.getsize("D:/PYE/file.txt")`<br/>`180768` |

  

## 进程管理

- 启动系统中其他程序

  `os.system(command)`

  ```python
  import os
  os.system("C:\\Windows\\System32\\calc.exe")
  >>>
  0
  #打开“计算器”，成功则返回“0”
  ```

  

## 环境参数

- 获得系统软硬件信息等环境参数

  |       函数       | 描述                                                         |
  | :--------------: | ------------------------------------------------------------ |
  | `os.chdir(path)` | 修改当前程序操作的路径<br/>`>>>os.chdir("D:")`               |
  |  `os.getcwd()`   | 返回程序的当前路径<br/>`>>>os.getcwd()`<br/>`'D:\\'`         |
  | `os.getlogin()`  | 获得当前系统登录用户名称<br/>`>>>os.getlogin()`<br/>`'Tian Song'` |
  | `os.cpu_count()` | 获得当前系统的CPU数量<br/>`>>>os.cpu_count()`<br/>`8`        |
  | `os.urandom(n)`  | 获得n个字节长度的随机字符串，通常用于加解密运算<br/>`>>>os.urandom(10)`<br/>`b'7\xbe\xf2!\xc1=\x01gL\xb3'` |

  

