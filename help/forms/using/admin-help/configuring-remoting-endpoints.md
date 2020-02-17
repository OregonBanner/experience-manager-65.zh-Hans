---
title: 配置远程处理端点
seo-title: 配置远程处理端点
description: 了解如何配置远程处理端点。
seo-description: 了解如何配置远程处理端点。
uuid: 4d4f9274-dcae-4b9f-975a-575376c2f89c
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: aab9d622-d76b-4100-9ca6-e5b86f543381
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 配置远程处理端点 {#configuring-remoting-endpoints}

远程处理端点使用Flex构建的应用程序能够使用（AEM表单已弃用）AEM表单远程处理调用服务。 将为每个已激活的服务自动创建远程处理端点。 创建的Flex目标与端点同名，Flex客户端可以创建指向该目标的远程对象以调用相关服务上的操作。

## 远程处理端点设置 {#remoting-endpoint-settings}

**** Flex客户端身份验证方法：确定当被调用的服务启用安全性、被调用的操作不支持匿名调用且客户端传入无或无效凭据时，服务器向客户端发送的响应类型。
