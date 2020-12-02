---
title: '"IBM DB2数据库：运行命令以进行定期维护”'
seo-title: '"IBM DB2数据库：运行命令以进行定期维护”'
description: 此文档列表IBM DB2命令，建议定期维护AEM表单数据库。
seo-description: 此文档列表IBM DB2命令，建议定期维护AEM表单数据库。
uuid: 235d59df-b9b9-4770-8b7d-00713701c3c2
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a62b68b4-7735-49b1-8938-f0d9e4c4a051
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 0%

---


# IBM DB2数据库：运行用于常规维护的命令{#ibm-db-database-running-commands-for-regular-maintenance}

建议使用以下IBM DB2命令定期维护AEM表单数据库。 有关DB2数据库的维护和性能调整的详细信息，请参见&#x200B;*IBM DB2管理指南*。

* **runstats:** 此命令更新描述数据库表的物理特性及其关联的索引的统计信息。AEM表单生成的动态SQL语句会自动使用这些更新的统计信息，但在数据库中构建的静态SQL语句也要求运行`db2rbind`命令。
* **db2rbind：此命** 令重新绑定数据库中的所有包。运行`runstats`实用程序后，使用此命令重新验证数据库中的所有包。
* **重组表或索引：** 此命令检查是否需要重组某些表和索引。

   随着数据库的增长和变化，重新计算表统计信息对于提高数据库性能至关重要，应定期进行。 这些命令可以通过使用脚本或使用cron作业手动运行。

>[!NOTE]
>
>运行`runstats`命令之前，数据库必须包含数据，并且至少已执行一个目录同步。

对于小型数据库（如10,000个用户或2,500个用户组），调用`runstats`命令可以减少同步定时。

对于较大的数据库，如对100,000个用户或10,000个用户组，在运行`runstats`命令之前运行`reorg`命令。

## 在AEM forms数据库{#use-the-runstats-command-on-your-aem-forms-database}上使用runstats命令

对以下AEM表单数据库表和索引运行`runstats`命令。

>[!NOTE]
>
>`runstats`命令只需在第一个数据库同步期间运行。 但是，在该过程中必须运行两次：在用户和用户组同步期间和在用户组成员同步期间。 确保每次运行脚本时脚本都完全执行。

有关正确的语法和用法，请参阅数据库制造商的文档。 下面，`<schema>`用于表示与DB2用户名关联的模式。 如果安装了简单的默认DB2，则这是数据库模式名。

```sql
     TABLE <schema>.EDCPRINCIPALGROUPENTITY
 
     TABLE <schema>.EDCPRINCIPALGRPCTMNTENTITY
 
     TABLE <schema>.EDCPRINCIPALENTITY
 
     TABLE <schema>.EDCPRINCIPALUSERENTITY
 
     TABLE <schema>.EDCPRINCIPALEMAILALIASENTITY
 
     TABLE <schema>.EDCPRINCIPALENTITY FOR INDEXES ALL
 
     TABLE <schema>.EDCPRINCIPALEMAILALIASENTITY FOR INDEXES ALL
 
     TABLE <schema>.EDCPRINCIPALUSERENTITY FOR INDEXES ALL
 
     TABLE <schema>.EDCPRINCIPALGROUPENTITY FOR INDEXES ALL
 
     TABLE <schema>.EDCPRINCIPALGRPCTMNTENTITY FOR INDEXES ALL
```

## 在AEM表单数据库{#run-the-reorg-command-on-your-aem-forms-database}上运行reorg命令

对以下AEM表单数据库表和索引运行`reorg`命令。 有关正确的语法和用法，请参阅数据库制造商的文档。

```sql
     TABLE <schema>.EDCPRINCIPALGROUPENTITY
 
     TABLE <schema>.EDCPRINCIPALGRPCTMNTENTITY
 
     TABLE <schema>.EDCPRINCIPALENTITY
 
     TABLE <schema>.EDCPRINCIPALUSERENTITY
 
     TABLE <schema>.EDCPRINCIPALEMAILALIASENTITY
 
     INDEXES ALL FOR TABLE <schema>.EDCPRINCIPALENTITY
 
     INDEXES ALL FOR TABLE <schema>.EDCPRINCIPALEMAILALIASENTITY
 
     INDEXES ALL FOR TABLE <schema>.EDCPRINCIPALUSERENTITY
 
     INDEXES ALL FOR TABLE <schema>.EDCPRINCIPALGROUPENTITY
 
     INDEXES ALL FOR TABLE <schema>.EDCPRINCIPALGRPCTMNTENTITY
```

