# Delta Calculator

支持计算当前Record以及该Record的attr字段中的LastRecord的delta值。该算子为电量计算专用，依赖于Last Record Appender算子。



## 配置详情

该算子的配置包括General，DeltaCalculator的详细信息，各字段的配置如下：

### General

| 名称            | 是否必须 | 描述                                                                                                               |
|:----------------|:---------|:-------------------------------------------------------------------------------------------------------------------|
| Name            | Yes      | 算子名称                                                                                                           |
| Description     | No       | 算子描述                                                                                                           |
| Stage Library   | Yes      | 算子所属的库                                                                                                       |
| Required Fields | No       | 数据必须包含的字段，如果未包含指定字段，则record将被过滤掉                                                         |
| Preconditions   | No       | 数据必须满足的前提条件，如果不满足指定条件，则record将被过滤掉                                                     |
| On Record Error | Yes      | 对错误数据的处理方式：<br/>Discard：直接丢弃 <br/>Send to Error：发送至错误中心 <br/>Stop Pipeline：停止流任务运行 |

### DeltaCalculator

| 名称                | 是否必须 | 描述                                                                                                       |
|:--------------------|:---------|:-----------------------------------------------------------------------------------------------------------|
| Config              | Yes      | 设置Record差值计算参数                                                                                     |
| Input Model::Point  | Yes      | 数据输入点，格式为：{模型标识}::{测点标识}。同一行的输入点和输出点之间的modelId必须相同，pointId必须不同。 |
| Scale Type          | Yes      | 设置电能表倍率类型。0为属性值，1为固定值。                                                                 |
| Scale               | Yes      | 设置电能表倍率                                                                                             |
| Slope Type          | Yes      | 设置斜率类型。0为属性值，1为固定值。                                                                       |
| Min Slope           | Yes      | 设置斜率范围的下限                                                                                         |
| Max Slope           | Yes      | 设置斜率范围的上限                                                                                         |
| Output Model::Point | Yes      | 数据输出点，格式为：{模型标识}::{测点标识}。同一行的输入点和输出点之间的modelId必须相同，pointId必须不同。 |



## 输出结果

该算子的配置参数值，计算出的斜率，和输出结果包含在Attribute结构体中。

### 输出示例

**无LastRecord**

.. image:: media/delta_calculator_result_1.png

**有LastRecord**

.. image:: media/delta_calculator_result_2.png

<!--end-->
