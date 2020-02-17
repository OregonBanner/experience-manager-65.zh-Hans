---
title: '"Microsoft SQL server数据库：微调配置”'
seo-title: '"Microsoft SQL server数据库：微调配置”'
description: 了解如何微调Microsoft SQL server数据库的配置。
seo-description: 了解如何微调Microsoft SQL server数据库的配置。
uuid: 2d618aab-3c67-4edb-a28f-a20904689e6f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 70559a94-42ea-411a-a32f-5f38bc17ff96
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Microsoft SQL server数据库：微调配置 {#microsoft-sql-server-database-fine-tuning-the-configuration}

使用Microsoft SQL server时，应更改默认配置设置。 在Oracle Enterprise manager中右键单击本地服务器以访问属性对话框。

## 内存设置 {#memory-settings}

将最小内存分配更改为尽可能大的数字。 如果数据库在另一台计算机上运行，请使用所有内存。 默认设置不会大幅分配内存，这会妨碍几乎任何数据库的性能。 在生产机器上分配内存时，您应该最积极。

## 处理器设置 {#processor-settings}

修改处理器设置，最重要的是，选中“Boost SQL Server Priority On Windows”复选框，以使服务器使用尽可能多的循环。 “使用NT纤维”设置不那么重要，但您可能也希望选择它。

## 数据库设置 {#database-settings}

更改数据库设置。 最重要的设置是恢复间隔，它指定在崩溃后等待恢复的最大时间。 默认设置为1分钟。 使用5到15分钟的较大值可提高性能，因为它使服务器有更多时间将数据库日志中的更改写入数据库文件。

>[!NOTE]
>
>此设置不会危害事务行为，因为它只更改启动时必须完成的日志文件重播的长度。

将日志和数据文件的“已分配空间”大小设置为比初始数据库大得多。 考虑一年内数据库可以增长多少。 理想情况下，日志和数据文件以连续的范围分配，这样数据不会在整个磁盘上被碎片化。
