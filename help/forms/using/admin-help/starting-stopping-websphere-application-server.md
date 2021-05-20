---
title: 启动和停止WebSphere应用程序服务器
seo-title: 启动和停止WebSphere应用程序服务器
description: 有几个步骤要求您停止或启动要在其中部署AEM表单产品的WebSphere实例。 本文档介绍如何启动和停止WebSphere应用程序服务器。
seo-description: 有几个步骤要求您停止或启动要在其中部署AEM表单产品的WebSphere实例。 本文档介绍如何启动和停止WebSphere应用程序服务器。
uuid: e0373197-aa57-4087-933d-92a86840a11a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: bcd16691-67ab-4694-9e6b-c9d3e0c7bf0b
exl-id: 1a4e8f20-0644-4c96-9f52-f7a59521eac9
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 0%

---

# 启动和停止WebSphere应用程序服务器{#starting-and-stopping-websphere-application-server}

有几个步骤要求您停止或启动要在其中部署AEM表单产品的WebSphere实例。 如果不确定应用程序服务器是否已启动，您可以首先查看WebSphere应用程序服务器的状态。

## 查看WebSphere应用程序服务器{#view-the-status-of-websphere-application-server}的状态

1. 在命令提示符下，转到`[appserver root]/bin`目录。
1. 输入以下命令，将&#x200B;*server_name*&#x200B;替换为WebSphere应用程序服务器的名称：

   * (Windows)`serverStatus.bat`*server_name*
   * (Linux、UNIX)。/ `serverStatus.sh`*server_name*

## 启动WebSphere应用程序服务器{#start-websphere-application-server}

1. 在命令提示符下，转到`[appserver root]/bin`目录。
1. 输入以下命令，将&#x200B;*server_name*&#x200B;替换为WebSphere应用程序服务器的名称：

   * (Windows)`startServer.bat`*server_name*
   * (Linux、UNIX)。/ `startServer.sh`*server_name*

## 停止WebSphere应用程序服务器{#stop-websphere-application-server}

1. 在命令提示符下，转到`[appserver root]/bin`目录。
1. 输入以下命令，将&#x200B;*server_name*&#x200B;替换为WebSphere应用程序服务器的名称：

   * (Windows)`stopServer.bat`*server_name*
   * (Linux、UNIX)。/ `stopServer.sh`*server_name*
