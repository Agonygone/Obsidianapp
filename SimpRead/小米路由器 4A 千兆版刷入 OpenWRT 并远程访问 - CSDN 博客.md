---
url: https://blog.csdn.net/ljq_up/article/details/134378659
title: 小米路由器 4A 千兆版刷入 OpenWRT 并远程访问 - CSDN 博客
date: 2023-11-14 20:44:44
tag: 
summary: 
---
## 小米路由器 4A 千兆版刷入 [OpenWRT](https://so.csdn.net/so/search?q=OpenWRT&spm=1001.2101.3001.7020) 并远程访问

#### 文章目录

*   [小米路由器 4A 千兆版刷入 OpenWRT 并远程访问](#4AOpenWRT_0)
*   *   [前言](#_3)
    *   [1. 安装 Python 和需要的库](#1_Python_11)
    *   [2. 使用 OpenWRTInvasion 破解路由器](#2__OpenWRTInvasion__23)
    *   [3. 备份当前分区并刷入新的 Breed](#3_Breed_45)
    *   [4. 安装 cpolar 内网穿透](#4_cpolar_75)
    *   *   [4.1 注册账号](#41__79)
        *   [4.2 下载 cpolar 客户端](#42_cpolar_87)
        *   [4.3 登录 cpolar web ui 管理界面](#43_cpolar_web_ui_93)
        *   [4.4 创建公网地址](#44__99)
    *   [5. 固定公网地址访问](#5__123)

### 前言

OpenWRT 是一个高度[模块化](https://so.csdn.net/so/search?q=%E6%A8%A1%E5%9D%97%E5%8C%96&spm=1001.2101.3001.7020)、高度自动化的嵌入式 Linux 系统，可以让路由器变得更智能，简单的说，路由器刷了 OpenWrt 就相当于一个 Linux 系统带无线带多网卡的电脑。

举个栗子：有 usb 功能的路由器刷后可以实现多端文件共享 ，挂站，远程监控甚至智能家居 ；无线可桥接，可以无线连接一般的 chinanet 热点并拨号；组建局域网无线网络传输数据等。

今天就分享一下如何在小米路由器 4A 千兆版刷入 OpenWRT 并通过内网穿透工具实现公网远程访问。

### 1. 安装 Python 和需要的库

首先打开 [www.python.org](https://www.python.org/) 下载一个 Python3 的安装包并安装。

安装完成后执行以下命令升级 pip 与安装需要的库：

```
python -m pip install --upgrade pip
pip install pycryptodome
pip install requests
```

### 2. 使用 OpenWRTInvasion 破解路由器

打开 [OpenWRTInvasion 的 releases 页面](https://github.com/acecilia/OpenWRTInvasion/releases)，下载一个可用的版本，我这里选择的是支持 Windows 的版本的是 0.0.7。

下载后得到的压缩包名为：OpenWRTInvasion-0.0.7，将改文件解压缩到一个无中文的路径即可。

![](https://img-blog.csdnimg.cn/img_convert/477689941303eb91f636fe3d52ca5f93.png)

小米路由器联网，登录路由器，在地址栏中找到参数 stok 并复制等号后的字符，保持网页不要关闭。

![](https://img-blog.csdnimg.cn/img_convert/1e5e60ca6c1ff26baaa1b47b458e6c2a.png)

在解压 OpenWRTInvasion 的目录打开 cmd（本教程中使用的是 Windows PowerShell）

输入`python remote_command_execution_vulnerability.py`指令运行破解脚本

根据提示输入路由器 IP（192.168.31.1），粘贴之前复制的 stok 等号后的字符，开始破解

破解成功后会有提示，可以复制提示的指令连接 Telent 或者 SSH，用户名、密码都是 root

![](https://img-blog.csdnimg.cn/img_convert/62c0a7d6fd11c76276cbd2c5697cdab4.png)

### 3. 备份当前分区并刷入新的 Breed

首先执行以下指令查看与备份分区

```
cat /proc/mtd   #显示路由分区
dd if=/dev/mtd0 of=/tmp/all.bin   #备份所有分区到/tmp/all.bin
dd if=/dev/mtd1 of=/tmp/Bootloader.bin   #备份引导分区到/tmp/Bootloader.bin
```

![](https://img-blog.csdnimg.cn/img_convert/429800b93e87e727c967916c324abd87.png)

然后使用 WinSCP 或者其他 FTP 工具创建 FTP 连接，地址是路由器 IP，用户名 root，没有密码，连接后将刚才备份的两个文件`all.bin`,`Bootloader.bin`传输出来，并且将 [breed-mt7621-pbr-m1.bin](https://breed.hackpascal.net/breed-mt7621-pbr-m1.bin) 上传到 tmp 目录下。

![](https://img-blog.csdnimg.cn/img_convert/2860fa70005a0ed7b76b96d331be7b3b.png)

上传完成后执行`mtd -r write /tmp/breed-mt7621-pbr-m1.bin Bootloader`刷入 Breed，刷入完成后重启路由器

![](https://img-blog.csdnimg.cn/img_convert/8258b12a88c3d79ce06c94a818c0ec06.png)

使用浏览器打开 192.168.1.1 打开 Breed 控制台，刷入 [openwrt-ramips-mt7621-xiaomi_r4a-squashfs-sysupgrade.bin](https://downloads.openwrt.org/releases/21.02.3/targets/ramips/mt7621/)。点击确定后，会进行更新读条。

![](https://img-blog.csdnimg.cn/img_convert/0de28daa491c4e8d9e0115157b1b40db.png)

等待读条结束后，浏览器输入 192.168.31.1 即可看到 OpenWrt 登录界面

默认账号为 root，密码是 coolxiaomi，登录后显示下方界面即刷入成功。

![](https://img-blog.csdnimg.cn/img_convert/d38563d4011a76718598a03af5859a1a.png)

### 4. 安装 cpolar 内网穿透

此时已经可以成功登录 OpenWrt 并运行，不过只能在本地访问，如果打算在公网环境随时随时访问内网的 OpenWrt 进行文件传输等操作，我们需要安装 cpolar 内网穿透工具来实现。

#### 4.1 注册账号

进入 cpolar 官网：https://www.cpolar.com/

点击右上角的`免费注册`，使用邮箱免费注册一个 cpolar 账号并登录

![](https://img-blog.csdnimg.cn/img_convert/017468adb3703a7162555f49d87df47c.png)

#### 4.2 下载 cpolar 客户端

登录成功后，点击下载 cpolar 到本地并安装（一路默认安装即可）本教程选择下载 Windows 版本。

![](https://img-blog.csdnimg.cn/img_convert/b305d3850b76dbef7973d45942c44dd5.png)

#### 4.3 登录 cpolar web ui 管理界面

在浏览器上访问 [127.0.0.1:9200](http://127.0.0.1:9200/#/dashboard)，使用所注册的 cpolar 邮箱账号登录 cpolar web ui 管理界面（默认为本地 9200 端口）

![](https://img-blog.csdnimg.cn/img_convert/1807765987ae598a0db900c6eac94b23.png)

#### 4.4 创建公网地址

登录成功进入主界面后，我们点击左侧仪表盘的`隧道管理`——`隧道列表`，再点击`创建隧道`.

![](https://img-blog.csdnimg.cn/img_convert/18e45bb2e85dff0ea9ffe4d7358b2016.png)

*   隧道名称：可自定义命名，不能与已有的隧道名重复，这里我填写了`website`
    
*   协议：选择`http`
    
*   本地地址：`192.168.31.1:80`
    
*   域名类型：免费套餐选择`随机域名`
    
*   地区：`China Top`
    

点击`创建`

![](https://img-blog.csdnimg.cn/img_convert/7af08ebbd5c326f2db0449e6230f3e95.png)

此时，点击左侧`状态`中的`在线隧道列表`，可以看到刚才创建的 wamp 隧道，生成了两个公网地址，有两种访问方式，分别是 http 和 https，随意复制一个地址，在公网电脑浏览器打开即可，如下图所示即代表成功实现公网访问本地内网路由器的 OpenWrt。

![](https://img-blog.csdnimg.cn/img_convert/2ba367c2798676b1d3c25741408b5f76.png)

### 5. 固定公网地址访问

需要注意的是，本次教程中使用的是免费 cpolar 所生成的公网随机临时地址，该地址 24 小时内会发生变化，对于需要长期在外使用 OpenWrt 的用户来讲，配置一个固定地址就很有必要。

我一般会使用固定二级子域名，原因是这样一个固定、易记的公网地址（例如：open.cpolar.cn），这样远程路由器时更方便也更快捷。

登录 cpolar 官网，点击左侧的预留，选择保留二级子域名，设置一个二级子域名名称，点击`保留`，保留成功后复制保留的二级子域名名称。

![](https://img-blog.csdnimg.cn/img_convert/e62ca0edfeebbdb2dd284bdd05866a03.png)

以本次教程为例，地区选择`China VIP`，二级域名填写`open`，描述填写 1，点击`保留`。

![](https://img-blog.csdnimg.cn/img_convert/9c77a012079dc17ddbff69a1a7d3db1c.png)

保留成功后复制保留的二级子域名地址，登录 cpolar web UI 管理界面，点击左侧仪表盘的`隧道管理`——`隧道列表`，找到所要配置的隧道：website，点击右侧的`编辑`

![](https://img-blog.csdnimg.cn/img_convert/9e1f3ab24f209f7bc4d4097beb42b13a.png)

修改隧道信息，将保留成功的二级子域名配置到隧道中

*   域名类型：选择`二级子域名`
*   Sub Domain：填写保留成功的二级子域名`open`
*   地区：选择`China VIP`

点击`更新`

![](https://img-blog.csdnimg.cn/img_convert/a4605b43c588fa777d286cfdeb607f32.png)

更新完成后, 打开`在线隧道列表`, 此时可以看到公网地址已经发生变化, 地址名称也变成了保留和固定的二级子域名名称。

![](https://img-blog.csdnimg.cn/img_convert/d50c1c1ec3145b2501db1e9a0c5e9508.png)

最后，我们使用固定的公网地址进行连接访问，复制二级子域名：http://open.vip.cpolar.cn / 到另一台公网电脑浏览器打开，无报错和连接异常，可以看到连接成功，这样一个固定不变的地址访问就设置好了，您可以随时随地使用该域名来公网访问内网路由器 OpenWrt 进行操作了。

![](https://img-blog.csdnimg.cn/img_convert/4f70746528283e8f84cc5523e4cd5f8b.png)