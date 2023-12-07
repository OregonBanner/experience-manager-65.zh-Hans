---
title: “DB2数据库：每周运行一个进程”
description: 了解如何提高AEM Forms DB2数据库的性能。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: ca2cfe35-b602-4ef8-b4e3-af846105d4de
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 0%

---

# DB2数据库：每周运行一个进程{#db-database-running-a-process-weekly}

如果AEM表单DB2数据库开始运行缓慢，则每周运行以下进程可以提高其性能：

1. 启动DB2控制中心：

   (Windows)选择“开始”>“程序”>“IBM DB2”>“常规管理工具”>“控制中心”。

   （Linux和UNIX）在命令提示符下，键入 `db2jcc` 命令。

1. 在DB2 Control Center对象树中，单击所有数据库。
1. 单击为AEM表单创建的数据库，然后单击“表”文件夹。
1. 在内容窗格中选择所有数据库表，右键单击它们，然后选择运行统计信息。
1. 转到“统计信息”>“索引统计信息”。
1. 选择收集所有索引的统计信息，选择收集具有扩展详细统计信息的索引的统计信息，然后单击确定。

进程完成后，将显示一条消息。 关闭消息。
