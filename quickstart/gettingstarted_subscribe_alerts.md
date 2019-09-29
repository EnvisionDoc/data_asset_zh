# 订阅告警数据
本文介绍如何快速使用EnOS订阅配置界面进行数据订阅配置并使用订阅Java SDK消费告警数据。

## 前提条件

- 已被授权数据订阅模块
- 已接入设备并且设备已经在发送数据
- 订阅数据的服务账号（SA）已被授权获取资产数据
- 已安装好IDE（IDEA或者Eclipse）的电脑

## 目标及数据准备

**目标场景**

实现的场景：对原始AI采集点 *test_raw* 进行告警配置，并订阅其告警数据。

**数据准备**

- **模型配置**：使用的模型（*test_Model*）配置如下：

| 功能类型 | 名称     | 标识符   | 测点类型 | 数据类型 |
|:---------|:---------|:---------|:---------|:---------|
| 测点     | test_raw | test_raw | AI       | DOUBLE   |

- **数据接入**：*test_raw*为告警数据采集点，请参考 [设备连接](/docs/device-connection/zh_CN/2.0.8/quickstart/gettingstarted_device_connection.html) 来完成 *test_raw* 点数据的采集。
- **告警配置**：请参考 [资产告警](/docs/device-connection/zh_CN/2.0.8/howto/alert/alert_overview.html) 来完成 *test_raw* 点数据的告警配置。


## 操作步骤

订阅并消费告警数据步骤如下：
- 创建并配置告警数据订阅Topic
- 保存并启动订阅Topic
- 使用订阅SDK消费订阅数据
- 查看数据消费结果



## 第一步：创建并配置告警数据订阅Topic

进入 **EnOS Portal > 控制台 > 数据订阅** 模块，可查看当前组织创建的所有订阅Topic；请参考如下步骤完成告警数据订阅Topic的创建及配置：

1. 创建订阅：点击**添加订阅**按钮，可添加订阅Topic，本教程中选择**告警数据订阅**。

2. 选择订阅关联的SA账号：每个订阅实例都必须关联一个SA账号，目前EnOS平台上只有创建应用才能生成一个SA账号，具体SA生成方法请参考 [管理应用](/docs/app-development/zh_CN/2.0.8/managing_apps.html)。

   .. note:: 数据订阅关联的SA账号必须已被授权获取资产的数据，否则订阅任务会认证失败，而不能成功订阅数据。授权SA账号的详细信息，请参考 [管理服务账号](/docs/iam/zh_CN/2.0.8/howto/service_account/managing_service_account.html)。

3. 选择需要订阅的客户数据：每个SA可访问多个客户的数据（通过应用购买），订阅可根据需要进行客户选择。

4. 选择模型过滤条件：本教程中选择 *test_Model* 这个模型作为条件，订阅系统则会过滤出符合模型条件的数据。

5. （可选）可根据业务需要，添加设备标签或资产树标签，过滤订阅的数据，仅订阅指定设备或指定资产树相关的告警数据。



## 第二步：保存并启动订阅Topic

配置好订阅Topic之后，点击**保存**，返回至列表页面，开启保存好的订阅Topic，启动数据的生产。



## 第三步：线下使用订阅Java SDK消费订阅数据

EnOS平台提供对应的订阅Java SDK帮助开发者快速进行线下开发并消费订阅数据，请参考如下步骤进行线下开发。
- 在IDE中引用对应的Maven地址，SDK的Maven仓库地址是：https://mvnrepository.com/artifact/com.envisioniot/enos-subscribe/2.2.0

  IDE中Maven引用示例如下：

  ```java
  <dependency>
    <groupId>com.envisioniot</groupId>
    <artifactId>enos-subscribe</artifactId>
    <version>2.2.0</version>
  </dependency>
  ```

- 使用IDE进行线下开发；本教程示例代码如下：

  ```java
  String sub_server_host ="sub_server_host";
  int sub_server_port ="sub_server_port";
  String accessKey ="access_Key";
  String secretKey ="secret_Key";
  String subId = "subscriptionId";
  String consumerGroup = "consumerGroup";

  /* service */
  EOSClient eosClient = new EOSClient(sub_server_host, sub_server_port, accessKey, secretKey);
  IAlertService alertService = eosClient.getAlertService();

  /* handler */
  IAlertHandler alertHandler = new IAlertHandler(){
      @Override
     public void alertRead(Alert alert) {
          System.out.println(alert);
      }
  };

  /* subscribe */
  alertService.subscribe(alertHandler, subId);

  /* subscribe with consumer group (optional) */
  alertService.subscribe(alertHandler, subId, consumerGroup);
  ```

.. note:: 在以上示例中， `sub_server_host` 和 `sub_server_port` 指订阅服务的地址和端口号。由于不同的云服务和实例的服务地址和端口号不同，请联系远景智能项目经理或技术支持获取对应的服务和端口信息。

有关数据订阅SDK的详细信息，请参考 [数据订阅SDK参考](../reference/data_subscription_sdk)。

## 第四步：查看数据消费结果

运行订阅消费程序，通过运行日志能查看应用是否已消费告警数据。
