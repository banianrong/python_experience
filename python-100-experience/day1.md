# **day1**
> 应是天仙狂醉，乱把白云揉碎。
****

## **python进化小记**

- 1989，世界上多了一门编程语言，你我也多了一门课程
- 1994，迎来python1.0
- 2000，python2.0降临大家庭
- 2008，python3.0缓缓来临
- python命名规则，多为**Python a.b.c**
  - a代表大版本更新
  - b表示新功能出现
  - c表示小改动，只要有修改都会变动c

## **python优缺点**

|优点|缺点|
|:----:|:----:|
|简单易上手|执行效率低(相对)|
|开放源码|无法加密|
|解释性语言，可移植性高||
|代码规范高，可读性高||

## **python之旅**

### **物资准备**
**安装python解释器**

[python官网](https://www.python.org/)，点击即可去往官网，找到download根据自己的操作系统以及喜欢的版本选择下载就可以了。

笔者用的是windows系统，这里需要注意，windows系统中可能会有坑，也就是下载后，通过cmd窗口检查是否下载成功的时候输入python并不会成功启动python，而是会跳转到microsoft shop下载其打包好的python编辑器，重启电脑就可以了。这里推荐去官网下载好，注意官网安装包中有一个含有path的选择，安装的时候勾选就可以了，可以省去配置环境变量的麻烦。

检验是否安装成功，可以打开windows的cmd窗口，然后输入

`python --version`

如果有给出对应的python版本，则python安装成功，此时再输入

'python'

就可以打开python的单行执行窗体了

python是解释器，直接对其语言进行解释运行，所以不同于C，C++的编译，需要先产生exe文件才能运行

**初见python**
接下来就可以运行你的第一个python程序啦

直接新建一个txt文件，然后将文件的拓展名改成py就可以了。显示文件的拓展名，就是打开文件夹窗口，**左上角**有**查看**，点击后，在右上边有一个**文件扩展名**勾选就可以了。

笔者在里面输入

`print("hello rongrong")`

在双引号中可以输入自己喜欢的语句，中英文都可以，utf-8支持的语言范围很广

**Ctrl+S**保存后，可以打开cmd窗口，**Windows+R**，输入**cmd**就可以打开一个黑窗口，通过**cd**命令移动到py所在的文件夹，然后输入

`python xxx.py`

xxx是自己的python文件名字，就可以看到运行结果了

如果之前没有接触过cmd命令，那么笔者这边提供一个样板，可以先感受python的魅力，仍然是打开cmd窗口，然后按顺序输入一下语句

```
md python
cd python
echo print("hello world") >> hello_world.py
python hello_world.py
```

其作用大致为
- 建立一个python文件夹
- 进入python文件夹
- 建立一个hello_world.py文件，里面的内容为print("hello world")
- 解释hello_world.py，也就是运行这个py文件
