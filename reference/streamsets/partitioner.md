# Partitioner

将每个batch内的records按照特定条件进行分区，一般用于同一个不同点之间的联合运算，或者不同设备之间点的运算。
具体功能如下:

- 支持用户自定义分区条件
- 自定义分区条件支持路径表达方式，比如/assetId表示根据每个record下assetId字段的value进行分区
- 不支持血缘注册


## 配置详情

该算子的配置包括General、Partitioner的详细信息，各字段的配置如下：

### General

| 名称            | 是否必须 | 描述                                                                                                 |
|:----------------|:---------|:-----------------------------------------------------------------------------------------------------|
| Name            | Yes      | 算子名称                                                                                             |
| Description     | No       | 算子描述                                                                                             |
| Stage Library   | Yes      | 算子所属的库                                                                                         |
| Required Fields | No       | 数据必须包含的字段，如果未包含指定字段，则record将被过滤掉                                           |
| Preconditions   | No       | 数据必须满足的前提条件，如果不满足指定条件，则record将被过滤掉                                       |
| On Record Error | Yes      | 对错误数据的处理方式  Discard:直接丢弃；Send to Error：发送至错误中心；Stop Pipeline：停止流任务运行 |

### Partitioner

| 名称                                    | 是否必须 | 描述                                                                                                                         |
|:----------------------------------------|:---------|:-----------------------------------------------------------------------------------------------------------------------------|
| Parallelism (Standalone Mode Only)      | Yes      | standalone模式下本stage需要worker数量                                                                                        |
| Application Name (Standalone Mode Only) | Yes      | standalone模式下本stage的运行Application name，默认值为：SDC Spark App                                                       |
| Init Method Arguments                   | Yes      | 分区rules，每一条必须输入分区字段，输入的字段格式为record的字段，比如/assetId 表示将同一assetId下的records分配到同一个分区内 |


## 输出结果

该算子的输出结果为进行分区后的records


### 输出示例

.. image:: media/partitioner_result.jpg

<!--end-->
