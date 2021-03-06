# 管理数据归档任务

在 **数据归档** 页面上，可以查看所有数据归档任务的运行状态，并可以对归档任务状态设置邮件告警、编辑归档任务配置、停止归档任务、或删除归档任务。

## 设置告警

当归档任务运行失败时或归档过程中出现数据丢失等异常情况时，归档任务负责人会收到告警邮件或短信提醒。按照以下步骤设置邮件告警：

1. 打开 **数据归档** 页面，在归档任务列表中，找到已提交的归档任务。
2. 点击 **操作 > 告警**，打开 **告警配置** 窗口。
3. 选择告警信息 **接收者** 和发送告警的 **方式**（短信或邮件）。
4. 点击 **确定**，保存告警设置。

<!--

## 查看日志

对于正在归档周期内的归档任务，可查看运行日志。

1. 在**数据归档**页面，点击**操作 > 查看日志**，打开当前归档周期的运行日志。
2. 点击**下载日志**，可下载保存归档任务的运行日志。

运行日志主要包含数据归档策略的配置信息，归档任务状态，归档任务进度，已归档文件数量和已同步至目标存储系统的文件数。

-->

## 编辑归档任务配置

如业务需要，可编辑更新已提交的数据归档任务配置。

1. 打开 **数据归档** 页面，在归档任务列表中，找到已提交的归档任务。
2. 点击 **编辑** 图标，打开 **编辑任务** 页面。
3. 根据业务需要，更新数据归档任务配置信息。
4. 点击 **确认**，提交归档任务配置更新。

更新后的数据归档任务提交后，将立即生效。如当前归档周期的数据归档任务未完成，将立即按照新提交的归档任务配置重新运行，已同步至存储系统的数据不受影响。对于新增模型的数据，也将立即开始归档。

## 停止任务

对于数据源为离线消息通道的数据归档任务，可通过点击 **操作 > 停止** 图标，手动停止数据归档任务。如重新启动数据归档任务，则从启动任务的时间点重新开始数据归档，不会延续任务停止时的归档任务。

对于数据源为实时消息通道的数据归档任务，不支持手动停止。若需停止归档，可删除归档任务。归档任务删除后，已归档的文件不受影响。

## 删除任务

可通过以下步骤删除数据归档任务：

1. 打开 **数据归档** 页面，在归档任务列表中，找到已提交的归档任务。
2. 点击 **操作 > 删除**，确认删除数据归档任务。

删除数据归档任务后，当前归档任务将立即停止。已同步至存储系统的数据，不受影响。对于平台内缓存的归档文件，直接删除，不再继续同步到存储系统。处在同步过程中的文件，继续同步直至完成。
