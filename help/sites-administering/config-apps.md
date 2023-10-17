---
title: 为AEM应用程序配置
description: 了解如何使用Adobe Experience Manager应用程序更新应用程序OTA（空中）的内容。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
exl-id: f7aa5ac0-3d03-4c04-b9c2-1bda427b0588
source-git-commit: 06a6d4e0ba2aeaefcfb238233dd98e8bbd6731da
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 0%

---

# 为AEM应用程序配置{#configuring-for-aem-apps}

Adobe Experience Manager应用程序允许您更新应用程序OTA的内容（空中）。 更新的内容存储在发布实例上。 要允许设备上的应用程序连接到发布实例并检查更新，必须将发布实例配置为允许空的反向链接标头。

## 配置空反向链接标头 {#configuring-empty-referrer-header}

配置反向链接筛选服务：

* 打开Apache Felix控制台(**配置**)位于：
* https://&lt;server>：&lt;port_number>/system/console/configMgr
* 以管理员身份登录。
* 在 **配置** 菜单，选择： *Apache Sling引用过滤器*
* 选中允许空字段，以便您可以允许为空/缺少反向链接标头。
* 单击 **保存** 以保存更改。

![chlimage_1-58](assets/chlimage_1-58a.png)

请参阅 [OSGI配置设置](/help/sites-deploying/osgi-configuration-settings.md) 和 [安全核对清单 — 跨站点请求伪造问题](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery) 以了解更多详细信息。
