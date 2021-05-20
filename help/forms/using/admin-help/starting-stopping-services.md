---
title: 启动和停止服务
seo-title: 启动和停止服务
description: 了解如何启动和停止与AEM Forms模块以及应用程序服务器和数据库相关的服务。
seo-description: 了解如何启动和停止与AEM Forms模块以及应用程序服务器和数据库相关的服务。
uuid: 8c831cb2-4165-4118-8a09-764cec4e5e05
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_services
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b93060bd-c6e1-40d2-8acd-ccafb8ed56da
exl-id: 55bf5196-22c6-4286-8c92-ff44d81dde49
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 0%

---

# 启动和停止服务{#starting-and-stopping-services}

AEM表单包含两种类型的服务：

* 控制AEM Forms应用程序服务器和数据库的服务。
* 控制AEM表单模块的服务

## 启动或停止与AEM表单模块关联的服务{#start-or-stop-the-services-associated-with-aem-forms-modules}

AEM表单模块(例如，Forms、Rights Management、输出)作为服务运行。 有时，您可能需要停止或启动这些AEM表单模块的服务。 例如，在更改服务的设置后，必须停止并重新启动AEM表单服务。

1. 在管理控制台中，单击&#x200B;**服务** > **应用程序和服务** > **服务管理**。
1. 在“服务管理”页面上，选中服务旁边的复选框以停止或启动，然后单击停止或启动。

## 启动或停止应用程序服务器和数据库{#start-or-stop-services-for-the-application-server-and-database}的服务

AEM表单的完整实施包括应用程序服务器和数据库服务：

* *`[application server]`* 用于AEM表单
* *`[database]`* 用于AEM表单

在Windows上，可通过&#x200B;**管理工具** > **服务面板**&#x200B;访问这些服务。 例如，如果您使用turnkey方法在JBoss上安装了AEM表单，则系统上可以使用以下服务：

* 适用于Adobe Experience Manager表单的JBoss
* MySQL for Adobe Experience Manager表单

通过从“服务”面板的列表中选择这些服务，然后单击面板上的相应操作按钮，开始或停止这些服务。

在UNIX®或Linux上，从命令行中输入以下文本，其中&#x200B;*`[service name]`*&#x200B;是您正在验证的服务的名称：

```java
     ps -A | grep [service name]
```
