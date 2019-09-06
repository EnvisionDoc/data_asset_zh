# Time Sort

对每一个batch中的records按照时间字段(/time)进行升序排序

## 配置详情

该算子的配置包括General、Sort的详细信息，各字段的配置如下：

### General

| 名称            | 是否必须 | 描述                                                                                                 |
|:----------------|:---------|:-----------------------------------------------------------------------------------------------------|
| Name            | Yes      | 算子名称                                                                                             |
| Description     | No       | 算子描述                                                                                             |
| Stage Library   | Yes      | 算子所属的库                                                                                         |
| Required Fields | No       | 数据必须包含的字段，如果未包含指定字段，则record将被过滤掉                                           |
| Preconditions   | No       | 数据必须满足的前提条件，如果不满足指定条件，则record将被过滤掉                                       |
| On Record Error | Yes      | 对错误数据的处理方式  Discard:直接丢弃；Send to Error：发送至错误中心；Stop Pipeline：停止流任务运行 |

### Sort

| 名称                 | 是否必须 | 描述                                                               |
|:---------------------|:---------|:-------------------------------------------------------------------|
| QualityControl Level | No       | 根据数据质量过滤处理数据，只有符合质量条件的record才会进行此次处理 |


## 输出结果

该算子的输出结果为经过排序过后的的streaming records


### 输出示例

.. image:: media/time_sort_result.png

<!--end-->
