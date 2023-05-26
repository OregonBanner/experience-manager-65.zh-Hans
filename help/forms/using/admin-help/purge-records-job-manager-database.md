---
title: 从作业管理器数据库中清除记录
seo-title: Purge records from the Job Manager database
description: 较大的流程数据可能会导致AEM表单性能降低。 当不再需要记录时，最好清除流程数据。
seo-description: Large process data can result in lower AEM forms performance. It is good practice to purge process data when records are no longer necessary.
uuid: cf214498-36e9-4dcc-b4d4-e7c46f80dbab
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 69a406f2-4fa8-40bb-b671-7b0f5b6a2c4c
exl-id: 5279f6c3-5954-472c-9ea0-18e8a7ec860e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 0%

---

# 从作业管理器数据库中清除记录 {#purge-records-from-the-job-manager-database}

在调用长期进程时生成的进程数据可能会变得太大，从而导致AEM表单性能降低和使用不必要的磁盘空间。 当不再需要记录时，最好清除流程数据。

您可以使用管理控制台执行一次性清除过时记录，或计划定期自动清除。 有关清除过时记录的其他方法，请参见 [清除流程数据](/help/forms/using/admin-help/purging-process-data.md#purging-process-data).

**访问“作业清除调度程序”页**

1. 在Administration Console中，单击页面右上角的运行状况监视器。
1. 单击“作业清除调度程序”选项卡。

“作业清除计划程序信息”框中显示有关当前已调度清除的信息。

>[!NOTE]
>
>单击“停止计划程序”可停止未来计划的任何清除，但不会停止正在进行的清除作业。

**计划一次性清除**

1. 仅选择一次。
1. 在“清除完成的记录过滤器”区域中，指定天数（或周数），在此天数或周数之后，记录将被视为过时并可供清除。

   >[!NOTE]
   >
   >与尚未完成的进程相关的记录不会被清除，即使这些记录早于指定的期限。

1. 指定何时执行清除。 选中使用当前日期和时间复选框，或清除此复选框并单击日历和时钟图标以指定执行清除的日期和时间。

   >[!NOTE]
   >
   >如果指定的开始日期和时间是过去的时间，则在单击“启动调度程序”后，清除会立即发生。

1. 单击“Start Scheduler（启动计划程序）”。 任何以前计划的计划程序设置都将替换为新设置。

**配置自动清除计划**

1. 选择重复间隔，并指定两次清除间隔的天数或周数。
1. 在“清除完成的记录过滤器”区域中，指定天数（或周数），在此天数或周数之后，记录将被视为过时并可供清除。 不能将该值设置为 `0`.

   >[!NOTE]
   >
   >与尚未完成的进程相关的记录不会被清除，即使这些记录早于指定的期限。

1. 指定清除的开始时间。 选中使用当前日期和时间复选框，或清除此复选框并单击日历和时钟图标以指定执行清除的日期和时间。

   >[!NOTE]
   >
   >如果指定的开始日期和时间是过去的时间，AEM forms会根据指定的日期计算逻辑的下一个开始日期。 例如，如果您计划从4月7日开始每周执行作业清除，现在为4月9日，则第一次清除将在4月14日执行。

1. 单击“Start Scheduler（启动计划程序）”。 任何以前计划的计划程序设置都将替换为新设置。
