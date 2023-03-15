---
title: PDF生成器备份限制
seo-title: PDF Generator backup limitations
description: 了解PDF生成器备份限制。
seo-description: Learn about PDF Generator backup limitations.
uuid: 9537ffde-4396-46d1-81ea-edcd25923ffb
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 23386353-b2bf-49f1-947a-dd7587bba175
noindex: true
exl-id: a23db58d-1236-4689-93fc-dea508f8eb81
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '55'
ht-degree: 0%

---

# PDF生成器备份限制 {#pdf-generator-backup-limitations}

无法备份PDF生成器用于转换文件的临时目录。 即使可以正确恢复服务，数据也会丢失，因为PDF生成器会按设定的时间间隔查看和清除临时目录的内容。
