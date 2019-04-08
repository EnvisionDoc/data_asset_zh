# 有关数据资产管理

EnOS数据资产管理服务支持流数据处理、实时资产数据和告警数据订阅、自定义数据存储策略，以及存储数据检索API。EnOS数据资产管理服务具备以下能力，帮助你实现对设备资产数据的高效管理。

- 强大的数据分析处理能力
- 易用的流数据处理功能
- 灵活的数据存储策略
- 实时资产数据订阅
- 高效的数据存储和读取

## 主要功能

EnOS数据资产管理服务提供如下主要功能：

**数据存储策略**

根据你的数据存储和读取需求，EnOS提供多种数据存储选项。按照不同的数据类型和存储时间分别存储数据，从而降低数据存储成本，提高数据读取效率。

注：在完成设备连接，设备开始发送数据到EnOS云端之前，必须完成数据存储策略配置。否则，上传的数据不会被默认存储到TSDB。更多详细信息，请参考[存储策略概览](/docs/data-asset/zh_CN/latest/learn/storage_policy_overview.html)。

**流数据分析**

EnOS流数据分析具有高可扩展性、高吞吐量、和高容错性等优点。EnOS还致力于沉淀IoT领域的流处理常用算法，开发者只需通过简单的模板配置即可完成流数据处理任务的开发及运维。流数据分析能充分满足用户处理设备和资产的实时数据的需求。更多详细信息，请参考[流数据处理](/docs/data-asset/zh_CN/latest/learn/index.html)。

**数据订阅**

数据订阅支持订阅实时资产数据和资产警报数据。通过数据订阅服务，应用程序不需要反复频繁地调用API来获取资产数据。相反，应用程序只在推送数据时调用API，从而提高API调用效率并降低成本。更多详细信息，请参考[数据订阅](/docs/data-asset/zh_CN/latest/learn/data_subscription_overview.html)。

**数据服务API**

数据资产服务提供一整套数据服务API接口，供查询存储于EnOS TSDB中的数据。



## 相关角色

EnOS数据资产管理主要服务于以下角色：

**数据工程师**

登录EnOS控制台，通过设计数据处理流任务、配置数据订阅功能、自定义不同数据类型的存储策略，更高效地管理设备资产数据。

**应用开发者**

基于EnOS提供的API和SDK，线下开发应用，获取订阅的实时数据或经处理之后存储的数据，以进行业务应用开发。



## 相关服务

### 设备管理服务

EnOS设备管理服务帮助你快速将物理设备安全连接至EnOS云端并开始数据传输，管理设备周期，及将物理世界的资产结构映射至数字世界。[了解更多 >>](https://www.envisioniot.com/docs/device-connection/zh_CN/latest/device_management_overview.html)

### 应用开发

使用Enos SDK开发应用程序，并通过EnOS API获取存储的数据。[了解更多 >>](https://www.envisioniot.com/docs/app-development/zh_CN/latest/app_dev_overview.html)

 