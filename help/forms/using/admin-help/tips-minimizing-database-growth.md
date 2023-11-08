---
title: 最大程度地减少数据库增长的提示
seo-title: Tips for minimizing database growth
description: 长期进程将进程数据存储在AEM表单数据库中。 使用一些简单的流程设计和产品配置策略，可以最大限度地减少AEM表单数据库的增长。
seo-description: Long-lived processes store process data in the AEM forms database. The growth of the AEM forms database can be minimized using a few easy process design and product configuration strategies.
uuid: 13f99d4f-848e-451e-90d9-55e202dc0bdb
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 89441336-babc-4d1f-9053-d1566cd42d22
exl-id: f64efb06-815a-4608-ba1c-39e22f344ebb
source-git-commit: c4cd9a61a226ace2a72d60b5b7b7432de12cb873
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 0%

---

# 最大程度地减少数据库增长的提示 {#tips-for-minimizing-database-growth}

长期进程将进程数据存储在AEM表单数据库中。 使用一些简单的流程设计和产品配置策略，可以最大限度地减少AEM表单数据库的增长。

## 流程设计提示 {#process-design-tips}

尽可能使用短期进程。 短期进程不会将进程数据存储在数据库中。 使用短期进程的缺点是，它们的状态和状态不会在管理控制台中进行跟踪，并且没有进程的历史记录。

某些服务操作(如分配任务操作（用户服务）)要求在长生命周期进程中使用它们。 在这种情况下，您可以将流程划分为多个子流程，并在可能的情况下使其短暂可用。 如果使用此策略，则短期子进程应处理大型数据项，如文档值。

请谨慎使用变量。 使用长生命周期进程时，会为进程中的每个变量在数据库中分配空间。 战略性地使用变量可以节省大量空间。 例如，您可以在此过程中不再需要旧值时覆盖变量值。 并删除您已创建且未使用的任何变量。 您可以验证该流程以查找未使用的变量。

使用简单的变量类型（例如，字符串或int），并尽可能避免使用复杂的变量类型。 即使变量不包含值，也会为变量分配数据库空间。 复杂变量通常比简单变量需要更多的空间。

## 产品管理提示 {#product-administration-tips}

有效地使用全局文档存储(GDS)。 Forms服务器上的GDS目录用于存储（其中包括）传递到进程中AEM表单一部分的服务的文件。 为了提高性能，较小的文档存储在内存中并保留在数据库中。

管理控制台显示Default Document Max Inline Size属性，用于配置存储在内存中并保留在数据库中的文档的最大大小。 (请参阅 [配置常规AEM表单设置](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings).) 如果将此属性设置为低值，则大多数文档将保留在GDS目录而非数据库中。 优点在于，当文件存储在GDS目录中时，可以更轻松地删除不再需要的文件。
