# Arcgis 计算公路用地面积的方法

## 1.原始数据准备 

主要包括三类数据：

|  类型  |                          数据要求                          | 数据格式 |
| :----: | :--------------------------------------------------------: | :------: |
| 用地图 |       包括新用地界、旧用地界两个文件，应为闭合多段线       | dxf/dwg  |
| 区划图 | 村界、镇界等行政边界，闭合多段线，不同行政区放置在不同图层 | dxf/dwg  |
| 地类图 |             闭合多段线，不同地类放置在不同图层             | dxf/dwg  |

详细说明：

- 数据类型均为dxf/dwg格式，推荐使用dxf，闭合多段线是必须条件，需要注意的是，**多段线标高应为0**

- 区划图、地类图必须分图层，否则难以计算；如果测绘部门提供的是图层文件（lyr)或者Arcgis项目文件（mxd)等，可导入软件后进行相关操作

  例如

  ![image-20230612171129324](C:\Users\chen\AppData\Roaming\Typora\typora-user-images\image-20230612171129324.png)

  ![image-20230612171152817](C:\Users\chen\AppData\Roaming\Typora\typora-user-images\image-20230612171152817.png)

  

## 2.数据处理

打开Arcgis，连接文件夹并导入原始数据

![image-20230612171402163](C:\Users\chen\AppData\Roaming\Typora\typora-user-images\image-20230612171402163.png)

![image-20230612171429273](C:\Users\chen\AppData\Roaming\Typora\typora-user-images\image-20230612171429273.png)

![image-20230612171543791](C:\Users\chen\AppData\Roaming\Typora\typora-user-images\image-20230612171543791.png)

可以看到，dxf文件中又包含了多种要素，包括point、polyline(多段线)、polygon(面)等，我们只要其中的面要素即可。方便查看，这里我们可以右击图层创建一个新的图层组，将面要素移动到该图层

![image-20230612172005026](C:\Users\chen\AppData\Roaming\Typora\typora-user-images\image-20230612172005026.png)

将用地界转为shp文件（实际上，如果多段线不多的话，用奥维也可以转）

![image-20230612172440513](C:\Users\chen\AppData\Roaming\Typora\typora-user-images\image-20230612172440513.png)

![image-20230612172526225](C:\Users\chen\AppData\Roaming\Typora\typora-user-images\image-20230612172526225.png)

导出后记得将新生成的文件加载进来

![image-20230612172710317](C:\Users\chen\AppData\Roaming\Typora\typora-user-images\image-20230612172710317.png)

此时图层中包含了四个shp文件

![image-20230612172829520](C:\Users\chen\AppData\Roaming\Typora\typora-user-images\image-20230612172829520.png)

## 3.计算新增用地面积

计算思路：新增用地面积=新用地面积—重合面积

首先求重合面积：

点击地理处理中的相交

![image-20230612172957737](C:\Users\chen\AppData\Roaming\Typora\typora-user-images\image-20230612172957737.png)

![image-20230612190339353](C:\Users\chen\AppData\Roaming\Typora\typora-user-images\image-20230612190339353.png)

![image-20230612190430870](C:\Users\chen\AppData\Roaming\Typora\typora-user-images\image-20230612190430870.png)

![image-20230612190256636](C:\Users\chen\AppData\Roaming\Typora\typora-user-images\image-20230612190256636.png)



然后求新面积和重合面积的差，Arcgis中为交集取反

在搜索中查找“交集取反”

![image-20230612191048786](C:\Users\chen\AppData\Roaming\Typora\typora-user-images\image-20230612191048786.png)

或者在以下目录中

![image-20230612191138857](C:\Users\chen\AppData\Roaming\Typora\typora-user-images\image-20230612191138857.png)



![image-20230612191232073](C:\Users\chen\AppData\Roaming\Typora\typora-user-images\image-20230612191232073.png)

输入要素为新面积，更新要素为相交

点确定运行计算，可以看到新增面积已经提取

![image-20230612191337251](C:\Users\chen\AppData\Roaming\Typora\typora-user-images\image-20230612191337251.png)

右键点击新增面积图层，打开属性表

![image-20230612191452397](C:\Users\chen\AppData\Roaming\Typora\typora-user-images\image-20230612191452397.png)

![image-20230612191533215](C:\Users\chen\AppData\Roaming\Typora\typora-user-images\image-20230612191533215.png)

可以看到新增面积数值，点击导出，可将表格导出为数据库或文本格式，例如导出dBASE表，可以用Excel打开

![image-20230612191822840](C:\Users\chen\AppData\Roaming\Typora\typora-user-images\image-20230612191822840.png)

## 4.按地类计算用地面积

这一步主要使用的是“裁剪”功能，可以在地理处理菜单栏里找到，也可以在以下路径找到

![image-20230612192053951](C:\Users\chen\AppData\Roaming\Typora\typora-user-images\image-20230612192053951.png)

![image-20230612192152574](C:\Users\chen\AppData\Roaming\Typora\typora-user-images\image-20230612192152574.png)

其中，

输入要素为地类图 ，即需要被剪裁的要素，剪裁要素是“剪子”，这里选择新增面积

![image-20230612192225612](C:\Users\chen\AppData\Roaming\Typora\typora-user-images\image-20230612192225612.png)

裁剪后，可以看到，地类图被裁剪成与新增面积一致的形状，双击新增地类要素，修改标注样式，能够看到新增面积中包含了多种地类，也包含着相对应的面积



![image-20230612192519510](C:\Users\chen\AppData\Roaming\Typora\typora-user-images\image-20230612192519510.png)



这一步同样可以导出属性表作为后续数据核查

## 5.按区划计算用地面积

用地面积通常包含了不同区划内的用地，因此还需要结合区划数据进行裁剪

右键点击村界图层，打开属性表，点击按属性选择，在对话框中进行公式计算，如“layer”=“东大洋”（通过获取唯一值得到字符串信息），点击应用，选择所有layer字段等于“东大洋”的要素。这一步主要是考虑字段较多时的操作，如果字段要素较少可手动选取。

![image-20230612192959919](C:\Users\chen\AppData\Roaming\Typora\typora-user-images\image-20230612192959919.png)

再次右键点击村界图，将所选要素导出为shp要素，并加载到当前项目中。

同样，将每一个行政区划分为不同的图层加载

继续进行裁剪，输入要素为上一步准备好的新增地类图（注意是新增地类，不是新增面积），裁剪要素分别为不同的行政区划图层

完成裁剪后，可以导出属性表，作为最终的统计结果，后续输出公路用地相关可以基于该统计结果进行整理。

![image-20230612194134359](C:\Users\chen\AppData\Roaming\Typora\typora-user-images\image-20230612194134359.png)



## 6.注意事项

- 第一步不导出为shp文件或许也可行，本说明中只是为了统一文件格式，避免不同格式文件相互裁剪出现异常值，但无论裁剪还是相交都是面域之间的计算，务必确保源文件不存在高程数值。

- 统计结果可能会与CAD中直接计算的存在一些差距，这一点需要大量案例验证该方法是否足够可靠，推测如果要素均为多段线，不存在样条曲线或者圆弧等，差值并不大。关于CAD文件中的面积和shp文件中的面积可能出现差值的原因，可以参考公众号GIS前沿中的相关文章。如下：

------

大家应该经常会遇到这种情况，   就是同样一个数据， CAD、SHP、地理数据库要素类的三个面积， 竟然是不同的！！！ 这究竟是为啥呢？？？

​    **我们来分两种情况说一下：**

 **1\. 三类数据面积相差很大，这种时候你就要考虑下图斑的拓扑关系了；** 

**2\. 三类数据面积相差很小，甚至只有个位数或小数点后几位数的不同，这个时候，就是数据类型本身的特点决定的。**



 **情况一：面积相差很大**    当你发现，CAD的数据和SHP、以及地理数据库要素类数据的面积相差很大，这个时候，你大概率要考虑下图斑的拓扑关系了。    换句话说，就是CAD数据的图斑与图斑之间，出现了相互压盖、重叠或者有空隙的情况，所以转为了SHP或地理数据库要素类后，计算出的面积会和原来的CAD的面积相差很大。 

   **举个例子说明吧——**    下图所示是在CAD中常见的用地规划图，其中方案一、方案二在图面上观察并无差异，但是从统计数据看确存在明显不同——    其中A地块在方案一、二中的面积分别为**7.53ha、15.06ha**；B地块在方案一、二中的面积分别为**7.53ha、8.37ha**；只有C地块在两个方案中的面积相等。    ![图片](https://mmbiz.qpic.cn/mmbiz_png/YN5ps6DRpuLLHJHT46haFo1bqsM3M2UnI2mEapRtPuPp1yIQqpeMAXWFn7cicgA44cnUATfhRc27pAcjJywN0Ng/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1) ▲不同方案统计结果对比图 （图片来源于公众号“城市技师”）    由此对比可以发现其中必有一个方案存在错误，这种错误在实际项目中很容易出现的，这就会成为方案成果中一个很大的技术漏洞，也会成为后期规划管理中的技术隐患。       **这种错误的原因，就是地类图斑空间重叠。**    也就是说其中方案一中的A、B、C三块用地彼此以各自对应的边界衔接，不存在彼此叠压盖的情况； ![图片](https://mmbiz.qpic.cn/mmbiz_png/YN5ps6DRpuLLHJHT46haFo1bqsM3M2UnES0Q4HVicTXX4RCg0ibUibzDOLAmYXtzdmHzynvOVq2hdIouZ1LARkIwg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1) ▲方案一图层空间关系示意图 （图片来源于公众号“城市技师”）    而方案二中存在A、B地块以及A、C地块部分重叠的情况，且重叠之后因为图层要素绘制顺序是C在顶层，B在底层，因此在CAD中所呈现的可视化效果和方案一是相同的，无法凭肉眼直接识别出来。这种情况在实际项目中由于绘制精度及多次修改等原因很容易出现，导致空间统计结果必然存在较大的误差甚至是错误。    ![图片](https://mmbiz.qpic.cn/mmbiz_png/YN5ps6DRpuLLHJHT46haFo1bqsM3M2Un4uaBicuKJzicQUI4g40JdT0vNfvxdkZ0dk5Zc2B4PibzWiaQ52PkhoM6xQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1) ▲方案二图层空间关系示意图 （图片来源于公众号“城市技师”)    这种问题，用GIS里面的拓扑进行一下修复就可以了，拓扑修复的操作流程就不细说了哈            

 **情况二：面积相差很小**    首先要确认是在**同一种面积计算方式下计算的面积，**例如都是椭球体面积（同一地理坐标系）或都是投影面积（同一投影坐标系）。      然后你会惊奇的发现，CAD数据和地理数据库要素类的面积几乎一样，但和SHP文件的面积却有些偏差，这是为啥呢？    ![图片](https://mmbiz.qpic.cn/mmbiz_png/jYicjbq67iaQleBp3uicboia81l4F5d0qdFITM54VyCysdUFaAYF4Gy3fZf6a3Wy4p2ic9KbkRuDxxMaJjzuOj3iadWg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)    例如上图，同样是一个圆形的面状图斑，但是SHP文件的面积与CAD和地理数据库的面积是有些偏差，这个是由于数据本身的特性决定的，这个特性就是——**SHP数据在弧段的处理上，与其他两种数据不太一样，**我们仔细看下:    **CAD和地理数据库要素类在弧段的表达上，就是一个典型的圆弧——**    ![图片](https://mmbiz.qpic.cn/mmbiz_png/jYicjbq67iaQleBp3uicboia81l4F5d0qdFISCAzU2e8ib87mdRRzMuMfGfCYQp0INuQQYyZ6jRb57eD46v39OJgEog/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)    **而SHP数据的弧段，是由很多折线组成的——**    ![图片](https://mmbiz.qpic.cn/mmbiz_png/jYicjbq67iaQleBp3uicboia81l4F5d0qdFIVY4tibBGEQYekqz8wyMibNTH3qcyBpiaLfolMQfMUh2oP8vOpmhLqeHlg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)    也就是说，SHP数据的弧段，是很多折线拟合的圆弧，而不是像CAD数据和地理数据库要素类那样，是一个标准的弧段，所以，在计算面积的时候，是会有一些差异的！！！     



