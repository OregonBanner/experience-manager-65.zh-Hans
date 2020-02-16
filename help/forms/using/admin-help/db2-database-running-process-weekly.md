---
title: '"DB2数据库：每周运行进程”'
seo-title: '"DB2数据库：每周运行进程”'
description: 了解如何提高AEM表单DB2数据库的性能。
seo-description: 了解如何提高AEM表单DB2数据库的性能。
uuid: 36070087-c250-41df-a841-aa922e777697
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: fc0e8183-5d50-4fc0-997a-5f3168ba0d70
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# DB2数据库：每周运行进程{#db-database-running-a-process-weekly}

如果您的AEM表单DB2数据库开始运行缓慢，则每周运行以下进程可以提高其性能：

1. 启动DB2控制中心：

   (Windows)选择“开始”>“程序”>“IBM DB2”>“常规管理工具”>“控制中心”。

   （Linux和UNIX）在命令提示符下，键入命 `db2jcc` 令。

1. 在DB2 Control center对象树中，单击“所有数据库”。
1. 单击您为AEM表单创建的数据库，然后单击表文件夹。
1. 在内容窗格中选择所有数据库表，右键单击它们，然后选择运行统计信息。
1. 转到“统计信息”>“索引统计信息”。
1. 选择“收集所有索引的统计信息”，选择“收集包含扩展详细统计信息的索引的统计信息”，然后单击“确定”。

完成该过程后，将显示一条消息。 关闭消息。
