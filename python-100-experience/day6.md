# **day6**
>落花人独立，微雨燕双飞。
****

## **函数**

这里先来个离散数学组合中最常见的题目：

x1+x2+x3+x4=8，请问一共有几组正整数解？

```
cnt = 0
for i in range(1, 9):
    for j in range(1, 9):
        for k in range(1, 9):
            if 8 - i - j - k > 0:
                cnt += 1
                print('kase %d:' % cnt, i, j, k, 8-i-j-k)
```

仍然是暴力解决，不过学习过相关的组合数只是就知道道最后的答案是`C(7, 3)`，现在尝试编程实现`C(m, n)`的实现

```
m = int(input('input m:'))
n = int(input('input n:'))

num = 1

for i in range(1, m+1):
    num *= i
for i in range(1, n+1):
    num //= i
for i in range(1, m-n+1):
    num //= i
print(f'C({m}, {n}) = {num}')
```

如果我们只是调用一次，那么也就写一次，但是如果我们在main函数中要多次使用组合数求解，那么这段代码要一直copy，paste，重复率极高。

### **函数的意义**

函数的出现很大部分就是为了解决重复代码的问题。或者说，函数的出现也是为了摸鱼。如果我们发现自己的代码中有一些部分的功能类似，所需要的代码类似，只是数据略有不同，此时就可以考虑函数化，然后下次要使用的时候，调用那个函数就可以了。

## **函数的诞生**

### **起名字**

在python中可以使用`def`来定义函数，函数名字的命名规则和变量的命名规则是一样的。通常为下面的构造：

```
def funcname(var1, var2, ..., varn):
  ....
  ....
  return ...
```

其中`funname`中填写的是函数的名字，`var1, var2,...`中是所需要传递的变量名字，这里注意，python中不需要指定变量的类型，只需要给出变量的名字就可以了(注意这里和C中的区别)，最后的`return `是需要通过函数返回的值，注意函数内部的变量如果是按值传递，那么没有return回去赋值的话，原先地方存储的值并不会修改。注意python支持返回多个值。

```
def printlen(a, b, c):
    return a, b

a, b = printlen(1, '2', 3) # 合法的

print(a, b)

```

这样之前的代码就可以编程下面的形式：

```
def fac(n):
    num = 1
    for i in range(2, n+1):
        num *= i
    return num

def C(m, n):
    return fac(m) // fac(n) // fac(m-n)

m = int(input("input m:"))
n = int(input("input n:"))

print('C(%d, %d) = %d' % (m, n, C(m, n)))
```

注意有了函数，我们就有了一种新的编程思想。对于解决一个问题，我们可以先将问题拆分成无数的小问题，然后对于每一个小问题，逐个解决，也就是可以用一个函数来表示解决，那么最后其实就可以先简化成许多函数的罗列，至于函数怎么实现的，就看各自的思想了。

```
getData()
solve()
output()
# 类似这样的一种解决过程
```

### **函数的参数**

python中的函数，同C++中的函数一样，同样支持默认参数的设置。不过要注意，默认参数的设置要在没有默认参数之后。

```
def f(a, b=1):
    ...
# True

def f(b, a=1):
    ...
# False
```

注意默认参数的加入，其实蕴含了函数的重载，也就是说，注意在python中，不允许一个命名空间中拥有两个同名函数，如果有，只会认为最后一个是合法的。

也就是说：

```
def f(a):
    print('world')
def f():
    print('hello')
```

这样子定义出来的函数，python解释器对于f函数的调用认为只有`f()`调用才是正确的，其他的调用都是错误的

在python中，函数的参数可以有默认值，也支持使用可变参数，所以python不想C/C++一样需要支持函数重载来实现。关于函数重载，参考下面的代码

```
def add(a=0, b=0, c=0):
    return a + b + c

print(add()) # 调用的实质上是add(0, 0, 0)
print(add(1)) # 调用的实质上是add(1, 0, 0)
print(add(1, 2)) # 调用的实质上是add(1, 2, 0)
print(add(1, 2, 3)) # 调用的实质上是add(1, 2, 3)
print(add(b=1, a=2, c=3)) # 调用的实质上是add(2, 1, 3)
```

我们会发现虽然我们只定义了一个函数，但是我们可以使用`add()`,`add(a)`,`add(a, b)`和`add(a, b, c)`这四个函数，这就是函数的重载。注意python中还有一个特殊的地方，那就是传递参数的时候，我们可以不按照指定的顺序进行传递，而是可以自己指定传递到顺序，即最后一个例子`print(add(b=1, a=2, c=3))`，非常自由。

python中的函数参数还支持可变参数。这里对可变参数进行一个简要的介绍，因为涉及到数据的存储结构，笔者没有进行详细的了解，后面将会补上更加详细的解释。

函数参数有三种

|参数类型|参数的数据结构&存储对象|
|:-----:|:-------------------:|
|`args`|常规参数，接收一个对象，比如`1`，`asd`之类的|
|`*args`|可变参数，本质上是一个元组，可以接收任意多个参数|
|`**args`|可变参数，本质上是一个字典，接受的数据为`a = 123`之类的|

```
def f(a, *b, **c):
    print(a)
    print(b)
    print(c)

f(1, 2, 'a', 'bc', d = 123, e = 'asd')
'''
output:
1
(2, 'a', 'bc')
{'d': 123, 'e': 'asd'}
'''
```

注意这边的顺序，一般然说常规参数在最前面，之后是元组类型的可变参数，最后才是字典类型的可变参数。了解了上述的可变参数的知识，我们就可以将之前的add函数改的更加强大。那就是可以接收任意多的参数(如果是合法的话，你要输入字符串类型，那就暂时没办法了)

```
def add(*args):
    total = 0
    for i in args:
        total += i
    return total

print(add())
print(add(1))
print(add(1, 2))
print(add(1, 2, 3))
print(add(1, 2, 3, 4))
print(add(1, 2, 3, 4, 5))
```

### **模块管理函数**

世界上同名的人非常多，函数也是一样的，python遇到命名冲突的时候，后面的函数定义会覆盖前面的函数定义(没办法，python并没有函数重载的概念)。

命名冲突我们通常是通过模块(命名空间)来解决的。对于python来说，每个文件就代表了一个模块，我们可以在不同的模块中拥有同名的函数，使用函数的时候我们通过`import`来导入具体使用哪个模块中的函数，例子如下：

`module1.py`

```
def foo():
    print('hello')
```

`module2.py`

```
def foo():
    print('goodbye')
```

`module3.py`

```
from module1 import foo
foo()
from module2 import foo
foo()

'''
output:
hello
goodbye
'''
```

注意将这三个文件放在同一个文件夹下面，然后运行第三个文件`module3`，这就是通过模块来调用不同的同名函数的使用。

当然也可以通过下面的方式来调用不同模块中的同名函数。

```
import module1
import module2
module1.foo()
module2.foo()
'''
import module1 as m1
import module2 as m2
m1.foo()
m2.foo()
# 这样也是可以的，减少打字
'''
```

需要注意的是，如果是用`from ... import`的形式，那么后面导入的同名函数将会覆盖前面的同名函数，也就是说：

```
from module1 import foo
from module2 import foo
foo()

'''
output:
goodbye
'''
```

这里后导入的`module2`中的foo函数将前面从`moduld1`中导入的foo函数给覆盖了，所以此时调用foo函数调用的是后面导入的foo函数，而不是之前导入的foo函数。注意如果此时在`module3.py`这个文件中同样定义了foo函数，那么最近一次调用foo函数，系统认为的是从调用开始往上，最先出现的foo函数的定义的地方就为这里foo函数真正执行的操作。

```
from module1 import foo
def foo():
    print('hello, goodbye')
from module2 import foo
foo()

'''
output:
goodbye
'''
```

注意这边import的导入，除了导入了定义的函数之外，我们同时还导入了可执行的代码。python解释器在导入的时候，同时也会执行这些可执行代码，很明显，在大多数情况下，我们并不希望这样意外的情况发生，尽量减少bug的出现，虽然说能够运行就是成功。

我们通常的情况就是将会执行的代码段加入下面的语句之下：

`if __name__ == '__main__:'`

### **pass**

这里再插入一个小知识点，很明显我们发现如果我写了下面的语句

`if a > 10:`

但是我还没想好`a > 10`的时候程序需要执行什么，我想先看看其他地方运行情况，此时点击运行会出错，python对于这种情况，特意给出了一个关键字`pass`，这相当于C/C++中的空语句，就是我什么都不做，只是占个位置，仅此而已。

```
if a > 10:
    pass
```

这样就可以运行了。

### **__main__**

回到刚才的话题，那么为了不让意外的代码被执行，我们一般采用这样子的方式：

`module1.py`

```
def foo():
    print('hello world')

if __name__ == '__main__':
    print('goodbye world')
```

`module3.py`

```
from module1 import foo
foo()
```

此时的输出就只有`hello world`啦，这里的`if __name__ == '__main__'`中的`__name__`是python中的一个隐含变量，他表示模块的名字，只有被python解释器直接执行的模块的名字才会是`__main__`

****

## **课后练习**

**写出求最大公约数和最小公倍数的函数形式**

```
def gcd(a, b):
    if a > b:
        a, b = b, a
    for i in range(a, 0, -1):
        if a % i == 0 and b % i == 0:
            return i

def lcd(a, b):
    return a * b // gcd(a, b)
```

**写出判断一个数是不是回文数的函数形式**

```
def check(a):
    b = 0
    c = a
    while c:
        b = c % 10 + b * 10
        c //= 10
    if a == b:
        return True
    else:
        return False
```

**写出判断一个数是不是素数的函数形式**

```
import math
def isPrime(num):
    if num == 1:
        return False
    for i in range(2, int(math.sqrt(num)+1)):
        if num % i == 0:
            return False
    return True
```

## **变量作用域**

```
def foo():
    b = 'hello'
    def bar():
        c = True
        print(a)
        print(b)
        print(c)
    bar()

if __name__ == '__main__':
    a = 100
    foo()

'''
output:100
hello
True
'''
```

注意bar函数中并没有直接定义a，b两个变量，但是我们可以访问他们，这与python中的变量作用域有关。变量a所在的地方定义的地方称为全局变量，属于全局作用域(本质上就是没有定义在任何一个函数内的，就叫做全局变量)，foo函数中定义的变量b我们叫做局部变量(一般定义在函数内部的，都是局部变量)，属于局部作用域，在函数外部没法访问到。但是对于foo函数内部的bar函数来说，b属于嵌套作用域(因为bar函数内部是局部变量域，而定义在foo函数的变量对于foo函数本身是局部变量域，对bar函数来说就不能说是局部变量域了，所以这时候我们给了一个新的名字，嵌套作用域)，同理bar中的c对于bar来说就处于局部作用域。

一般来说，python查找一个变量的时候会按照**局部作用域**，**嵌套作用域**，**全局作用域**和**内置作用域**的顺序进行进行搜索。所谓的内置作用域就是说python内置的那些标识符，之前所用过的`input`,`print`,`int`都属于内置作用域。

虽然这样说，但是下面的代码并不会修改a的值

```
def foo():
    a = 200
    print(a)

a = 100

foo()

print(a)
```

事实上，这是符合前面所说的作用域的，因为对于python来说`a = 100`，这条语句可以有两种解释，一种是修改a的值，一种是创建一个变量名为a，存储的值为100的变量。所以在foo函数中的a，python解释器认为是新定义的变量a，他的作用域是局部变量域。如果，我们希望通过foo函数来修改全局变量域中的a，可以采用下面的方式

```
def foo():
    global a
    a = 200
    print(a)

a = 100

foo()

print(a)
```

我们可以使用`global`关键字来说明foo函数中的a来自于全局作用域，如果全局作用域中没有a，那么下面一行的代码就会定义变量a并将其放于全局作用域。注意global是参与声明，也就是说`global a`可以，但是`global a = 100`是不允许的。

```
def foo():
    global a
    a = 200
    print(a, 'foo')

def bar():
    print(a, 'bar')

foo()
print(a, 'main')
bar()
```

这边就是全局作用域中没有a，但是我在函数中申明了a是全局作用域的，因此后面系统自动在全局作用域中创建了一个全局变量a

同理嵌套作用域也有自己的关键字`nonlocal`

```
def foo():
    a = 100
    def bar():
        nonlocal a
        a = 200
        print(a)
    bar()
    print(a)

foo()
```

当然目前主流的思想对于全局变量的使用是尽量减少，因为全局变量对于所有人来说都是可以访问，以及可以修改的。非常不稳定，容易造成一些奇怪的bug。同时全局变量的生命周期远比局部变量长很多，如果不长时间使用，就会造成内存使用效率低下。减少全局变量，也就是局部变量的增多，但是如果我们希望将一个局部变量的生命周期延长，使其在定义它的函数调用结束后依然可以使用它的值，这时候我们就需要使用闭包。

往后推荐的格式为：

```
def main():
    pass

if __name__ == '__main__':
    main()
```

以后的代码可以书写在`def main():`下面

### **闭包&匿名函数**

- #### **匿名函数**

使用关键字`def`定义的函数时**具名函数**，具有函数名字，而可以方便我们多次调用，**匿名函数**没有具体的名字，往往用于一次性实现某种功能的场合。合理的使用匿名函数，可以大大简化代码的复杂度，提高代码可读性(说白了，一切为了摸鱼)。

匿名函数的关键字是`lambda`，好吧，C++中的`lambada`函数，老lambda了，久远的回忆。

语法格式如下：

`lambda arg1, arg2, ..., argn : expression`

比如：

```
f = lambda x, y: x + y # 这里的变量就是一个函数变量

print(f(1, 2))
```

匿名函数lambda和常规函数差不多，用法也是类似的，不过需要注意的是匿名函数是一个表达式，而不是一个语句。也就是说，匿名函数只能做表达式的功能，而难以做到类似选择，循环之类的高级一点的功能。但是由于匿名函数lambda本质上就是一个表达式，所以其可以作为列表或者某些函数的参数。

```
def foo(x, y):
    return x+y

f = lambda x, y : x + y

def fun(a):
    print(a(2, 3))

def main():
    fun(foo)
    fun(f)

if __name__ == '__main__':
    main()
```

上面的例子就是作为函数的参数传递，可以将lambda函数看成对于一个复杂表达式的别名，它所作的是一些较为简单的任务(相对于def函数来说，毕竟你让一个匿名函数循环输出hello world，是强人所难的啦)。

- #### **闭包**

闭包的形成首先需要一个嵌套函数，由内嵌函数和外部函数定义时候的环境变量构成，总的来说有三个条件：

- 首先得有一个内嵌函数
- 同时内嵌函数必须使用外部函数中定义的变量(自由变量)
- 最后外部函数返回内嵌函数

```
def pre():
    a = 25
    def insert(x):
        return x * x * a

    return insert

print(pre()(2))
```

这里的自由变量指的是未在本地作用域绑定的变量。比如这边的变量a，a绑定的是pre，也就是对于pre来说，a是局部变量，但是对于insert来说a就是自由变量，a和insert没有绑定关系。

注意我们还可以这样调用

```
f = pre()
print(f(2))
```

这里pre函数已经结束了，但是我们仍然通过f函数来使用里面的变量a，也就是a的生命周期被我们通过闭包延长了。

```
def pre(a):
    def insert(x):
        return x * x * a

    return insert

f = pre(3)

print(f(2))
```

> 遗忘才是真正的死亡

f记住了pre，a的生命周期延长了，如果f消失了，那么a的生命周期一样到此终结，找不回来了。

> 不求同日生，但求同日死
