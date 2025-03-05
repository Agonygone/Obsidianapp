
## **前言：**

本讲为如何基于 xml 定义仿真路网的第三个子专题：基于 xml 定义车道连接关系。通过本课程的学习，读者可以全面掌握基于 xml 定义车道连接关系的方法，为 sumo 路网的构建打下基础。

本讲的内容主要包括：

1. 什么是车道连接关系

2.sumo 中定义车道连接关系的方法

3.sumo 中车道连接的参数解析

4. 如何定义车道连接关系的简单示例

### **1. 什么是车道连接关系**

在 SUMO（Simulation of Urban MObility）中，车道连接（connection）通常是指上游路段的车道与下游路段的车道之间的连接关系，用于描述车辆在交叉口、道路交汇处、车道数变化处如何在不同上下游车道之间的转换规则。如在交叉口中，东进口道的哪几条车道可以左转，与南出口的哪几条车道相连接，都需要通过车道连接关系来定义。

### **2.sumo 中定义车道连接关系的方法**

sumo 中通过 connect.xml 文件来定义车道连接关系，车道连接关系具体定义了上游路段的第几车道与下游路段的第几车道相连接，车道连接关系中包含上游路段 id(from)、下游路段 id(to)、上游路段车道 id(fromLane)，下游路段车道 id(toLane) 等参数。其中 connect.xml 文件可以通过记事本的方式进行打开和编辑，如下图所示：

![](https://pic1.zhimg.com/v2-3ef2f36cc1c6ff87bd5bc81302e80744_r.jpg)

在 connect.xml 文件中，具体的每一个车道连接都用一行描述，如下所示：

<table data-draft-node="block" data-draft-type="table" data-size="normal" data-row-style="normal"><tbody><tr><td>&lt;connection from="&lt;FROM_EDGE_ID&gt;" to="&lt;T0_EDGE_ID&gt;" [fromLane="&lt;INT&gt;"] [...]/&gt;</td></tr></tbody></table>

其中直括号（'['和']'）表示参数是可选的。这些参数每一个都有一定的含义和取值值范围，具体车道连接有哪些参数及参数的含义见下一节。

### **3.sumo 中车道连接的参数解析**

sumo 中描述车道连接的参数有 18 个，具体如下表：

![](https://pic1.zhimg.com/v2-47d7bd64bea6834a8c70dc75026139e8_r.jpg)

### **4. 如何定义车道连接关系的简单示例**

如上游路段 "1si" 相邻的下游路段为路段 "3o"，路段 "1si" 的第 1 车道与路段 "3o" 的第一车道连接，路段 "1si" 的第 2 车道与路段 "3o" 的第 2 车道连接。则此连接关系在 connect.xml 中定义示例如下：

<table data-draft-node="block" data-draft-type="table" data-size="normal" data-row-style="normal"><tbody><tr><td>&lt;connections&gt; &lt;connection from="1si" to="3o" fromLane="0" toLane="0"/&gt; &lt;connection from="1si" to="3o" fromLane="1" toLane="1"/&gt;&lt;/connections&gt;</td></tr></tbody></table>

注意：路段 "1si"、路段 "3o" 必须是在 edge.xml 中定义的边 id