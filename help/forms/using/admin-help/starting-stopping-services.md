---
title: 启动和停止服务
seo-title: 启动和停止服务
description: 了解如何开始和停止与AEM Forms模块、应用程序服务器和数据库相关的服务。
seo-description: 了解如何开始和停止与AEM Forms模块、应用程序服务器和数据库相关的服务。
uuid: 8c831cb2-4165-4118-8a09-764cec4e5e05
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_services
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b93060bd-c6e1-40d2-8acd-ccafb8ed56da
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 0%

---


# 启动和停止服务{#starting-and-stopping-services}

AEM表单包含两种类型的服务：

* 控制AEM表单应用程序服务器和数据库的服务。
* 控制AEM表单模块的服务

## 开始或停止与AEM表单模块{#start-or-stop-the-services-associated-with-aem-forms-modules}关联的服务

AEM表单模块(例如，Forms、Rights Management、输出)作为服务运行。 有时，您可能需要停止或开始这些AEM表单模块的服务。 例如，在更改服务设置后，必须停止并重新启动AEM forms服务。

1. 在管理控制台中，单击&#x200B;**服务** > **应用程序和服务** > **服务管理**。
1. 在“服务管理”页面上，选中服务旁边的复选框以停止或开始，然后单击停止或开始。

## 开始或停止应用程序服务器和数据库{#start-or-stop-services-for-the-application-server-and-database}的服务

AEM表单的完整实施包括应用程序服务器和数据库服务：

* *`[application server]`* 适用于AEM表单
* *`[database]`* 适用于AEM表单

在Windows上，可通过&#x200B;**管理工具** > **服务面板**&#x200B;访问这些服务。 例如，如果您使用整套方法在JBoss上安装了AEM表单，则系统上提供以下服务：

* JBoss forAdobe Experience Manager表单
* MySQL forAdobe Experience Manager表单

开始或停止这些服务，方法是从“服务”面板的列表中选择这些服务，然后单击面板上的相应操作按钮。

在UNIX®或Linux上，从命令行输入以下文本，其中&#x200B;*`[service name]`*&#x200B;是要验证的服务的名称：

```java
     ps -A | grep [service name]
```

