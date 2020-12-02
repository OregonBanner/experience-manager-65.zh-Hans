---
title: 单一登录和超时处理程序
seo-title: 单一登录和超时处理程序
description: 如何设置AEM Forms工作区的会话超时值。
seo-description: 如何设置AEM Forms工作区的会话超时值。
uuid: 17583fd5-6453-41d3-bb63-a639983fbea9
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 698990a2-dd3f-480f-9d15-d87563860297
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 0%

---


# 单一登录和超时处理程序{#single-sign-on-and-timeout-handlers}

AEM Forms工作区启用了SSO。 如果用户已登录AEM Forms应用程序(如Forms管理器或PDF Generator用户界面)并在同一浏览器会话中访问AEM Forms工作区，则该用户将登录AEM Forms工作区，反之亦然。

## 处理AEM Forms工作区{#handling-server-timeout-in-nbsp-aem-forms-workspace}中的服务器超时

可以在管理控制台中配置用户的会话超时。

要设置超时，请登录`https://'[server]:[port]'/adminui`，导航到&#x200B;**设置>用户管理>配置>配置高级系统属性**，然后设置所需的设置。

在AEM Forms工作区中，超时处理为：

* 用户的会话持续时间可用于响应初始化用户会话的`initialize`调用。
* 弹出对话框会通知用户会话即将过期，时间为会话到期前15秒。

在此弹出对话框中：

* 单击确定以结束用户会话。
* 单击“取消”重新初始化用户会话。

>[!NOTE]
>
>如果未采取任何操作，则会在会话到期前三秒内自动从AEM Forms工作区注销用户。
