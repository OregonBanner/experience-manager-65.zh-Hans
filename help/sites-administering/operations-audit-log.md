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

符合审核日志记录条件的AEM事件会生成大量存档数据。 由于复制、资产上传和其他系统活动，此数据会随着时间的推移而快速增长。

审核日志维护包括若干部分功能，利用这些功能，可以自动执行特定策略下的审核日志维护。

它是作为可配置的每周维护任务实施的，可通过Operations Dashboard监控控制台访问。

欲了解更多信息，请参见 [操作功能板文档](/help/sites-administering/operations-dashboard.md).

有三种类型的审核日志清除选项：

1. [页面审核日志清除](/help/sites-administering/operations-audit-log.md#configure-page-audit-log-purging)
1. [DAM审核日志清除](/help/sites-administering/operations-audit-log.md#configure-dam-audit-log-purging)
1. [复制审核日志分析](/help/sites-administering/operations-audit-log.md#configure-replication-audit-log-purging)

每种规则都可以通过在AEM Web Console中创建规则来配置。 配置完毕后，您可以通过转到 **工具 — 操作 — 维护 — 每周维护窗口** 并运行 **审核日志维护任务**.

## 配置页面审计日志清除 {#configure-page-audit-log-purging}

要配置审计日志清除，请执行以下步骤：

1. 通过将您的浏览器指向，转到Web控制台管理员 `http://localhost:4502/system/console/configMgr/`

1. 搜索名为的项目 **页面审核日志清除规则** 然后点击它。

   ![chlimage_1-365](assets/chlimage_1-365.png)

1. 接下来，根据您的要求配置清除调度程序。 可用的选项为：

   * **规则名称：** 审计策略规则的名称；
   * **内容路径：** 规则将应用于的内容的路径；
   * **最低年龄：** 审核日志需要保存的时间（以天为单位）；
   * **审核日志类型：** 应清除的审核日志的类型。

   >[!NOTE]
   >
   >内容路径仅适用于 `/var/audit/com.day.cq.wcm.core.page` 节点。

1. 保存规则。
1. 您刚刚创建的规则需要显示在操作仪表板中才能执行。 要执行此操作，请转到 **工具 — 操作 — 维护** 从AEM欢迎屏幕。

1. 按 **每周维护时段** 信息卡。

1. 您会发现维护任务已存在于 **审核日志维护任务** 信息卡。

   ![chlimage_1-366](assets/chlimage_1-366.png)

1. 您可以检查下一次执行的日期、配置该日期，或通过按播放按钮手动执行该日期。

在AEM 6.3中，如果计划的维护窗口在审核日志清除任务完成之前关闭，则该任务将自动停止。 当下一个维护窗口打开时，它将恢复。

**使用AEM 6.5**，您可以通过单击 **停止** 图标。 在下次执行时，该任务将安全地恢复。

>[!NOTE]
>
>停止维护任务意味着暂停其执行，而不会丢失已正在进行的作业的跟踪。

## 配置DAM审核日志清除 {#configure-dam-audit-log-purging}

1. 导航到位于的系统控制台 *https://&lt;serveraddress>：&lt;serverport>/system/console/configMgr*
1. 搜索 **DAM审核日志清除** 规则并单击结果。
1. 在下一个窗口中，相应地配置规则。 选项包括：

   * **规则名称：** 审计策略规则的名称；
   * **内容路径：** 规则将应用于的内容的路径
   * **最低年龄：** 需要保留审核日志的时间（以天为单位）
   * **审核日志DAM事件类型：** 应清除的DAM审核事件的类型。

1. 单击 **保存** 保存配置

## 配置复制审核日志清除  {#configure-replication-audit-log-purging}

1. 导航到位于的系统控制台 *https://&lt;serveraddress>：&lt;serverport>/system/console/configMgr*
1. 搜索 **复制审核日志清除计划程序** 并单击结果
1. 在下一个窗口中，相应地配置规则。 选项包括：

   * **规则名称：** 审计策略规则的名称
   * **内容路径：** 规则将应用于的内容的路径
   * **最低年龄：** 需要保留审核日志的时间（以天为单位）
   * **审核日志复制事件类型：** 应清除的复制审核事件类型

1. 单击 **保存** 以保存您的配置。
