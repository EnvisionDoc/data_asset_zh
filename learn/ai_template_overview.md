# 时间窗口聚合模板

针对数值类型的设备上传数据，EnOS流式计算系统提供统一的**时间窗口聚合模板**，能将某一设备上的某个数值类型的测点数据进行聚合处理后赋值给同一设备上的另一个测点。帮助您方便、快速地完成对单设备单测点数值类型数据的处理。

## 优势

**丰富的算法**

提供丰富的数据聚合算法，包括求最大值（max）、求最小值（min）、求平均值（avg）、求和（sum）、计数（cnt）。

**基于时间窗口处理数据**

基于数据事件时间，对时间窗口内的数据进行聚合处理。对时间窗口的详细介绍，请参考[时间窗口参考说明](/docs/data-asset/zh_CN/latest/reference/time_window.html)。

**时间窗口延迟设置**

通过设置窗口延迟，可将迟到的数据加入到窗口中进行再次计算。并且支持中间结果的输出（当下一个时间窗口产生时，上一个时间窗口会输出一个中间结果），此中间结果会输出TSDB，但不会归档。

**异常数据过滤**

支持有效数据阈值区间设置，对超出阈值的异常数据进行插补处理。


## 配置时间窗口数据聚合任务

可通过以下两大步骤，使用时间窗口聚合模板快速创建流数据处理任务：

1. 创建流数据处理任务时，选择**时间窗口聚合模板**。详见[创建流数据处理任务](/docs/data-asset/zh_CN/latest/howto/stream/creating_job.html)。
2. 配置流数据处理策略。详见[配置时间窗口数据聚合任务](/docs/data-asset/zh_CN/latest/howto/stream/configuring_ai_template.html)。
