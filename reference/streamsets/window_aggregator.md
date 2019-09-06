# Window Aggregtor

支持单设备单测点数据按时间窗口聚合，

具体功能如下:
- 窗口类型：支持滚动窗口和滑动窗口
- 聚合策略：支持 max/min/avg/count/sum/first/last/delta
- 延迟策略：支持0~60min的数据延迟，该范围内乱序到达的数据仍会参与计算
- 提前输出：支持在当前窗口结束前，按固定频率提前输出中间结果

## 配置详情

该算子的配置包括General，Basic，Trigger，Rules的详细信息，各字段的配置如下：

### General

| 名称            | 是否必须 | 描述                                                                                                 |
|:----------------|:---------|:-----------------------------------------------------------------------------------------------------|
| Name            | Yes      | 算子名称                                                                                             |
| Description     | No       | 算子描述                                                                                             |
| Stage Library   | Yes      | 算子所属的库                                                                                         |
| Required Fields | No       | 数据必须包含的字段，如果未包含指定字段，则record将被过滤掉                                           |
| Preconditions   | No       | 数据必须满足的前提条件，如果不满足指定条件，则record将被过滤掉                                       |
| On Record Error | Yes      | 对错误数据的处理方式  Discard:直接丢弃；Send to Error：发送至错误中心；Stop Pipeline：停止流任务运行 |

### Basic

| 名称                    | 是否必须 | 描述                             |
|:------------------------|:---------|:---------------------------------|
| Aggregation Window Type | Yes      | 窗口类型，可选滚动窗口或滑动窗口 |
| Fixed Window Unit       | Yes      | 滚动窗口的时间单位               |
| Fixed Window Size       | Yes      | 滚动窗口的时长                   |
| Sliding Window Unit     | Yes      | 滑动窗口的时间单位               |
| Sliding Window Size     | Yes      | 滑动窗口的时长                   |
| QualityControl Level    | No       | 数据质量控制                     |

### Trigger

| 名称               | 是否必须 | 描述                                                     |
|:-------------------|:---------|:---------------------------------------------------------|
| Latency (Minute)   | Yes      | 数据延迟策略设置，支持0~60min的延迟                      |
| On-time Trigger    | No       | 下一窗口开始时，是否提前输出当前窗口的结果（默认不输出） |
| Early Trigger      | No       | 是否支持在当前窗口结束前，提前输出中间结果（默认不输出） |
| Frequency (Minute) | No       | 提前输出中间结果的频率,单位默认为min                     |

### Rules

| 名称              | 是否必须 | 描述                                                      |
|:------------------|:---------|:----------------------------------------------------------|
| Model::PointIn    | Yes      | 数据输入点，格式为：{模型标识}::{测点标识}                |
| Aggregator Policy | Yes      | 数据聚合算法，支持 max/min/avg/count/sum/first/last/delta |
| Model::PointOut   | Yes      | 数据输出点，格式为：{模型标识}::{测点标识}                |



## 输出结果

该算子的输出结果包含在Attribute结构体中，各字段的描述如下：

| 名称       | 数据类型         | 描述                                                                                                                                                                     |
|:-----------|:-----------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| lastOutput | Int/Double/Float | 该测点在该timestamp，上一次输出的值；上一次无输出则为NAN                                                                                                                 |
| calMode    | String           | 输出模式：<br/>超出延迟时，输出最终结果 “final”; <br/>配置On-time Trigger时，窗口结束，输出准时结果 “onTime”; <br/>配置Early Trigger时，窗口未结束，输出提前结果 “early” |
| calType    | String           | 聚合策略：max/min/avg/count/sum/first/last/delta                                                                                                                         |
| calDetail  | Map              | 计算详情：如calType=avg时，输出value&lastValue的sum和count信息                                                                                                           |


### 输出示例

.. image:: media/window_aggregator_result.png

<!--end-->
