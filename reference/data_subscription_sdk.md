# 数据订阅SDK参考
完成数据订阅配置之后，可以使用数据订阅SDK来获取已订阅的数据。数据订阅SDK的参考文档如下：

## SDK 依赖

在使用数据订阅SDK之前，需要在Java开发项目文件中添加如下Maven依赖：

```
<dependency>
  <groupId>com.envisioniot</groupId>
  <artifactId>enos-subscribe</artifactId>
  <version>2.0.0</version>
</dependency>
<dependency>
  <groupId>com.google.code.gson</groupId>
  <artifactId>gson</artifactId>
  <version>2.8.0</version>
</dependency>
<dependency>
  <groupId>log4j</groupId>
  <artifactId>log4j</artifactId>
  <version>1.2.16</version>
</dependency>
```



## 实时数据订阅

### 订阅Client类：EosClient

.. list-table::
   :widths: 20 40 30 10

   * - 函数
     - 函数说明
     - 参数说明
     - 返回
   * - EosClient(String host,int port,String accessKey,String accessSecret)
     - 获取构造函数
     - + host: 订阅服务端地址
       + port: 端口
       + accesskey: accessKey
       + accessSecret: 对应accesskey的secret
     - EosClient实例
   * - getDataService()
     - 获取实时数据订阅服务实例
     - 无
     - IDataService实例


### 实时数据订阅服务类：IDataService

.. list-table::
   :widths: 20 40 30 10

   * - 函数
     - 函数说明
     - 参数说明
     - 返回
   * - subscribe(IDataHandler dataHandler,String subId)
     - 获取subId的订阅的实时数据
     - + dataHandler: 实时订阅数据处理对象
       + subId: 云端配置的subId
     - null
   * - subscribe(IDataHandler dataHandler,String subId,String consumerGroup)
     - 获取subId的订阅的实时数据，同时指定订阅分组说明：consumerGroup指定了当前订阅client所属的订阅组，属于同一个订阅组的client共同处理订阅内容，这在单个订阅client处理能力有限的情况下，可以通过增加属于同一个订阅组的client来提升整体订阅处理能力。注意：同一条消息只能被一个订阅组内的某一个client消费。
     - + dataHandler: 实时订阅数据处理对象
       + subId：云端配置的subId
       + consumerGroup：订阅分组名称 （如果consumerGroup传null，系统默认使用“DefaultConsumerGroup”作为consumerGroup的值。自行定义时，需避免使用“DefaultConsumerGroup”作为consumerGroup的值）
     - null


### 订阅数据处理类：IDataHandler

.. list-table::
   :widths: 20 40 30 10

   * - 函数
     - 函数说明
     - 参数说明
     - 返回
   * - dataRead(MeasurePoint point)
     - 读取实时订阅数据函数
     - point：实时订阅数据
     - 无

### 示例

```
import com.envisioniot.sub.client.EosClient;
import com.envisioniot.sub.client.data.IDataHandler;
import com.envisioniot.sub.client.data.IDataService;
import com.envisioniot.sub.common.model.dto.StreamMessage;
 
public class DataServiceDemo {
    public static void main(String[] args) throws Exception {
        // 订阅服务地址，请根据使用环境填写
        String host = "subscription_server";
        // 订阅服务端口，请根据使用环境填写
        int port = 9001;
        // 应用身份验证，在应用创建时生成
        String accessKey = "access_key";
        // 应用身份验证，在应用创建时生成
        String secretKey = "secret_key";

        // 订阅ID，创建订阅时生成
        String subId = "subscription_id";
 
        // 订阅分组，相关概念见以上接口定义（可选）
        String consumerGroup = "consumer_group";
 
        EosClient eosClient = new EosClient(host, port, accessKey, secretKey);
 
        // 根据订阅类型获取相应的service，本示例获取实时数据service
        IDataService dataService = eosClient.getDataService();
 
        // 在启动订阅之前需要创建订阅数据处理函数
        IDataHandler dataHandler = new IDataHandler(){
            public void dataRead(StreamMessage message) {
                System.out.println(message);
            }
        };
 
        // 需要调用subscribe函数创建订阅连接，调用后订阅连接被创建
        dataService.subscribe(dataHandler, subId);
 
        // 和上面的subscribe任选其一使用来创建连接
        // 同时指定订阅分组，关于订阅分组的概念在上面的接口定义有说明
        dataService.subscribe(dataHandler, subId, consumerGroup);
    }
}
```

.. note:: 在以上示例中， `host` 和 `port` 指订阅服务的地址和端口号。由于不同的云服务和实例的服务地址和端口号不同，请联系远景智能项目经理或技术支持获取对应的服务和端口信息。

## 告警数据订阅

### 订阅Client类：EosClient

.. list-table::
   :widths: 20 40 30 10

   * - 函数
     - 函数说明
     - 参数说明
     - 返回
   * - EosClient(String host,int port,String accessKey,String accessSecret)
     - 获取构造函数
     - + host: 订阅服务端地址
       + port: 端口
       + accesskey: accessKey
       + accessSecret: 对应accesskey的secret
     - EosClient实例
   * - getAlertService()
     - 获取告警数据订阅服务实例
     - 无
     - IAlertService实例


### 告警数据订阅服务类：IAlertService

.. list-table::
   :widths: 20 40 30 10

   * - 函数
     - 函数说明
     - 参数说明
     - 返回
   * - subscribe(IAlertHandler alertHandler,String subId)
     - 获取subId的订阅的告警数据，使用这个方法的订阅client属于默认的订阅分组
     - + alertHandler：告警订阅数据处理对象
       + subId: 云端配置的subId
     - null
   * - subscribe(IAlertHandler alertHandler,String subId,String consumerGroup)
     - 获取subId的订阅的告警数据，同时指定订阅分组说明：consumerGroup指定了当前订阅client所属的订阅组，属于同一个订阅组的client共同处理订阅内容，这在单个订阅client处理能力有限的情况下，可以通过增加属于同一个订阅组的client来提升整体订阅处理能力。注意：同一条消息只能被一个订阅组内的某一个client消费。
     - + alertHandler：告警订阅数据处理对象
       + subId：云端配置的subId
       + consumerGroup：订阅分组名称，与kafka consumerGroup含义相同（如果consumerGroup传null，系统默认使用“DefaultConsumerGroup”作为consumerGroup的值。自行定义时，需避免使用“DefaultConsumerGroup”作为consumerGroup的值）
     - null


### 订阅数据处理类：IAlertHandler

.. list-table::
   :widths: 20 40 30 10

   * - 函数
     - 函数说明
     - 参数说明
     - 返回
   * - alertRead(Alert alert)
     - 读取告警订阅数据函数
     - alert：告警订阅数据
     - 无

### 示例

```
import com.envisioniot.sub.client.EosClient;
import com.envisioniot.sub.client.event.IAlertHandler;
import com.envisioniot.sub.client.event.IAlertService;
import com.envisioniot.sub.common.model.Alert;
 
public class AlertServiceDemo1 {
    public static void main(String[] args) throws Exception {
        // 订阅服务地址，请根据使用环境填写
        String host = "subscription_server";
        // 订阅服务端口，请根据使用环境填写
        int port = 9001;
        // 应用身份验证，在应用创建时生成
        String accessKey = "access_key";
        // 应用身份验证，在应用创建时生成
        String secretKey = "secret_key";

        // 订阅ID，创建订阅时生成
        String subId = "subscription_id";
 
        // 订阅分组，相关概念见以上接口定义（可选）
        String consumerGroup = "consumer_group";
 
        EosClient eosClient = new EosClient(host, port, accessKey, secretKey);
 
        // 根据订阅类型获取相应的service，本示例获取告警service
        IAlertService alertService = eosClient.getAlertService();
 
        // 在启动订阅之前需要创建订阅数据处理函数
        IAlertHandler alertHandler = new IAlertHandler (){
            @Override
            public void alertRead(Alert alert) {
                System.out.println(alert);
            }
        };
 
        // 需要调用subscribe函数创建订阅连接，调用后订阅连接被创建
        alertService.subscribe(alertHandler, subId);
 
        // 和上面的subscribe任选其一使用来创建连接
        // 同时指定订阅分组，关于订阅分组的概念在上面的接口定义有说明
        alertService.subscribe(alertHandler, subId, consumerGroup);
    }
}
```
<!--end-->
