---
url: https://www.cnblogs.com/connect/p/office-excel-python-conf.html
title: 配置 Office Excel 运行 Python 宏脚本
date: 2023-12-26 10:57:49
tag: 
banner: "https://img2018.cnblogs.com/blog/1222343/201908/1222343-20190831092255019-95385403.png"
banner_icon: 🔖
---
## 基本环境

<table><thead><tr><th>名称</th><th>版本</th></tr></thead><tbody><tr><td>操作系统</td><td>Windows 10 x64</td></tr><tr><td>Office</td><td>2016</td></tr></tbody></table>

## 安装 Python

#### 1. 下载 Python 安装包

登录 [https://www.python.org/downloads/windows/](https://www.python.org/downloads/windows/) 进行下载  
Python2.x 或 Python3.x 均可，推荐 Python3.x（因为 2020 年 1 月 1 日起 Python2 就停止服务了...）

![](https://img2018.cnblogs.com/blog/1222343/201908/1222343-20190831092255019-95385403.png)

#### 2. 安装 Python

安装前，勾选`Add Python 3.x to PATH`选项。安装完毕之后，在 Windows 控制台可直接使用`python`命令。

![](https://img2018.cnblogs.com/blog/1222343/201908/1222343-20190831092302886-323650828.png)

#### 3. 检查是否安装成功

按`Win+R`，打开`运行`，输入`PowerShell`，打开命令行。  
输入`python -V`，查看 Python 版本号。

![](https://img2018.cnblogs.com/blog/1222343/201908/1222343-20190831092310197-860512816.png)

#### 4. 安装 PythonWin32 库

Python2.x 按以下方式安装

```
pip install pypiwin32 -i https://mirrors.aliyun.com/pypi/simple/
```

Python3.x 按以下方式安装

```
pip install pywin32 -i https://mirrors.aliyun.com/pypi/simple/
```

## 安装 ExcelPython

1. 从 [https://sourceforge.net/projects/excelpython/files/](https://sourceforge.net/projects/excelpython/files/) 处，下载`ExcelPython`

或[点击此处](https://files.cnblogs.com/files/connect/excelpython-2.0.8.zip)直接下载

![](https://img2018.cnblogs.com/blog/1222343/201908/1222343-20190831092342047-1468543555.png)

![](https://img2018.cnblogs.com/blog/1222343/201908/1222343-20190831092329673-1675303885.png)

![](https://img2018.cnblogs.com/blog/1222343/201908/1222343-20190831092333528-1290691080.png)

![](https://img2018.cnblogs.com/blog/1222343/201908/1222343-20190831092346325-1417461786.png)

![](https://img2018.cnblogs.com/blog/1222343/201908/1222343-20190831092351932-607478569.png)

2. 新建一个 Excel 文件，打开可在标签栏显示`ExcelPython`标签

![](https://img2018.cnblogs.com/blog/1222343/201908/1222343-20190831092358384-1021410875.png)

3. 打开 Excel 选项——信任中心——信任中心设置——宏设置——安全性，选中 “信任对于 VBA 工程对象模型的访问”，按确定即可。

![](https://img2018.cnblogs.com/blog/1222343/201908/1222343-20190831092405777-2074065778.png)

## 测试安装是否正确

1. 将创建的`data.xlsx`文件另存为`data.xlsm`宏文件。

2. 回到 Excel，点击`ExcelPython`标签的`Setup ExcelPython`按钮

![](https://img2018.cnblogs.com/blog/1222343/201908/1222343-20190831092412801-1359115693.png)

3. 桌面上会出现一个名为`xlpython`的文件夹，以及一个与`*.xlsm`文件同名的`*.py`文件。

![](https://img2018.cnblogs.com/blog/1222343/201908/1222343-20190831092420257-2067159413.png)

4. 打开`data.py`编辑，写入以下内容

```
from xlpython import *
import random

@xlfunc
def getRandomBirth():
    y = random.randint(1980, 2000)
    m = random.randint(1, 12)
    d = random.randint(1, 28)
    return str(y)+'/'+str(m)+'/'+str(d)

@xlfunc
def getAge(d):
    _today = [ 2019, 8, 30 ]
    _list = str(d).split('/')
    age = _today[0] - int(_list[0])
    if _today[1] < int(_list[1]):
        age -= 1
    elif _today[1] == int(_list[1]):
        if _today[2] < int(_list[2]):
            age -= 1
        else:
            pass
    else:
        pass
    return age
```

![](https://img2018.cnblogs.com/blog/1222343/201908/1222343-20190831092428224-842254209.png)

5. 回到 Excel 中，点击`ExcelPython`标签的`Import Python UDFs`按钮

![](https://img2018.cnblogs.com/blog/1222343/201908/1222343-20190831092435670-2046374140.png)

6. 使用 Python 中定义的函数  
在输入框中输入`=getRandomBirth()`

![](https://img2018.cnblogs.com/blog/1222343/201908/1222343-20190831092441609-1316517101.png)

效果如图

![](https://img2018.cnblogs.com/blog/1222343/201908/1222343-20190831092447912-1371195262.png)

7. 在 Excel 中使用定义的第二个函数

![](https://img2018.cnblogs.com/blog/1222343/201908/1222343-20190831092455337-902773659.png)

效果如图

![](https://img2018.cnblogs.com/blog/1222343/201908/1222343-20190831092502852-129357836.png)

至此，可以使用 Python 进行 Excel 宏的开发

**本文链接:** [https://www.cnblogs.com/connect/p/office-excel-python-conf.html](https://www.cnblogs.com/connect/p/office-excel-python-conf.html)