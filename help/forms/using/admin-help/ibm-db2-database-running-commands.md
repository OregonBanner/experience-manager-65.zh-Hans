---
title: '"IBM DB2数据库：运行命令以进行定期维护”'
seo-title: '"IBM DB2数据库：运行命令以进行定期维护”'
description: 本文档列出了为定期维护AEM Forms数据库而建议使用的IBM DB2命令。
seo-description: 本文档列出了为定期维护AEM Forms数据库而建议使用的IBM DB2命令。
uuid: 235d59df-b9b9-4770-8b7d-00713701c3c2
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a62b68b4-7735-49b1-8938-f0d9e4c4a051
exl-id: 7a4281e7-1544-473a-a471-e9a4c2819a58
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 0%

---

# IBM DB2数据库：运行用于定期维护的命令{#ibm-db-database-running-commands-for-regular-maintenance}

建议使用以下IBM DB2命令来定期维护AEM表单数据库。 有关DB2数据库的维护和性能优化的详细信息，请参阅&#x200B;*IBM DB2管理指南*。

* **运行状态：** 此命令更新描述数据库表的物理特征及其关联索引的统计信息。由AEM表单生成的动态SQL语句会自动使用这些更新的统计信息，但数据库内构建的静态SQL语句要求也运行`db2rbind`命令。
* **db2rbind:** 此命令重新绑定数据库中的所有包。运行`runstats`实用程序后，使用此命令重新验证数据库中的所有包。
* **重组表或索引：** 此命令检查是否需要对某些表和索引进行重组。

   随着数据库的增长和变化，重新计算表统计信息对于提高数据库性能至关重要，应定期执行。 这些命令可以通过使用脚本或通过使用cron作业手动运行。

>[!NOTE]
>
>在运行`runstats`命令之前，数据库必须包含数据，并且必须至少执行了一个目录同步。

对于小型数据库（如10,000个用户或2,500个组），只需调用`runstats`命令即可减少同步计时。

对于较大的数据库（如100,000个用户或10,000个组），在运行`runstats`命令之前先运行`reorg`命令。

## 在AEM forms数据库{#use-the-runstats-command-on-your-aem-forms-database}上使用runstats命令

对以下AEM表单数据库表和索引运行`runstats`命令。

>[!NOTE]
>
>`runstats`命令只需要在第一次数据库同步期间运行。 但是，在该过程中必须运行两次：在用户和群组同步期间，在群组成员同步期间，先执行一次。 确保脚本在您每次运行时都完全执行。

有关正确的语法和用法，请参阅数据库制造商的文档。 下面，使用`<schema>`表示与DB2用户名关联的架构。 如果安装了简单的缺省DB2，则此为数据库架构名称。

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

## 在AEM Forms数据库{#run-the-reorg-command-on-your-aem-forms-database}上运行reorg命令

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
