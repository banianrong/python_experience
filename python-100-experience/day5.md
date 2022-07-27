# **day5**
> 昨夜西风凋碧树，独上高楼，望尽天涯路。
****

## **让知识去旅行**

> 顺序，分支，循环，构成了程序之美

顺序，分支，循环结构学完，理论上大多数的程序都可以自己编程实现了，惊不惊喜，意不意外。

之所以感到诧异，是还没有养成从01的角度看待这个世界。想想之前所学，变量，类型，运算符，表达式，顺序结构，分支结构，循环结构，这些都是从日常生活中的经验不断抽象出来的范式(或者说一种总结)。我们现在需要做的就是尝试从01的角度看待这个世界。

听起来比较抽象，但是总结出来也就是一句话

> 按照自己的思维去coding，你是怎么想的，机器也是如此。程序只是我们思维的延申。

### **一些栗子**

#### **水仙花数**

老生常谈的话题了，堪比`hello world`的出场率。

水仙花数：如果一个三位数，该数字每个位上的数字的立方之和恰好等于它本身，那么这个数字就是水仙花数

能否找齐所有的水仙花数呢？

```
for i in range(100, 1000):
    a = i % 10
    b = i // 10 % 10
    c = i // 100
    if c ** 3 + b ** 3 + a ** 3 == i:
        print(i)
```

最简单的方法就是从100一直枚举到999，把每个数字判断过去是否是水仙花数，如果是则输出，否则不输出。难点是如何取出每个数位上的数字，这里善于利用整除和取余的性质就好了，具体见上面的代码。

对于数位上还有一个有意思的题目，给出一个数字要去输出他的回文串(123的回文串就是321)

```
a = int(input("请输入一个数字："))

b = 0
while a:
    b = a % 10 + b * 10
    a //= 10
print(b)
```

|运算符号|作用|
|:-----:|:--:|
|`//`|一般是位移作用，也就是如果想要取出十位上的数字，那就除以10，如果是百位上的数字，那就除以100|
|`%`|与整除配套使用，对10取余就能去除最后的数字了|

### **百钱百鸡**
小学的噩梦重现，这回会成为程序的噩梦吗？

公鸡5元一只，母鸡3元一只，小鸡一元三只，用100块钱买100只鸡，问公鸡，母鸡，小鸡各要买多少只

> 枚举过百万，暴力碾标算

```
for i in range(100//5+1):
    for j in range(100//3+1):
        if i * 5 + j * 3 > 100:
            break
        if (100 - 5 * i - 3 * j) * 3 == 100 - i - j:
            print(f'公鸡{i}', f'母鸡{j}', f'小鸡{100-i-j}')
```

暴力枚举完事，记得判断条件即可。注意python中的除法出来的结果仍然可以与整数进行比较，即

```
6/2.1 == 3 # False
6/2 == 3 # True
```

另外，插入一条print函数的用法：

`print('%d' % (i), '%d' % (j))`

这就是print之间有分隔的时候的格式化输出格式，了解即可

如果不考虑时间的情况下，枚举非常受欢迎，只要确定答案存在，那么剩下的就交给时间，把每一种情况枚举出来，总能找到对的那个。

> 众里寻他千百度。蓦然回首，那人却在，灯火阑珊处。

我会一直找下去的。一直一直，直到自然规律的降临，直到你的出现。

### **CRAPS赌博游戏**

规则如下：玩家第一次摇骰子(注意一次是两枚)摇出了7点或者11点，玩家赢，如果摇出2点，3点，12点那么庄家赢，其他点数继续。第二次之后，如果玩家摇出了7点，庄家胜，如果玩家摇出了第一次摇的点数，玩家胜，一直摇到决出胜负为止。

```
from random import randint

money = 10000
sign = True
while sign:
    if money <= 0:
        break
    print('你的资产为:%d' % (money))
    real = True
    while real:
        debt = int(input("请输入本轮投入金额："))
        if debt > 0 and debt <= money:
            real = False
        else:
            print('本轮无效，请重新输入：', end='')
    flag = 0
    real = True
    while True:
        a = randint(1, 6)
        b = randint(1, 6)
        c = a + b
        print('你摇出了%d点' % c)
        if flag == 0:
            if c == 7 or c == 11:
                real = True
                break
            elif c == 2 or c == 3 or c == 12:
                real = False
                break
        else:
            if c == 7:
                real = False
                break
            elif flag == c:
                real = True
                break
        flag = c
    if real:
        print('你赢了，鸿运当头')
        money += debt
    else:
        money -= debt
        if money > 0:
            print('可惜，只差一点，下次一定可以赚回来')
        else:
            print('下辈子吧')
print('你没钱了，再见')

```

****

## **课后练习**

**斐波那契数列**

生成斐波那契数列的前20个数

```
a = 1
b = 1
print(a, b, sep='\n')
for i in range(18):
    a, b = b, a+b
    print(b)
```

**找出10000以内的完美数**

完美数：它的所有真因子(除了自身以外的所有因子)的和恰好等于它本身。如`6=1+2+3`

```
for i in range(1, 10001):
    cnt = 0
    for j in range(1, i // 2+1):
        if i % j == 0:
            cnt += j
    if cnt == i:
        print(i)
```

**输出100以内所有的素数**

素数：因子只包括1和自己本身

```
for i in range(2, 101):
    flag = True
    for j in range(2, int(i ** 0.5)+1):
        if i % j == 0:
            flag = False
            break
    if flag:
        print(i)
```