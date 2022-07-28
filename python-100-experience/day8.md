# **day8**
> 醉后不知天在水，满船清梦压星河。
****

## **入派**

学过C知道面向过程，学过C++知道面向对象。接下来讲述的便是面向对象的思想。

面向对象更加贴近于生活，与面向过程中的方法集合的不同，面向对象，倾向于将方法与数据封装在一起。即概括出一种类别，比如动物，然后动物下可以延伸出海鸥，猴子等对象。

> 一切的程序，本质上来说，不过是现实世界的模拟。你的世界怎样，你的程序就该怎样。

程序是指令的集合，为了简化程序的设计，我们引入了函数的概念。但是这样还是不够方便，于是我们加入了对象的概念，也就是说此时我可以通过对象来指明做什么事情，使得编程的门槛更加通俗易懂。我们不断地将指令泛化，试图与自然语言形成一种复杂地映射。同时也是不断地利用前人地经验，比如说在C++中，排序地时候，我可以不知道排序算法，调用sort函数就可以了。这时候，我们考虑地方面是更加高层地一种高度集合指令地排列。当然，这并不是终点，编程语言与自然语言地映射地路还有很长。

### **类和对象**

对象是类的实例，类是对象的抽象化模板。java中有万物皆对象的思想，在面向对象的流派中，一切的东西都是对象，都具有方法和属性(也可以只有其中的一种)，每个对象都是独一无二的，而其中有一些对象因为拥有相同的方法和属性存储需求，因此我们将他们的集体抽象为类。

## **教义**

### **类定义**

在python中可以使用`class`来定义类。类中的方法的定义和前面的函数的定义是一样的。

```
class Student(object): # 之所以写成class Student(object)是为了让Student继承object类拥有更多的属性，如果没有这么多的需求，那么本质上直接class Student()也是可以的
    a = 1
    b = 2
    c = "hello world"  # 定义属性成员(注意这是类的属性)
    def __init__(self, name, age): # 这是一个特殊的方法，用于在创建对象的时候进行初始化操作
        self.name = name
        self.age = age # 通过初始化方法，我们可以让学生对象绑定name和age两个属性

    def sayhello(self):
        print(f'hello, I\'m {self.name}, my age is {self.age}')
```

上面就是基本的类定义，以及类的初始化，类中的函数成员和属性成员的定义。

### **创建和使用对象**

```
class Student(object): # 之所以写成class Student(object)是为了让Student继承object类拥有更多的属性，如果没有这么多的需求，那么本质上直接class Student()也是可以的
    a = 1
    b = 2
    c = "hello world"  # 定义属性成员(注意这是类的属性)
    def __init__(self, name, age): # 这是一个特殊的方法，用于在创建对象的时候进行初始化操作
        self.name = name
        self.age = age # 通过初始化方法，我们可以让学生对象绑定name和age两个属性

    def sayhello(self):
        print(f'hello, I\'m {self.name}, my age is {self.age}')

def main():
    stu1 = Student('hh', 18)
    stu1.sayhello()
    print(stu1.c)
    print(Student.c)

if __name__ == '__main__':
    main()
```

定义好类后，我们可以创建对象，这里的方法和C/C++中是类似的，同时调用也是一样的。这里也能体现对象的思想，如果我们假设对方已经将该对象的类实现好，那么我们现在只要告诉这个对象要做什么就可以了，怎么实现的我们不需要去管。

### **访问可见性问题**

C++中对于类成员的访问有着明确的规定，而在python中，其访问权限只有私有和公开，如果希望是私有的就在命名前加`__`，这样外界直接访问的时候就会报错

```
class Student:
    def __init__(self, name):
        self.__name = name

    def __sayhello(self):
        print('hello world')

def main():
    stu = Student('me')
    # print(stu.__name)
    # stu.__sayhello

if __name__ == '__main__':
    main()
```

但是python语法上并没有提供私有属性严格的保护机制，所以我们换一个名字就可以访问私有属性了

```
class Student:
    def __init__(self, name):
        self.__name = name

    def __sayhello(self):
        print('hello world')

def main():
    stu = Student('me')
    # print(stu.__name)
    # stu.__sayhello()
    print(stu._Student__name)
    stu._Student__sayhello()
if __name__ == '__main__':
    main()
```

也就是通过`_类名+私有属性名`就可以像前面的访问方式正常访问了，当然正常使用中，我们一般不讲属性设置成为私有，这样子会使得子类无法访问。一般情况下，我们人为认为单下划线开头的属性或者方法是受保护的，本类之外的代码访问的时候需要注意。不过这只是建议，在语法上并没有任何保障措施。

## **三大天王**

面向对象由三大天王构成，封装，继承，多态。封装本质上就是我对于自己创建的类，我自己将属性和方法封装在一起。也就是平常我想要让这个对象排序，可能我要向怎么排序好，需要自己构想，但是封装就是此时我只需要和该对象说排序就可以了，至于这个对象怎么实现排序的，和我没有关系(假设此时我是使用者)。

****

## **课后练习**

**数字时钟**

```
from time import sleep
import turtle as t

class Clock(object):
    def __init__(self, hour, min, sec):
        self.hour = hour
        self.min = min
        self.sec = sec

    def addsec(self):
        self.sec += 1
        if self.sec >= 60:
            self.sec -= 60
            self.min += 1
        if self.min >= 60:
            self.min -= 60
            self.hour += 1
        if self.hour >= 24:
            self.hour -= 24

    def show(self):
        a = str(self.hour)
        b = str(self.min)
        c = str(self.sec)
        return '%02d : %02d : %02d' % (self.hour, self.min, self.sec) # 注意还有这种返回方式
        # return a.rjust(2, '0')+' : '+b.rjust(2, '0')+' : '+c.rjust(2, '0')

def main():
    clock = Clock(0, 0, 0)
    t.delay(0)
    t.penup()
    t.speed(0)
    t.hideturtle()
    t.right(180)
    t.forward(200)
    t.right(180)
    t.pendown()
    while True:
        t.clear()
        t.write(clock.show(), font=("Arial", 64))
        clock.addsec()
        sleep(1)
if __name__ == '__main__':
    main()
```

**为平面上的点建立对象**

```
from math import sqrt

class Point(object):
    def __init__(self, x, y):
        self.x = x
        self.y = y

    def setx(self, x):
        self.x = x

    def sety(self, y):
        self.y = y

    def dist(self, point):
        return sqrt((self.x-point.x)**2+(self.y-point.y)**2)

def main():
    point1 = Point(0, 0)
    point2 = Point(1, 1)
    print(point1.dist(point2))
    point2.setx(3)
    point2.sety(4)
    print(point1.dist(point2))

if __name__ == '__main__':
    main()
```


注意下面这种对于if的使用方法：(if可以简化赋值的时候对于值是否合法的判断)
```
a = int(input())
b = a if a > 0 else 0
print(b)
```

### **装饰器**
- @property定义只读属性
- @setter定义可读可写属性
- @deleter定义可读可写可删属性

上面所列举的都是装饰器

```
class Test:
    def __init__(self, age = 12, name = 'hh'):
        self._age = age
        self._name = name
    @property
    def hello(self):
        print('hello world')

    @property
    def f(self):
        return self._age

    @f.setter
    def f(self, age):
       self._age = age

    @property
    def name(self):
        return self._name
    @name.setter
    def name(self, name):
        self._name = name
    @name.deleter
    def name(self):
        del self._name

def main():
    test = Test() # Test(12, 'hello')
    test.hello # 装饰函数的第一种用法 @property 可以让方法的调用和成员一样，注意这样需要函数没有要传递的参数
    print(test.f)
    test.f = 18
    print(test.f)
    test.name = '12345'
    print(test.name)
    del test.name
    test.name = '234'
    print(test.name)

if __name__ == '__main__':
    main()
```

本质上就是将一个函数装饰成类似属性

### **获取本地时间的方法**

首先借用`time.time()`获取本地时间

然后借用`time.localtime(time.time())`将其直接转换为我们平常所认识的年月日

```
tm = time.localtime(time.time())
tm.tm_hour # 时
tm.tm_min # 分
tm.tm_sec # 秒
```

### **析构函数&控制输出**

```
class Student(object):
    def __init__(self):
        print('create')
    def __del__(self): # 析构函数
        print('delete')
    def __str__(self): # 输出控制
        return "hello world"

def f():
    stu = Student()

def main():
    stu = Student()
    print(stu)
    del stu
    f()

if __name__ == '__main__':
    main()
```

- `__del__` 析构函数
- `__str__` 控制输出的时候的格式

### **类的另外一种定义方式**

```
def study(self, work):
    print(f'{self._name} study {work}')

def foo(self, name):
    self._name = name

class Test(object):
    def __init__(self):
        pass
    def goonnext(self):
        pass

def main():
    Student = type('Student', (object, ), dict(__init__ = foo, study = study))
    stu = Student('hello')
    stu.study('world')
    print(Test)

if __name__ == '__main__':
    main()
```

当type有三个参数的时候返回一个类对象

`type(name, object, dict)`

name是类名，object是父类，dict存储的是方法和属性对应形成的键值对
