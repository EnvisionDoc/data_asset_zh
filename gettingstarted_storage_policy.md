# 数据存储配置和读取
该教程能帮助你快速学习如何使用存储策略进行数据存储配置及进行数据读取。

## 前提条件
- EnOS平台登录账号
- 已被授权存储策略模块
- 已接入设备并且设备已经在发送数据

## 教程目标及数据准备
**教程目标**

本教程要实现的场景是：将原始AI采集点*test_raw*的数据进行分钟级TSDB存储，并通过Open API获取一段时间内*test_raw*点每五分钟的最大值。

**数据准备**
- 模型配置：配置教程请参考[模型配置](https://www.envisioniot.com/docs/device-connection/zh_CN/latest/model/model_overview.html)。

本教程使用的模型*testModel*的配置如下：

Feature Type|Name|Identifier|Point Type |Data Type	|Unit
---|---|---|---|---|---
Measure Point	 | test_raw | test_raw|AI |DOUBLE|- -

## 操作步骤
使用存储策略实现本教程场景的操作步骤如下：
- 创建存储分组
- 配置存储策略并发布
- 使用Open API获取聚合数据

## 第一步：创建存储分组
进入存储策略配置模块，点击**新建分组**，填写存储分组名称，关联资产模型，即可完成存储分组创建。本教程关联的资产模型为*testModel*。

## 第二步：配置存储策略并发布
创建好存储分组后，选择TSDB，可看到TSDB下提供的几种不同类型的存储，本教程需选择**AI分钟级归一化数据**，点击进入该策略之后，需进行如下配置：
- 保留时长：可按需配置数据存储时长，比如1个月；
- 存储测点选择：选择需要存储的模型测点，本教程选择*testModel*下的*test_raw*这个测点；

内容配置完成后，点击**确认**按钮即可完成存储策略的保存和发布，系统会根据新的配置对数据进行存储。

## 第三步：使用Open API获取聚合数据

使用AI分钟级规一化数据对应的Open API接口 *getAssetsAINormalizedData*，可获取已存储的测点数据。Open API的使用方法，请参考[调用 EnOS REST API](https://www.envisioniot.com/docs/app-development/zh_CN/latest/call_enos_api.html)。