---
title: 清除流程数据
seo-title: 清除流程数据
description: 当调用长期进程时生成的进程数据可能过大，导致AEM表单性能降低，并且会使用不必要的磁盘空间。 了解如何清除流程数据。
seo-description: 当调用长期进程时生成的进程数据可能过大，导致AEM表单性能降低，并且会使用不必要的磁盘空间。 了解如何清除流程数据。
uuid: 2f04452c-71c6-452c-88c2-7560d35e7dec
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 3157bb92-4b07-40f2-be4c-8f5807f9a380
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 清除流程数据 {#purging-process-data}

当调用长期进程时生成的进程数据可能过大，导致AEM表单性能降低，并且会使用不必要的磁盘空间。 最好在不再需要记录时清除流程数据。 AEM表单提供了几种清除流程数据的方法：

* 您可以使用管理控制台执行与长期进程相关的过时记录一次性清除，或计划定期自动清除。 (请参 [阅从作业管理器数据库清除记录](/help/forms/using/admin-help/purge-records-job-manager-database.md#purge-records-from-the-job-manager-database)。)
* 您可以使用AEM表单Java API和Web服务API以编程方式清除与长期进程相关的进程数据。 (请参阅使用AEM表单进行编程 [中的“清除流程数据](https://www.adobe.com/go/learn_aemforms_programming_63)”。)
* 使用流程清除工具根据流程名称和其他参数清除流程。 有关详细信息，请参阅进程清除工具自述文件，该文件位于 *[aem_forms根目录]*\sdk\misc\Foundation\ProcessPurgeTool\ReadMe.txt中。

