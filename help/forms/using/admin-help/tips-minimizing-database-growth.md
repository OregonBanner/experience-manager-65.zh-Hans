---
title: 最小化数据库增长的提示
seo-title: 最小化数据库增长的提示
description: 长期的进程将进程数据存储在AEM表单数据库中。 使用一些简单的流程设计和产品配置策略，可以将AEM表单数据库的增长降至最低。
seo-description: 长期的进程将进程数据存储在AEM表单数据库中。 使用一些简单的流程设计和产品配置策略，可以将AEM表单数据库的增长降至最低。
uuid: 13f99d4f-848e-451e-90d9-55e202dc0bdb
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 89441336-babc-4d1f-9053-d1566cd42d22
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 最小化数据库增长的提示 {#tips-for-minimizing-database-growth}

长期的进程将进程数据存储在AEM表单数据库中。 使用一些简单的流程设计和产品配置策略，可以将AEM表单数据库的增长降至最低。

## 流程设计提示 {#process-design-tips}

尽可能使用短时间流程。 短时间进程不会在数据库中存储进程数据。 使用短时间进程的缺点是它们的状态和状态在管理控制台中不跟踪，并且该进程没有历史记录。

某些服务操作(如“分配任务”操作（用户服务）)要求它们用于长寿命进程。 在这种情况下，您可以将流程细分为多个子流程，并尽可能缩短它们的使用时间。 如果您使用此策略，则短期子进程应处理大数据项，如文档值。

少用变量。 在使用长寿命进程时，对于每个进程实例，在数据库中为进程中的每个变量分配空间。 战略性地使用变量可节省大量空间。 例如，当流程中不再需要旧值时，可以覆盖变量值。 并删除您已创建且未使用的任何变量。 您可以验证该过程以查找未使用的变量。

使用简单的变量类型（例如，字符串或int），并尽可能避免使用复杂的变量类型。 即使变量不包含值，也会为变量分配数据库空间。 复杂变量通常需要比简单变量更多的空间。

## 产品管理提示 {#product-administration-tips}

有效地使用全局文档存储(GDS)。 表单服务器上的GDS目录用于存储传递给作为AEM表单一部分的服务的文件，等等。 为了提高性能，较小的文档会存储在内存中并保留在数据库中。

管理控制台显示“默认文档最大内联大小”属性，用于配置存储在内存中并保留在数据库中的文档的最大大小。 (请参阅 [配置常规AEM表单设置](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings)。)如果将此属性设置为低值，则大多数文档将保留在GDS目录中，而不是数据库中。 优点是，当文件存储在GDS目录中时，不再需要时，您可以更轻松地删除它们。
