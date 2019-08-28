# Point Selector

从每个ou对应的kafka中选取流式计算需要处理的测点，

具体功能如下:
- 根据用户配置的模型点条件进行选择;
- 支持多条模型点条件设置
- 如果输入的数据不在配置的模型点列表中,则不输出;
- 如果输入的数据在配置的模型点列表中,则输出;
- 不支持血缘注册


## 配置详情

该算子的配置包括General、PointSelector的详细信息，各字段的配置如下：

### General

| 名称            | 是否必须 | 描述                                                                                                 |
|:----------------|:---------|:-----------------------------------------------------------------------------------------------------|
| Name            | Yes      | 算子名称                                                                                             |
| Description     | No       | 算子描述                                                                                             |
| Stage Library   | Yes      | 算子所属的库                                                                                         |
| Required Fields | No       | 数据必须包含的字段，如果未包含指定字段，则record将被过滤掉                                           |
| Preconditions   | No       | 数据必须满足的前提条件，如果不满足指定条件，则record将被过滤掉                                       |
| On Record Error | Yes      | 对错误数据的处理方式  Discard:直接丢弃；Send to Error：发送至错误中心；Stop Pipeline：停止流任务运行 |

### PointSelector

| 名称            | 是否必须 | 描述                                                       |
|:----------------|:---------|:-----------------------------------------------------------|
| orgId           | Yes      | 数据所属组织id，只能填写当前组织                           |
| Select Policy   | Yes      | 选点策略集合                                               |
| Policy::pointId | Yes      | 选择当前pipeline需要处理的输入点,包括模型条件和pointId条件 |


## 输出结果

该算子的输出结果为经过模型及测点过滤后的的streaming records


### 输出示例

.. image:: media/point_selector_result.jpg

<!--end-->
