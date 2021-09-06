# 配置/调试/定时运行pipeline

### 创建pipeline

路径：训练->任务流->新建

![](../pic/tapd_20424693_1630650436_41.png)

主要配置： 参考每个配置参数的描述

### 编排pipeline

![](../pic/tapd_20424693_1630651816_13.png)

task公共参数：参考每个配置的描述  
task的模板参数：参考每个模板的链接教程文档

### 运行调试

##### task运行调试：

使用task的run按钮和log按钮可单独调试一个task

![](../pic/tapd_20424693_1630652726_69.png)

##### pipeline运行调试：

pipeline的运行按钮发起调度

![](../pic/tapd_20424693_1630652948_17.png)

##### pipeline日志效果：

![](../pic/tapd_20424693_1606994509_86.png)

### pod查看示意图

![](../pic/tapd_20424693_1630652786_45.png)

pod效果：

![](../pic/tapd_20424693_1630652346_97.png)

### 实例记录

![](../pic/tapd_20424693_1630652888_5.png)

调度实例记录。停止可以清除调度容器

![](../pic/tapd_20424693_1630652863_77.png)

### 定时调度

配置定时：pipeline编辑界面

![](../pic/tapd_20424693_1630653430_19.png)

查看路径：训练-定时调度记录

![](../pic/tapd_20424693_1630567772_14.png)

字段说明：执行时间为这个pipeline本次调度该发起的时间点  
状态：comed，为调度配置已经产生。created为调度已经发起。

##### 操作说明

	1、平台会根据pipeline的配置决定是否发起调度。
	2、状态链接中可以看到本地调度发起的workflow的运行情况
	3、日志链接中可以看到本地调度发起的日志