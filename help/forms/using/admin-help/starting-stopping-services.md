---
title: 启动和停止服务
seo-title: 启动和停止服务
description: 了解如何启动和停止与AEM Forms模块以及应用程序服务器和数据库关联的服务。
seo-description: 了解如何启动和停止与AEM Forms模块以及应用程序服务器和数据库关联的服务。
uuid: 8c831cb2-4165-4118-8a09-764cec4e5e05
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_services
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b93060bd-c6e1-40d2-8acd-ccafb8ed56da
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 启动和停止服务 {#starting-and-stopping-services}

AEM表单包含两种类型的服务：

* 控制AEM Forms应用程序服务器和数据库的服务。
* 控制AEM表单模块的服务

## 启动或停止与AEM表单模块关联的服务 {#start-or-stop-the-services-associated-with-aem-forms-modules}

AEM表单模块（例如，表单、权限管理、输出）作为服务运行。 有时，您可能需要停止或启动这些AEM表单模块的服务。 例如，在更改服务设置后，必须停止并重新启动AEM表单服务。

1. 在管理控制台中，单 **击“服务** ”>“应 **用程序和服务** ” **>“**&#x200B;服务管理”。
1. 在“服务管理”页面上，选中服务旁边的复选框以停止或启动，然后单击停止或启动。

## 启动或停止应用程序服务器和数据库的服务 {#start-or-stop-services-for-the-application-server-and-database}

AEM表单的完整实施包括应用程序服务器和数据库服务：

* *`[application server]`* for AEM forms
* *`[database]`* for AEM forms

在Windows上，可通过“管理工具” **>“服务”** 面板访问 **这些服务**。 例如，如果您使用统包方法在JBoss上安装了AEM表单，则系统上提供以下服务：

* JBoss for Adobe Experience Manager forms
* MySQL for Adobe Experience Manager表单

通过从“服务”面板的列表中选择这些服务，然后单击面板上的相应操作按钮，启动或停止这些服务。

在UNIX®或Linux上，从命令行输入以下文本，其 *`[service name]`* 中是要验证的服务的名称：

```as3
     ps -A | grep [service name]
```

