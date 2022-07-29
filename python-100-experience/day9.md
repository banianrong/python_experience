# **day9**
>竹杖芒鞋轻胜马，谁怕？一蓑烟雨任平生。
***

## **教主之位**

前天只是初步了解面向对象这种思想，今天将要对于面向对象进行更深入的阐释，毕竟面向对象的教主之位可没有那么好拿的。

### **@property装饰器**

该问题是对前面python属性和方法访问权限的延申，毕竟虽然一般不将属性设置为私有，但是如果直接由外界修改我们的属性值是有很大风险的，比如规定属性i为正数，但是外界可以直接修改i的值为负数，这样会造成程序的崩溃。我们是人为的增加单下划线说明不希望外界直接访问，而是通过属性的getter(访问器)和setter(修改器)来访问，增加数据的安全性。这就要用到我们的`@property`装饰器语法(之前有写到过)

```
class Student(object):

    def __init__(self, name, age):
        self._name = name
        self._age = age

    @property
    def name(self):
        return self._name

    @property
    def age(self):
        return self._age

    @age.setter
    def age(self, age):
        self._age = age

    def study(self):
        if self._age <= 16:
            print('%s正在看书' % self._name)
        else:
            print('%s正在读书' % self._name)

def main():
    student = Student('hello', 13)
    student.study()
    student.age = 19
    student.study()

if __name__ == '__main__':
    main()
```

这里@property就是将函数给装饰成属性，此时该属性自带只读功能，如果加入setter，那么就可以拥有可写功能，最后deleter则是增加删除功能。

### **__slots__强制绑定**

```
class f:
    def __init__(self):
        print("create")
    def __del__(self):
        print("delete")

def main():
    F = f()
    f.a = 1
    print(f.a)

if __name__ == '__main__':
    main()
```

观察上面的代码我们发现F对象本身没有a属性，但是我们可以让它动态绑定新的方法或者属性。如果我们需要先定自定义类，让其中只绑定某些属性，那么就要通过`__slots__`

```
class f(object):
    __slots__ = ('_name')
    def __init__(self, name):
        self._name = name
        print("create")
    def __del__(self):
        print("delete")

def main():
    F = f()
    # F.a = 1 # error
    # print(F.a)

if __name__ == '__main__':
    main()
```

使用`__slots__`的时候，只有括号中的变量名可以被绑定，其他的变量名不能被绑定，这仅仅是针对当前类的对象来说。

```
class f(object):
    __slots__ = ('_name')
    def __init__(self, name):
        self._name = name
        print("create")
    def __del__(self):
        print("delete")

def main():
    F = f('hello')
    # F.a = 1 # error
    # print(F.a)
    f.a = 12
    print(F.a)

if __name__ == '__main__':
    main()
```

我们还是可以通过类名来动态绑定，同时子类不会收到父类绑定的影响，只要子类不指定__slots__就可以

```
class f(object):
    __slots__ = ('_name')
    def __init__(self, name):
        self._name = name
        print("create")
    def __del__(self):
        print("delete")

class A(f):
    __slots__ = ('_age')
    def __init__(self):
        print('son create')


def main():
    AA = A()
    # AA.c = 18 # 如果没有重新指定__slots__，子类不受父类影响，随便定义
    # print(AA.c)
    print(AA.__slots__)
    AA._age = 12 # 如果子类重新指定__slots__，那么子类绑定的对象就只能是父类加上子类
    AA._name = 'na'
if __name__ == '__main__':
    main()

```

### **静态方法和类方法**

#### **静态方法**

我们`def`定义的方法本质上是属于类对象的，也就是说如果没有对象之前，我们是没有办法通过类直接使用这些方法，但是有些时候我们需要在创建对象之前判断对象是否合法，因此我们引入了静态方法来解决这个问题。

```
class Tri(object):
    def __init__(self, a, b, c):
        self._a = a
        self._b = b
        self._c = c

    @property
    def a(self):
        return self._a

    @a.setter
    def a(self, a):
        self._a = a

    @a.deleter
    def a(self):
        del a

    @staticmethod
    def isTri(a, b, c):
        return a + b > c and b + c > a and c + a > b

    def f(self):
        print('hello world')

def main():
    if Tri.isTri(3, 4, 5):
        tri = Tri(3, 4, 5)
        tri.f()
        Tri.f(tri)

if __name__ == '__main__':
    main()
```

静态方法之前需要`@staticmethod`修饰，表示这是一个静态方法，同时注意这里的参数之前不是self。同时，注意静态方法和类方法都是通过类名调用的，所以我们要使用也是通过类名来访问，不过是创建对象之前先访问一下类这样是否合法罢了。

当然也不是说不能间接通过类名调用一般方法，不过此时我们调用的方法里面的第一个参数要加入一个对象，也就是self此时不是系统帮忙传递，而是要我们手动指定。这也是符合逻辑的，一般方法本身就是要求对象存在，才可以调用的，传递对象，本质上就是使用对象的一般方法，只不过是不同的写法罢了。

当不需要对象，也不需要使用到类对象的时候我们一般使用静态方法，减少内存消耗。

#### **类方法**

```
import time

class Clock(object):
    def __init__(self, hour, min, sec):
        self._hour = hour
        self._min = min
        self._sec = sec

    @classmethod
    def systemclock(cls):
        tm = time.localtime(time.time())
        return f'{tm.tm_hour} : {tm.tm_min} : {tm.tm_sec}'

def main():
    print(Clock.systemclock())

if __name__ == '__main__':
    main()

```

类方法的模板就是，在函数之前加上`@classmethod`修饰，同时注意此时约定第一个参数是cls，代表当前类相关的信息的对象(类本身也是一个对象，不然怎么叫万物皆对象，也叫做元数据对象)，通过这个参数我们可以获取类的相关信息，以及创造出类的对象。

也就是我们可以通过cls这个参数来创建对象

## **关系**

类和类之间的关系包括：

- 继承关系(泛化)，也就是从原先的类中引申出另一个类，比如从人引申出学生这个关系

- 关联关系，是整体和部分的关系(聚合关系)，如果整体负责了部分的生命周期，那么这就是最强的关联关系叫做合成关系。

- 依赖关系，a的操作利用到了b，a和b构成依赖关系

### **继承和多态**

#### **继承**

继承是一种减少重复代码的方式，就是让另一个类拥有另一个类的方法和属性，同时可以定义自己的属性和方法。

```
class People(object):
    def __init__(self, name, age):
        self._name = name
        self._age = age

    def hello(self):
        print('hello, I\'m %s' % self._name)

class Student(People):
    def __init__(self, name, age, grade):
        # self._name = name
        # self._age = age
        super().__init__(name, age)
        self._grade = grade

def main():
    stu = Student('hello', 18, 6)
    stu.hello()

if __name__ == '__main__':
    main()

```

可以调用父类`super()`的初始化方法来进行初始化，或者自己一个个手动写过去，建议父类的方法，因为可以少写好多字。这边的继承目前和C++类似，但是不确定细节方面是否大致一样。

#### **多态**

```
class People(object):
    def __init__(self, name, age):
        self._name = name
        self._age = age

    def hello(self):
        print('hello, I\'m %s' % self._name)

class Student(People):
    def __init__(self, name, age, grade):
        super().__init__(name, age)
        self._grade = grade

    def hello(self):
        print('hello, I\'m %s in grade %d' % (self._name, self._grade))


class Teacher(People):
    def __init__(self, name, age, school):
        super().__init__(name, age)
        self._school = school

    def hello(self):
        print(f"hello, I'm {self._name} in school {self._school}")

class Parent(People):
    def __init__(self, name, age, child):
        super().__init__(name, age)
        self._child = child

    def hello(self):
        print(f"hello, I'm {self._name}, {self._child}'s parent")

def main():
    list1 = [Parent('c', 35, 'a'), Student('a', 10, 6), Teacher('b', 36, 'xxx')]
    for i in list1:
        i.hello()

if __name__ == '__main__':
    main()

```

子类在继承父类的方法，同时也可以对父类的方法进行重写。注意，因为python非常强大的动态绑定，所以这里的多态和C++中的略微有点差异，但是大体上就是，继承自同一父类，但是在同一方法表现上，由于不同的类的对象而产生了不同的行为。这就是多态的定义。
