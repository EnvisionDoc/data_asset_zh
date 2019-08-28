# HTTP Lookup

支持通过GET，POST，或Restful方式发起HTTP请求。并支持开启缓存（以URL+请求参数生成key），以便二次查询。



## 配置详情

该算子的配置包括General，BasicConfig，HttpConfig，CacheConfig的详细信息，各字段的配置如下：

### General

| 名称            | 是否必须 | 描述                                                                                                               |
|:----------------|:---------|:-------------------------------------------------------------------------------------------------------------------|
| Name            | Yes      | 算子名称                                                                                                           |
| Description     | No       | 算子描述                                                                                                           |
| Stage Library   | Yes      | 算子所属的库                                                                                                       |
| Required Fields | No       | 数据必须包含的字段，如果未包含指定字段，则record将被过滤掉                                                         |
| Preconditions   | No       | 数据必须满足的前提条件，如果不满足指定条件，则record将被过滤掉                                                     |
| On Record Error | Yes      | 对错误数据的处理方式：<br/>Discard：直接丢弃 <br/>Send to Error：发送至错误中心 <br/>Stop Pipeline：停止流任务运行 |

### BasicConfig

| 名称           | 是否必须 | 描述                                       |
|:---------------|:---------|:-------------------------------------------|
| OrgId          | Yes      | 所属的组织ID                               |
| Points         | Yes      | 数据输入点，格式为：{模型标识}::{测点标识} |
| Output PointId | No       | 数据输出点，格式为：{模型标识}::{测点标识} |

### HttpConfig

| 名称                 | 是否必须 | 描述                                                 |
|:---------------------|:---------|:-----------------------------------------------------|
| Request Style        | Yes      | 选择请求方式，可选GetRequest，PostRequest，或Restful |
| RESTful URL          | Yes      | 输入请求的URL                                        |
| URLParam Type        | Yes      | 选择参数类型，可选FieldValAsParam或InputValAsParam   |
| ParamName            | Yes      | 输入请求参数名称                                     |
| Request Content-Type | No       | 当选择PostRequest方法时，选择相应的请求头格式        |

### CacheConfig

| 名称               | 是否必须 | 描述                           |
|:-------------------|:---------|:-------------------------------|
| Enable CacheFields | No       | 选择是否开启缓存               |
| ExpireRule         | No       | 开启缓存时，选择缓存的失效时间 |



## 输出结果

该算子的输出结果包含在Attribute结构体中的lookupTag字段中。各字段的描述如下：

| 名称     | 数据类型 | 描述                                                                                        |
|:---------|:---------|:--------------------------------------------------------------------------------------------|
| hasData  | Boolean  | 表示请求是否成功                                                                            |
| response | Object   | 如果请求成功，显示相应请求的（字符串）返回值，并在returnBy字段中注明是来自Redis还是来自Http |


### 输出示例

.. image:: media/http_lookup_result.png

<!--end-->
