# 实时数据流

EnOS流数据处理中的实时数据流，可以从3个层面来分析：数据引擎层、数据存储层、和数据应用层。

## 数据引擎层

设备连接配置完成之后，通过IoT Hub接收设备上传的原始数据。流数据会被以Topic的形式保存在Kafka中，然后由规则引擎和流数据引擎对数据进行处理。

1. 通过**规则引擎**，不同用户的数据被分发到单独的Kafka Topic中。
2. 资产原始数据被分发到**Origin Data Topic**中，经过流数据引擎之后的数据被分发到**Cal Data Topic**中。
3. 流数据处理引擎处理数据的逻辑包括如下2种：
   - 用户自定义逻辑：你可以通过EnOS控制台中的**流开发**功能设计流数据处理任务。详见[开发流数据处理任务](/docs/data-asset/zh_CN/latest/howto/stream/index.html)。
   - 系统默认逻辑：系统内置逻辑，可完成数据格式转换等操作。

下图为数据引擎层的数据流图：

.. image:: ../media/data_flow_1.png

## 数据存储层

分发到**Origin Data Topic**和**Cal Data Topic**中的数据会被同时写入**内存数据库（IMDB）**、**时序数据库（TSDB）**和**数据归档（Archive）**存储中。存储逻辑如下：

1. IMDB：只存储资产的最新一条数据，实现数据的快速查询。
2. TSDB：按照配置的时序数据存储策略，存储资产时序数据。存储的数据类型和存储时效可以通过EnOS控制台中的**存储策略**功能来自行定义。存储在TSDB中的数据可以通过`getAssetsRawDataByTimeRange`，`getAssetsAIRawData`， `getAssetsAINormalizedData`，`getAssetsStatusData`, `getAssetsElectricPowerData`, `getAssetsGenericData`等API接口来查询。
3. Archive：按照配置的数据归档策略，归档资产数据。数据归档存储的数据源、文件属性、归档的存储系统和路径可以通过EnOS控制台中的**数据归档**功能来自行定义。

有关数据存储的详细信息，请参考[数据存储类型](storage_types)。

下图为数据存储层的数据流图：

.. image:: ../media/data_flow_2.png

## 数据应用层

资产原始数据和经流式计算引擎处理之后的数据，都可以通过EnOS控制台中的**数据订阅**功能进行订阅。EnOS提供Java SDK供开发者消费订阅数据，被订阅的资产数据可以直接用于应用开发。有关数据订阅的详细信息，请参考 [开发数据订阅任务](/docs/data-asset/zh_CN/latest/howto/obtain/managing_data_subscription.html)。

下图为数据应用层的数据流图：

.. image:: ../media/data_flow_3.png

<!--end-->
