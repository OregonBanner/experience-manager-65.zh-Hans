---
title: 启动和停止WebSphere应用程序服务器
description: 多个过程要求您停止或启动要部署AEM表单产品的WebSphere实例。 本文档介绍如何启动和停止WebSphere应用程序服务器。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 1a4e8f20-0644-4c96-9f52-f7a59521eac9
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 0%

---

# 启动和停止WebSphere应用程序服务器 {#starting-and-stopping-websphere-application-server}

多个过程要求您停止或启动要部署AEM表单产品的WebSphere实例。 如果不确定应用程序服务器是否已启动，可以首先查看WebSphere应用程序服务器的状态。

## 查看WebSphere应用程序服务器的状态 {#view-the-status-of-websphere-application-server}

1. 在命令提示符下，转到 `[appserver root]/bin` 目录。
1. 输入以下命令，替换 *server_name* 使用WebSphere应用程序服务器的名称：

   * (Windows) `serverStatus.bat`*server_name*
   * (Linux、UNIX) 。/ `serverStatus.sh`*server_name*

## 启动WebSphere应用程序服务器 {#start-websphere-application-server}

1. 在命令提示符下，转到 `[appserver root]/bin` 目录。
1. 输入以下命令，替换 *server_name* 使用WebSphere应用程序服务器的名称：

   * (Windows) `startServer.bat`*server_name*
   * (Linux、UNIX) 。/ `startServer.sh`*server_name*

## 停止WebSphere应用程序服务器 {#stop-websphere-application-server}

1. 在命令提示符下，转到 `[appserver root]/bin` 目录。
1. 输入以下命令，替换 *server_name* 使用WebSphere应用程序服务器的名称：

   * (Windows) `stopServer.bat`*server_name*
   * (Linux、UNIX) 。/ `stopServer.sh`*server_name*
