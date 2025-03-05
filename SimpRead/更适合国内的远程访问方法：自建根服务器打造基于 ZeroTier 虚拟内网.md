---
url: https://sspai.com/post/85130
title: 更适合国内的远程访问方法：自建根服务器打造基于 ZeroTier 虚拟内网
date: 2023-12-31 09:24:13
tag: 
banner: "https://cdn.sspai.com/12/27/2023/article/713f3f34-f9cf-1aee-e598-044437652779.jpg"
banner_icon: 🔖
---
多款公有云产品出现宕机问题，越来越多人开始选择私有云来存储数据。拍摄的照片、下载的电视剧、音乐和电影如今都被存储在家中的 NAS 设备或者电脑上。这样，我们可以在不受公网环境限制的情况下，随时随地访问和使用这些数据。有时候我们需要在外网环境访问家中 NAS 的资料和数据，但目前很多方案都缺少一定的灵活性。

况且，随着假期临近，相信不少朋友都有出门或者回家的打算。考虑到会出现的需要访问家中 / 公司设备的场景，又或许是临时下载放在服务器中的文件，还或许是连上住所的 NAS 和亲朋好友一起观看自己收藏的电影和照片。这个时候，稳定靠谱的远程访问能力就更加至关重要了。

**关联阅读：**

*   《异地网络远程访问指北》[上](https://sspai.com/prime/story/remote-lan-access-guide-01) [中](https://sspai.com/prime/story/remote-lan-access-guide-02) [下](https://sspai.com/prime/story/remote-lan-access-guide-03)
*   [过年返乡之后，我是如何远程访问家中设备的？](https://sspai.com/post/77971)

## 目前的远程访问方案

总的来说，从外网访问内网的服务大致有三种方案：

*   获取公网 IP + DDNS 解析
*   隧道穿透
*   构建虚拟局域网

![](https://cdn.sspai.com/2023/12/17/c491f349a20efdcdbb5419aaf193751f.png)

使用 DDNS 是最为简单的访问方法，但目前可行性越来越低

如果你家的宽带能获得公网 IP，直接使用 DDNS 是一种灵活的解决方案。只需配置好 DDNS 解析及端口转发，便可通过域名加端口的方式在公网访问内网映射的服务。这种配置简单，速度只受家庭上行带宽限制。但这种方案的可行性正逐渐降低。主要是因为 IPv4 地址枯竭，国内宽带运营商不再为家庭用户分配公网 IP，导致许多家用宽带的 IP 地址是内网地址，无法实现动态地址解析，从而使得外部访问变得越发艰难。

![](https://cdn.sspai.com/2023/12/17/a61378b9e9776d72f3a22ddfbe77b1ba.png)

frp 作为最为常用的内网穿透工具，难点主要是客户端配置编辑较为复杂

隧道穿透方案，即通过一台具有公网 IP 的服务器作为跳板，暴露内网服务到公网中实现访问，这个方案的优点在于网络访问稳定，带宽速度取决于公网 IP 服务器的带宽。缺点则是配置较为复杂，需要在服务器上安装相关的服务，还需要在内网服务端写配置项。同时隧道穿透对一些网络协议支持较差，尤其是 HTTPS 协议配置极其复杂繁琐。

![](https://cdn.sspai.com/2023/12/17/702a770c092b8577b347fc849b5454b0.png)

最后一种方案则是构建虚拟局域网，简单来说就是将分处不同网络下的设备跨网络组建在一个虚拟局域网中，从而实现基于内网 IP 的设备间互访，这种方案最大的好处在于不受限于网络协议，并且部署安装客户端较为简单并支持私有化部署，缺点则是提供该服务的厂商多来自国外，相对应的是服务在国内网络环境下稳定下较差。

基于构建虚拟局域网的服务目前主流的有 ZeroTier、Tailscale 以及国产的蒲公英。而在我的横向对比以及测试中最终选择了更为灵活的 ZeroTier，首先就是家用的情况下，即便是官方的 ZeroTier 也几乎不产生任何费用，支持通过 ID 的方式就可以直接加入自建的虚拟局域网中（Tailscale 添加新设备需要单点登录授权），更重要的是目前 ZeroTier 提供了更为灵活的自部署方案，无论是操作上还是方法上都远比另两款服务更为简单。

## Zerotier 官方服务的问题

虽然我选择了 Zerotier 来构建虚拟局域网实现外网访问内网，但却并不使用其官方服务，最重要的一点就是官方的根服务器（行星服务器）都部署在海外，由于国内互联网的特殊性导致会出现较高的延迟，从而就会影响到组网的稳定性。虽然可以通过在国内自建 Moon 服务器（卫星服务器）来来缓解解决访问问题，但由于虚拟局域网解析依旧取决于根服务器，所以最为直接的办法就是完全在国内互联网上自建行星服务器（根服务器）以及网络控制器，从而从本质上实现最为高效稳定的虚拟局域网构建。

![](https://cdn.sspai.com/2023/12/17/38f8952d6215153561003a1885fa7ea4.png)

而这样做的优点是：不受制于国外网络访问速度，整个流程完全自主可控，而实际上费用也是最低的——你仅仅只需要从国内各大云服务器厂商那里购买一台配置极低的云服务器，一年费用可能都不到百元。

## 自建 ZeroTier 行星服务器

和 Tailscale 类似，Zerotier 同样也可以实现网络控制器以及根服务器的自部署，只不过以前我们只能自建卫星服务器（Moon 服务器）以及网络控制器，而现在则可以实现自部署根服务器（行星服务器），这样你完全不需要注册官方的 Zerotier 的任何账号也可以实现整个虚拟局域网的自建。

### 在云服务器中安装 Zerotier 行星服务器

首先第一件事就是购买一台国内云服务提供的云服务器，整体规格上「1 核 2G」或者「2 核 2G」就可以，最重要的需要有一个公网 IP 方便进行设备管理，在开始之前我们需要打开云服务器的防火墙，额外放行 3443 端口（TCP）和 9993 端口（TCP 和 UDP）。

![](https://cdn.sspai.com/2023/12/17/8565f110ba3a243a9f19791474c1fd46.png)

接下来我们使用 SSH 客户端以 root 权限登录云服务器，然后根据服务器中发行版不同先更新系统组件并安装 Git、docker 并启动 docker：

```
# debian 系检查更新
apt update
 # debian 系无需确认安装 git
apt install -y git 
 # 通过 docker 官方源安装 docker
curl -fsSL https://get.docker.com |bash
 # 通过 systemd 启动 docker 服务
systemctl start docker
```

```
# red hat 系检查更新
yum update
 # red hat 系无需确认安装 git
yum install git -y
 # 通过 docker 官方源安装 docker
curl -fsSL https://get.docker.com |bash
 # 通过 systemd 启动 docker 服务
systemctl start docker
```

接着，我们需要复制一份 [xubiaolin 制作了自建行星服务器安装脚本](https://sspai.com/link?target=https%3A%2F%2Fgithub.com%2Fxubiaolin%2Fdocker-zerotier-planet)：

```
# 复制一份 xubiaolin 制作了自建行星服务器安装脚本
git clone https://ghproxy.markxu.online/https://github.com/xubiaolin/docker-zerotier-planet.git

# 进入具体目录
cd docker-zerotier-planet

# 运行脚本
./deploy.sh
```

脚本会给出相关的提示选择，这里直接输入 `1` 回车来安装，安装过程中要你输入相应的端口，这里全部选择默认即可。之后就是创建容器的过程，如果你和我一样使用的是性能比较低的云服务器，那么整个安装等待会比较长（十分钟左右）。

当你看到类似终端界面出现`Successfully copied 2.048kB to /tmp/planet` 的字样就表示整个安装过程已经结束，当然你如果不确定的话可以使用如下命令来判断该容器是否已经启动：

```
docker ps
```

如果在 `STATUS` 下面显示为 Up 表示容器已经启动，那么接下来直接在浏览器的地址栏输入 `http://云服务器ip:3443`来打开网络管理后台，如果可以看到如下登录页面就算是服务器端安装成功了。

![](https://cdn.sspai.com/2023/12/17/d3a7033e184ead4a424cac32f5aa06b0.png)

所有运行完成之后，这个自建的虚拟局域网服务会生成一个名为`planet` 的文件，这个也是后面我们在配置客户端时需要的，这里使用 SSH 客户端进入到 `docker-zerotier-planet` 目录，然后继续运行 `./deploy.sh` 这个脚本，输入数字 3 回车后将 `planet` 文件拷贝到当前目录，然后使用 sFTP 客户端将文件复制回本地待用即可。

![](https://cdn.sspai.com/2023/12/17/16f7ca25afce5d65816ed1cf487deb46.png)

### 给自建的 Zerotier 设置网络

在本地打开浏览器，然后访问`http://云服务器ip:3443` 进入到网络控制器登录页面：

![](https://cdn.sspai.com/2023/12/17/861f4c9769ed711133659b33ee9b4b11.png)

使用默认账号：`admin`、密码：`password` 登录后，点击选项卡中的 `Add Network` 来创建一个网络。

![](https://cdn.sspai.com/2023/12/17/eda5e3a422046c08ac54cbc29bf48214.png)

创建完成后会自动跳转到新建的这个网络详情页面中，然后点击上方 `IPv4 Assign Mode` ，再勾选`Auto-assign from IP Assignment Pool` 来让新加入网络的设备自动从地址池中获取一个 IP。

![](https://cdn.sspai.com/2023/12/17/55732fad6c46e605bf9fa95372699937.png)

另外需要单独保存的是对应的网络 ID，比如说我创建的这个名为`ceshi` 网络后面对应的一串字符，这个单独保存下来备用，后面需要通过这个 ID 让客户端加入到你创建的这个 ID 中。

### 客户端加入

由于我的主要用途是让随身携带的笔记本电脑可以随时访问到家中的群晖，因此需要的是将家中的群晖、Mac 电脑以及 Windows 笔记本加入到同一个虚拟局域网中。

#### Windows 系统设备设置

首先下载[官方的 ZeroTier Windows 客户端安装包](https://sspai.com/link?target=https%3A%2F%2Fdownload.zerotier.com%2Fdist%2FZeroTier%2520One.msi)并进行安装。

第二步：安装完毕之后使用文件资源管理器访问如下路径：`C:\ProgramData\ZeroTier\One`，使用此前从云服务器中拷贝复制下来的 `planet` 文件替换目录下的同名文件。

![](https://cdn.sspai.com/2023/12/17/7b7493406f7b7aef78a60d1c9dc3a4cd.png)

第三步：打开`服务` 并选中服务列表中的 ZeroTier One，点击左上方的`重启动服务`。

![](https://cdn.sspai.com/2023/12/17/2e50cdb039ddfa7704a80a2f355e1ae9.png)

第四步：右键任务栏的 Windows 徽标按钮，选择`终端管理员`，然后输入如下命令：

```
cd C:\Windows\system32
zerotier-cli.bat join 网络 ID
```

输入后看到 200 Join OK 就表示当前设备已经加入到我们创建的这个虚拟局域网中了，这时再使用浏览器打开`http://云服务器 ip:3443`，点击 `Network` 选择你创建的网络，会看到网络详情列表下面就会出现一个新的设备，你可以在 `Nember name` 下面给他进行备注，然后勾选 `Authorized` 让其加入网络即可，稍后你就可以在 IP assignment 下看到这台设备分配的内网 IP 地址了。

![](https://cdn.sspai.com/2023/12/17/ae0837d5a9cffdad35bdf75e6bccd09d.png)

#### macOS 系统设备的设置

首先依旧是[下载官方的 ZeroTier macOS 客户端](https://sspai.com/link?target=https%3A%2F%2Fdownload.zerotier.com%2Fdist%2FZeroTier%2520One.pkg)并进行安装。

第二步：安装完毕之后，使用访达进入到目录`/Library/Application Support/ZeroTier/One`，使用此前从云服务器中下载的 `planet` 文件替换目录下的同名文件。

![](https://cdn.sspai.com/2023/12/17/a301c58ec7c1c6440762c60906b9e8ca.png)

第三步：打开终端，输入如下命令重启 ZeroTier One 客户端：

```
cat
 /Library/Application Support/ZeroTier/One/zerotier-one.pid | 
sudo
 xargs 
kill
```

紧接着在终端中输入如下命令加入你创建的虚拟局域网网络：

```
zerotier-cli join 网络 id
```

如果显示`200 join OK` 则表示加入成功。

最后，我们使用浏览器输入 `http://云服务器ip:3443`访问网络管理后台，点击 `Network` 选择你创建的网络，会看到网络详情列表下面就会出现一个新的设备，你可以在 `Nember name` 下面给他进行备注，然后勾选 `Authorized` 让其加入网络即可。

![](https://cdn.sspai.com/2023/12/17/5be9674e6b4d352c7e75df16800fab2b.png)

同步在终端输入命令：`zerotier-cli peers` 可以看到加入设备的角色以及对应的网络，如果云服务器对应的角色是 Planet 而刚刚加入网络的设备角色是 LEAF 就表示基于国内网络的虚拟局域网已经创建成功了。

#### **群晖设备的设置**

我的主要目的是让群晖和我随身携带的笔记本电脑处于相同的局域网中，其实最重要的就是群晖了，这里我首先将从云服务器中下载的`planet`文件拷贝到群晖的文件目录中，这里我将其拷贝到 `soft backup`这个文件夹下面。

![](https://cdn.sspai.com/2023/12/17/2059b767f5868ae5ae92c5cc1dc9f928.png)

接下来，我们打开群晖的套件中心，在`设置`-`套件来源` 里面加上「矿神源」——[https://spk7.imnks.com/](https://sspai.com/link?target=https%3A%2F%2Fspk7.imnks.com%2F)。然后在套件中心侧边栏中选择「社群」，找到 ZeroTier 并选择安装。

![](https://cdn.sspai.com/2023/12/17/4a2ec597a9649cabc4cb75d4e5526250.png)

套件安装完成后先不要启动。而是通过 SSH 客户端链接群晖，输入以下命令修复套件：

```
sudo sed -i 's/package/root/g' /var/packages/zerotier/conf/privilege
```

然后再输入一下命令将刚才我们上传的 `planet`文件复制到套件目录中：

```
mv /volume1/@appdata/zerotier/planet /volume1/@appdata/zerotier/planet.bak 
cp /volume1/soft backup/planet /volume1/@appdata/zerotier/
```

这时再回到群晖的`套件中心`启动 ZeroTier。这时在 SSH 客户端输入如下命令来让群晖加入到你自建的虚拟局域网中：

```
cd /var/packages/zerotier/target/bin 

./zerotier-one -q join 网络 ID
```

显示 200 join OK 就表示链接成功，使用浏览器访问`http://云服务器ip:3443`管理后台，在网络详情页面中找到新增的群晖，然后勾选 `Authorized` 让其加入网络即可。

## **结语**

自建 Zerotier 行星服务器可以所有设备均在国内网络环境下直连，相比官方根服务器设在海外，延迟显著降低。由于这种自建虚拟局域网对网络协议限制较少，通过 Samba 协议创建的文件服务可直接通过内网 IP 访问，无需配置域名即可使用 webdav 协议访问，简化了操作。

考虑到群晖官方 QuickConnect 连接将仅支持中继访问，自建 ZeroTier 虚拟局域网有效提升了互访性能。例如，依赖 Synology Drive 的用户如我，客户端连接群晖的问题大大减少。

如果你也希望提升不同网络下桌面设备与家中内网服务器的互访性能，可以尝试完全自部署的 ZeroTier，或许会带来不同的新体验。

> 下载少数派 [客户端](https://sspai.com/page/client)、关注 [少数派小红书](https://sspai.com/link?target=https%3A%2F%2Fwww.xiaohongshu.com%2Fuser%2Fprofile%2F63f5d65d000000001001d8d4)，感受精彩数字生活 🍃

> 实用、好用的[正版软件](https://sspai.com/mall)，少数派为你呈现🚀