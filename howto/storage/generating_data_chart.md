# 生成时序数据图表

对存储在TSDB中的时序数据，可通过指定的规则进行筛选，并且以图表的方式显示，方便快速查看和分析数据。

## 任务描述

本文介绍了配置时序数据筛选条件、生成时序数据图表、快速查看和分析数据的步骤。

## 开始前准备

- 设备测点已配置存储策略，并且测点数据是数值类型。
- 设备已上传数据，并且存储在TSDB中。

## 步骤

1. 登录EnOS控制台，选择 **时序数据管理 > 数据洞察**，完成数据筛选的条件配置。
2. 在 **时间选择** 一栏中，选择或指定查询数据的时间范围。各选项代表的具体时间范围如下：

  - 1H：从1小时前至当前时刻
  - 1D：从当日零点至当前时刻
  - 7D：从7日前零点至当前时刻
  - 自定义：按需指定查询数据的时间范围

3. 点击 **设备选择** 输入框，从下拉菜单中选择一个或多个需查询数据的设备。选中的设备会动态展示在 **已选测点** 一栏中供测点选择。如需重新选择设备，点击 **重置**，清空已选设备名单。

4. 在 **数据选择** 一栏中，选择需要显示的数据类型。选中不同的数据类型后，已选测点一栏会动态展示对应的测点列表。

   - 如选择 **ALL**，**已选测点** 一栏会相应地展示已选设备的所有测点。并且在查询数据时，不对测点数据进行聚合处理或变位查询。
   - 如选择 **AI** 或 **PI** 类型，则相应地选择处理数据的聚合函数和聚合算法作用的时间间隔。目前支持的聚合函数如下：

       - count：以每个时间范围内的数据点的数目作为结果
       - sum：以每个时间范围内的测点数值的总和作为结果
       - avg：以每个时间范围内的测点数值的平均值作为结果
       - max：以每个时间范围内的测点数值的最大值作为结果
       - min：以每个时间范围内的测点数值的最小值作为结果
       - first：以每个时间范围内的第一个测点数值作为结果
       - last：以每个时间范围内的最后一个测点数值作为结果

   - 如选择 **DI** 类型，则相应地选择是否需要变位查询设备状态数据。如开启变位查询，则只展示设备状态变化的数据点。
5. 在 **已选测点** 一栏中，点击已选择的设备名称，展开测点列表，选择一个或多个需查询数据的测点。查询到的测点数据将会展示在右侧图表中。


## 结果

查询到的测点数据展示在页面右侧的图表中。拖动图表下的时间轴或使用图表右上角的区域缩放工具，查看图表中特定时间段的数据信息，包括数据时间戳、测点名、测点数据、以及数据波动曲线。如下图所示：

.. image:: ../../media/data_chart.png

在数据图表下，可查看已选测点的最新数据以及数据最后更新时间。如下图所示：

.. image:: ../../media/latest_data.png

点击**数据列表**，可分页查看查询到的数据信息。如下图所示：

.. image:: ../../media/data_list.png

## 后续操作

如需查看其它设备或测点的数据，选择相应的设备名称、测点类型和测点名称进行查询。
