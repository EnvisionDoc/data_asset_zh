# Last Record Appender

支持将同一设备、同一点的前一个符合条件的Record，附加到当前Record的attr字段中。该算子的处理过程分为两步：

1. 第一步，将LastRecord附加到Record的attr字段中。如果某个设备的某个点第一次经过该算子，则还没有LastRecord。如果该设备的该点已经经过该算子，则会将LastRecord附加到attr字段中。
2. 将当前Record根据Conditions进行判断，如果符合Conditions，则用当前Record更新LastRecord；如果不符合条件，则不更新。Conditions如果为*，则任意的Record都满足条件，更新LastRecord。



## 配置详情

该算子的配置包括General，LastRecordAppender的详细信息，各字段的配置如下：

### General

| 名称            | 是否必须 | 描述                                                                                                               |
|:----------------|:---------|:-------------------------------------------------------------------------------------------------------------------|
| Name            | Yes      | 算子名称                                                                                                           |
| Description     | No       | 算子描述                                                                                                           |
| Stage Library   | Yes      | 算子所属的库                                                                                                       |
| Required Fields | No       | 数据必须包含的字段，如果未包含指定字段，则record将被过滤掉                                                         |
| Preconditions   | No       | 数据必须满足的前提条件，如果不满足指定条件，则record将被过滤掉                                                     |
| On Record Error | Yes      | 对错误数据的处理方式：<br/>Discard：直接丢弃 <br/>Send to Error：发送至错误中心 <br/>Stop Pipeline：停止流任务运行 |

### LastRecordAppender

| 名称                 | 是否必须 | 描述                                                                                                       |
|:---------------------|:---------|:-----------------------------------------------------------------------------------------------------------|
| Rules                | Yes      | 设置对Record的处理规则                                                                                     |
| Input Model::Point   | Yes      | 数据输入点，格式为：{模型标识}::{测点标识}。同一行的输入点和输出点之间的modelId必须相同，pointId必须不同。 |
| Conditions           | Yes      | 输入处理Record的条件。写法为*或者StreamSets的EL语句。                                                      |
| Output Model::Point  | Yes      | 数据输出点，格式为：{模型标识}::{测点标识}。同一行的输入点和输出点之间的modelId必须相同，pointId必须不同。 |
| QualityControl Level | No       | 数据质量位选择，表示该算子可以支持或需要处理哪些类型的数据质量。                                           |



## 输出结果

经过该算子的Record，会根据数据属性和设置的条件，确定是否会将LastRecord附加到Record的attr字段中。

### 输出示例

**没有LastRecord**

.. image:: media/last_record_result_1.png

**有LastRecord**

.. image:: media/last_record_result_2.png

<!--end-->
