---
url: https://zhuanlan.zhihu.com/p/670596856
title: [sumo 基础篇 | 路网建模 4-1] - 如何基于 xml 定义节点 / 交叉口
date: 2024-02-27 20:24:26
tag: 
banner: "https://picx.zhimg.com/v2-02bffbe29c556e95a5719c2f92214c7e_720w.jpg?source=172ae18b"
banner_icon: 🔖
---
### **前言：**

本讲为如何基于 xml 定义仿真路网的第一个子专题：基于 xml 定义节点 / 交叉口。本讲主要向读者介绍 sumo 路网中什么是节点 / 交叉口、定义节点 / 交叉口的方法、节点 / 交叉口参数有哪些、如何定义节点 / 交叉口的简单示例。通过本课程的学习，读者可以初步掌握基于 xml 定义节点 / 交叉口的方法，为构建真实路网场景的仿真模型打下基础。

本讲的内容主要包括：

1. 什么是节点 / 交叉口

2.sumo 定义节点 / 交叉口的方法

3. 节点 / 交叉口参数解析

4. 节点 / 交叉口定义示例

### **1. 什么是节点 / 交叉口**

在 SUMO 中节点主要用于描述路网拓扑关系中的点，它既可以表示路段之间的连接处，也可以表示为路网中的交叉口。

### **2.sumo 定义节点 / 交叉口的方法**

sumo 中通过 node.xml 文件来定义节点 / 路口要素，节点 / 路口要素中包含节点的 id、x 坐标、y 坐标、通行管控方式 (type）、信号控制模式（tlType、tlLayout）、通行优先权（rightOfWay）等属性参数，其中 node.xml 文件可以通过记事本的方式进行打开和编辑，如下图所示：

![](https://pic2.zhimg.com/v2-50eb8c810d3014851a26c6cac2ef8ad9_r.jpg)

在节点 node.xml 文件中，每一个节点都用一行描述，如下所示：

<table data-draft-node="block" data-draft-type="table" data-size="normal" data-row-style="normal"><tbody><tr><td>&lt;node x="&lt;FLOAT&gt;" y="&lt;FLOAT&gt;" [type="&lt;type&gt;"]/&gt;</td></tr></tbody></table>

其中直括号（'['和']'）表示参数是可选的。这些参数每一个都有一定的含义和取值值范围，具体节点 / 交叉口有哪些参数及参数的含义见下一节。

### **3. 节点 / 交叉口参数解析**

sumo 中描述节点 / 交叉口参数有 14 个，具体如下表：

<table data-draft-node="block" data-draft-type="table" data-size="normal" data-row-style="normal"><tbody><tr><td>参数名</td><td>值类型型</td><td>含义说明</td></tr><tr><td>id</td><td>id (string)</td><td>节点的 id 编号</td></tr><tr><td>x</td><td>float</td><td>节点的 x 坐标</td></tr><tr><td>y</td><td>float</td><td>节点的 y 坐标</td></tr><tr><td>z</td><td>float</td><td>节点的 z 坐标</td></tr><tr><td>type</td><td>string</td><td>节点通行管控方式，取值为 "priority", "traffic_light","right_before_left" 等 13 种，具体各取值含义见下一讲：[sumo 基础篇 | 路网建模 4-1-1] - 如何设置交叉口通行管控方式</td></tr><tr><td>tlType</td><td>string</td><td>信号控制类型，取值："static", "actuated"，具体取值含义见下一讲：[sumo 基础篇 | 路网建模 4-1-2] - 如何设置交叉口信号控制模式及放行方式</td></tr><tr><td>tlLayout</td><td>string</td><td>信号放行方式，取值为 "opposites" 等 3 种，具体各取值含义见：[sumo 基础篇 | 路网建模 4-1-2] - 如何设置交叉口信号控制模式及放行方式</td></tr><tr><td>tl</td><td>id (string)</td><td>信号配时方案 id</td></tr><tr><td>radius</td><td>float</td><td>所有转向的转弯半径，默认为 1.5 米</td></tr><tr><td>shape</td><td>List</td><td>点组成的列表，自定义的路口几何形状，如果给定列表不足两个点元素，在使用 netconvert 转换工具生成路网时，会自动推算出其形状</td></tr><tr><td>keepClear</td><td>bool</td><td>是否激活避免路口锁死机制</td></tr><tr><td>rightOfWay</td><td>string</td><td>路权，取值：default、edgePriority、mixedPriority、allwayStop，具体各取值含义见：[sumo 基础篇 | 路网建模 4-1-3] - 如何设置车流在交叉口的优先通行方式</td></tr><tr><td>fringe</td><td>string</td><td>不允许进入该路段的车辆类型</td></tr><tr><td>controlledInner</td><td>list</td><td>与节点相连接的边</td></tr></tbody></table>

### **4. 节点 / 交叉口定义示例**

1）示例 1：定义一个节点 id 为 "0"，节点 x 坐标为 12，节点 y 坐标为 15 的节点，则在 node.xml 示例如下：

<table data-draft-node="block" data-draft-type="table" data-size="normal" data-row-style="normal"><tbody><tr><td>&lt;nodes&gt; &lt;node x="12" y="15" /&gt;&lt;/nodes&gt;</td></tr></tbody></table>

2）示例 2：同时定义多个节点， 一个节点 id 为 "0"，节点 x 坐标为 12，节点 y 坐标为 15 的节点；另一个节点 id 为 "1"，节点 x 坐标为 100，节点 y 坐标为 100 的节点；...，则在 node.xml 示例如下：

<table data-draft-node="block" data-draft-type="table" data-size="normal" data-row-style="normal"><tbody><tr><td>&lt;nodes&gt; &lt;node x="12" y="15" /&gt; &lt;node x="100" y="100" /&gt; ...&lt;/nodes&gt;</td></tr></tbody></table>