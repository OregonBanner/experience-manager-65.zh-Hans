---
title: 啟用和停用安全備份模式
seo-title: Enabling and disabling safe backup mode
description: 您可以在「備份設定值」頁面以安全的備份模式操作AEM表單，以便可靠地備份資料庫和全域檔案儲存(GDS) (GDS)目錄。 瞭解如何啟用和停用安全備份模式。
seo-description: On the Backup Settings page, you can operate AEM forms in safe backup mode so that you can reliably back up your database and Global Document Storage (GDS) (GDS) directory. Learn how to enable and disable safe backup mode.
uuid: 2fdeaeaf-e969-40a4-8aee-1f2b627d3942
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9fda71e4-78a1-4581-9d02-bf06a75c3bcb
exl-id: f0ab712f-ecd9-4be8-a7a5-fd1a7a8c9a0b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---

# 啟用和停用安全備份模式 {#enabling-and-disabling-safe-backup-mode}

您可以在「備份設定值」頁面以安全的備份模式操作AEM表單，以便可靠地備份資料庫和全域檔案儲存(GDS) (GDS)目錄。

當AEM Forms處於安全備份模式時，它會正常運作，但不會主動從GDS目錄移除檔案。

>[!NOTE]
>
>設定這個選項並不會備份您的系統，而是讓您的系統準備進行備份。

## 啟用安全備份模式 {#enable-safe-backup-mode}

1. 在管理控制檯中，按一下「設定>核心系統設定>備份設定」。
1. 在「備份設定值」頁面上，選取「在安全備份模式下作業」，然後按一下「確定」。

>[!NOTE]
>
>如果系統已經在安全備份模式下執行，則按一下「確定」時將不會建立新的預訂。

## 停用安全備份模式 {#disable-safe-backup-mode}

1. 在管理控制檯中，按一下「設定>核心系統設定>備份設定」。
1. 在「備份設定值」頁面上，取消選取「在安全備份模式下作業」，然後按一下「確定」。
