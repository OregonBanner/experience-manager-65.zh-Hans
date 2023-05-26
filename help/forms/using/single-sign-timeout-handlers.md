---
title: 单点登录和超时处理程序
seo-title: Single Sign On and timeout handlers
description: 如何设置AEM Forms工作区的会话超时值。
seo-description: How-to set the session timeout value for AEM Forms workspace.
uuid: 17583fd5-6453-41d3-bb63-a639983fbea9
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 698990a2-dd3f-480f-9d15-d87563860297
exl-id: 4f824d80-f3f8-4010-9583-5a9ab1151a7b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---

# 单点登录和超时处理程序 {#single-sign-on-and-timeout-handlers}

AEM Forms工作区已启用SSO。 如果用户已登录到AEM Forms应用程序(如Forms管理器或PDF生成器用户界面)并在同一浏览器会话中访问AEM Forms工作区，则用户将登录到AEM Forms工作区，反之亦然。

## 在AEM Forms工作区中处理服务器超时 {#handling-server-timeout-in-nbsp-aem-forms-workspace}

可以在管理控制台中配置用户的会话超时。

要设置超时，请登录 `https://'[server]:[port]'/adminui`，导航到 **设置>用户管理>配置>配置高级系统属性**，然后进行所需的设置。

在AEM Forms中，工作区超时可按如下方式处理：

* 用户的会话持续时间可用于响应 `initialize` 调用初始化用户会话。
* 弹出对话框通知用户会话即将过期，此时距离会话过期还有15秒。

在此弹出对话框中：

* 单击确定结束用户会话。
* 单击“取消”重新初始化用户会话。

>[!NOTE]
>
>如果未执行任何操作，则会在会话到期前三秒自动将用户从AEM Forms工作区注销。
