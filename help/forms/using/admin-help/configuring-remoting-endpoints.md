---
title: 配置远程端点
seo-title: Configuring Remoting endpoints
description: 了解如何配置远程端点。
seo-description: Learn how to configure remoting endpoints.
uuid: 4d4f9274-dcae-4b9f-975a-575376c2f89c
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: aab9d622-d76b-4100-9ca6-e5b86f543381
exl-id: 891d7d75-555a-46c6-a8a0-d5238b48bc79
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 0%

---

# 配置远程端点 {#configuring-remoting-endpoints}

利用远程端点，使用Flex构建的应用程序可以使用(对于AEM表单已弃用) AEM Forms Remoting调用服务。 将为每个激活的服务自动创建远程端点。 将创建与端点同名的Flex目标，并且Flex客户端可以创建指向此目标的远程对象，以调用对相关服务的操作。

## 远程端点设置 {#remoting-endpoint-settings}

**Flex客户端身份验证方法：** 确定在调用的服务启用了安全性、调用的操作不支持匿名调用、客户端未传递凭据或凭据无效时，服务器发送回客户端的响应类型。
