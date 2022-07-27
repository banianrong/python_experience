# **day7**
> 江南无所有，聊赠一枝春。
****

## **朋友**

温馨提示：接下来将会有大量新朋友加入

### **字符串**

计算机除了数值计算外，如今还有许多的文本操作，这就促使**字符串**这种数据对象的诞生

字符串在python中的表示方式一般通过单引号`'`，双引号`"`，三引号`'''`或者`"""`来表示，当然字符串直观来看，就是一堆字符的集合。(注意只有三引号才能换行，其他的形式不行)

```
a = 'hello world'
b = "hello world"
c = """
  hello
  world
"""

print(a, b, c, sep='\n')
'''
output:
hello world
hello world

  hello
  world

'''
```

#### **转义字符`\`**

##### **后面加入字符**

转义字符都是借由`\`开头，来进行转义的，转义的含义就是说之后的字符不是原来的含义了。比如`\n`，就变成了换行符，`\t`就变成了制表符，同时如果想要输出`\`，就必须写成`\\`，同样python想要在单引号输出`'`，就必须用这样的方式`\'`

```
s1 = 'I\'m hungry!\\'
print(s1)
'''
output:
I'm hungry!\
'''
```

##### **后面加入数字**

在`\`后面也可以加入八进制或者十六进制数字来表示字符。其中八进制有三个数字位，而十六进制前面加一个`x`然后两个数字位

```
s1 = '\141\142' # 八进制
s2 = '\x61\x62' # 十六进制

print(s1, s2)
'''
output:
ab ab
'''
```

### **原始字符串**

如果不希望出现上面转义的情况，我们可以通过原始字符串来实现，也就是在字符串前面加上r来修饰，这样就会输出原始的内容

```
s1 = r'I\'m hungry!\\'
print(s1)
'''
output:
I\'m hungry!\\
'''
```

### **和字符串相关的运算符**

|运算符|功能|
|:---:|:--:|
|`+`|实现字符串的拼接|
|`*`|重复字符串内容，注意跟的类型是整型，不然会报错|
|`in`,`not in`|判断一个字符串是否包含另一个字符串(成员运算)|
|`[]`|从字符串中取出某个字符(切片运算)|
|`[:]`|从字符串中取出某些字符(切片运算)|

可以通过下面的程序来测试：

```
s1 = 'hello' * 3
print(s1)

s2 = 'world' * 3
print(s2)

s1 += s2
print(s1)

print('lloworl' in s1)
print('a' in s1)
print('llo' not in s1)
print('a' not in s1)

s3 = '123456789'

print(s3[2])
print(s3[2:])
print(s3[2: : 2])
print(s3[ : : 2])
print(s3[ : : -1])
print(s3[-1])
print(s3[0])
print(s3[-1:-3:-1])
print(s3[-3:])
```

#### **切片运算**

这边对于切片运算做一些解释：

- 首先切片运算本质上有三个参数：`[a:b:c]`
- a控制的是起始位置，b控制的是终止位置，注意这边的范围是[a,b)，也就是左闭右开，是不包括下标为b的内容，c控制的是步长，也就是取出来的每个元素的相邻位置是多少
- 但是注意在python中，下标不只从0开始(也就是下标不一定都是正的)，下标也可以是负数，此时他是从[-len, -1]，这里的len指的是字符串的长度，而常规的是[0, len-1]，所以我们也可以进行逆序操作，也就是`s3[::-1]`，就可以很方便的获得字符串的逆序，这里的a默认是0或者-len开始，b默认一直到尽头，c默认是1）

在python中的字符串还有以下函数处理：

```
str1 = 'hello, world! world'

print(len(str1)) # len计算字符串的长度

print(str1.capitalize()) # 注意这里是将字符串的首字母变大写

print(str1.title()) # 将每个单词的字母变大写

print(str1.find('world')) # 寻找字符串中有没有类似的字串，如果存在，返回第一次出现的下标
print(str1.find('wld')) # 如果不存在，返回-1

print(str1.index('world'))
# print(str1.index('wld')) # 与find类似的作用，但是如果源字符串里面没有这个字符串，就会报异常

print(str1.startswith('hello'))
print(str1.startswith('world')) # 检查字符串是不是以指定内容开头

print(str1.endswith('world'))
print(str1.endswith('hello')) # 检查字符串是不是以指定内容结尾

print(str1.center(50, '*')) # 将字符串放在指定宽度的中间，左右两侧填充指定的字符

print(str1.rjust(50, '*')) # 将字符串放在指定宽度的右边，左侧填充指定的字符

str1 = '123'
str2 = 'abc'
str3 = str1 + str2

print(str1.isdigit())
print(str3.isdigit()) # 判断字符串是否只由数字构成

print(str3.isalpha())
print(str2.isalpha()) # 判断字符串是否只由字母构成

print(str3.isalnum()) # 判断字符串是不是由字母和数字构成

str1 = "    123     134  "
print(str1)
print(str1.strip()) # 获得字符串省略最左右两侧的空格
```

|函数|作用|
|:-:|:--:|
|`len(str)`|返回字符串str的长度|
|`str.capitalize()`|返回字符串str首字母大写的拷贝|
|`str.title()`|返回字符串str每个单词开头字母大写的拷贝|
|`str.upper()`|返回字符串str所有字母大写的拷贝|
|`str.lower()`|返回字符串str所有字母小写的拷贝|
|`str.find(substr)`|在字符串str中寻子串substr，如果存在，返回第一个出现的下标，如果不存在，返回-1|
|`str.index(substr)`|在字符串str中寻找子串substr，如果存在，返回第一个出现的下标，如果不存在，抛出异常|
|`str.startswith(substr)`|判断字符串str是不是以substr字符串开头的|
|`str.endswith(substr)`|判断字符串str是不是以substr字符串结尾的|
|`str.center(width, ch)`|返回长度为width，str内容在中间，左右两边用ch填充的字符串|
|`str.rjust(width, ch)`|返回长度为width，str内容在最右侧，左侧用ch填充的字符串|
|`str.isdigit()`|判断字符串str是不是只由数字构成|
|`str.isalph()`|判断字符串str是不是只由字母构成|
|`str.isalnum()`|判断字符串str是不是只由字母和数字构成|
|`str.strip()`|返回删除字符串最左边和最右边的空白的拷贝|

### **字符串和print的结合**

#### **格式化输出**

- `print('(%d, %d)' % (a,b))`

这是最为常见的一种格式化输入输出，和C/C++中的printf非常相似，这里不表。

- `print('({1}, {0})'.format(a, b))`

这是字符串提供的方法来完成格式化输入输出，大括号里面的数字对应后面的参数，本质上可以理解为就是下标

- print(f'({a}, {b})')

对于上面方式的更加简洁的书写方式，只要在字符串前面加上`f`就可以直接使用上面的类似的格式化输出方式

## **列表**

之前所说的int和float类型是数值类型，其内部没有可以访问的结构，标量但是前面讲述的字符串类型由可以访问的内部结构，非标量化。

列表是值得有序序列，每个值可以通过索引进行标识(感觉类似整型映射)，定义列表可以将列表得元素放在`[]`之间，通过`,`分隔，使用`for`循环进行遍历，同样也可以使用前面所说的分片运算进行取数，取区间的操作`[]`,`[:]`，注意，这边并没有强制要求列表中的元素类型是一样的(非常强大的容器)

```
list1 = [1, 3, 5, 7, 9] # 定义列表的方式
print(list1) # 列表也可以看作是一个对象，可以打印

list2 = [1, 'hello'] * 3 # 和字符串非常类似的一种定义
print(list2)

print(len(list1), len(list2)) # 同样也具有len内置函数

print(list1[0], list1[4]) # 下标同样有正负之分，或许结构型数据类型都具有这样的特性

print(list1[-1], list1[-5])

list1[2] = 10 # 通过修改对应下标的数据

print(list1)
print(list1[::-1]) # 一样的逆序输出

for i in range(len(list1)): # 通过索引来遍历整个列表
    print(list1[i])

for i in list1: # 列表本身就是可便利的，此时i就是列表中的元素
    print(i)

for i, j in enumerate(list1): # enumerate函数就是将一个可枚举的对象的索引和对应的数据类型组合在一起，返回枚举对象
    print(i, j)

print(enumerate(list1)) # 通过一个枚举函数enumerate，我们就可以方便的得到索引和对应存储的数据
```

下面将演示如何向列表中添加元素，以及删除元素

```
list1 = [1, 3, 5, 7, 9]
list1.append(200) # 默认在最后插入元素
print(list1)
list1.insert(-5, 200) # 根据索引来判断，如果是在[-len,len)那么就是在对应索引的后面添加，但是如果超出，小于-len，那就是放在最前面，如果大于等于len，那就是放在最后插入
print(list1)
list1.extend([100, 200]) # 合并两个列表，list1在前，列表参数在后面
print(list1)
list1 = [1, 3, 5, 7, 9]
list1 += [11, 13, 15] # 列表对象支持直接相加拼接
print(list1)
list1 = [1, 2]
list2 = [2, 3]
list3 = list1 + list2
list4 = list2 + list1 # +保持位置
print(list3, list4)

list1 = [1, 3, 5, 3, 7, 9]
if 3 in list1:
    list1.remove(3) # 注意使用remove函数的时候，最好进行判断，因为如果列表没有想要移出的元素，那么就会抛出异常
if 123 in list1:
    list1.remove(3)
print(list1) # remove只会移出第一个出现的相关元素

list1.pop(0) # 移出对应位置的元素，注意这边的下标必须是合法的，不然会抛出异常
print(list1)
list1.pop(-len(list1))
print(list1)

list1.clear() # 清空列表元素，此时列表就变成了空列表
print(list1)
```

|函数|功能|
|:--:|:-:|
|`list.append(num)`|在列表末尾添加元素num|
|`list.insert(index, num)`|在位置index后添加num，注意index可以超出范围，但是不建议这样使用|
|`list.extend(otherlist)`|拼接list和otherlist，效果上等于list+otherlist|
|`list.remove(num)`|在列表中元素找到第一个为num的元素删除|
|`list.pop(index)`|删除对应index下标的元素|
|`list.clear()`|清空列表|

和字符串一样，列表也可以做切片操作，通过切片操作我们可以取出子列表

```
list1 = [1, 3, 5, 7, 9]

print(list1[:])
print(list1[2: 4])
print(list1[-5: -1])
print(list1[::-1])
```
列表的切片操作和字符串的是一样的，这里不表

### **列表的排序操作**

```
list1 = ['orange', 'apple', 'zebra', 'interesting', 'banana']
list2 = sorted(list1)
print(list1)
print(list2)

list3 = sorted(list1, reverse=True)
print(list3)

list4 = sorted(list1, key=len) # 不改变原来的顺序
print(list4)

list4 = sorted(list1, key=lambda x : -len(x))
print(list4)

list4 = sorted(list1, key=lambda x:-len(x), reverse=True)
print(list4)

print(list1)
list1.sort(reverse=True)
print(list1)
```

这里分为两种方式
- 内置函数`sorted`，对于所有对象都可以使用
- list自己的函数`sort`

同时这边的排序是稳定的，不改变原先的顺序(如果相同key值的情况下)

他们都有以下的参数

- key：排序的参照值
- reverse：是否逆序排序

这边的key就可以用上前面所说的匿名函数lambda了(终于有用武之地了)

### **生成式和生成器**

创建列表的第二种方式，借用列表的生成式语法(如果对于空间要求紧张，同时不要求存在真实对象，仅仅只是需要数据的时候可以使用生成器，一样的遍历，非常节省空间)

```
import sys

f = [x for x in range(1, 10)] # 一维向量的定义类似
print(f)

f = [x + y for x in "abc" for y in "1234"] # 有点像两个向量相乘，构成矩阵
print(f)

# 上述的方式创建的列表一定义就占用了相应的空间

f = [x ** 2 for x in range(1, 1000)]
print(sys.getsizeof(f)) # 使用sys中的getsizeof函数可以获取对象占用内存的字节数
print(f)

# 下面的代码创建的不是列表而是一个生成器对象，通过生成器同样可以获取到数据，而且不会占用额外的空间，但是获取数据的时候，需要经过运算，典型的时间换空间

f = (x ** 2 for x in range(1, 1000))
print(sys.getsizeof(f))
print(f)
for val in f:
    print(val, end=', ')
print()
```

这里是生成式的语法的结构就是

`x for x in "...."`

in后面跟的应该是一个可迭代的对象(诸如列表，字符串这种可以迭代的对象)

而生成器这种时间换空间的对象，其实就是将生成式的中括号换成小括号就可以了。

python中还定义了另外一种生成器的生成方法，就是通过`yield`关键字将一个普通函数改造成生成器函数，下面的代码就演示了一个斐波那契数列的生成器函数的构造：

```
def fib(n):
    a, b = 0, 1
    for _ in range(n):
        a, b = b, a+b
        yield a

def main():
    for i in fib(20):
        print(i)

if __name__ == '__main__':
    main()
```

其本质上就是将所需要放入的数据通过yield依次放入，仅此而已。不然一旦数据量巨大，手动输入实在难以接受，不然摸鱼是不可能的。

## **元组**

python中的元组与列表类似，他们都是一种容器，可以存储许多数据(类型可以不同)，但是注意元组和列表最大的区别在于，元组的元素不可以修改，但是列表的元素可以修改。我们把多个元素集合在一起就形成了元组，只不过不能修改里面的元素罢了。

```
t = (1, 3, 5, 7, 9)
print(t) # 我们这边通过小括号完成元组的定义

print(t[0])
print(t[1])
print(t[-1]) # 一样的通过下标获取元组之间的数据

for i in range(5):
    print(t[i])

for i in t:
    print(i)

t = (1, 3, 5) # 如果变量t指向了新的元组，之前的元组将被作为垃圾回收
print(t)

list1 =list(t)
print(list1) # 将元组转换成了列表
list1[0] = 5
print(list1)
t = tuple(list1)
print(t)
```

- 元组通过小括号进行定义，其他的和列表基本上是一样的
- 虽然说元组中的元素不可以被修改，但是一定要修改，我们可以先将元组tuple转换成列表list，然后列表可以修改元素，最后再抓换回tuple元组就可以了

### **元组的优势**
- 元组中的数据不可以更改，所以在多线程的时候使用元组，就可以非常放心元组里面的数据，因为他不能被修改，换言之，就是非常安全。所以，如果不需要对数据进行增删改，那么推荐使用元组。如果一次性返回多个值，使用元组也是不错的选择。
- 元组创建时间和占用空间上都比列表好。

## **集合**

python中的集合的含义和之前数学中的集合的含义是一致的，其中的元素不允许重复。

```
set1 = {1, 2, 2, 2, 3, 3, 2}
print(set1)

print(f'length = {len(set1)}')

set2 = set(range(1, 10))
print(set2)
t = (1, 2, 3, 3, 4)
list1 = [1, 2, 3, 3, 4]
set1 = set(t)
set2 = set(list1)
print(set1)
print(set2)

set3 = {num for num in range(1, 100) if num % 3 == 0 or num % 5 == 0}
print(set3)

list1 = [x for x in range(100) if x % 3 == 0]
print(list1)
```

集合的创建借用的是大括号，其余的语法本质上和列表是一样的，注意第三种生成式元组不行(因为被生成器抢了)，当然这边生成式还可以用if添加进来也是非常的丰富。

### **集合元素的添加删除**

```
set1 = {1, 2, 4}
print(set1)
set1.add(3)
print(set1)
set1.add(3)
print(set1)

set1.update('123') # 可以理解为将一些列后面迭代器的东西添加进集合
print(set1)
set1 = {0,1,2,3,4,5,6, 11, 9}
print(set1)
set1.discard(11) # 删除指定元素，如果没有则不进行任何操作
print(set1)
if 11 in set1:
    set1.remove(11)
print(set1)
if 2 in set1:
    set1.remove(2)
print(set1)
print(set1.pop())
print(set1)
print(set1.pop()) # 返回第一个元素并将其删除
print(set1)
```

|函数|作用|
|:-:|:--:|
|`set.add(ele)`|向集合set中加入元素ele|
|`set.update(subject)`|本质上其实就是将可迭代对象转换为集合，然后两个集合做并集|
|`set.discard(ele)`|从集合中删除ele元素，没有不会报错|
|`set.remove(ele)`|从集合中删除ele元素，没有该元素时会抛出异常，注意和if配套使用|
|`set.pop()`|弹出元素，目前看来是第一个，通过是返回值就是被弹出来的元素|
|`set.clear()`|清空集合|

### **交集，并集，差集，对称差集**

```
set1 = {1, 2, 3, 4, 5}
set2 = {3, 4, 5, 6, 7}

print(set1 & set2) # 交集
print(set1.intersection(set2)) # 交集

print(set1 | set2) # 并集
print(set1.union(set2))

print(set1 - set2) # 差集
print(set1.difference(set2))

print(set1 ^ set2) # 对称差
print(set1.symmetric_difference(set2))

set2 = set1 & set2
print(set1 <= set2)
set2 = set1
print(set1 <= set2) # 判断set1是不是set2的子集
print(set2 == set1) # 判断两个集合是否相等
print(set1 < set2) # 判断set1是不是set2的真子集

set2 = {3, 4, 5, 6, 7, 8}
set2 = set1 & set2
print(set1 >= set2) # 判断set2是不是set1的子集，或者set1是不是set2的超集

```

这里应该是python充分利用了对象可以对运算符重载，所以集合交，并，差，对称差可以用更加直观的符号来表示。

对于集合元素的遍历也是一样的：

```
set1 = {1, 2, 3, 4}
for i in set1:
    print(i)
```

## **字典**
python中的字典是有一个键和一个值一起构成键值对，键和值通过冒号分开，有点像高级的映射。

```
direc = {'a': 1, 'c': 2, 'b': 3} # 创造字典的字面量语法
print(direc)

direc = dict(one=1, two=2, three=3) # 创造字典的构造器语法，注意有点类似于变量的定义，前面的其实就是字符串，还记得前面的可变变量，**c，他的变量的传输的方式就是这个
print(direc)

direc = dict(zip(['a', 'b', 'c'], ['3', '2', '1']))
print(direc)

direc = dict(zip(['a', 'b', 'c'], "123"))
print(direc) # 通过zip函数将两个序列压成字典，注意其中元素的个数以两个序列中元素个数最少的那个为主，从左到右，一次匹配

direc = dict(zip((x for x in range(1, 10)), "123abcdef123")) # 也可以使用生成器
print(direc)

direc = {num: num ** 2 for num in range(1, 10)} # 创建字典的推导式语法(字典推导式的语法有很多，这只是其中的一种)
print(direc)

print(direc[1]) # 通过键来找到对应的值

for key in direc:
    print(f'{key}: {direc[key]}') # 通过键的遍历来获取键值对的遍历

direc = {x: x+x for x in "abcd"}
print(direc)

direc['a'] = 1
direc['b'] = 2
print(direc)

direc.update(aa=1, bb='c') # 与集合类似的更新拓展
print(direc)

if 'a' in direc: # 注意如果键不在字典中，那么通过该键寻找对应的值会泡壶异常
    print(direc['a'])

print(direc.get('a'))
print(direc.get(123)) # get方法也是通过键获得对应的值，如果没有这个键就会返回None
print(direc)
print(direc.get('b', 1)) # get方法可以设置默认值，也就是说如果没有找到这个键，那么就会返回默认值
print(direc)

print(direc.popitem()) # 删除元素
print(direc)
print(direc.popitem())
print(direc)

print(direc.pop('a', 1324)) # 可以设置默认值，如果没有对应的键，就返回默认值，否则就删除对应的键，返回对应的值
print(direc)

direc.clear() # 清空字典
print(direc)
```
