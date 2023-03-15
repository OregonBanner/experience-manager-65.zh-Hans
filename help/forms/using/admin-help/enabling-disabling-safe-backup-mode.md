---
title: 启用和禁用安全备份模式
seo-title: Enabling and disabling safe backup mode
description: 在“备份设置”页上，您可以在安全备份模式下操作AEM表单，以便可靠地备份数据库和全局文档存储(GDS) (GDS)目录。 了解如何启用和禁用安全备份模式。
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

# 启用和禁用安全备份模式 {#enabling-and-disabling-safe-backup-mode}

在“备份设置”页上，您可以在安全备份模式下操作AEM表单，以便可靠地备份数据库和全局文档存储(GDS) (GDS)目录。

当AEM Forms处于安全备份模式时，它会正常运行，只是它不会主动从GDS目录中删除文件。

>[!NOTE]
>
>设置此选项不会备份您的系统；它可为您的系统准备备份。

## 启用安全备份模式 {#enable-safe-backup-mode}

1. 在管理控制台中，单击设置>核心系统设置>备份设置。
1. 在“备份设置”页上，选择“在安全备份模式下操作” ，然后单击“确定”。

>[!NOTE]
>
>如果系统已经在安全备份模式下运行，则单击“确定”时不会创建新的预留。

## 禁用安全备份模式 {#disable-safe-backup-mode}

1. 在管理控制台中，单击设置>核心系统设置>备份设置。
1. 在“备份设置”页上，取消选择“在安全备份模式下操作” ，然后单击“确定”。
