---
url: https://www.jb51.net/article/158533.htm
title: 详解 python 中 @的用法_python_脚本之家
date: 2023-12-26 10:46:39
tag: 
banner: "https://img.jbzj.com/file_images/article/202104/2021416141955635.png"
banner_icon: 🔖
---


python 中 @的用法

@是一个装饰器，针对函数，起调用传参的作用。  
有修饰和被修饰的区别，[‘@function'](mailto:%E2%80%98@function')作为一个装饰器，用来修饰紧跟着的函数（可以是另一个装饰器，也可以是函数定义）。

代码 1

```
def funA(desA):
 print("It's funA")
 
def funB(desB):
 print("It's funB")
 
@funA
def funC():
 print("It's funC")
```

结果 1

It's funA  

分析 1

@funA 修饰函数定义 def funC()，将 funC() 赋值给 funA() 的形参。  
执行的时候由上而下，先定义 funA、funB，然后运行 funA(funC())。  
此时 desA=funC()，然后 funA() 输出‘It's funA'。  

代码 2

```
def funA(desA):
 print("It's funA")
 
def funB(desB):
 print("It's funB")
 
@funB
@funA
def funC():
 print("It's funC")
```

结果 2

It's funA  
It's funB  

分析 2

@funB 修饰装饰器 @funA，@funA 修饰函数定义 def funC()，将 funC() 赋值给 funA() 的形参，再将 funA(funC()) 赋值给 funB()。  
执行的时候由上而下，先定义 funA、funB，然后运行 funB(funA(funC()))。  
此时 desA=funC()，然后 funA() 输出‘It's funA'；desB=funA(funC())，然后 funB() 输出‘It's funB'。  

代码 3

```
def funA(desA):
 print("It's funA")
 
 print('---')
 print(desA)
 desA()
 print('---')
 
def funB(desB):
 print("It's funB")
 
@funB
@funA
def funC():
 print("It's funC")
```

结果 3

It's funA  
<function funC at 0x000001A5FF763C80>  
It's funC  
It's funB

分析 3

同上，为了更直观地看参数传递，打印 desA，其传的是 funC() 的地址，即 desA 现在为函数 desA()。  
执行 desA() 即执行 funC()，desA=desA()=funC()。

代码 4

```
def funA(desA):
 print("It's funA")
 
def funB(desB):
 print("It's funB")
 print('---')
 print(desB)
 
@funB
@funA
def funC():
 print("It's funC")
```

结果 4

It's funA  
It's funB  
None

分析 4

上面将 funC() 作为参数传给 funA，那么 funA(funC()) 怎么传给 funB() 呢？打印 desB，发现并没有参数传递。  
是否可以理解为当‘装饰器'修饰 ‘装饰器'时，仅是调用函数。  

原文链接：https://blog.csdn.net/occamo/article/details/80842311

