---
title: “IBM DB2数据库：运行命令以进行常规维护”
description: 本文档列出了为定期维护AEM表单数据库而推荐的IBM DB2命令。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 7a4281e7-1544-473a-a471-e9a4c2819a58
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 0%

---

# IBM DB2数据库：运行命令以进行常规维护 {#ibm-db-database-running-commands-for-regular-maintenance}

建议使用以下IBM DB2命令来定期维护AEM表单数据库。 有关DB2数据库的维护和性能调优的详细信息，请参见 *IBM DB2 Administration指南*.

* **运行数据：** 此命令更新描述数据库表物理特性的统计信息及其关联的索引。 由AEM表单生成的动态SQL语句自动使用这些更新的统计信息，但构建在数据库中的静态SQL语句需要 `db2rbind` 命令也可以运行。
* **db2rbind：** 此命令重新绑定数据库中的所有包。 运行 `runstats` 用于重新验证数据库中所有包的实用程序。
* **重组表或索引：** 此命令检查是否需要对某些表和索引进行重组。

  随着数据库的增长和变化，重新计算表统计信息对于提高数据库性能至关重要，应定期进行。 这些命令可以使用脚本手动运行，也可以使用cron作业手动运行。

>[!NOTE]
>
>运行之前 `runstats` 命令，数据库必须包含数据，并且必须至少执行了一个目录同步。

对于小型数据库（如10,000个用户或2,500个组），调用 `runstats` 命令来缩短同步时间。

对于较大的数据库（如100,000个用户或10,000个组），请运行 `reorg` 命令 `runstats` 命令。

## 在AEM表单数据库上使用runstats命令 {#use-the-runstats-command-on-your-aem-forms-database}

运行 `runstats` 命令对以下AEM forms数据库表和索引执行。

>[!NOTE]
>
>此 `runstats` 命令只需要在第一次数据库同步期间运行。 但是，该进程必须运行两次：一次是在用户和组同步期间，另一次是在组成员同步期间。 确保每次运行脚本时脚本都会完全执行。

有关正确的语法和用法，请参阅数据库制造商的文档。 下， `<schema>` 用于表示与您的DB2用户名关联的架构。 如果您有一个简单的默认DB2安装，则这是数据库架构名称。

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

## 在AEM forms数据库上运行reorg命令 {#run-the-reorg-command-on-your-aem-forms-database}

运行 `reorg` 命令对以下AEM forms数据库表和索引执行。 有关正确的语法和用法，请参阅数据库制造商的文档。

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
