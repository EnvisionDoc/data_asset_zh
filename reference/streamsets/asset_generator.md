# Asset Generator

根据用户配置的模型点条件产生新的数据（record）。

具体功能如下:
- 支持配置多条模型点条件
- 模型点条件运行原理如下:
    - 如果配置的模型点不存在,则这条规则被忽略;
    - 如果配置的模型及测点存在, 则查询当前ou下所有符合模型条件的Instance，使用这些Instance 的 assetId 和测点条件，生成新的record
- 产生record触发条件
     - 该算子根据上一个stage输出流的batch触发新record产生
     - 每一个batch到来都会触发一次新record产生动作
     - 当上一个stage没有输出数据时，系统也会自动输出空batch到下一个stage，默认产生batch频率为1s

## 配置详情

该算子的配置包括General、assetGenerator的详细信息，各字段的配置如下：

### General

| 名称            | 是否必须 | 描述                                                                                                 |
|:----------------|:---------|:-----------------------------------------------------------------------------------------------------|
| Name            | Yes      | 算子名称                                                                                             |
| Description     | No       | 算子描述                                                                                             |
| Stage Library   | Yes      | 算子所属的库                                                                                         |
| Required Fields | No       | 数据必须包含的字段，如果未包含指定字段，则record将被过滤掉                                           |
| Preconditions   | No       | 数据必须满足的前提条件，如果不满足指定条件，则record将被过滤掉                                       |
| On Record Error | Yes      | 对错误数据的处理方式  Discard:直接丢弃；Send to Error：发送至错误中心；Stop Pipeline：停止流任务运行 |

### assetGenerator

| 名称           | 是否必须 | 描述                                           |
|:---------------|:---------|:-----------------------------------------------|
| modelIdPointId | Yes      | 配置模型及测点条件，填写格式为modelId::pointId |


## 输出结果

该算子的输出结果为新的records，record各字段的描述如下：

| 名称    | 数据类型 | 描述          |
|:--------|:---------|:--------------|
| pointId | String   | 测点Id        |
| modelId | String   | 测点所属model |
| assetId | String   | 资产实例id    |
| ts      | Long     | 时间戳        |


### 输出示例

**配置示例图**

.. image:: media/asset_generator_config.png

**结果输出示例**

.. image:: media/asset_generator_result.png

<!--end-->
