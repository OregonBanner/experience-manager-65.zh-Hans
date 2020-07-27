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


# 启动和停止服务 {#starting-and-stopping-services}

AEM表单包含两种类型的服务：

* 控制AEM forms应用程序服务器和数据库的服务。
* 控制AEM表单模块的服务

## 开始或停止与AEM表单模块关联的服务 {#start-or-stop-the-services-associated-with-aem-forms-modules}

AEM表单模块（例如，表单、权限管理、输出）作为服务运行。 有时，您可能需要停止或开始这些AEM表单模块的服务。 例如，在更改服务设置后，必须停止并重新启动AEM表单服务。

1. 在管理控制台中，单 **击“服务** ”>“ **应用程序和服务** ”>“ **服务管理”**。
1. 在“服务管理”页面上，选中服务旁边的复选框以停止或开始，然后单击停止或开始。

## 开始或停止应用服务器和数据库的服务 {#start-or-stop-services-for-the-application-server-and-database}

AEM表单的完整实施包括应用程序服务器和数据库服务：

* *`[application server]`* for AEM forms
* *`[database]`* for AEM forms

在Windows上，可以通过“管理工具”>“服 **务”面板** 访 **问这些服务**。 例如，如果您使用统包方法在JBoss上安装了AEM表单，则系统上提供以下服务：

* Adobe Experience Manager表单的JBoss
* MySQL forAdobe Experience Manager表单

开始或停止这些服务，方法是从“服务”面板的列表中选择这些服务，然后单击面板上的相应操作按钮。

在UNIX®或Linux上，从命令行中输入以下文本， *`[service name]`* 其中是要验证的服务的名称：

```java
     ps -A | grep [service name]
```

