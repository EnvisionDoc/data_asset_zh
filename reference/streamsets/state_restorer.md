# State Restorer

支持解析流经该Stage的数据，将当前批次数据中所有的assetId和pointId抽取出来，并从Redis中将设备和数据点对应的数据抽取来作为输出。该算子依赖于State Capturer算子。



## 配置详情

该算子的配置包括General，StateRestorer的详细信息，各字段的配置如下：

### General

| 名称            | 是否必须 | 描述                                                                                                               |
|:----------------|:---------|:-------------------------------------------------------------------------------------------------------------------|
| Name            | Yes      | 算子名称                                                                                                           |
| Description     | No       | 算子描述                                                                                                           |
| Required Fields | No       | 数据必须包含的字段，如果未包含指定字段，则record将被过滤掉                                                         |
| Preconditions   | No       | 数据必须满足的前提条件，如果不满足指定条件，则record将被过滤掉                                                     |
| On Record Error | Yes      | 对错误数据的处理方式：<br/>Discard：直接丢弃 <br/>Send to Error：发送至错误中心 <br/>Stop Pipeline：停止流任务运行 |

### StateRestorer

| 名称                 | 是否必须 | 描述                                                             |
|:---------------------|:---------|:-----------------------------------------------------------------|
| PointIds             | Yes      | 设置待处理的模型和测点列表，格式为：{模型标识}::{测点标识}。     |
| QualityControl Level | No       | 数据质量位选择，表示该算子可以支持或需要处理哪些类型的数据质量。 |



## 输出结果

指定的设备和测点数据，会被从缓存中抽取出来。

### 输出示例

.. image:: media/state_restorer_result.png

<!--end-->
