---
url: https://blog.csdn.net/Vicissitufe/article/details/138014300
title: 打造便携式 Python 环境——把 Python 装进 U 盘_python 便携版 - CSDN 博客
date: 2024-12-10 14:52:12
tag: 
banner: "https://i-blog.csdnimg.cn/blog_migrate/e6d527ccbaac55530089d43d0cee309c.png"
banner_icon: 🔖
---
**本文于 2024/6/23 最新更正**

有时我们需要在一台新设备上进行 Python 编程，重新安装太麻烦，相关的库还要重新安装，而且如果是别人的设备也不太方便，那么最好的办法就是把 Python 装进 U 盘，即插即用。内容全部亲自验证过，适合小白，简单易懂。这里只讨论 Windows 系统。

## 一、 Python 坏境安装

这里我们要将 python 安装进 U 盘，可以直接使用我们已经安装过的库。

选择什么版本是关键，版本不是越高越好，会导致系统或者相关库不适配。这里我推荐 3.8 版本的，在 win7 上也可以运行（3.8 为 win7 上能运行的最高版本，3.7 版本有点老了，有的库已经不支持了，如 requests-html 最低支持 3.7.2）。我这里以 python3.7.0 为例。

顺便提一下嵌入版 python，原本我以为这玩意很好用。但还要自己装 [pip](https://edu.csdn.net/cloud/sd_summit?utm_source=glcblog&spm=1001.2101.3001.7020) 程序，我之前执行 pip 安装语句时还会有一些 zip 报错，很麻烦。光查资料都用去不少时间，而且 vscode 还不能识别。不如直接装正常 python。所以这里我不推荐，安装正常的 python 即可。

这里放一个华为的 python 镜像  [https://mirrors.huaweicloud.com/python/](https://mirrors.huaweicloud.com/python/ " https://mirrors.huaweicloud.com/python/")

**1、下载安装包**

选择以下两个安装包之一，选离线安装包。amd64 与 Windows 是 32 位还是 64 位没关系，是指 CPU 是 x64 的，如果没有特别需求，推荐安装 32 位的 Python，兼容性更好。

![](https://i-blog.csdnimg.cn/blog_migrate/e6d527ccbaac55530089d43d0cee309c.png)

**2、**选择自定义安装，可以选择添加路径看一下格式。

![](https://i-blog.csdnimg.cn/blog_migrate/9f0359db0db835a6f584a73a9118a698.png)

**3、**这步什么都不用动，直接 Next

![](https://i-blog.csdnimg.cn/blog_migrate/67a353b68f360f234d8a9fcb9f6fc650.png)

**4、**将安装位置选择在 U 盘中一个提前建好的文件夹，推荐写明 python 版本。

![](https://i-blog.csdnimg.cn/blog_migrate/495d187d9e436f0a5300fc87b2bd5390.png)

**5、**点击 Install 安装

![](https://i-blog.csdnimg.cn/blog_migrate/4616f50d49e334b3fe46ace37710bada.png)

![](https://i-blog.csdnimg.cn/blog_migrate/a0d1e12d3a1e1c9feb9a999652078d5b.png)

然后我们打开此电脑 -> 属性 -> 高级系统设置 -> 环境变量 ->Path，查看格式。win10 是表格，而 win7 是一条横框。  
G:\python3.7.0\Scripts\  
G:\python3.7.0\  
G:\python3.7.0\python.exe

或  
G:\python3.7.0\Scripts\;G:\python3.7.0\;G:\python3.7.0\python.exe;

复制进 U 盘中的一个 txt 备用。

## 二、便携式 IDE

常用的 IDE 有很多，我这里主要推荐 vscode 和 pycharm，强烈推荐 vscode，体积小，打开快，界面好看，插件多。

### **（一）VScode**

vscode 是我最喜欢的编辑器，并且提供免安装版，启动无需添加路径，且插件随身携带，如果你机房的电脑是 win10 的，可以直接去官网下载 zip 版。

![](https://i-blog.csdnimg.cn/blog_migrate/54e3a2ace39336c4d106ed9f38e75b47.png)

vscode 官方网址：[https://code.visualstudio.com/](https://code.visualstudio.com/ "https://code.visualstudio.com/")

由于官网上最新的 VScode 已经不支持 win7，如果你的电脑是 win7，可以下载老版本，最高不超过 1.7.2。我下面放了一个 1.6.7 版本的，需要自取。

**蓝奏云链接：https://wwt.lanzouq.com/ijSkZ1vy80di       密码：63d6**

解压在 U 盘里后，在同级文件夹中创建一个名叫 data 的文件夹，这个文件夹将会储存你安装的插件和用户数据。

![](https://i-blog.csdnimg.cn/blog_migrate/8ba3c3866d32664e0ea373696beaa87a.png)

**下面介绍几个插件。**

**1、中文简体**

![](https://i-blog.csdnimg.cn/blog_migrate/c6cad932f8d26b2d87fd0e4444d2b42e.png)

这自然是最重要的，在插件商城安装后，在 vscode 上方的输入框内输入

>Configure Display Language

![](https://i-blog.csdnimg.cn/blog_migrate/c1484d42d33d16e9a114f2e50725ecc3.png)

后选择中文 - CN 即可，不过你安装完之后右下角就会有弹窗提示你是否更换语言，restart 即可。

说明：vscode 第一次打开时自动读取中文包时，有可能翻译不全，此时重新手动选择语言即可。

**2、Python 插件**

![](https://i-blog.csdnimg.cn/blog_migrate/4131625a94eb15c3fb23a9197bad494e.png)

你没插件编个啥？直接用 Microsoft 的就行了，里面包含 Python，Pylance，Python Debugger 三个包。

下载完成后在文件中创建 New File，选择 python，然后在右下角选择不同版本的 python 解释器，如果你添加的是系统变量，后面会带一个 system。

**3、z-reader / any-reader**

![](https://i-blog.csdnimg.cn/blog_migrate/873a4cb34613abf789095028724f18be.png)

摸鱼插件，可以在 vscode 中看小说，支持 txt 和 equb，是不是很炸裂？它支持在代码层面上改页面和功能。点击左侧插件图标，再点击弹出的目录框右上角的 “···”，可以打开放书的本地文件夹，将 txt 文件或 equb 文件直接拖进去（不要放进文件夹，再将文件夹拖进去）。在点击” 本地“即可读取（会自动排序），代码编累了可以看一会小说（bushi

作者还有一个升级版 [any](https://marketing.csdn.net/p/3127db09a98e0723b83b2914d9256174?pId=2782&utm_source=glcblog&spm=1001.2101.3001.7020)-reader，但由于一般用不到更多功能，所以推荐使用轻量版的 z-reader

**4、Windows Opacity**

![](https://i-blog.csdnimg.cn/blog_migrate/aeece105d8b6d1cafe284acaf66323f4.png)

摸鱼插件，可以让你的 vscode 变得半透明，一边看视频一边编程。

5、 Qwerty Learner

![](https://i-blog.csdnimg.cn/blog_migrate/652da393ec24a661cf72bcdcaff7f7e1.png)

可以在 vscode 中练习打字，shift+Alt+Q 启动，启动后会屏蔽你的输入，不用担心练习时破坏代码，并且这个打字插件采用的模式是打错就重新打，帮助形成正确的肌肉记忆。

### （二）pycharm

很受欢迎的 IDE，不过体积偏大，打开较慢，而且颜色给我一种偏老气的感觉，即使颜色换成白色，和 Sublime Text 一样，蒙了一层布一样。并且 pycharm 没有官方的绿色版，你的配置换设备后不会得到保存，所以不推荐。

这个就不多作介绍了，主要是我一般用 vscode，用 pycharm 比较少。

绿色版压缩包都有 300 多 MB，蓝奏云放不了，放个脚本之家的地址。

[https://www.jb51.net/softs/759789.html#downintro2](https://www.jb51.net/softs/759789.html#downintro2 "https://www.jb51.net/softs/759789.html#downintro2")

## 三、添加环境变量

### （一）程序实现（不嫌麻烦可跳）

因为不是嵌入式 python，所以在一台新设备上如果想用 pip 命令的话需要添加环境变量，每次都手动添加嫌麻烦，可以程序实现。（只用解释器的话不需要添加环境变量，直接在 vscode 中选择就行了）

将下面示例修改后，用 Pyinstaller 打包成 exe，每次只要输入 U 盘插入的盘符和 python 版本即可。

这里用的是最简单的 os.system()

```
import os
m=""
while True:
    pan=input("输入盘符：")
    if len(pan)==1 and 65<=ord(pan[0])<=90:
        while m !="310" and m!="372":
            m=input('输入python版本')
        if m =="310":
            path_1=pan+':\\python-3.10.0\\Scripts\\'
            path_2=pan+':\\python-3.10.0\\'
            path_3=pan+':\\python-3.10.0\\python.exe'
 
        if m =="372":
            path_1=pan+':\\python-3.7.2\\Scripts\\'
            path_2=pan+':\\python-3.7.2\\'
            path_3=pan+':\\python-3.7.2\\python.exe'
 
        break
path_0=os.environ['path']
path_0=path_0[path_0.index('C:\\Users'):]  
# 让你添加的python在变量最上方，pip指令就会优先选择
path='"'+path_1 + ";"+ path_2 + ";" + path_3+';'+path_0+'"'
command =r"setx PATH %s "%path
os.system(command)
input() # 阻塞看一下结果
```

修改完后进行打包。没有库的用 pip 安装，用镜像源更快。

```
python -m pip install Pyinstaller -i https://pypi.tuna.tsinghua.edu.cn/simple
```

安装完后在想打包的 py 文件的文件夹中打开 cmd。

```
Pyinstaller -F path.py #换成你的文件名
```

打包完后 exe 文件在 dist 文件夹中，因为采用的是 -F 打包方式，所以除了那个 exe 文件，其他新生成的文件都可以直接删掉。

![](https://i-blog.csdnimg.cn/blog_migrate/4fa43622b14472c9c14f520e613181e7.png)

![](https://i-blog.csdnimg.cn/blog_migrate/ca9c6b4c1ba167c031cd65236e4be9de.png)

看到这个文件说明你已经成功了。

这里推荐去掉 /m （不添加系统变量），因为用户变量效果是一样的，用 / m 有时会没有权限修改注册表导致添加失败。

在一台新设备上，运行程序，如果出现下图，则说明添加成功，如果失败，则要手动添加。

![](https://i-blog.csdnimg.cn/blog_migrate/32220883a0d8575824b05585029b8347.png)

### （二）手动添加

**1、**右键此电脑打开属性，左键高级系统设置。

![](https://i-blog.csdnimg.cn/blog_migrate/8bc58357f6b6dd570fbdaf6607ad51f5.png)

**2、**左键环境变量，选中 path，用户变量，系统变量都可以。

![](https://i-blog.csdnimg.cn/blog_migrate/35c3c1aee46cf00f6e038a202379e4f7.png)

![](https://i-blog.csdnimg.cn/blog_migrate/39fdd27b3bce788228a51fc2be813884.png)

**3、**左键新建，将之前复制到 U 盘的三条路径依次复制进去，再用上移将这三条移至最上面，这样你运行 pip 指令匹配到的才是你这个 python 解释器，然后确定保存。

![](https://i-blog.csdnimg.cn/blog_migrate/29a06d26aa059216f0a663171274d246.png)

**说明：**

你如果只是想用解释器（python.exe）来运行程序，是不需要添加环境变量的，你在 vscode 查找解释器路径时选择 python 文件中的 python.exe 就行了。但调用 pip 没路径肯定是不行的。

## 四、报错总结

### （一）python 无法运行

主要表现为运行时带出多个控制台（黑框），或缺少相关 dll 或出现类似 0xc000007b 的报错，如果是这个问题基本上你 U 盘刚插进去就会弹黑框了。

#### **1、热插拔导致 python 损坏**

U 盘热插拔造成的文件丢失，用你安装 python 的安装包 repair，或者选择修复驱动器。如果不行就卸了重装（在你试完全部方法以后）

#### **2、与系统，硬件不适配**

电脑本身确实可能缺少相关系统文件，但你在你在新设备上重装所有 dll 不太现实。一般情况下可通过换 python 版本实现。

首先是 win7 版本最多支持 3.8.x，其次在可选的 python 版本中选择较低较稳定的版本，如有的机子 3.8 的运行不了，3.7 可运行；64-bit 运行不了，用 32-bit 可运行。最好装多个版本的 python 以防某一个出现问题。

### （二）VScode 缺少动态链接库

打开 VScode 时显示缺少动态链接库，缺少 kernel.dll

#### **1、与系统，硬件不适配**

##### **1.1 换版本**

还是老话，就算真的缺少 dll，重装很麻烦，网上的修复器大多要钱还不一定管用，如 dll 修复. site （我不知道为什么全网都在推这个）所以最好的办法是换版本。

kernel.dll 是一个很重要的 dll，如果真的少了很多程序都会打不开，不只是 vscode。通常情况下是 windows 版本不适配导致的。如你在 win7 上运行高版本的 vscode（只支持 win10/11）就会出现这样的问题（此电脑 kernel.dll 存在），而换低版本就不会报错。你可以用微 PE 或虚拟机尝试一下。

##### **1.2 手动添加 dll**

从网上下载相关的 dll，放在系统文件夹内。

32 位系统放在 C:\Windows\System32，64 位系统放在 C:\Windows\SysWOW64

你可能会发现自己其实有这个 dll，报错的原因大概率是 64 位系统中用的是 32 位的 dll。替换的过程中可能会出现没有权限，或正在运行导致无法替换。可以 win+r 输入 gpedit.msc 在本地策略中给所有用户升级为管理员，或进 PE 替换，这里不做展开。

放入后 win+r 输入 xxx.dll 运行，重启电脑

放个 kernel.dll 的链接，防止被城际网盘，喵网盘，小牛网盘给恶心了。

[https://wwt.lanzouq.com/iQPtF1z0xtod](https://wwt.lanzouq.com/iQPtF1z0xtod "https://wwt.lanzouq.com/iQPtF1z0xtod")   密码：9i80

##### **1.3 其他方法**

1、系统文件检查器（SFC）扫描

在打开的命令提示符窗口中，键入 sfc /scannow 后按回车键启动

2、进行 Windows 更新，会修复缺失或损坏的 dll

对于上述两种方法，一句话，成功率低，不好用，不推荐。

3、dll 修复工具

网上一大堆，这里不做推荐，总之就是花钱办事。

### （三）VScode 点击没反应

点击后没报错，但也不弹出窗口。

#### **1、驱动器损坏**

通常这种情况还带有你可以从 U 盘中拖出文件，但把文件放进 U 盘时就会报错的问题。此时修复驱动器即可。

说一下这个 bug 的神奇之处，就是它这个驱动器损坏是针对特定设备的，就是你在自己的设备上可以运行（尽管也显示推荐修复驱动器），但放在其他设备上就运行不了，必须要修复以后才能运行

### （四）运行 pip 命令报错

#### 1、路径未添加好

出现 ‘pip’ 不是内部或外部命令，也不是可运行的程序或批处理文件。

G:\python3.7.0\Scripts\    这条路径没添加好，识别不了 pip 命令

#### 2、有多个 python 无法指定版本

新设备中可能原本就有 python，你运行 pip 命令会默认选用原设备中的 python，不会将库安装进 U 盘中的 python 中。

最好的办法：找到原设备 python 的环境变量路径，将你的 python 路径添加进去并移到原 python 路径的上方，一般情况下无需重启电脑。

一般的方法：将 python.exe 复制一遍，重命名为 python370.exe。将所有版本的 python 都进行以上操作。之后用 python370 -m pip xxx 执行命令

#### 3、Visual C++ 14.0 is required

老生常谈的问题。

##### 3.1  用 Visual tools 安装

从根本上解决问题，缺点是安装慢，并且动辄几个 GB 的空间，看着有些吓人。

蓝奏云链接：[https://wwt.lanzouq.com/iPeLb1z1no6b](https://wwt.lanzouq.com/iPeLb1z1no6b "https://wwt.lanzouq.com/iPeLb1z1no6b")   密码：h0yi

##### 3.2 下载 whl 文件离线安装

去 pip 国外官网下载太慢了，推荐使用清华源，搜索你需要的库 + Links 比较容易搜到

### 

![](https://i-blog.csdnimg.cn/blog_migrate/f1fe06e318954fd45320aaee59c347be.png)

但版本很多，怎么选？

输入 pip debug

![](https://i-blog.csdnimg.cn/blog_migrate/018e8c9c9ffaa894edf4a89520f0d20d.png)

这里会显示你安装的 python 版本所适合的 whl 版本（用 pip install 有线安装会自动选择最佳版本）

下载完 whl 文件后，在 whl 所在文件夹打开 cmd。运行 pip install xxx.whl

如 pip install PyQt5-5.15.3-cp36.cp37.cp38.cp39-none-win_amd64.whl

缺点：下载慢，速度与电脑本身关系很大

## 五、总结

推荐 python3.8 32 位 + VScode1.63 zip + 程序添加路径

提前安装好所有的库，尽量不要在新设备上使用 pip 命令，报错概率很高，无论什么问题，重装永远是最有效的办法。

本文主要启发于在机房编写 pyqt 程序时要用到 designer.exe，每次都要安装 pyqt5 库很麻烦，便产生了将 python 装进 U 盘的想法，踩了很多坑，便写成经验总结。

第一次写文章，有错误请见谅，欢迎批评指正。