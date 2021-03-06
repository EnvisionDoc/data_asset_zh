# 数据存储

EnOS为设备采集原始数据和经流数据处理之后的数据提供多样化的存储选择和配置。您可根据业务对数据的存储和读取需求，选择对应的存储类型，降低存储成本、提升数据读取效率。

## 时序数据存储（TSDB）
TSDB存储适用于存储需要频繁访问的数据，同时支持存储经实时通道和离线通道集成的数据，并且对AI原始数据、AI归一化数据、DI数据、PI数据、通用数据等类型的数据提供分类存储、读取、和删除的能力。

有关配置TSDB存储的详细信息，参见 [配置TSDB存储](../configuring_tsdb_storage)。

## 归档存储

归档存储适用于存储访问频率较低且占用存储空间很大的业务数据，同时支持归档经实时通道上送的和离线通道集成的数据。数据经归档后生成的文件将根据配置的存储路径信息，自动同步到指定的存储系统中，实现数据备份。

有关配置数据归档的详细信息，参见 [配置数据归档任务](../howto/archive/configuring_archive_storage)。
