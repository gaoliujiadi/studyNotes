# Python-beautiful soup库入门

- 演示HTML页面地址：http://python123.io/ws/demo.html

  ```python
  >>> import requests
  >>> r = requests.get("http://python123.io/ws/demo.html")
  >>> r.text
  '<html><head><title>This is a python demo page</title></head>\r\n<body>\r\n<p class="title"><b>The demo python introduces several python courses.</b></p>\r\n<p class="course">Python is a wonderful general-purpose programming language. You can learn Python from novice to professional by tracking the following courses:\r\n<a href="http://www.icourse163.org/course/BIT-268001" class="py1" id="link1">Basic Python</a> and <a href="http://www.icourse163.org/course/BIT-1001870001" class="py2" id="link2">Advanced Python</a>.</p>\r\n</body></html>'
  >>> demo = r.text
  >>> from bs4 import BeautifulSoup
  >>> soup = BeautifulSoup(demo,'html.parser')
  >>> print(soup.prettify())
  <html>
   <head>
    <title>
     This is a python demo page
    </title>
   </head>
   <body>
    <p class="title">
     <b>
      The demo python introduces several python courses.
     </b>
    </p>
    <p class="course">
     Python is a wonderful general-purpose programming language. You can learn Python from novice to professional by tracking the following courses:
     <a class="py1" href="http://www.icourse163.org/course/BIT-268001" id="link1">
      Basic Python
     </a>
     and
     <a class="py2" href="http://www.icourse163.org/course/BIT-1001870001" id="link2">
      Advanced Python
     </a>
     .
    </p>
   </body>
  </html>
  ```

- **`from bs4 import BeautifulSoup`**

  `soup = BeautifulSoup('<p>data</p>',html.parser)`

## Beautiful Soup库的基本元素

### Beautiful Soup类

- BeautifulSoup对应一个HTML/XML文档的全部内容

```python
>>> from bs4 import BeautifulSoup
>>> soup = BeautifulSoup("<html>data</html>","html.parser")
>>> soup2 = BeautifulSoup(open("F://program//spider//demo.html"),"html.parser")
```

### BeautifulSoup类的基本元素

| 基本元素        | 说明                                                     |
| --------------- | -------------------------------------------------------- |
| Tag             | 标签，最基本的信息组织单元，分别用<>和</>标明开头和结尾  |
| Name            | 标签的名字，`<p>…</p>`的名字是'p'，格式：`<tag>.name`    |
| Attributes      | 标签的属性，字典形式组织，格式：`<tag>.attrs`            |
| NavigableString | 标签内非属性字符串，<>…</>中字符串，格式：`<tag>.string` |
| Comment         | 标签内字符串的注释部分，一种特殊的Comment类型            |

#### Tag标签

标签，最基本的信息组织单元，分别用<>和</>标明开头和结尾

```python
>>> from bs4 import BeautifulSoup
>>> soup = BeautifulSoup(demo,'html.parser')
>>> soup.title
<title>This is a python demo page</title>
>>> tag = soup.a
>>> tag
<a class="py1" href="http://www.icourse163.org/course/BIT-268001" id="link1">Basic Python</a>
```

- 任何存在于HTML语法中的标签都可以用`soup.<tag>`访问获得
  当HTML文档中存在多个相同<tag>对应内容时，`soup.<tag>`返回第一个

#### Tag的name

标签的名字，`<p>…</p>`的名字是'p'，格式：`<tag>.name`

```python
>>> from bs4 import BeautifulSoup
>>> soup = BeautifulSoup(demo,'html.parser')
>>> soup.a.name
'a'
>>> soup.a.parent.name
'p'
>>> soup.a.parent.parent.name
'body'
```

- 每个`<tag>`都有自己的名字，通过`<tag>.name`获取，字符串类型

#### Tag的attrs

标签的属性，字典形式组织，格式：`<tag>.attrs`

```python
>>> tag = soup.a
>>> tag.attrs
{'href': 'http://www.icourse163.org/course/BIT-268001', 'class': ['py1'], 'id': 'link1'}
>>> tag.attrs['class']
['py1']
>>> tag.attrs['href']
'http://www.icourse163.org/course/BIT-268001'
>>> type(tag.attrs)
<class 'dict'>
>>> type(tag)
<class 'bs4.element.Tag'>
```

- 一个`<tag>`可以有0或多个属性，字典类型

#### Tag的NavigableString

标签内非属性字符串，<>…</>中字符串，格式：`<tag>.string`

```python
>>> soup.a
<a class="py1" href="http://www.icourse163.org/course/BIT-268001" id="link1">Basic Python</a>
>>> soup.a.string
'Basic Python'
>>> soup.p
<p class="title"><b>The demo python introduces several python courses.</b></p>
>>> soup.p.string
'The demo python introduces several python courses.'
>>> type(soup.p.string)
<class 'bs4.element.NavigableString'>
```

- NavigableString可以跨越多个层次

#### Tag的Comment

标签内字符串的注释部分，一种特殊的Comment类型

```python
>>> newsoup = BeautifulSoup("<b><!--This is a comment--></b><p>This is not a comment</p>","html.parser")
>>> newsoup.b.string
'This is a comment'
>>> type(newsoup.b.string)
<class 'bs4.element.Comment'>#注释
>>> newsoup.p.string
'This is not a comment'
>>> type(newsoup.p.string)
<class 'bs4.element.NavigableString'>#非注释
```

- Comment是一种特殊类型


### Beautiful Soup库解析器

| 解析器           | 使用方法                          | 条件                   |
| ---------------- | --------------------------------- | ---------------------- |
| bs4的HTML解析器  | `BeautifulSoup(mk,'html.parser')` | 安装bs4库              |
| lxml的HTML解析器 | `BeautifulSoup(mk,'lxml')`        | `pip install lxml`     |
| lxml的XML解析器  | `BeautifulSoup(mk,'xml')`         | `pip install lxml`     |
| html5lib的解析器 | `BeautifulSoup(mk,'html5lib')`    | `pip install html5lib` |

## 基于bs4库的HTML内容遍历方法

### 标签树的下行遍历

| 属性           | 说明                                                    |
| -------------- | ------------------------------------------------------- |
| `.contents`    | 子节点的列表，将`<tag>`所有儿子节点存入列表             |
| `.children`    | 子节点的迭代类型，与.contents类似，用于循环遍历儿子节点 |
| `.descendants` | 子孙节点的迭代类型，包含所有子孙节点，用于循环遍历      |

- `contents`

  ```python
  >>> soup = BeautifulSoup(demo,'html.parser')
  >>> soup.head
  <head><title>This is a python demo page</title></head>
  >>> soup.head.contents
  [<title>This is a python demo page</title>]
  >>> soup.body.contents
  ['\n', <p class="title"><b>The demo python introduces several python courses.</b></p>, '\n', <p class="course">Python is a wonderful general-purpose programming language. You can learn Python from novice to professional by tracking the following courses:
  <a class="py1" href="http://www.icourse163.org/course/BIT-268001" id="link1">Basic Python</a> and <a class="py2" href="http://www.icourse163.org/course/BIT-1001870001" id="link2">Advanced Python</a>.</p>, '\n']
  >>> len(soup.body.contents)
  5
  >>> soup.body.contents[1]
  <p class="title"><b>The demo python introduces several python courses.</b></p>
  >>> 
  ```

- `.children`（遍历儿子节点）

  ```python
  >>> for child in soup.body.children:
  	print(child)
  
  <p class="title"><b>The demo python introduces several python courses.</b></p>
  
  <p class="course">Python is a wonderful general-purpose programming language. You can learn Python from novice to professional by tracking the following courses:
  
  <a class="py1" href="http://www.icourse163.org/course/BIT-268001" id="link1">Basic Python</a> and <a class="py2" href="http://www.icourse163.org/course/BIT-1001870001" id="link2">Advanced Python</a>.</p>
  ```

- `.descendants`（遍历子孙节点）

  ```python
  >>> for child in soup.body.descendants:
  	print(child)
  
  <p class="title"><b>The demo python introduces several python courses.</b></p>
  <b>The demo python introduces several python courses.</b>
  The demo python introduces several python courses.
  
  <p class="course">Python is a wonderful general-purpose programming language. You can learn Python from novice to professional by tracking the following courses:
  
  <a class="py1" href="http://www.icourse163.org/course/BIT-268001" id="link1">Basic Python</a> and <a class="py2" href="http://www.icourse163.org/course/BIT-1001870001" id="link2">Advanced Python</a>.</p>
  Python is a wonderful general-purpose programming language. You can learn Python from novice to professional by tracking the following courses:
  
  <a class="py1" href="http://www.icourse163.org/course/BIT-268001" id="link1">Basic Python</a>
  Basic Python
   and 
  <a class="py2" href="http://www.icourse163.org/course/BIT-1001870001" id="link2">Advanced Python</a>
  Advanced Python
  .
  ```



### 标签树的上行遍历

| 属性       | 说明                                         |
| ---------- | -------------------------------------------- |
| `.parent`  | 节点的父亲标签                               |
| `.parents` | 节点先辈标签的迭代类型，用于循环遍历先辈节点 |

- `.parent`

  ```python
  >>> soup = BeautifulSoup(demo,"html.parser")
  >>> soup.title.parent
  <head><title>This is a python demo page</title></head>
  >>> soup.html.parent
  <html><head><title>This is a python demo page</title></head>
  <body>
  <p class="title"><b>The demo python introduces several python courses.</b></p>
  <p class="course">Python is a wonderful general-purpose programming language. You can learn Python from novice to professional by tracking the following courses:
  
  <a class="py1" href="http://www.icourse163.org/course/BIT-268001" id="link1">Basic Python</a> and <a class="py2" href="http://www.icourse163.org/course/BIT-1001870001" id="link2">Advanced Python</a>.</p>
  </body></html>
  >>> soup.parent
  ```

- `.parents`

  ```python
  >>> soup = BeautifulSoup(demo,"html.parser")
  >>> for parent in soup.a.parents:
  	if parent is None:
  		print(parent)
  	else:
  		print(parent.name)
  		
  p
  body
  html
  [document]
  ```

  - 遍历所有先辈节点，包括soup本身，所以要区别判断

### 标签树的平行遍历

平行遍历发生在同一个父节点下的各节点间

| 属性                 | 说明                                                 |
| -------------------- | ---------------------------------------------------- |
| `.next_sibling`      | 返回按照HTML文本顺序的下一个平行节点标签             |
| `.previous_sibling`  | 返回按照HTML文本顺序的上一个平行节点标签             |
| `.next_siblings`     | 迭代类型，返回按照HTML文本顺序的后续所有平行节点标签 |
| `.previous_siblings` | 迭代类型，返回按照HTML文本顺序的前续所有平行节点标签 |

- `.next_sibling`&`.previous_sibling`

  ```python
  >>> soup = BeautifulSoup(demo,"html.parser")
  >>> soup.a.next_sibling
  ' and '
  >>> soup.a.next_sibling.next_sibling
  <a class="py2" href="http://www.icourse163.org/course/BIT-1001870001" id="link2">Advanced Python</a>
  >>> soup.a.previous_sibling
  'Python is a wonderful general-purpose programming language. You can learn Python from novice to professional by tracking the following courses:\r\n'
  >>> soup.a.previous_sibling.previous_sibling
  >>> soup.a.parent
  <p class="course">Python is a wonderful general-purpose programming language. You can learn Python from novice to professional by tracking the following courses:
  
  <a class="py1" href="http://www.icourse163.org/course/BIT-268001" id="link1">Basic Python</a> and <a class="py2" href="http://www.icourse163.org/course/BIT-1001870001" id="link2">Advanced Python</a>.</p>
  ```

- `.next_siblings`

  ```python
  >>> for sibling in soup.a.next_siblings:
  	print(sibling)
  
  	
   and 
  <a class="py2" href="http://www.icourse163.org/course/BIT-1001870001" id="link2">Advanced Python</a>
  .
  ```

- `.previous_siblings`

  ```python
  >>> for sibling in soup.a.previous_siblings:
  	print(sibling)
  
  	
  Python is a wonderful general-purpose programming language. You can learn Python from novice to professional by tracking the following courses:
  ```

  

## 美化

### bs4库的prettify()方法

```python
>>> import requests
>>> r = requests.get("http://python123.io/ws/demo.html")
>>> demo = r.text
>>> demo
'<html><head><title>This is a python demo page</title></head>\r\n<body>\r\n<p class="title"><b>The demo python introduces several python courses.</b></p>\r\n<p class="course">Python is a wonderful general-purpose programming language. You can learn Python from novice to professional by tracking the following courses:\r\n<a href="http://www.icourse163.org/course/BIT-268001" class="py1" id="link1">Basic Python</a> and <a href="http://www.icourse163.org/course/BIT-1001870001" class="py2" id="link2">Advanced Python</a>.</p>\r\n</body></html>'
>>> from bs4 import BeautifulSoup
>>> soup = BeautifulSoup(demo,"html.parser")
>>> soup.prettify()
'<html>\n <head>\n  <title>\n   This is a python demo page\n  </title>\n </head>\n <body>\n  <p class="title">\n   <b>\n    The demo python introduces several python courses.\n   </b>\n  </p>\n  <p class="course">\n   Python is a wonderful general-purpose programming language. You can learn Python from novice to professional by tracking the following courses:\n   <a class="py1" href="http://www.icourse163.org/course/BIT-268001" id="link1">\n    Basic Python\n   </a>\n   and\n   <a class="py2" href="http://www.icourse163.org/course/BIT-1001870001" id="link2">\n    Advanced Python\n   </a>\n   .\n  </p>\n </body>\n</html>'
>>> print(soup.prettify())
<html>
 <head>
  <title>
   This is a python demo page
  </title>
 </head>
 <body>
  <p class="title">
   <b>
    The demo python introduces several python courses.
   </b>
  </p>
  <p class="course">
   Python is a wonderful general-purpose programming language. You can learn Python from novice to professional by tracking the following courses:
   <a class="py1" href="http://www.icourse163.org/course/BIT-268001" id="link1">
    Basic Python
   </a>
   and
   <a class="py2" href="http://www.icourse163.org/course/BIT-1001870001" id="link2">
    Advanced Python
   </a>
   .
  </p>
 </body>
</html>
```

- prettify()可用于标签，方法：`<tag>.prettify()`

  ```python
  >>> print(soup.a.prettify())
  <a class="py1" href="http://www.icourse163.org/course/BIT-268001" id="link1">
   Basic Python
  </a>
  ```

### bs4库的编码

- bs4库将任何HTML输入都变成utf‐8编码
  Python 3.x默认支持编码是utf‐8,解析无障碍

  ```python
  >>> soup = BeautifulSoup("<p>中文</p>","html.parser")
  >>> soup.p.string
  '中文'
  >>> print(soup.p.prettify())
  <p>
   中文
  </p>
  ```

## 基于bs4库的HTML内容查找方法

<b>`<>.find_all(name, attrs, recursive, string, **kwargs)`</b>

返回一个**列表**类型，存储查找的结果

- name:对标签名称的检索字符串

  ```python
  >>> soup.find_all('a')
  [<a class="py1" href="http://www.icourse163.org/course/BIT-268001" id="link1">Basic Python</a>, <a class="py2" href="http://www.icourse163.org/course/BIT-1001870001" id="link2">Advanced Python</a>]
  >>> soup.find_all(['a','b'])
  [<b>The demo python introduces several python courses.</b>, <a class="py1" href="http://www.icourse163.org/course/BIT-268001" id="link1">Basic Python</a>, <a class="py2" href="http://www.icourse163.org/course/BIT-1001870001" id="link2">Advanced Python</a>]
  ```

  - 若标签名称为"True"，将显示所有标签信息:

    ```python
    >>> for tag in soup.find_all(True):
    	print(tag.name)
    
    html
    head
    title
    body
    p
    b
    p
    a
    a
    ```

  - 若只想搜索有"b"的标签，用正则表达式库:

    ```python
    >>> import re
    >>> for tag in soup.find_all(re.compile('b')):
    	print(tag.name)
    	
    body
    b
    ```

- attrs:对标签属性值的检索字符串，可标注属性检索

  ```python
  >>> soup.find_all('p','course')
  [<p class="course">Python is a wonderful general-purpose programming language. You can learn Python from novice to professional by tracking the following courses:
  
  <a class="py1" href="http://www.icourse163.org/course/BIT-268001" id="link1">Basic Python</a> and <a class="py2" href="http://www.icourse163.org/course/BIT-1001870001" id="link2">Advanced Python</a>.</p>]
  >>> soup.find_all(id='link1')
  [<a class="py1" href="http://www.icourse163.org/course/BIT-268001" id="link1">Basic Python</a>]
  ```

- recursive:是否对子孙全部检索，默认True

  ```python
  >>> soup.find_all('a')
  [<a class="py1" href="http://www.icourse163.org/course/BIT-268001" id="link1">Basic Python</a>, <a class="py2" href="http://www.icourse163.org/course/BIT-1001870001" id="link2">Advanced Python</a>]
  >>> soup.find_all('a',recursive=False)
  []
  ```

- string:<>…</>中字符串区域的检索字符串

  ```python
  >>> soup.find_all(string='Basic Python')
  ['Basic Python']
  >>> import re
  >>> soup.find_all(string=re.compile('python'))
  ['This is a python demo page', 'The demo python introduces several python courses.']
  ```

*`<tag>(..) `等价于`<tag>.find_all(..)`
`soup(..) `等价于`soup.find_all(..)`*

### 扩展方法

|             方法              | 说明                                                    |
| :---------------------------: | ------------------------------------------------------- |
|          `<>.find()`          | 搜索且只返回一个结果，同`.find_all()`参数               |
|      `<>.find_parents()`      | 在先辈节点中搜索，返回列表类型，同`.find_all()`参数     |
|      `<>.find_parent()`       | 在先辈节点中返回一个结果，同`.find()`参数               |
|   `<>.find_next_siblings()`   | 在后续平行节点中搜索，返回列表类型，同`.find_all()`参数 |
|   `<>.find_next_sibling()`    | 在后续平行节点中返回一个结果，同`.find()`参数           |
| `<>.find_previous_siblings()` | 在前序平行节点中搜索，返回列表类型，同`.find_all()`参数 |
| `<>.find_previous_sibling()`  | 在前序平行节点中返回一个结果，同`.find()`参数           |

