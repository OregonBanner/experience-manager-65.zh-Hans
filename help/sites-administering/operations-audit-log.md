---
title: AEM 6中的审核日志维护
seo-title: AEM 6中的审核日志维护
description: 了解AEM中的审核日志维护。
seo-description: 了解AEM中的审核日志维护。
uuid: 212de4df-6bf4-434c-94e1-74186d21945a
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 565d89de-b3ca-41a5-8e1c-d10905c25fb5
translation-type: tm+mt
source-git-commit: 2fc35bfd93585a586cb1d4e3299261611db49ba6
workflow-type: tm+mt
source-wordcount: '615'
ht-degree: 0%

---


# AEM 6{#audit-log-maintenance-in-aem}中的审核日志维护

符合审核记录资格的AEM事件会生成大量归档数据。 由于复制、资产上传和其他系统活动，这些数据会随着时间的推移而快速增长。

“审核日志维护”包括几个功能部分，这些功能允许根据特定策略自动执行审核日志维护。

它作为可配置的每周维护任务实施，并可通过“操作仪表板”监控控制台访问。

有关详细信息，请参阅[操作仪表板文档](/help/sites-administering/operations-dashboard.md)。

审核日志清除选项有三种类型：

1. [页面审核日志清除](/help/sites-administering/operations-audit-log.md#configure-page-audit-log-purging)
1. [DAM审核日志清除](/help/sites-administering/operations-audit-log.md#configure-dam-audit-log-purging)
1. [复制审核日志更新](/help/sites-administering/operations-audit-log.md#configure-replication-audit-log-purging)

每项配置均可通过在AEM Web控制台中创建规则来进行。 配置完这些任务后，您可以转到&#x200B;**工具——操作——维护——每周维护窗口**&#x200B;并运行&#x200B;**审核日志维护**&#x200B;来触发它们。

## 配置页面审核日志清除{#configure-page-audit-log-purging}

按照以下步骤配置审核日志清除：

1. 将浏览器指向`http://localhost:4502/system/console/configMgr/`，转到Web控制台管理员

1. 搜索名为&#x200B;**页面审核日志清除规则**&#x200B;的项，然后单击它。

   ![chlimage_1-365](assets/chlimage_1-365.png)

1. 然后，根据您的要求配置清除调度程序。 可用选项有：

   * **规则名称** ：审计策略规则的名称；
   * **内容路** 径：规则将应用到的内容的路径；
   * **最低年龄：** 需要保存审计日志的天数；
   * **审核日志类** 型：应清除的审核日志类型。

   >[!NOTE]
   >
   >内容路径仅适用于存储库中`/var/audit/com.day.cq.wcm.core.page`节点的子项。

1. 保存规则。
1. 您刚刚创建的规则需要在“操作”仪表板中公开才能执行。 为此，请从AEM欢迎屏幕转至&#x200B;**工具——操作——维护**。

1. 按&#x200B;**每周维护窗口**&#x200B;卡。

1. 在&#x200B;**AuditLog Maintenance任务卡**&#x200B;下，您会发现已存在维护任务。

   ![chlimage_1-366](assets/chlimage_1-366.png)

1. 您可以检查下次执行的日期、对其进行配置或通过按播放按钮手动执行。

在AEM 6.3中，如果计划的维护窗口在“审核日志清除”任务完成之前关闭，则任务会自动停止。 下次维护窗口打开时，它将恢复。

**在AEM 6.5中**，您可以单击停止图标，手动停止正在运行的审核日志清除 **** 任务。下次执行时，任务将安全恢复。

>[!NOTE]
>
>停止维护任务意味着暂停其执行，而不丢失对已进行作业的跟踪。

## 配置DAM审核日志清除{#configure-dam-audit-log-purging}

1. 导航到位于&#x200B;*https://&lt;serveraddress>的系统控制台：&lt;serverport>/system/console/configMgr*
1. 搜索&#x200B;**DAM审核日志清除**&#x200B;规则，然后单击结果。
1. 在下一个窗口中，相应地配置您的规则。 选项有：

   * **规则名称** ：审计策略规则的名称；
   * **内容路** 径：规则将应用到的内容的路径
   * **最低年龄：** 需要保留审计日志的天数
   * **审核日志事件类型:** 应清除的DAM审核事件类型。

1. 单击&#x200B;**保存**&#x200B;以保存配置

## 配置复制审核日志清除{#configure-replication-audit-log-purging}

1. 导航到位于&#x200B;*https://&lt;serveraddress>的系统控制台：&lt;serverport>/system/console/configMgr*
1. 搜索&#x200B;**复制审核日志清除调度程序**&#x200B;并单击结果
1. 在下一个窗口中，相应地配置您的规则。 选项有：

   * **规则名称** ：审计策略规则的名称
   * **内容路** 径：规则将应用到的内容的路径
   * **最低年龄：** 需要保留审计日志的天数
   * **审核日志复制事件类型** ：应清除的复制审核事件的类型

1. 单击&#x200B;**保存**&#x200B;以保存配置。

