# Earliest Change Record Appender

自动缓存每个测点最新一条数据，并在每条记录上打上这条最新数据的信息。

具体功能如下:
对于同一个设备的同一个测点
- 若该点record首次到达：
    + 将当前测点更新至缓存
    + 将当前缓存值附加至record的/attr/earliestChangeAttr中
- 若该测点record非首次到达：
    + 将当前缓存附加至record的/attr/earliestChangeAttr中
    + 与缓存比较，测点value改变则将当前测点更新至缓存中，否则不更新

## 配置详情

该算子的配置包括General、Info的详细信息，各字段的配置如下：

### General

| 名称            | 是否必须 | 描述                                                                                                 |
|:----------------|:---------|:-----------------------------------------------------------------------------------------------------|
| Name            | Yes      | 算子名称                                                                                             |
| Description     | No       | 算子描述                                                                                             |
| Stage Library   | Yes      | 算子所属的库                                                                                         |
| Required Fields | No       | 数据必须包含的字段，如果未包含指定字段，则record将被过滤掉                                           |
| Preconditions   | No       | 数据必须满足的前提条件，如果不满足指定条件，则record将被过滤掉                                       |
| On Record Error | Yes      | 对错误数据的处理方式  Discard:直接丢弃；Send to Error：发送至错误中心；Stop Pipeline：停止流任务运行 |

### Info

| 名称                 | 是否必须 | 描述                                                                                                                                                                               |
|:---------------------|:---------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Input Output         | Yes      | 查找规则，由于上一条更新数据信息是打在每一条record上的，所以每一条规则需设置要附加上一条更新数据属性信息的测点，最终结果需要用输出点进行承载，输入输出点必须一致；可增、删、改规则 |
| Input Model::Point   | Yes      | 单条规则的输入点，即需要附加测点上一条更新数据信息的测点                                                                                                                           |
| Output Model::Point  | Yes      | 单条规则的输出点，即承载输出结果的测点                                                                                                                                             |
| QualityControl Level | No       | 根据数据质量过滤处理数据，只有符合质量条件的record才会进行此次处理                                                                                                                 |


## 输出结果

该算子的输出结果包含在Attribute结构体中，各字段的描述如下：

| 名称                                    | 数据类型 | 描述                     |
|:----------------------------------------|:---------|:-------------------------|
| /attr/earliestChangeAttr                | Map      | 测点属性信息对象         |
| earliestChangeAttr.earliestChangeTs     | Long     | 上一条更新数据的时间戳   |
| earliestChangeAttr.earliestChangeValue  | Object   | 上一条更新数据的value    |
| earliestChangeAttr.earliestChangeRecord | Map      | 上一条更新数据的完整记录 |

### 输出示例

.. image:: media/earliest_change_record_appender_result.png

<!--end-->
