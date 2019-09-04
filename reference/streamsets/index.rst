StreamSets算子参考说明
=========================

.. contents::
   :depth: 1
   :hidden:

EnOS™流数据分析服务开放多个底层封装好的StreamSets算子，支持主数据关联、聚合算法、插补策略、基于事件时间的时间窗口、以及阈值过滤等计算。供开发者通过编排算子创建流数据分析任务，满足更多复杂场景的业务计算。

资产主数据算子
-----------------------------------
.. toctree::
   :maxdepth: 1

   tsl_asset_lookup
   tsl_child_asset_lookup
   tsl_parent_asset_lookup
   tsl_point_lookup
   site_lookup


数据处理算子
-----------------------------------
.. toctree::
   :maxdepth: 1

   point_selector
   asset_generator
   partitioner
   asset_partitioner
   point_partitioner
   time_sort
   window_aggregator
   fixed_batch_pivotor
   earliest_change_record_appender
   state_capturer
   state_restorer

其他数据处理算子

.. toctree::
   :maxdepth: 1

   python_evaluator
   http_lookup

数据质量算子
-----------------------------------
.. toctree::
   :maxdepth: 1

   late_point_filter
   min_max_outlier

电量计算算子
-----------------------------------
.. toctree::
   :maxdepth: 1

   last_record_appender
   delta_calculator
   delta_down_sampler
