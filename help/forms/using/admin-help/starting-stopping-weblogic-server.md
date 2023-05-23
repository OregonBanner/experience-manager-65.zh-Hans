---
title: 啟動和停止WebLogic Server
seo-title: Starting and stopping WebLogic Server
description: 數個程式需要您啟動或停止要部署AEM表單模組的WebLogic Server執行個體。 本檔案說明如何啟動和停止WebLogic Server。
seo-description: Several procedures require you to start or stop the instance of WebLogic Server where you want to deploy AEM forms modules. This document describes how to start and stop the WebLogic Server.
uuid: 957787fe-4cea-4ecd-b49a-c33023c5c309
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c908d064-6596-473a-b218-22a2496c83f7
source-git-commit: d1fc2ff44378276522c2ff3208f5b3bdc4484bba
workflow-type: tm+mt
source-wordcount: '601'
ht-degree: 1%

---


# 啟動和停止WebLogic Server {#starting-and-stopping-weblogic-server}

數個程式需要您啟動或停止要部署AEM表單模組的WebLogic Server執行個體。 請確定WebLogic Server已停止或正在執行，視您正在執行的工作而定。

<table>
 <thead>
  <tr>
   <th><p>活动</p></th>
   <th><p>必要的WebLogic狀態</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>建立WebLogic領域</p></td>
   <td><p>已停止</p></td>
  </tr>
  <tr>
   <td><p>建立WebLogic受管理伺服器</p></td>
   <td><p>正在运行</p></td>
  </tr>
  <tr>
   <td><p>增加伺服器執行緒計數</p></td>
   <td><p>正在运行</p></td>
  </tr>
  <tr>
   <td><p>部署AEM表單產品</p></td>
   <td><p>正在运行</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>如果您在Red Hat® Enterprise Linux Advanced Server 4.0上執行WebLogic Server，請將 `LD_ASSUME_KERNEL` 環境變數升級至2.4.19，方法是使用 `export LD_ASSUME_KERNEL=2.4.19` 命令。 然後，從您設定此環境變數的相同殼層執行WebLogic Server。

## 啟動WebLogic Server {#start-weblogic-server}

1. 在命令提示字元中，前往 *[appserver根目錄]*/user_projects/domains/*[appserverdomain]*.
1. 輸入下列命令：

   * (Windows) `startWebLogic.cmd`
   * (Linux、UNIX) ./ `startWebLogic.sh`

## 停止WebLogic Server {#stop-weblogic-server}

1. 輸入「 」以啟動WebLogic Server管理主控台 `https://[host name]:7001/console` 在網頁瀏覽器的URL行中。
1. 輸入建立此WebLogic組態時使用的使用者名稱和密碼來登入，然後按一下[登入]。
1. 在「變更中心」下，按一下「鎖定與編輯」。
1. 在「網域結構」下，按一下「環境」>「伺服器」。
1. 按一下「AdminServer」，然後在「AdminServer設定」窗格中按一下「控制」標籤。
1. 確定已選取[伺服器狀態]表格中的[AdminServer]，然後按一下[關機]。
1. 選取「工作完成時」以正常關閉伺服器，或選取「立即強制關閉」以立即停止伺服器而不完成正在進行的工作。
1. 在「伺服器生命週期輔助程式」窗格中，按一下「是」以完成關機。

WebLogic Server管理主控台已無法使用，而且您執行start命令的命令提示字元已可使用。

## 啟動WebLogic管理主控台 {#start-weblogic-administration-console}

1. 如果WebLogic Admin Server尚未執行，請從命令提示字元移至 *[appserver根目錄]\user_projects\domains\[domainname]* 目錄，然後輸入下列命令：

   * (Windows) `startWebLogic.cmd`
   * (Linux、UNIX) ./ `startWebLogic.sh`

1. 輸入「 」以存取WebLogic伺服器管理主控台 `https://[host name]:[port]/console` 在網頁瀏覽器的URL行中，其中 *[連線埠]* 是不安全的接聽連線埠。 依預設，此連線埠值為7001。
1. 在登入畫面上，輸入您的管理員使用者名稱和密碼，然後按一下「登入」。

## 啟動節點管理員 {#start-node-manager}

1. 請確定WebLogic Server正在執行。
1. 在新的命令提示字元中，前往 *[appserver根目錄]*/server/bin。
1. 輸入下列命令：

   * (Windows) `startNodeManager.cmd`
   * (Linux、UNIX) `./startNodeManager.sh`

## 停止節點管理員 {#stop-node-manager}

關閉WebLogic伺服器後，您可以關閉呼叫節點管理員的命令提示字元。

## 啟動WebLogic管理的伺服器 {#start-a-weblogic-managed-server}

>[!NOTE]
>
>只有在建立WebLogic網域和Managed Server之後，才能執行此工作。

1. 請確定WebLogic伺服器和節點管理員正在執行。
1. 輸入「 」以啟動WebLogic Server管理主控台 `https://host name]:[port]/console` 在網頁瀏覽器的URL行中。
1. 在「網域結構」下，按一下「環境」>「伺服器」。
1. 在右窗格中，按一下[控制]索引標籤。
1. 選取您要啟動的受管理伺服器。
1. 按一下您要啟動的受管理伺服器下方的「啟動」按鈕。

## 停止WebLogic管理的伺服器 {#stop-a-weblogic-managed-server}

1. 輸入「 」以啟動WebLogic Server管理主控台 `https://`*[主機名稱]：[連線埠&#x200B;]*`/console` 在網頁瀏覽器的URL行中。
1. 在「網域結構」下，按一下「環境」>「伺服器」。
1. 在右窗格中，按一下[控制]索引標籤。
1. 選取您要停止的受管理伺服器。
1. 按一下要停止的受管理伺服器下方的「關機」按鈕。
1. 選取「工作完成時」以正常關閉伺服器，或選取「立即強制關閉」以立即停止伺服器而不完成正在進行的工作。
1. 在「伺服器生命週期輔助程式」窗格中，按一下「是」以完成關機。

