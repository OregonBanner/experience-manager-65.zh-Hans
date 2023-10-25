---
title: 对配置属性的加密支持
seo-title: Encryption Support for Configuration Properties
description: 了解AEM中提供的对配置属性的加密支持。
seo-description: null
uuid: 26dc5e46-9332-4d9b-8874-895b90391e8c
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: security
discoiquuid: 4e08c297-aa4b-44cf-84c8-1e11582d9ebb
exl-id: 3c3db1c8-5b22-45dd-aeaf-5cf830a9486b
source-git-commit: e54c1d422f2bf676e8a7b0f50a101e495c869c96
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 0%

---

# 对配置属性的加密支持{#encryption-support-for-configuration-properties}

## 概述 {#overview}

此功能允许所有OSGi配置属性都以受保护的加密形式存储，而不是以明文形式存储。 Web控制台UI中的表单用于使用系统范围加密主密钥从明文创建加密文本。

添加了OSGi配置插件支持，以便在服务使用属性之前对其进行解密。

>[!NOTE]
>
>需要加密值的服务需要使用IsProtected检查，在尝试解密值之前查看值是否已加密，因为它可能已经解密。

## 启用加密支持 {#enabling-encryption-support}

这些步骤显示如何加密Mail服务的SMTP密码。 您可以为要加密的OSGI属性完成这些步骤。

1. 转到位于的AEM Web控制台 *https://&lt;serveraddress>：&lt;serverport>/system/console/configMgr*
1. 在左上角，转到 **主要 — 加密支持**

   ![chlimage_1-325](assets/chlimage_1-325.png)

1. 此 **Adobe Experience Manager Web控制台加密支持** 页面。

   ![screen_shot_2018-08-01at113417am](assets/screen_shot_2018-08-01at113417am.png)

1. 在 **纯文本** 字段，输入要保护的敏感数据的文本。
1. 选择 **Protect**. 受保护文本显示为加密文本。

   ![screen_shot_2018-08-01at113844am](assets/screen_shot_2018-08-01at113844am.png)

1. 从Step#5中复制受保护的文本并将其粘贴到OSGI表单值中。 在本例中，加密的 **SMTP密码** 已添加到 *Day CQ邮件服务*.

   ![screen_shot_2016-12-18at105809pm](assets/screen_shot_2016-12-18at105809pm.png)

1. 保存Day CQ Mail Service属性。 SMTP密码现在将作为加密值发送。

## 解密支持 {#decryption-support}

AEM现在提供了一个用于解密配置属性的配置插件。 此AEM插件将自动解密和检索明文属性。
