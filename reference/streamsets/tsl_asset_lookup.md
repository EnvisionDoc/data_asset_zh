# TSL Asset Lookup

支持查找指定设备的属性/标签/时区的值;
具体功能如下：
- 默认查找上一个stage输出record对应设备的数据
- 允许用户自定义查询设备，并将该设备的查询信息写入每一个满足输入条件的record中
- 支持用户指定需要查询的属性、tag
- 详细信息封装在每条record的/attr/tslAssetLookup中


## 配置详情

该算子的配置包括General，Basic，Config的详细信息，各字段的配置如下：

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

| 名称                 | 是否必须 | 描述                                                                                                                                                                   |
|:---------------------|:---------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Input Output         | Yes      | 查找规则，由于资产主数据信息是打在每一条record上的，所以每一条规则需设置要附加资产主数据信息的测点，最终结果需要用输出点进行承载，输入输出点必须一致；可增、删、改规则 |
| Input Model::Point   | Yes      | 单条规则的输入点，即需要附加资产主数据信息的测点                                                                                                                       |
| Output Model::Point  | Yes      | 单条规则的输出点，即承载输出结果的测点                                                                                                                                 |
| QualityControl Level | No       | 根据数据质量过滤处理数据，只有符合质量条件的record才会进行此次处理                                                                                                     |

### Config

| 名称                  | 是否必须 | 描述                                                                                                                                     |
|:----------------------|:---------|:-----------------------------------------------------------------------------------------------------------------------------------------|
| Enable User-Defined   | No       | 是否支持用户自定义需要获取主数据信息的asset                                                                                              |
| User-Defined Asset Id | No       | 支持通过自定义表达式获取满足条件的asset；比如：${record:value('/attr/xxx')}表示以record下attr字段的xxx的value为assetId条件获取主数据信息 |
| Attributes            | No       | 属性条件，只返回指定属性条件的属性值                                                                                                     |
| Tags                  | No       | tag条件，只返回指定tag id的tag value                                                                                                     |
| Timezone              | No       | 是否开启获取资产的Timezone信息                                                                                                           |

## 输出结果

该算子的输出结果包含在Attribute结构体中，各字段的描述如下：

| 名称                 | 数据类型 | 描述                            |
|:---------------------|:---------|:--------------------------------|
| /attr/tslAssetLookup | Asset    | 资产主数据信息对象              |
| Asset.attributes     | Map      | 父节点上绑定的属性key-value列表 |
| Asset.tags           | Map      | 父节点上绑定的标签key-value列表 |
| Asset.timezone       | String   | 资产上绑定的时区                |


### 输出示例

.. image:: media/tsl_asset_lookup_result.jpg

<!--end-->
