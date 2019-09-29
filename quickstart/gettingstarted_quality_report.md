# 入门指引：生成数据质量报告

该教程能帮助你快速学习使用流式计算StreamSets算子对数据进行质量打标，并且查询数据质量报告。

## 前提条件

- 已通过资源管理申请开通流数据处理计算资源和TSDB存储资源
- 已被授予数据质量模块和流数据处理StreamSets模块权限
- 已接入设备并且设备已经在发送数据

## 教程目标及数据准备

**教程目标场景**

本教程要实现的场景是：对AI类型的原始数据采集测点*test_raw*进行质量打标，并查询该测点的质量报告。

**数据准备**

- 模型配置

本教程使用的模型(*testModel*)配置如下：

| 功能类型 | 名称            | 标识符          | 测点类型 | 数据类型 |
|:---------|:----------------|:----------------|:---------|:---------|
| 测点     | test_raw        | test_raw        | AI       | DOUBLE   |
| 测点     | test_raw_filter | test_raw_filter | AI       | DOUBLE   |
| 测点     | test_raw_dq     | test_raw_dq     | AI       | DOUBLE   |

.. note:: - 其中 *test_raw* 为原始数据采集点，*test_raw_filter* 是原始数据经阈值过滤之后的数据点名称，*test_raw_dq* 是原始点要经过流数据处理后输出的数据点名称。

     - 必须保证需要处理的输入点和输出点的测点类型都是AI类型。


- 数据接入：请参考 [设备连接](/docs/device-connection/zh_CN/latest/quickstart/gettingstarted_device_connection.html) 来完成 *test_raw* 点数据的采集。


## 操作步骤

数据质量打标并查看质量报告的步骤如下：
- 创建并编写流数据处理任务对原始数据进行质量打标
- 保存、发布并启动流任务
- 查看数据质量报告

### 第一步：创建并编写流式计算任务对原始数据进行质量打标

1. 进入 **EnOS 控制台 > 流数据处理 > StreamSets** 菜单，创建并编辑流数据处理任务。
2. 点击 **Create New Pipeline** 按钮，添加流数据处理任务。
3. 进入任务编辑器，使用以下StreamSets算子，编辑流数据处理任务。具体Stage配置内容如下：

| No.  | 算子名称            | 参数配置                                                     | 说明                                                         |
| :--- | :------------------ | :----------------------------------------------------------- | :----------------------------------------------------------- |
| 1    | Kafka Consumer User | Topic：MEASURE_POINT_INTERNAL；Data Format：JSON             | 配置数据源                                                   |
| 2    | Point Selector      | Select Policy：testModel::test_raw                           | 选择流数据处理任务要处理的原始点                             |
| 3    | MinMax Outlier      | Model Point：testModel::test_raw；OpenClose：(x,y)；Min-Max：0,90.00；Output PointId：test_raw_filter | 配置阈值规则，输入点*test_raw*阈值为（0，90.00），输出点为*test_raw_filter* |
| 4    | Window Aggregator   | Aggregation Window Type：Fixed Window Aggregator；Fixed Window Unit：minute；Fixed Window Size：2；Latency (Minute)：0；Model::PointIn：testModel::test_filter；Aggregator Policy：avg；PointOut：test_raw_dq | 配置窗口聚合规则，窗口类型为固定窗口，窗口大小为2分钟，延迟设置为0，聚合算法为取测点平均值。 |
| 5    | Kafka Producer      | Topic：MEASURE_POINT_INTERNAL；Data Format：JSON             | 配置数据输出位置                                             |

配置完成的流数据处理任务，如下图所示：

.. image:: ../media/streamsets_job.png

### 第二步：保存、发布并启动流数据处理任务

配置好流数据处理任务之后，点击Start图标，启动任务。返回至任务列表页面，可查看任务运行状态。

### 第三步：查看数据质量报告

进入**EnOS 控制台 > 数据质量** 模块，输入查询条件（模型：*testModel*；测点：*test_raw_filter* 和 *test_raw_dq*），查询测点的数据质量报告。数据质量报告的详细介绍，请参考 [查询数据质量报告](../howto/quality/managing_data_quality)。
