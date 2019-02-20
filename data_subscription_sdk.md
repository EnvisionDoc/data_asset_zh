# 数据订阅SDK参考
完成数据订阅配置之后，可以使用数据订阅SDK来获取已订阅的数据。数据订阅SDK的参考文档如下：

## 实时数据订阅

**订阅Client类：EOSClient**

函数|函数说明|参数说明|返回
---|---|---|---
EosClient(String host,int port,String accessKey,String secret)	 | 获取构造函数 |host:订阅服务端地址;port：端口;accesskey：accesskey;secret：对应accesskey的secret|EosClient实例
getDataService()	 | 获取实时数据订阅服务实例 |无|IDataService实例

**实时数据订阅服务类：IDataService**

函数|函数说明|参数说明|返回
---|---|---|---
subscribe（IDataHandler dataHandler,String subId）	 | 获取subId的订阅的实时数据 |dataHandler：实时订阅数据处理对象;subId：云端配置的subId|null
subscribe(IDataHandler dataHandler,String subId,String consumerGroup);	 |获取subId的订阅的实时数据，同时指定订阅分组说明：consumerGroup指定了当前订阅client所属的订阅组，属于同一个订阅组的client共同处理订阅内容，这在单个订阅client处理能力有限的情况下，可以通过增加属于同一个订阅组的client来提升整体订阅处理能力。注意：同一条消息只能被一个订阅组内的某一个client消费。 |dataHandler：实时订阅数据处理对象;subId：云端配置的subId；consumerGroup：订阅分组名称 （如果consumerGroup传null，系统默认使用“DefaultConsumerGroup”作为consumerGroup的值。自行定义时，需避免使用“DefaultConsumerGroup”作为consumerGroup的值）|null

**订阅数据处理类：IDataHandler**

函数|函数说明|参数说明|返回
---|---|---|---
dataRead(MeasurePoint point) | 读取实时订阅数据函数 |point：实时订阅数据|无



## 告警数据订阅

**订阅Client类：EOSClient**

函数|函数说明|参数说明|返回
---|---|---|---
EosClient(String host,int port,String accessKey,String secret)	 | 获取构造函数 |host:订阅服务端地址;port：端口;accesskey：accesskey;secret：对应accesskey的secret|EosClient实例
getAlertService()	 | 获取告警数据订阅服务实例 |无|IIAlertService实例

**告警数据订阅服务类：IAlertService**

函数|函数说明|参数说明|返回
---|---|---|---
subscribe（IAlertHandler alertHandler,String subId）	 | 获取subId的订阅的告警数据，使用这个方法的订阅client属于默认的订阅分组 |alertHandler：告警订阅数据处理对象;subId：云端配置的subId|null
subscribe(IAlertHandler alertHandler,String subId,String consumerGroup); |获取subId的订阅的告警数据，同时指定订阅分组说明：consumerGroup指定了当前订阅client所属的订阅组，属于同一个订阅组的client共同处理订阅内容，这在单个订阅client处理能力有限的情况下，可以通过增加属于同一个订阅组的client来提升整体订阅处理能力。注意：同一条消息只能被一个订阅组内的某一个client消费 |alertHandler：告警订阅数据处理对象;subId：云端配置的subId;consumerGroup：订阅分组名称，与kafka consumerGroup含义相同（如果consumerGroup传null，系统默认使用“DefaultConsumerGroup”作为consumerGroup的值。自行定义时，需避免使用“DefaultConsumerGroup”作为consumerGroup的值）|null

**订阅数据处理类：IAlertHandler**

函数|函数说明|参数说明|返回
---|---|---|---
alertRead(Alert alert) | 读取告警订阅数据 |alert：告警订阅数据|无
