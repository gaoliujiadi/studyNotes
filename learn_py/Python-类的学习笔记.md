# Python-类的学习笔记

- example:

  ```python
  class dog():
      #一次模拟小狗的简单尝试
      def __init__(self,name,color):
          #初始化属性name和color,设定age的默认值
          self.name = name
          self.color = color
          self.age = 0
      def sit(self):
          #模拟小狗被命令时蹲下
          print(self.name + " is now sitting.")
      def roll_over(self):
          #模拟小狗被命令时打滚
          print(self.name.title() + " rolled over!")
      #'self.name'在这里等价于'self.name.title()'
  
  ```

  - 方法

    类中的函数称为方法 ：

    `__init__()`、`sit()`、`roll_over`

    *`__init__()` 是一个特殊的方法，每当你根据`Dog` 类创建新实例时，Python都会自动运行它。在这个方法的名称中，开头和末尾各有两个下划线，这是一种约定，旨在避免Python默认方法与普通方法发生名称冲突。*

  - 默认值

    类中的每个属性都必须有初始值，哪怕这个值是0或空字符串。在有些情况下，如设置默认值时，在方法`__init__()` 内指定这种初始值是可行的，如：

    `self.age = 0`

  - 修改属性的值

    - 直接通过实例访问

      ```python
      >>> aDog = dog('John','White')
      >>> aDog.age
      0
      >>> aDog.age = 13
      >>> aDog.age
      13
      ```

    - 通过方法修改属性的值

      无需直接访问属性，而可将值传递给一个方法，由它在内部进行更新。

      ```python
      class dog():
          --snip--
          
          def updateAge(self,age):
              #更新年龄
              self.age = age
      ```

      ```python
      >>> aDog = dog('John','White')
      >>> aDog.age
      0
      >>> aDog.updataAge(13)
      >>> aDog.age
      13
      ```

      可对方法`updateAge` 进行扩展,禁止任何人将年龄改小

      ```python
      class dog():
          --snip--
          
          def updateAge(self,age):
              #更新年龄,并禁止任何人将年龄改小
              if age >= self.age:
                  self.age = age
              else:
                  print('不可改小')
      ```

      ```python
      >>> aDog = dog('John','White')
      >>> aDog.age
      0
      >>> aDog.uptadeAge(13)
      >>> aDog.age
      13
      >>> aDog.updateAge(10)
      no
      ```

    - 通过方法对属性的值进行递增

      有时候需要将属性值递增特定的量，而不是将其设置为全新的值。假设狗一开始卖来到目前增加了5岁。‘

      ```python
      class Car():
          --snip--
          
          def updateAge(self, mileage):
              --snip--
          def incrementAge(self,incre):
              self.age += incre
      ```

      ```python
      >>> aDog = dog('John','White')
      >>> aDog.age
      0
      >>> aDog.updateAge(13)
      >>> aDog.age
      13
      >>> aDog.incrementAge(5)
      >>> aDog.age
      18
      ```


## 继承

如果要编写的类是另一个现成类的特殊版本，可使用继承 。

- 一个类继承 另一个类时，它将自动获得另一个类的所有属性和方法。
- 原有的类称为父类 ，而新类称为子类 。
- 子类继承了其父类的所有属性和方法，同时还可以定义自己的属性和方法。

```python
class Samoyed(dog):#萨摩耶
	def __init__(self,name,color,sup):#先继承，再重构
		dog.__init__(self,name,color)#继承父类
		self.sup = sup
	def sup(self):
		print(self.sup)
```

### 将实例作属性

使用代码模拟实物时，可能会发现给类添加的细节越来越多。在这种情况下，可能需要将类的一部分作为一个独立的类提取出来。可以将大型类拆分成多个协同工作的小类。

```python
class SamoyedSuper():
    def __init__(self,sup1=1,sup2=2):
        self.sup1 = sup1
        self.sup2 = sup2
    def desSup(self):
        print(self.sup1,self.sup2)
        
class Samoyed(dog):
    def __init__(self,name,color):
        dog.__init__(self,name,color)
        self.sup = SamoyedSuper()

```



## 导入类

