---
title: 启动和停止WebSphere Application Server
seo-title: 启动和停止WebSphere Application Server
description: 几个过程要求您停止或开始要部署AEM表单产品的WebSphere实例。 本文档介绍如何开始和停止WebSphere Application Server。
seo-description: 几个过程要求您停止或开始要部署AEM表单产品的WebSphere实例。 本文档介绍如何开始和停止WebSphere Application Server。
uuid: e0373197-aa57-4087-933d-92a86840a11a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: bcd16691-67ab-4694-9e6b-c9d3e0c7bf0b
translation-type: tm+mt
source-git-commit: 67ea825215d1ca7cc2e350ed1c128c3146de45ec
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 0%

---


# 启动和停止WebSphere应用程序服务器{#starting-and-stopping-websphere-application-server}

几个过程要求您停止或开始要部署AEM表单产品的WebSphere实例。 如果不确定应用程序服务器是否已启动，可以先视图WebSphere Application Server的状态。

## 视图WebSphere应用程序服务器{#view-the-status-of-websphere-application-server}的状态

1. 从命令提示符中，转到`[appserver root]/bin`目录。
1. 输入以下命令，将&#x200B;*server_name*&#x200B;替换为WebSphere应用程序服务器的名称：

   * (Windows)`serverStatus.bat`*server_name*
   * (Linux、UNIX)。/ `serverStatus.sh`*server name*

## 开始WebSphere应用程序服务器{#start-websphere-application-server}

1. 从命令提示符中，转到`[appserver root]/bin`目录。
1. 输入以下命令，将&#x200B;*server_name*&#x200B;替换为WebSphere应用程序服务器的名称：

   * (Windows)`startServer.bat`*server_name*
   * (Linux、UNIX)。/ `startServer.sh`*server name*

## 停止WebSphere应用程序服务器{#stop-websphere-application-server}

1. 从命令提示符中，转到`[appserver root]/bin`目录。
1. 输入以下命令，将&#x200B;*server_name*&#x200B;替换为WebSphere应用程序服务器的名称：

   * (Windows)`stopServer.bat`*server_name*
   * (Linux、UNIX)。/ `stopServer.sh`*server name*

