---
title: Python 风格指南
date: 2018-04-13 09:36:01
tags: Python
---

## 1. 分号 

**不要在行尾加分号，也不要用分号将两条命令放在同一行。**

## 2. 行长度

**每行不超过 80 个字符。**
例外：1. 长的导入模块语句，2. 注释里的URL。

**不要使用反斜杠连接行。**Python 会将**圆括号、中括号和花括号中的行隐式的连接起来，**可以利用这个特点。如果需要，可以在表达式外围增加一对额外的圆括号。<!--more-->

**1). 变量申明：**

```python
# bad
s = 'This will build a very long long long long long long long long long long long string'
# good
s = ('This will build a very long long long long'
     'long long long long long long long string')
```

**2). 条件判断：**

```python
# bad
if (width == 0 and height == 0 and color == 'red' and emphasis == 'strong' and sex='male' and age=25):
# good
if (width == 0 and height == 0 and
    color == 'red' and emphasis == 'strong' and
    sex='male' and age=25):
```

**3). 函数入参：**

```python
# bad
fun(self, name, width, height, color='black', height=170, age=0, sex='male', emphasis=None)
# good
fun(self, name, width, height, color='black', height=170,
    age=0, sex='male', emphasis=None)
```

## 3. 缩进

**用 4 个空格来缩进代码。**

绝对不要用 tab，也不要 tab 和空格混用。对于行连接的情况，你应该垂直对齐换行的元素，或者使用 4 空格的悬挂式缩进（这时第一行不应该有参数）。

```python
# bad
foo = long_function_name(var_one, var_two,
    var_three, var_four)
# good
foo = long_fuction_name(
    var_one, var_two, var_three,
    var_four)
# better
foo = long_function_name(var_one, var_two,
                         var_three, var_four)
```

## 4. 导入格式

**每个导入应该独占一行。**

```python
# bad
import os,sys,re
# good
import os
import sys
import re
```

导入总应该放在文件顶部，位于模块注释和文档字符串之后，模块全局变量和常量之前。导入应该按照从最通用到最不通用的顺序分组。

- 标准库导入
- 第三方库导入
- 应用程序指定导入

导入的分组中：应该根据每个模块的完整包路径按字典序排序，忽略大小写。

```python
import foo
from foo import bar
from foo.bar import baz
from foo.bar import Quux
from Foob import ar
```

## 5. 命名

命名是一个时时刻刻都要碰到，也是非常基本的技能！

**1). 全部小写**
如果名字长，中间用下划线连接。

1. 局部变量`local_var_name`
2. 函数名字`function_name`
3. 函数的参数名字`function_parameter_name`
4. 模块和包的名字`module_name` `package_name`

**2). 全部大写**
全局变量，中间用下划线连接`GLOBAL_VAR_NAME`

**3). 驼峰式命名法**

1. 类的名字`ClassName` 比如`PreparedRequest`
2. 异常的名字`ExceptionName` 比如`BaseException`

## 6. 字符串

字符串主要是**格式化和引号的引用**两大问题。

**1). 字符串格式化一般使用 % 或者 format 来格式化字符串，**其实 Python3 里面推荐使用 format 方法，灵活方便强大。 

```python
# good
x = '{}, {}'.format(imperation, expletive)
```

**2). 避免在循环中用 + 和 += 操作符来累加字符串**

```python
# bad
table = ''
for i in range(100000):
    table += 'abc'
print(table)
```

因为你每加一次，就会分配一个临时内存，如果运行10万次开销非常大，时间也很长。

```python
# good
table = []
for i in range(100000):
    table.append('abc')
print(''.join(table))
```

好的方法是把字符串都放在列表里面，用 join 方法一次性连接起来，时间会比上面那种方法快很多，内存开销也小一些。

**3). 引号使用**
同一个文件中，保持使用字符串引号的一致性。使用单引号`’`或者双引号`”`之一用以引用字符串，并在同一文件中沿用。 

```python
# bad
Python("Why are you hiding your eyes?")
Gollum('The lint. It burns us.')
Gollum("Always the great ling. Watching. Watching.")

# good
Python('Why are you hiding your eyes?')
Gollum("I'm scared of lint errors.")
Narrator('"Good!" thought a happy Python reviewer.')
```

## 7. 函数

一个函数必须要有详细的文档字符串说明，要包含以下 3 个部分：

**1). 参数Args**
列出每个参数的名字，并在名字后使用一个冒号和一个空格，分隔对该参数的描述。
描述应该包括所需的类型和含义。如果一个函数接受 *foo(可变长度参数列表)* 或者 *bar(任意关键字参数)* ，应该详细列出 *foo 和 bar*。

**2). 返回值 Returns: (或者 Yields: 用于生成器)**
描述返回值的类型和语义。如果函数返回 None，这一部分可以省略。

**3). 异常 Raises**
列出与接口有关的所有异常，这个是非常正规的写法。
当然大部分我们的函数都是短小精悍的，一般都只考虑参数说明和返回值，并不是每个人都会考虑到异常处理，比如：

- 列表下标越界
- 动态变量为空
- 类型不匹配等等

Google 这种写法其实对我们在构造一个新的函数，思考推敲函数的时候非常有借鉴意义，好的代码不仅精美还要安全。

## 8. 类

**如果一个类不继承自其它类，就显式的从 object 继承，嵌套类也一样。**

```python
# bad
class SampleClass:
    pass

# good
class SampleClass(object):
    pass
```

继承自 object 是为了使属性(properties)正常工作，并且这样可以保护你的代码，避免一些隐患。

另，类应有定义描述该类的文档字符串。如果你的类有公共属性(Attributes)，那么文档中应该有一个属性(Attributes)段，并且应该遵守和函数参数相同的格式。

```python
class SampleClass(object):
    """Summary of class here.
    
    Longer class information...
    Longer class information...
    
    Attributes:
        likes_spam: A boolean indicating if we like SPAM or not.
        eggs: An integer count of the eggs we have laid.
    """
    
    def __init__(self, likes_spam=False):
        """Inits SampleClass with blah."""
        self.likes_spam = likes_spam
        self.eggs = 0
        
    def public_method(self):
      """Performs operation blah."""
```

## 9. 文件和 Sockets

**在文件和 sockets 结束时，显式的关闭它。**

除了文件外，sockets 或其他类似文件的对象在没有必要的情况下打开，会有许多副作用，特别是安全问题，例如：

- 它们可能会消耗有限的系统资源，如文件描述符。如果这些资源在使用后没有及时归还系统，那么用于处理这些对象的代码会将资源消耗殆尽。
- 仅仅是从逻辑上关闭文件和 sockets，那么它们仍然可能会被其共享的程序在无意中进行读或者写操作。
- 只有当它们真正被关闭后，对于它们尝试进行读或者写操作将会抛出异常，并使得问题快速显现出来。

其实它们都是带上下文管理器的，建议用 with 自动关闭：

```python
with open('hello.txt') as hello_file:
    for line in hello_file:
        print(line)
```

## 10. 异常

异常这块非常重要，Google 花了很多的笔墨描述异常使用，异常有利有弊，小心使用。

**1. 优点**
正常操作代码的控制流不会和错误处理代码混在一起。当某种条件发生时，它也允许控制流跳过多个框架。例如，一步跳出 N 个嵌套的函数，而不必继续执行错误的代码。

**2. 缺点**
可能会导致让人困惑的控制流，调用库时容易错过错误情况。

**3. 异常必须遵守特定条件**

1). 触发异常
建议用 raise MyException("Error message") 或者 raise MyException。
不要使用两个参数的形式( raise MyException, "Error message" )或者过时的字符串异常( raise "Error message" )。

2). 自定义异常
模块或包应该定义自己特定域的异常基类，这个基类应该从内建的 Exception 类继承。模块的异常基类应该叫做”Error”。

```python
class Error(Exception):
    pass
```

3). 永远不要捕获所有异常
永远不要使用 except: 语句来捕获所有异常。也不要捕获 Exception 或者 StandardError，除非你打算重新触发该异常。
在异常这方面，Python非常宽容，except: 真的会捕获包括 Python 语法错误在内的任何错误。使用 except: 很容易隐藏真正的 bug。

4). 尽量减少 try / except 块中的代码量
try 块的体积越大，期望之外的异常就越容易被触发。这种情况下 try / except 块将隐藏真正的错误。

5). 使用 finally 子句
用 finally 来执行那些无论 try 块中有不发生异常都应该被执行的代码。这对于清理资源常常很有用，例如关闭文件。当捕获异常时，使用 as 而不要用逗号。这在 Python3 里面也是推荐使用的：

```python
try:
    raise Error
except Error as error:
    pass
```


**结论: **

代码的功力不是一朝一夕积累起来的，但是好的编程风格可以很快建立，越早了解越好，可以少走一些弯路，并且减少很多 debug 的时间，因为好的代码风格已经帮助你规避了一些风险，所以要早早养成良好的编程习惯。