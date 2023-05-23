---
title: 啟動和停止WebSphere Application Server
seo-title: Starting and stopping WebSphere Application Server
description: 數個程式需要您停止或啟動要部署AEM表單產品的WebSphere執行個體。 本檔案說明如何啟動和停止WebSphere Application Server。
seo-description: Several procedures require you to stop or start the instance of WebSphere where you want to deploy AEM forms products. This document describes how to start and stop the WebSphere Application Server.
uuid: e0373197-aa57-4087-933d-92a86840a11a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: bcd16691-67ab-4694-9e6b-c9d3e0c7bf0b
exl-id: 1a4e8f20-0644-4c96-9f52-f7a59521eac9
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---

# 啟動和停止WebSphere Application Server {#starting-and-stopping-websphere-application-server}

數個程式需要您停止或啟動要部署AEM表單產品的WebSphere執行個體。 如果您不確定應用程式伺服器是否已啟動，可以先檢視WebSphere Application Server的狀態。

## 檢視WebSphere應用程式伺服器的狀態 {#view-the-status-of-websphere-application-server}

1. 在命令提示字元中，前往 `[appserver root]/bin` 目錄。
1. 輸入下列命令，取代 *server_name* 使用WebSphere Application Server的名稱：

   * (Windows) `serverStatus.bat`*server_name*
   * (Linux、UNIX) 。/ `serverStatus.sh`*server_name*

## 啟動WebSphere Application Server {#start-websphere-application-server}

1. 在命令提示字元中，前往 `[appserver root]/bin` 目錄。
1. 輸入下列命令，取代 *server_name* 使用WebSphere Application Server的名稱：

   * (Windows) `startServer.bat`*server_name*
   * (Linux、UNIX) 。/ `startServer.sh`*server_name*

## 停止WebSphere Application Server {#stop-websphere-application-server}

1. 在命令提示字元中，前往 `[appserver root]/bin` 目錄。
1. 輸入下列命令，取代 *server_name* 使用WebSphere Application Server的名稱：

   * (Windows) `stopServer.bat`*server_name*
   * (Linux、UNIX) 。/ `stopServer.sh`*server_name*
