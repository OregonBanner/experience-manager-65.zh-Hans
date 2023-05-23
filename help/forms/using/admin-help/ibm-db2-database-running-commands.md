---
title: 「IBM DB2資料庫：執行命令以進行定期維護」
seo-title: "IBM DB2 database: Running commands for regular maintenance"
description: 本檔案列出AEM表單資料庫定期維護所建議的IBM DB2命令。
seo-description: This document lists IBM DB2 commands that are recommended for regular maintenance of your AEM forms database.
uuid: 235d59df-b9b9-4770-8b7d-00713701c3c2
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a62b68b4-7735-49b1-8938-f0d9e4c4a051
exl-id: 7a4281e7-1544-473a-a471-e9a4c2819a58
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 0%

---

# IBM DB2資料庫：執行命令以進行定期維護 {#ibm-db-database-running-commands-for-regular-maintenance}

建議您使用下列IBM DB2命令來定期維護AEM表單資料庫。 如需有關DB2資料庫維護與效能調整的詳細資訊，請參閱 *IBM DB2 Administration指南*.

* **runstats：** 這個命令會更新描述資料庫表格實體特性的統計資料，以及其關聯的索引。 AEM表單產生的動態SQL敘述句會自動使用這些更新的統計資料，但建置在資料庫中的靜態SQL敘述句需要 `db2rbind` 命令也可以執行。
* **db2rbind：** 這個命令會重新繫結資料庫中的所有套裝程式。 執行後，請使用此命令 `runstats` 用來重新驗證資料庫中所有套件的公用程式。
* **重組資料表或索引：** 此命令會檢查是否需要重新整理某些表格和索引。

   隨著資料庫的成長與變更，重新計算表格統計資料對於改善資料庫效能至關重要，應定期進行。 這些命令可以使用指令碼手動執行，也可以使用cron作業手動執行。

>[!NOTE]
>
>在您執行 `runstats` 命令，資料庫必須包含資料，而且至少必須已執行一個目錄同步處理。

若是小型資料庫（例如10,000位使用者或2,500個群組），只要叫用 `runstats` 減少同步時間計時的指令。

若是大型資料庫（例如100,000位使用者或10,000個群組），請執行 `reorg` 命令。 `runstats` 命令。

## 在您的AEM表單資料庫上使用runstats命令 {#use-the-runstats-command-on-your-aem-forms-database}

執行 `runstats` 命令來建立下列AEM forms資料庫表格和索引。

>[!NOTE]
>
>此 `runstats` 命令只需要在第一次資料庫同步處理期間執行。 不過，該程式必須執行兩次：一次是在使用者與群組同步化期間，另一次是在群組成員同步化期間。 請確定每次執行指令碼時，該指令碼都會完全執行。

如需正確語法和用法，請參閱資料庫製造商的檔案。 下， `<schema>` 用於表示與您的DB2使用者名稱相關聯的結構描述。 如果您有簡單的預設DB2安裝，這就是資料庫架構名稱。

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

## 在您的AEM表單資料庫上執行reorg命令 {#run-the-reorg-command-on-your-aem-forms-database}

執行 `reorg` 命令來建立下列AEM forms資料庫表格和索引。 如需正確語法和用法，請參閱資料庫製造商的檔案。

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
