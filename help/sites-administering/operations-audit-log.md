---
title: AEM 6中的审核日志维护
seo-title: Audit Log Maintenance in AEM 6
description: 了解AEM中的审核日志维护。
seo-description: Lear about Audit Log Maintenance in AEM.
uuid: 212de4df-6bf4-434c-94e1-74186d21945a
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 565d89de-b3ca-41a5-8e1c-d10905c25fb5
exl-id: 1e05faf5-619a-4ea3-acbf-2fd37c71e6d2
feature: Operations
source-git-commit: 9134130f349c6c7a06ad9658a87f78a86b7dbf9c
workflow-type: tm+mt
source-wordcount: '603'
ht-degree: 0%

---

# AEM 6中的审核日志维护{#audit-log-maintenance-in-aem}

符合审核日志记录条件的AEM事件会生成大量存档数据。 由于复制、资产上传和其他系统活动，此数据会随着时间而快速增长。

“审核日志维护”包括几个功能部分，这些功能允许在特定策略下自动维护审核日志。

它作为可配置的每周维护任务实施，并可通过操作仪表板监控控制台访问。

有关更多信息，请参阅 [操作功能板文档](/help/sites-administering/operations-dashboard.md).

审核日志清除选项有三种类型：

1. [页面审核日志清除](/help/sites-administering/operations-audit-log.md#configure-page-audit-log-purging)
1. [DAM审核日志清除](/help/sites-administering/operations-audit-log.md#configure-dam-audit-log-purging)
1. [复制审核日志记录](/help/sites-administering/operations-audit-log.md#configure-replication-audit-log-purging)

每个规则都可以通过在AEM Web Console中创建规则来配置。 配置完它们后，您可以通过转到 **工具 — 操作 — 维护 — 每周维护窗口** 运行 **审核日志维护任务**.

## 配置页面审核日志清除 {#configure-page-audit-log-purging}

请按照以下步骤配置审核日志清除：

1. 通过将浏览器指向 `http://localhost:4502/system/console/configMgr/`

1. 搜索名为 **页面审核日志清除规则** 然后单击它。

   ![chlimage_1-365](assets/chlimage_1-365.png)

1. 接下来，根据您的要求配置清除计划程序。 可用的选项为：

   * **规则名称：** 审计策略规则的名称；
   * **内容路径：** 应用规则的内容路径；
   * **最低年龄：** 需要保留审核日志的时间（以天为单位）；
   * **审核日志类型：** 应清除的审核日志类型。

   >[!NOTE]
   >
   >内容路径仅适用于 `/var/audit/com.day.cq.wcm.core.page` 节点。

1. 保存规则。
1. 您刚刚创建的规则需要显示在操作功能板中才能执行。 为此，请 **工具 — 操作 — 维护** 从AEM欢迎屏幕中。

1. 按 **每周维护窗口** 卡。

1. 您将在 **审核日志维护任务** 卡。

   ![chlimage_1-366](assets/chlimage_1-366.png)

1. 您可以检查下次执行的日期、对其进行配置，或通过按“播放”按钮手动执行。

在AEM 6.3中，如果计划维护窗口在审核日志清除任务完成之前关闭，则任务会自动停止。 在下一个维护窗口打开时，系统将恢复运行。

**使用AEM 6.5**，您可以通过单击 **停止** 图标。 下次执行时，任务将安全地恢复。

>[!NOTE]
>
>停止维护任务意味着暂停其执行，而不丢失已在进行中的作业的跟踪。

## 配置DAM审核日志清除 {#configure-dam-audit-log-purging}

1. 导航到位于 *https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr*
1. 搜索 **DAM审核日志清除** 规则，然后单击结果。
1. 在下一个窗口中，相应地配置规则。 选项包括：

   * **规则名称：** 审计策略规则的名称；
   * **内容路径：** 应用规则的内容路径
   * **最低年龄：** 需要保留审核日志的时间（以天为单位）
   * **审核日志Dam事件类型：** 应清除的DAM审核事件类型。

1. 单击 **保存** 保存配置

## 配置复制审核日志清除  {#configure-replication-audit-log-purging}

1. 导航到位于 *https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr*
1. 搜索 **复制审核日志清除计划程序** 并单击结果
1. 在下一个窗口中，相应地配置规则。 选项包括：

   * **规则名称：** 审计策略规则的名称
   * **内容路径：** 应用规则的内容路径
   * **最低年龄：** 需要保留审核日志的时间（以天为单位）
   * **审核日志复制事件类型：** 应清除的复制审核事件类型

1. 单击 **保存** 以保存配置。
