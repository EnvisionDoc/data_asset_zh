# Late Point Filter

支持判断迟到数据，并对迟到数据点进行数据质量打标。具体判断逻辑如下：

- 对经过该算子的数据，以timestamp字段作为标准，过滤迟到的Record。如果某个Record的timestamp比最新Record的timestamp晚，则会被判断为late。
- 时间标准以assetId:pointId:timestamp为粒度，相同设备、相同点的Record才会进行迟到点判断。
- 如果某个设备的某个点第一次经过该算子，没有参考标准，则判断为not late，并记录该assetId:pointId的timestamp，用作对后续Record的处理和判断。



## 配置详情

该算子的配置包括General，LatePointFilter的详细信息，各字段的配置如下：

### General

| 名称            | 是否必须 | 描述                                                                                                               |
|:----------------|:---------|:-------------------------------------------------------------------------------------------------------------------|
| Name            | Yes      | 算子名称                                                                                                           |
| Description     | No       | 算子描述                                                                                                           |
| Stage Library   | Yes      | 算子所属的库                                                                                                       |
| Required Fields | No       | 数据必须包含的字段，如果未包含指定字段，则record将被过滤掉                                                         |
| Preconditions   | No       | 数据必须满足的前提条件，如果不满足指定条件，则record将被过滤掉                                                     |
| On Record Error | Yes      | 对错误数据的处理方式：<br/>Discard：直接丢弃 <br/>Send to Error：发送至错误中心 <br/>Stop Pipeline：停止流任务运行 |

### LatePointFilter

| 名称                 | 是否必须 | 描述                                                                                                       |
|:---------------------|:---------|:-----------------------------------------------------------------------------------------------------------|
| Filter Rules         | Yes      | 设置对Record的过滤规则                                                                                     |
| Input Model::Point   | Yes      | 数据输入点，格式为：{模型标识}::{测点标识}。同一行的输入点和输出点之间的modelId必须相同，pointId必须不同。 |
| Output Model::Point  | Yes      | 数据输出点，格式为：{模型标识}::{测点标识}。同一行的输入点和输出点之间的modelId必须相同，pointId必须不同。 |
| QualityControl Level | No       | 数据质量位选择，表示该算子可以支持或需要处理哪些类型的数据质量。                                           |



## 输出结果

经过该算子的Record会被加上质量位。

### 输出示例

**正常点**

.. image:: media/late_point_filter_result_1.png

**迟到点**

.. image:: media/late_point_filter_result_2.png

<!--end-->
