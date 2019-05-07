# 消费订阅数据
数据订阅任务启动运行之后，可以使用数据订阅SDK开发应用，消费已订阅的数据。数据订阅SDK的安装和消费订阅数据的代码示例如下：

## 安装数据订阅SDK

在Java开发项目文件中添加如下Maven依赖，安装数据订阅SDK：

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



## 消费实时数据代码示例

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

        // 订阅分组，相关概念见订阅SDK参考（可选）
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
        // 同时指定订阅分组，关于订阅分组的概念见订阅SDK参考说明
        dataService.subscribe(dataHandler, subId, consumerGroup);
    }
}
```

.. note:: - 在以上示例中， `host` 和 `port` 指订阅服务的地址和端口号。由于不同的云服务和实例的服务地址和端口号不同，请联系远景智能项目经理或技术支持获取对应的服务和端口信息。
      - 每个Topic Partition数量为2，即同一个订阅Topic最多只支持2个Consumer同时消费数据。
      - 一个Consumer实例只能消费一个Topic。
      - 数据在Topic中的存储时长默认为3天。


## 消费告警数据代码示例

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

        // 订阅分组，相关概念见订阅SDK参考（可选）
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
        // 同时指定订阅分组，关于订阅分组的概念见订阅SDK参考说明
        alertService.subscribe(alertHandler, subId, consumerGroup);
    }
}
```


<!--end-->
