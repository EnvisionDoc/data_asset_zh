# 获取TSDB存储数据

当数据存储策略配置完成之后，上传到云端的设备原始数据和经过流数据引擎聚合处理之后的数据都将存储在TSDB中。可通过调用相应的数据服务API来获取已存储的数据。

## EnOS数据服务API

存储在每个TSDB存储类型中的数据，都可以通过调用相应的数据服务API来查询。数据服务API的功能和调用方法如下：

| API 名称                           | 功能                                                         | 调用方法                                                     |
| ---------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| `getAssetsAIRawData`               | 获取指定设备的某些测点在某段时间内的AI原始数据               | 通过传入设备模型ID、资产ID、测点ID、查询起止时间段来获取存储类型为*AI原始数据*的数据。 |
| `getAssetsAINormalizedData`        | 获取指定设备的某些测点在某段时间内的分钟级归一化AI数据       | 通过传入设备模型ID、资产ID、带数据聚合算法的测点ID、算法作用时间间隔、查询起止时间段来获取存储类型为*AI分钟级归一化数据*的数据。注：当不使用数据聚合算法时， 算法作用时间间隔参数`interval`的值必须为0。 |
| `getAssetsStatusData`              | 获取指定设备在某段时间内的状态（DI）数据                     | 通过传入设备模型ID、资产ID、测点ID、查询起止时间段来变位查询设备状态数据。 |
| `getAssetsCurrentDayElectricPower` | 获取指定设备当日已累计电量数据                               | 通过传入设备模型ID、资产ID、测点ID、查询设备从当日0点开始已累计的电量数据。 |
| `getAssetsElectricPowerData`       | 获取指定设备在某段时间内的电量（PI）数据                     | 通过传入设备模型ID、资产ID、带数据聚合算法的测点ID、算法作用时间间隔、查询起止时间段来获取存储类型为*PI数据*的数据。注：当不使用数据聚合算法时， 算法作用时间间隔参数`interval`的值必须为0。 |
| `getAssetsGenericData`             | 获取指定设备的某些测点在某段时间内通用类型的数据             | 通过传入设备模型ID、资产ID、测点ID、查询起止时间段来获取存储类型为*通用数据*的数据。 |
| `getAssetsRawDataByTimeRange`      | 获取指定设备的某些测点在某段时间内原始数据的值（包括AI、DI、和通用数据类型） | 通过传入设备模型ID、资产ID、测点ID、查询起止时间段来获取各种类型的设备原始数据。 |



## EnOS API SDK for Java

EnOS提供的API SDK 支持API请求的封装，签名加密，响应解释，应用性能优化等功能。只需很少的编程工作，就可方便地调用EnOS数据服务API来获取存储数据、开发应用。

你可以通过在Java开发项目的 `pom.xml` 文件中添加Maven依赖来安装EnOS API SDK。具体步骤如下：

1. 访问EnOS API SDK的Maven仓库地址：https://mvnrepository.com/artifact/com.envisioniot/enos-api/2.3.6，获取EnOS API SDK的Maven依赖坐标。

2. 打开Java开发环境，将EnOS API SDK的Maven依赖坐标加入到开发项目文件中。如下所示：

   ```
   <dependency>
       <groupId>com.envisioniot</groupId>
       <artifactId>enos-api</artifactId>
       <version>2.3.6</version>
   </dependency>
   ```

或者，你也可以从[GitHub](https://github.com/EnvisionIot/enos-api-sdk-java)下载EnOS API SDK的源代码，并将其安装到开发环境中。有关EnOS SDK的详细介绍，请参考[EnOS SDK 快速入门](/docs/app-development/zh_CN/2.0.8/gettingstarted_sdk.html)。

## 代码示例

以下代码为调用 `getAssetsAIRawData` API获取存储在TSDB中的测点原始数据：

```
import com.envisioniot.enos.enosapi.api.request.dataservice.GetAssetsAIRawDataRequest;
import com.envisioniot.enos.enosapi.common.exception.EnOSApiException;
import com.envisioniot.enos.enosapi.common.response.EnOSPage;
import com.envisioniot.enos.enosapi.common.response.EnOSResponse;
import com.envisioniot.enos.enosapi.sdk.client.EnOSDefaultClient;

import java.util.List;
import java.util.Map;

public class demo {
    public static void main(String[] args) {
    String enosApiUrl = "api_service_url";
    String accessKey = "access_key";
    String secretKey = "secret_key";
    int connectTimeout = 5000;
    int readTimeout = 5000;
    String orgId = "organization_id";
    String modelId = "model_id";
    String assetIds = "asset_id";
    String measurepoints = "measure_point_id";
    String startTime = "2019-03-21T09:00:00-08:00";
    String endTime = "2019-03-26T09:12:00-08:00";
    int pageSize = 100;

    EnOSDefaultClient client = new EnOSDefaultClient(enosApiUrl, accessKey, secretKey, connectTimeout, readTimeout);
    GetAssetsAIRawDataRequest request = new GetAssetsAIRawDataRequest(orgId, modelId, assetIds, measurepoints, startTime, endTime, pageSize);

    try {
        EnOSResponse<EnOSPage<Map<String, Object>>> response = client.execute(request);
        System.out.println("REQUEST："+request.getUrlParams());

        if (response.getData() != null) {

            System.out.println("DATA：" + response.getData().getData());
        }
        System.out.println("STATUS：" + response.getStatus());
        System.out.println("MSG：" + response.getMsg());
        System.out.println("SUBMSG：" + response.getSubmsg());

        EnOSPage<Map<String, Object>> tmpMap = response.getData();

        if (tmpMap != null) {

            List<Map<String, Object>> re = tmpMap.getData();

            for (Map<String, Object> r : re) {
                System.out.println("timestamp:" + r.get("timestamp"));
                break;
            }
        }

    } catch (EnOSApiException e) {
        e.printStackTrace();
    }
  }
}
```

## API参考文档

EnOS系统提供详细的API参考文档，包括API的调用方法、API路径、参数描述、调用示例、和返回示例。

登录EnOS控制台之后，在页面左侧导航栏点击 **EnOS API** > **API文档**，即可查看按服务分类的API列表。点击 **更多** 图标，即可打开每个API的详细文档，如下图所示。

.. image:: ../../media/api_doc.png

有关调用EnOS API的详细方法，请参考[EnOS REST API 快速入门](/docs/app-development/zh_CN/2.0.8/gettingstarted_api.html)。

<!--end-->
