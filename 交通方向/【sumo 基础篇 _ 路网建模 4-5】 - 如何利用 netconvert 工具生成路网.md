
## **前言：**

本讲为 [sumo 基础篇路网建模](https://mp.weixin.qq.com/mp/appmsgalbum?__biz=MzkzMzM0MzgwOQ==&action=getalbum&album_id=3199393822406017024&scene=173&subscene=&sessionid=svr_b2df061eb21&enterid=1703597153&from_msgid=&from_itemidx=&count=3&nolastread=1#wechat_redirect)系列课程的最后一讲。通过前面课程的学习，你已掌握如何通过 [xml 定义节点](http://mp.weixin.qq.com/s?__biz=MzkzMzM0MzgwOQ==&mid=2247483880&idx=1&sn=85f0a9f9e06f4aaad61e49a261f80790&chksm=c24ca6c6f53b2fd01e091f5dc412fd354d44b517db2a33207cf1a554f35a86203cef11b1cf13&scene=21#wechat_redirect)（node.xml）、[路段 / 边](http://mp.weixin.qq.com/s?__biz=MzkzMzM0MzgwOQ==&mid=2247483894&idx=1&sn=75dbd1c15d088c44d75537542285dadb&chksm=c24ca6d8f53b2fce29dbc9b92474ae01eae82d66eb94b0e02521cf6988a6537ca0a4a41b8eb2&scene=21#wechat_redirect)（edge.xml）、[车道连接关系](http://mp.weixin.qq.com/s?__biz=MzkzMzM0MzgwOQ==&mid=2247483942&idx=1&sn=c7bef34fa74e3a9dab4b3dadc390fc33&chksm=c24ca508f53b2c1e41f92c3a255ca599bbebb647a0af10a6b15132804f36a3453f5b4d15185f&scene=21#wechat_redirect)（connect.xml）、[路口信号配时](http://mp.weixin.qq.com/s?__biz=MzkzMzM0MzgwOQ==&mid=2247483943&idx=1&sn=d51def19b9ed24e350c47620bcb0d466&chksm=c24ca509f53b2c1fe30ee6cbcb36b7236729777b6c7f63518f572fd69dd2924246c8f56a1ba4&scene=21#wechat_redirect)（tll.xml）等路网基础要素的方法。本讲将教你如何通过 sumo 自带的 netconvert 工具，基于前述的路网基础要素，生成路网拓扑 net.xml 文件。课程中详细的介绍了每一步操作流程，且提供了两个案例的基础数据文件，读者可自行下载学习。

利用 netconvert 工具生成路网主要流程如下：

1. 准备基础数据文件

2. 复制基础数据文件所在的存储路径

3. 双击运行 start-command-line.bat

4. 在 cmd 命令行界面中，切换至基础数据文件所在目录

5. 在 cmd 命令行界面中，执行 netconvert 命令，生成路网

### **1. 准备基础数据文件**

读者可根据实际建模的需要，按作者基础篇 | 路网建模 4.1-4.4 节课程中所授的方法定义 node.xml、edge.xml、connect.xml、tll.xml 等基础数据文件，亦可下载作者提供的两个案例的基础数据文件（下载方式：读者请私信留下邮箱，24 小时内发送）。

两个案例的基础数据文件，一个是信号控制交叉口的案例，它包含 node.xml、edge.xml、connect.xml、tll.xml 基础数据文件；另一个是无信号控制交叉口的案例，它包含 node.xml、edge.xml、connect.xml 基础数据文件。

### **2. 复制基础数据文件所在的存储路径**

找到 node.xml、edge.xml 等基础数据文件所在的存储路径，如 D:\anzhuangruanjianmulu\sumo\doc\examples\4.5\signal_intersection_sample，并复制。

### **3. 双击运行 start-command-line.bat**

在 sumo 安装目录的 bin 文件夹中（如 D:\anzhuangruanjianmulu\sumo\bin）找到 start-command-line.bat。

![](https://pic1.zhimg.com/v2-2dca228d57e6855635a8bb92056d586c_r.jpg)

双击运行 start-command-line.bat，进入 cmd 命令行输入界面：

![](https://pic2.zhimg.com/v2-578df7757e94528df44d02edb05f5a01_r.jpg)

### **4. 在 cmd 命令行界面中，切换至基础数据文件所在目录**

在界面中分别输入如下两行命令：

<table data-draft-node="block" data-draft-type="table" data-size="normal" data-row-style="normal"><tbody><tr><td>1）cd D:\anzhuangruanjianmulu\sumo\doc\examples\4.5\signal_intersection_sample2）d:</td></tr></tbody></table>

切换至基础文件所在目录 signal_intersection_sample 文件夹中

![](https://pic3.zhimg.com/v2-0bb3a2bbee26a9bee4bf8a0a0eb2f3ce_r.jpg)

### **5. 在 cmd 命令行界面中，执行 netconvert 命令，生成路网**

在界面中输入如下 netconvert 命令，并回车。

<table data-draft-node="block" data-draft-type="table" data-size="normal" data-row-style="normal"><tbody><tr><td>netconvert --node-files=node.xml --edge-files=edge.xml --connection-files=connect.xml --tllogic-files=tll.xml --output-file=output.net.xml --no-turnarounds=true</td></tr></tbody></table>

![](https://pic1.zhimg.com/v2-999c6f4a11f9825ad703959da8628854_r.jpg)

显示 Success，即可在目录 D:\anzhuangruanjianmulu\sumo\doc\examples\4.5\signal_intersection_sample 中找到生成的 output.net.xml，在 sumo gui 中加载显示如下：

![](https://pic4.zhimg.com/v2-20431bb2d43ea0cbd7a99d667d95dd6b_r.jpg)

当无 tll.xml 文件时，netconvert 命令如下：

<table data-draft-node="block" data-draft-type="table" data-size="normal" data-row-style="normal"><tbody><tr><td>netconvert --node-files=node.xml --edge-files=edge.xml --connection-files=connect.xml --output-file=output.net.xml --no-turnarounds=true</td></tr></tbody></table>