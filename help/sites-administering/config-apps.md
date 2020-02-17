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
translation-type: tm+mt
source-git-commit: 684d2d5f73d571a15c8155e7870134c28dc892b7

---


# 为AEM应用程序配置{#configuring-for-aem-apps}

Adobe Experience Manager应用程序提供通过无线(OTA)更新应用程序内容的功能。 更新的内容存储在发布实例上。 要允许设备上的应用程序连接到发布实例并检查更新，需要将发布实例配置为允许空的引用标题。

## 配置空引用标题 {#configuring-empty-referrer-header}

要配置引用过滤器服务，请执行以下操作：

* 打开Apache Felix控制台(**配置**):
* https://&lt;server>:&lt;port_number>/system/console/configMgr
* 以管理员身份登录。
* 在“配 **置** ”菜单中，选择：Apache Sling *Referrer过滤器*
* 选中“允许为空”字段，以允许空／缺少引用标题。
* 单击 **保存** ，以保存更改。

![chlimage_1-58](assets/chlimage_1-58a.png)

有关更多 [详细信息，请参阅OSGI配置设置](/help/sites-deploying/osgi-configuration-settings.md)[和安全核对清单——跨站点请求伪造问题](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery) 。
