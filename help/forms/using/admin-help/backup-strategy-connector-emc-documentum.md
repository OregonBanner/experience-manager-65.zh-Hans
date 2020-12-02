---
title: 针对EMC Documentum用户的Connector备份战略
seo-title: 针对EMC Documentum用户的Connector备份战略
description: 检查如何为EMC Documentum用户创建Connector备份战略。
seo-description: 检查如何为EMC Documentum用户创建Connector备份战略。
uuid: 5d8a0476-5231-4e1d-96c4-ae3df68e09f0
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e83b1a59-a730-4d22-9d58-1c9c38e5d534
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 0%

---


# EMC Documentum用户的Connector备份战略{#backup-strategy-for-connector-for-emc-documentum-users}

如果您安装了Connector for EMC Documentum，除了本章中的说明之外，您的备份和恢复战略还必须包括备份（或恢复）相应ECM系统所安装的计算机。 （请参阅ECM Documentum文档）。

通过使用ECM存储库并执行以下环境备份AEM表单任务:

* 按照本文档所述的说明备份AEM表单。
* 按照[备份EMC Documentum Content Server](/help/forms/using/admin-help/backing-recovering-emc-documentum-repository.md#back-up-the-emc-documentum-content-server)中的说明备份您的ECM Documentum系统。

使用ECM存储库并执行以下环境来恢复AEM表单任务:

* 按照[恢复EMC Documentum Content Server](/help/forms/using/admin-help/backing-recovering-emc-documentum-repository.md#restore-the-emc-documentum-content-server)中的说明恢复您各自的ECM系统。
* 按照本文档所述的说明恢复AEM表单。

