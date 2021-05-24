---
title: 为AEM应用程序配置
seo-title: 为AEM应用程序配置
description: 了解如何配置AEM应用程序。
seo-description: 了解如何配置AEM应用程序。
uuid: ab9acd93-da7f-4bb7-8d26-224044899068
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 34f24837-f5e2-41f0-a359-fdb695e1b8f2
exl-id: f7aa5ac0-3d03-4c04-b9c2-1bda427b0588
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 0%

---

# 为AEM应用程序配置{#configuring-for-aem-apps}

Adobe Experience Manager应用程序提供通过空中(OTA)更新应用程序内容的功能。 更新的内容存储在发布实例上。 要允许设备上的应用程序连接到发布实例并检查更新，需要将发布实例配置为允许空的反向链接标头。

## 配置空反向链接标头{#configuring-empty-referrer-header}

要配置反向链接过滤器服务，请执行以下操作：

* 在以下位置打开Apache Felix控制台(**Configurations**):
* https://&lt;server>:&lt;port_number>/system/console/configMgr
* 以管理员身份登录。
* 在&#x200B;**Configurations**&#x200B;菜单中，选择：*Apache Sling反向链接过滤器*
* 选中允许空字段，以允许空/缺少反向链接标头。
* 单击&#x200B;**Save**&#x200B;以保存更改。

![chlimage_1-58](assets/chlimage_1-58a.png)

有关更多详细信息，请参阅[OSGI配置设置](/help/sites-deploying/osgi-configuration-settings.md)和[安全检查表 — 跨站点请求伪造问题](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery)。
