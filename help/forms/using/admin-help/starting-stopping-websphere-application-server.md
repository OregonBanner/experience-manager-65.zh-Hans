---
title: 启动和停止WebSphere Application Server
seo-title: 启动和停止WebSphere Application Server
description: 多个过程要求您停止或启动要在其中部署AEM表单产品的WebSphere实例。 本文档介绍如何启动和停止WebSphere应用程序服务器。
seo-description: 多个过程要求您停止或启动要在其中部署AEM表单产品的WebSphere实例。 本文档介绍如何启动和停止WebSphere应用程序服务器。
uuid: e0373197-aa57-4087-933d-92a86840a11a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: bcd16691-67ab-4694-9e6b-c9d3e0c7bf0b
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 启动和停止WebSphere Application Server {#starting-and-stopping-websphere-application-server}

多个过程要求您停止或启动要在其中部署AEM表单产品的WebSphere实例。 如果不确定应用程序服务器是否已启动，您可以首先查看WebSphere应用程序服务器的状态。

## 查看WebSphere Application server的状态 {#view-the-status-of-websphere-application-server}

1. 从命令提示符下，转到 *[appserver root]*/bin目录。
1. 输入以下命令，将 *server_name* 替换为WebSphere应用程序服务器的名称：

   * (Windows) `serverStatus.bat`*server_name *
   * (Linux、UNIX)。/ `serverStatus.sh`*server_name *

## 启动WebSphere Application Server {#start-websphere-application-server}

1. 从命令提示符下，转到 *[appserver root]*/bin目录。
1. 输入以下命令，将 *server_name* 替换为WebSphere应用程序服务器的名称：

   * (Windows) `startServer.bat`*server_name *
   * (Linux、UNIX)。/ `startServer.sh`*server_name *

## 停止WebSphere Application Server {#stop-websphere-application-server}

1. 从命令提示符下，转到 *[appserver root]*/bin目录。
1. 输入以下命令，将 *server_name* 替换为WebSphere应用程序服务器的名称：

   * (Windows) `stopServer.bat`*server_name *
   * (Linux、UNIX)。/ `stopServer.sh`*server_name *

