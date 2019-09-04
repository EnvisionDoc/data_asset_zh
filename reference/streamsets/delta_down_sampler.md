# Delta Down Sampler

支持对指定时间间隔内到达的Record进行窗口聚合，输出所有Record的总和。每当有Record到达时触发计算。该算子为电量计算专用。



## 配置详情

该算子的配置包括General，DeltaDownSampler的详细信息，各字段的配置如下：

### General

| 名称            | 是否必须 | 描述                                                         |
| :-------------- | :------- | :----------------------------------------------------------- |
| Name            | Yes      | 算子名称                                                     |
| Description     | No       | 算子描述                                                     |
| Stage Library   | Yes      | 算子所属的库                                                 |
| Required Fields | No       | 数据必须包含的字段，如果未包含指定字段，则record将被过滤掉   |
| Preconditions   | No       | 数据必须满足的前提条件，如果不满足指定条件，则record将被过滤掉 |
| On Record Error | Yes      | 对错误数据的处理方式：<br/>Discard：直接丢弃 <br/>Send to Error：发送至错误中心 <br/>Stop Pipeline：停止流任务运行 |

### DeltaDownSampler

| 名称                   | 是否必须 | 描述                                                         |
| :--------------------- | :------- | :----------------------------------------------------------- |
| Input Model::Point     | Yes      | 数据输入点，格式为：{模型标识}::{测点标识}。同一行的输入点和输出点之间的modelId必须相同，pointId必须不同。 |
| DeltaDownSamplerWindow | Yes      | 选择输出计算结果的时间间隔                                   |
| Output Model::Point    | Yes      | 数据输出点，格式为：{模型标识}::{测点标识}。同一行的输入点和输出点之间的modelId必须相同，pointId必须不同。所有的输出点不能重复。 |



## 输出结果

该算子的配置参数值和输出结果包含在Attribute结构体中。

### 输出示例

.. image:: media/delta_down_sampler_result.png

