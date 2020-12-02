---
title: 配置属性的加密支持
seo-title: 配置属性的加密支持
description: 'null'
seo-description: 'null'
uuid: 26dc5e46-9332-4d9b-8874-895b90391e8c
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: security
discoiquuid: 4e08c297-aa4b-44cf-84c8-1e11582d9ebb
translation-type: tm+mt
source-git-commit: 58fa0f05bae7ab5ba51491be3171b5c6ffbe870d
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 0%

---


# 配置属性的加密支持{#encryption-support-for-configuration-properties}

## 概述 {#overview}

此功能允许以受保护的加密形式存储所有OSGi配置属性，而不是明文。 Web控制台UI中的表单用于使用系统范围的加密主控密钥从明文创建加密文本。

添加了OSGi配置插件支持，以便在服务使用属性之前对其进行解密。

>[!NOTE]
>
>期望已加密值的服务需要使用IsProtected检查，以在尝试解密之前查看该值是否已加密，因为它可能已被解密。

## 启用加密支持{#enabling-encryption-support}

这些步骤说明如何为邮件服务加密SMTP密码。 您可以为要加密的OSGI属性完成这些步骤。

1. 转到位于&#x200B;*https://&lt;serveraddress>的AEM Web控制台：&lt;serverport>/system/console/configMgr*
1. 在左上角，转至&#x200B;**Main - Crypto Support**

   ![chlimage_1-325](assets/chlimage_1-325.png)

1. 将显示&#x200B;**Adobe Experience ManagerWeb控制台加密支持**&#x200B;页。

   ![screen_shot_2018-08-01at113417am](assets/screen_shot_2018-08-01at113417am.png)

1. 在&#x200B;**纯文本**&#x200B;字段中，输入要保护的敏感数据的文本。
1. 选择&#x200B;**Protect**。 “受保护”文本显示为加密文本。

   ![screen_shot_2018-08-01at113844am](assets/screen_shot_2018-08-01at113844am.png)

1. 从Step#5复制受保护文本并将其粘贴到OSGI表单值中。 在此示例中，加密的&#x200B;**SMTP密码**&#x200B;被添加到&#x200B;*Day CQ邮件服务*。

   ![screen_shot_2016-12-18at105809pm](assets/screen_shot_2016-12-18at105809pm.png)

1. 保存Day CQ邮件服务属性。 SMTP密码现在将作为加密值发送。

## 解密支持{#decryption-support}

AEM现在提供配置插件来解密配置属性。 此AEM插件将自动解密和检索明文属性。
