# Asset Partitioner

不建议使用，因为此算子功能已被算子Partitioner包含；
具体功能如下:

- 按所属资产(/assetId)字段进行将输入的record进行分区;属于同一资产的record将会被分配到同一个分区内
- 不支持血缘

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

| 名称                                    | 是否必须 | 描述                                                                   |
|:----------------------------------------|:---------|:-----------------------------------------------------------------------|
| Parallelism (Standalone Mode Only)      | Yes      | standalone模式下本stage需要worker数量                                  |
| Application Name (Standalone Mode Only) | Yes      | standalone模式下本stage的运行Application name，默认值为：SDC Spark App |
| Init Method Arguments                   | No       | 无效配置项                                                             |

## 输出结果

该算子的输出结果为进行分区后的records

### 输出示例

.. image:: media/asset_partitioner_result.jpg

<!--end-->
