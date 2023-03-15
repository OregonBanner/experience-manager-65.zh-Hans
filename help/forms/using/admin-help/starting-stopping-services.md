---
title: 启动和停止服务
seo-title: Starting and stopping services
description: 了解如何启动和停止与AEM Forms模块以及应用程序服务器和数据库关联的服务。
seo-description: Learn how to start and stop services associated with AEM Forms modules and the application server and database.
uuid: 8c831cb2-4165-4118-8a09-764cec4e5e05
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_services
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b93060bd-c6e1-40d2-8acd-ccafb8ed56da
exl-id: 55bf5196-22c6-4286-8c92-ff44d81dde49
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 0%

---

# 启动和停止服务 {#starting-and-stopping-services}

AEM表单中包含两种类型的服务：

* 控制AEM表单应用程序服务器和数据库的服务。
* 控制AEM表单模块的服务

## 启动或停止与AEM表单模块关联的服务 {#start-or-stop-the-services-associated-with-aem-forms-modules}

AEM表单模块(例如Forms、Rights Management、输出)作为服务运行。 有时，您可能需要停止或启动这些AEM表单模块的服务。 例如，在更改服务的设置后，必须停止AEM表单服务，然后重新启动该服务。

1. 在管理控制台中，单击 **服务** > **应用程序和服务** > **服务管理**.
1. 在“服务管理”页上，选中要停止或启动的服务旁边的复选框，然后单击停止或启动。

## 启动或停止应用程序服务器和数据库的服务 {#start-or-stop-services-for-the-application-server-and-database}

AEM Forms的完整实施包括应用程序服务器和数据库服务：

* *`[application server]`* 适用于AEM表单的
* *`[database]`* 适用于AEM表单的

在Windows上，这些服务可通过 **管理工具** > **“服务”面板**. 例如，如果您使用turnkey方法在JBoss上安装了AEM表单，则您的系统上可以使用以下服务：

* Adobe Experience Manager表单的JBoss
* 适用于Adobe Experience Manager的MySQL表单

通过从“服务”面板的列表中选择这些服务，然后单击面板上的相应操作按钮，启动或停止这些服务。

在UNIX®或Linux上，从命令行输入以下文本，其中 *`[service name]`* 是正在验证的服务的名称：

```java
     ps -A | grep [service name]
```
