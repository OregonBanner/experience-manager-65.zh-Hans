---
title: “IBM DB2数据库：运行命令以进行定期维护”
seo-title: “IBM DB2数据库：运行命令以进行定期维护”
description: 本文档列出了IBM DB2命令，建议这些命令用于定期维护AEM表单数据库。
seo-description: 本文档列出了IBM DB2命令，建议这些命令用于定期维护AEM表单数据库。
uuid: 235d59df-b9b9-4770-8b7d-00713701c3c2
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a62b68b4-7735-49b1-8938-f0d9e4c4a051
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# IBM DB2数据库：运行命令以进行定期维护 {#ibm-db-database-running-commands-for-regular-maintenance}

建议使用以下IBM DB2命令定期维护AEM表单数据库。 有关DB2数据库的维护和性能调整的详细信息，请参 *阅IBM DB2管理指南*。

* **** runstats:此命令更新描述数据库表的物理特性及其关联的索引的统计信息。 由AEM表单生成的动态SQL语句会自动使用这些更新的统计信息，但在数据库内构建的静态SQL语句也要 `db2rbind` 求运行该命令。
* **** db2rbind:此命令重新绑定数据库中的所有包。 运行该实用程序后，请使 `runstats` 用此命令重新验证数据库中的所有包。
* **** 重组表或索引：此命令检查是否需要对某些表和索引进行重组。

   随着数据库的增长和变化，重新计算表统计信息对于提高数据库性能至关重要，应定期进行。 这些命令可以通过使用脚本或使用cron作业手动运行。

>[!NOTE]
>
>运行命令之 `runstats` 前，数据库必须包含数据，并且必须至少执行了一个目录同步。

对于小型数据库（例如，对于10,000个用户或2,500个用户组），调用该命令可以减 `runstats` 少同步定时。

对于较大的数据库（如100,000个用户或10,000个用户组），在运行命令 `reorg` 之前运行该命 `runstats` 令。

## 在AEM表单数据库上使用runstats命令 {#use-the-runstats-command-on-your-aem-forms-database}

对以下 `runstats` AEM表单数据库表和索引运行该命令。

>[!NOTE]
>
>该命 `runstats` 令只需在第一个数据库同步期间运行。 但是，在该过程中必须运行两次：在用户和用户组的同步期间和用户组成员的同步期间，先进行一次。 确保脚本在每次运行时都完全执行。

有关正确的语法和用法，请参阅数据库制造商的文档。 下面， `<schema>` 用于表示与您的DB2用户名关联的架构。 如果安装了简单的默认DB2，则这是数据库架构名称。

```as3
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

## 在AEM表单数据库上运行reorg命令 {#run-the-reorg-command-on-your-aem-forms-database}

对以下 `reorg` AEM表单数据库表和索引运行该命令。 有关正确的语法和用法，请参阅数据库制造商的文档。

```as3
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

