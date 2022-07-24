# **day4**
> 问世间，情为何物？直教生死相许。
****

## **日复一日**

循环结构是三大结构中的最后一个，人类的本质是复读机啦。

### **前情导入**
如果这时候这时候要求打印`hello world`114514遍，就算copy，paste也是非常费力的事情。而且很明显这就是重复的动作，因此我们为了摸鱼，就产生了循环结构。

循环结构就是程序中控制某条或者某些指令重复执行的结构。在python中构造循环结构有两种方法，一种是`for-in`循环，一种是`while`循环。

## **for-in循环**

知道循环执行的次数或者对一个容器进行迭代(遍历其中的每一个元素)，一般使用`for-in`循环

经典高斯问题，1-100的累加和，数学上的逆序相加就不说了，现在我们来尝试编程实现

```
sum = 0
for x in range(101):
    sum += x
print(sum)
```

这里的`x`类似C/C++中的`for(int i = 0; i < 100; i++)`中的`i`，本质上是迭代计数器的一种实例体现。关于**range**的使用方法有如下介绍：

|参数类型|作用|
|:-----:|:--:|
|`range(11)`|用来产生0到10之间的整数，注意11是取不到的|
|`range(1,11)`|用来产生1到10之间的整数，注意11仍然是取不到的|
|`range(1,11,2)`|用来产生1到10之间的整数，不过此时每个数字之间的间隔是2|
|`range(10, 0, -2)`|用来产生10到1之间的整数，不过每个数字之间的间隔是2|

总结：`range(start, stop, step)`，start没有给参数的时候默认是0，一定要给出stop的值，然后从start开始产生数，他们之间的间隔由step决定。注意如果是`range(0, 10, -2)`这种，range函数将不会产生任何数字，直接跳出。注意冒号不要忘了。

此时修改前面的条件，要求统计1-100之间的奇数和

```
sum = 0
for x in range(1, 101, 2):
    sum += x
print(sum)
```

当然也可以结合前面的分支结构来实现：

```
sum = 0
for x in range(101):
    if x % 2 == 1:
        sum += x
print(sum)
```

从时间效率上来说，很明显后面的效率更低，一般可以直接构造的循环，我们不考虑分支结构的加入。

## **while循环**

如果循环的次数不知道，那么我们一般使用`while`循环。while循环由一个bool类型的值控制，如果为True，那么循环继续，如果为False，循环终止。

猜数字游戏，其规则就是计算机随机给出1-100之间的数字，由玩家来猜测，计算机会根据玩家输入的数字给出提示，如果玩家猜对了数字，则游戏结束。(很明显，这里并不知道次数会多少，因此选用while循环)

```
import random

num = random.randint(1, 100)
cnt = 0

while True:
    cnt += 1
    temp = int(input('请输入你心中的数字（1-100）：'))
    if temp > num:
        print('大了')
    elif temp < num:
        print('小了')
    else:
        print('猜对了')
        break
```

这里一样的有`continue`和`break`来控制循环，二者的共同点都是后面的代码都不会执行，不过`break`是终端当前循环，而`continue`是直接跳到下一个循环。注意这边的冒号不要忘了。

**嵌套结构**

九九乘法表的代码实现如下：

```
for i in range(1, 10):
    for j in range(1, i+1):
        print(f'{i} x {j} = {i*j}', end = ' ')
    print('')
```

这边也可以用`\t`制表符来使得表格更加美观，与分支结构一样，循环结构的嵌套也是一样的，只要缩进一样，那么就会被认为是一样的代码块，而不是通过达括号来区分。

****
## **课后练习**

判断一个数是不是素数：

```
import math
# 如果是from math import sqrt那么就可以直接使用sqrt
num = int(input("请输入一个数字："))
isPrime = True

for x in range(2, int(math.sqrt(num))):
    if num % 2 == 0:
      isPrime = False
      break

if isPrime and num != 1:
    print('T')
else:
    print('F')
```

求两个数的最大公约数和最小公倍数：

```
a = int(input('a = '))
b = int(input('b = '))

num = a
num2 = b
if a > b:
    num = b
    num2 = a
for x in range(a, 0, -1):
    if a % x == 0 and b % x == 0:
        print('gcd(a,b) is %d' % (x) )

while True:
    if num2 % a == 0 and num2 % b == 0:
        print('lcd(a,b) is %d' % (num2) )
        break
    num2 += 1
```

这里有一个新的交换方法，原先C中的三元交换法，还是麻烦，在python里面可以写成下面得形式

`a, b = b, a`

就可以实现将a的值赋值给b，将b的值赋值给a

打印三角形：

```
for i in range(1, 6):
    for j in range(i):
        print('*', end='')
    print()

for i in range(1, 6):
    for j in range(5, i, -1):
        print(end = ' ')
    for j in range(i):
        print('*', end='')
    print()

for i in range(1, 6):
    for j in range(5, i, -1):
        print(end=' ')
    for j in range(i*2-1):
        print('*', end='')
    for j in range(5, i, -1):
        print(end=' ')
    print()
```
