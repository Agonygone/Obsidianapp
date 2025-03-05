---
url: https://zhuanlan.zhihu.com/p/671899872
title: [sumo 基础篇 | 路网建模 4-2] - 如何基于 xml 定义路段
date: 2024-02-27 20:24:31
tag: 
banner: "https://pic1.zhimg.com/v2-3827ba7fe386bff043d5b882a872664d_720w.jpg?source=172ae18b"
banner_icon: 🔖
---
## **前言：**

本讲为如何基于 xml 定义仿真路网的第二个子专题：基于 xml 定义路段，主要介绍了 sumo 路网中什么是路段、定义路段的方法、路段及路段上各车道可定义的参数有哪些、如何定义路段的简单示例。通过本课程的学习，读者可以初步掌握定义路段的方法，为 sumo 路网的构建打下基础。

本讲的内容主要包括：

1. 什么是路段

2.sumo 中定义路段的方法

3.sumo 中路段及车道参数解析

4. 如何定义路段的示例讲解

### **1. 什么是路段**

在 sumo 中路段是路网的基本单元，定义为相邻两个节点 / 交叉口相连接的道路段。

### **2.sumo 中定义路段的方法**

sumo 中通过 edge.xml 文件来定义路段要素，路段要素中包含路段 id、起始节点 id(from)、到达节点 id(to)，车道数 numLanes、路段的几何走向（shape）、路权设置（allow/disallow）、路段限速（speed）等参数。其中 edge.xml 文件可以通过记事本的方式进行打开和编辑，如下图所示：

![](https://pic2.zhimg.com/v2-9ebe6e4878adfbadec947ca14d527cfd_r.jpg)

在节点 edge.xml 文件中，每一条路段都用一行描述，如下所示：

<table data-draft-node="block" data-draft-type="table" data-size="normal" data-row-style="normal"><tbody><tr><td>&lt;edge from="&lt;NODE_ID&gt;" to="&lt;NODE_ID&gt;" [type="&lt;STRING&gt;"] [numLanes="&lt;INT&gt;"] [...] /&gt;</td></tr></tbody></table>

其中直括号（'['和']'）表示参数是可选的。这些参数每一个都有一定的含义和取值值范围，具体路段有哪些参数及参数的含义见下一节。

同时，为精细化定义路段中各车道的属性，如设置路段中某一车道为公交专用道，可在路段中进一步定义各车道信息，如下图所示：

![](https://pic3.zhimg.com/v2-d0173118a6f74c1dfc1c3a5eb3b38192_r.jpg)

在 edge.xml 中，每一行 <lane index="<STRING>" [allow="<STRING>" ] [...] /> 表示一车道，其中直括号（'['和']'）表示参数是可选的。具体车道有哪些参数及参数的含义见下一节。

注：sumo 中车道的编号规则是按路段前进方向，从右往左依次从 0 开始编号，即第 0 车道为该路段的最右侧车道。

### **3.sumo 中路段及车道参数解析**

Sumo 中描述路段的参数有 14 个，具体如下表：

<table data-draft-node="block" data-draft-type="table" data-size="normal" data-row-style="normal"><tbody><tr><td>参数名</td><td>值类型型</td><td>含义说明</td></tr><tr><td>id</td><td>string</td><td>路段的 id 编号</td></tr><tr><td>from</td><td>string</td><td>路段的起点节点的 id 编号</td></tr><tr><td>to</td><td>string</td><td>路段的终点节点的 id 编号</td></tr><tr><td>type</td><td>type id</td><td>路段类型</td></tr><tr><td>numLanes</td><td>int</td><td>路段车道数</td></tr><tr><td>speed</td><td>float</td><td>路段的最大限速，默认 50km/h</td></tr><tr><td>priority</td><td>int</td><td>路权优先级</td></tr><tr><td>length</td><td>float</td><td>路段长度</td></tr><tr><td>shape</td><td>List</td><td>描述路段走向，包含路段起点、中心点、终点坐标</td></tr><tr><td>spreadType</td><td>string</td><td>表示路段沿参考线进行车道面域扩展，默认 "right"(从右向左展开)，还可设定为 "center" 或 "roadCenter"</td></tr><tr><td>allow</td><td>list</td><td>允许进入该路段的车辆类别，sumo 中定义了 24 种具体的车辆类别，具体见备注 1</td></tr><tr><td>disallow</td><td>list</td><td>不允许进入该路段的车辆类别，sumo 中定义了 24 种具体的车辆类别，具体见备注 1</td></tr><tr><td>width</td><td>float</td><td>路段宽度，所有车道宽度之和</td></tr><tr><td>name</td><td>string</td><td>路段名称</td></tr></tbody></table>

sumo 中描述车道的参数有 11 个，具体如下表：

<table data-draft-node="block" data-draft-type="table" data-size="normal" data-row-style="normal"><tbody><tr><td>参数名</td><td>值类型型</td><td>含义说明</td></tr><tr><td>index</td><td>int</td><td>车道编号</td></tr><tr><td>allow</td><td>list</td><td>允许进入该车道的车辆类别集合，sumo 中定义了 24 种具体的车辆类别，具体见备注 1</td></tr><tr><td>disallow</td><td>list</td><td>禁止进入该车道的车辆类别集合，sumo 中定义了 24 种具体的车辆类别，具体见备注 1</td></tr><tr><td>changeLeft</td><td>list</td><td>允许从当前车道换道至左侧的车辆类别集合，sumo 中定义了 24 种具体的车辆类别，见备注 1</td></tr><tr><td>changeRight</td><td>list</td><td>允许从当前车道换道至右侧的车辆类别集合，sumo 中定义了 24 种具体的车辆类别，见备注 1</td></tr><tr><td>speed</td><td>float</td><td>车道的最大限速</td></tr><tr><td>width</td><td>float</td><td>车道宽度</td></tr><tr><td>endOffset</td><td>float</td><td>车道的停车线后移距离，主要用于一些特殊路口</td></tr><tr><td>shape</td><td>list</td><td>描述车道走向，和路段元素 “shape” 含义一致</td></tr><tr><td>type</td><td>string</td><td>车道类型，可以自定义</td></tr><tr><td>acceleration</td><td>bool</td><td>是否为加速车道，默认 false</td></tr></tbody></table>

备注 1：sumo 中定义了 24 种具体的车辆类别：private（私家车）、truck（卡车 / 货车）、emergency（救护车）、trailer（带拖车的卡车）、authority（公务车）、motorcycle（摩托车）、army（军车）、moped（轻便摩托车）、vip （vip 车辆）、bicycle（自行车）、pedestrian（行人）、evehicle（电动汽车）、passenger（小型客车 sumo 默认车型）、tram（有轨电车）、hov（合乘车）、rail_urban（城轨）、taxi（出租车）、rail（重载铁路机车）、bus（公交车）、rail_electric（重载电气化铁路机车）、coach（长途客车）、rail_fast（高速铁路机车）、delivery（快递车）、ship（船）

### **4. 如何定义路段的示例讲解**

1）示例 1：定义一个路段 id 为 "4o"，起点节点 id 为 "0"，终点节点 id 为 "4"，车道数（numLanes）为 1 的路段，则在 edge.xml 中示例如下：

<table data-draft-node="block" data-draft-type="table" data-size="normal" data-row-style="normal"><tbody><tr><td>&lt;edges&gt; &lt;edge from="0" to="4" numLanes="1"/&gt;&lt;/edges&gt;</td></tr></tbody></table>

2）示例 2：定义一个路段 id 为 "4o"，起点节点 id 为 "0"，终点节点 id 为 "4"，车道数（numLanes）为 2 的路段，路段最右侧车道为公交专用道，则在 edge.xml 中示例如下：

<table data-draft-node="block" data-draft-type="table" data-size="normal" data-row-style="normal"><tbody><tr><td>&lt;edges&gt;&lt;edge from="0" to="4" numLanes="1"&gt;&lt;lane index="0" allow="bus" /&gt;&lt;/edge&gt;&lt;/edges&gt;</td></tr></tbody></table>

3）示例 3：同时定义多条路段：一个路段 id 为 "4o"，起点节点 id 为 "0"，终点节点 id 为 "4"，车道数（numLanes）为 1；一个路段 id 为 "5"，起点节点 id 为 "4"，终点节点 id 为 "8"，车道数（numLanes）为 2；...，则在 edge.xml 中示例如下：

<table data-draft-node="block" data-draft-type="table" data-size="normal" data-row-style="normal"><tbody><tr><td>&lt;edges&gt; &lt;edge from="0" to="4" numLanes="1"/&gt; &lt;edge from="4" to="8" numLanes="2"/&gt; ...&lt;/edges&gt;</td></tr></tbody></table>

**注意：起点节点 id 和终点节点 id 必须为 node.xml 中定义的节点**