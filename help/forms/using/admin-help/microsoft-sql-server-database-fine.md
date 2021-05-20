---
title: '"Microsoft SQL Server数据库：微调配置”'
seo-title: '"Microsoft SQL Server数据库：微调配置”'
description: 了解如何优化Microsoft SQL Server数据库的配置。
seo-description: 了解如何优化Microsoft SQL Server数据库的配置。
uuid: 2d618aab-3c67-4edb-a28f-a20904689e6f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS, SG_AEMFORMS
discoiquuid: 70559a94-42ea-411a-a32f-5f38bc17ff96
exl-id: 9c570827-86e2-47d5-b8ae-66c0767bff2e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 0%

---

# Microsoft SQL Server数据库：微调配置{#microsoft-sql-server-database-fine-tuning-the-configuration}

使用Microsoft SQL Server时，应更改默认配置设置。 在Oracle企业管理器中右键单击本地服务器以访问属性对话框。

## 内存设置{#memory-settings}

将最小内存分配更改为尽可能大的数字。 如果数据库在单独的计算机上运行，请使用所有内存。 默认设置不会主动分配内存，这会妨碍几乎任何数据库的性能。 在生产机器上分配内存时，您应该最积极。

## 处理器设置{#processor-settings}

修改处理器设置，最重要的是，选中Boost SQL Server Priority On Windows复选框，以使服务器使用尽可能多的周期。 “Use NT Fibres（使用NT纤维）”设置不那么重要，但您可能也希望选择它。

## 数据库设置{#database-settings}

更改数据库设置。 最重要的设置是“恢复间隔”，它指定在崩溃后等待恢复的最长时间。 默认设置为1分钟。 使用5到15分钟的较大值可提高性能，因为它为服务器提供了更多时间将更改从数据库日志写回数据库文件。

>[!NOTE]
>
>此设置不会损害事务行为，因为它只更改启动时必须完成的日志文件重播的长度。

将日志和数据文件的空间分配大小设置为比初始数据库大得多。 考虑一年内数据库的增长量。 理想情况下，日志和数据文件会以连续的范围进行分配，这样数据就不会在整个磁盘上碎片化。
