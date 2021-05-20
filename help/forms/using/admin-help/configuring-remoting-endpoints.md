---
title: 配置远程处理端点
seo-title: 配置远程处理端点
description: 了解如何配置远程端点。
seo-description: 了解如何配置远程端点。
uuid: 4d4f9274-dcae-4b9f-975a-575376c2f89c
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: aab9d622-d76b-4100-9ca6-e5b86f543381
exl-id: 891d7d75-555a-46c6-a8a0-d5238b48bc79
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 0%

---

# 配置远程处理端点{#configuring-remoting-endpoints}

远程处理端点允许使用Flex构建的应用程序使用(AEM forms已弃用)AEM forms远程处理来调用服务。 将自动为每个已激活的服务创建远程处理端点。 创建与端点同名的Flex目标，Flex客户端可以创建指向此目标的远程对象以调用相关服务上的操作。

## 远程端点设置{#remoting-endpoint-settings}

**Flex客户端身份验证方法：** 确定在启用了安全性、调用的操作不支持匿名调用且客户端传递了无或无效凭据时，服务器向客户端发回的响应类型。
