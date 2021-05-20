---
title: 启动和停止WebLogic服务器
seo-title: 启动和停止WebLogic服务器
description: 有几个过程要求您启动或停止要在其中部署AEM表单模块的WebLogic服务器实例。 本文档介绍如何启动和停止WebLogic服务器。
seo-description: 有几个过程要求您启动或停止要在其中部署AEM表单模块的WebLogic服务器实例。 本文档介绍如何启动和停止WebLogic服务器。
uuid: 957787fe-4cea-4ecd-b49a-c33023c5c309
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c908d064-6596-473a-b218-22a2496c83f7
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 1%

---


# 启动和停止WebLogic服务器{#starting-and-stopping-weblogic-server}

有几个过程要求您启动或停止要在其中部署AEM表单模块的WebLogic服务器实例。 根据您执行的任务，确保WebLogic服务器停止或运行。

<table>
 <thead>
  <tr>
   <th><p>活动</p></th>
   <th><p>所需的WebLogic状态</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>创建WebLogic域</p></td>
   <td><p>已停止</p></td>
  </tr>
  <tr>
   <td><p>创建WebLogic托管服务器</p></td>
   <td><p>正在运行</p></td>
  </tr>
  <tr>
   <td><p>增加服务器线程计数</p></td>
   <td><p>正在运行</p></td>
  </tr>
  <tr>
   <td><p>部署AEM Forms产品</p></td>
   <td><p>正在运行</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>如果您在Red Hat® Enterprise Linux Advanced Server 4.0上运行WebLogic Server，请使用`export LD_ASSUME_KERNEL=2.4.19`命令将`LD_ASSUME_KERNEL`环境变量设置为2.4.19。 然后，从设置此环境变量的同一外壳中运行WebLogic服务器。

## 启动WebLogic服务器{#start-weblogic-server}

1. 在命令提示符下，转到&#x200B;*[appserver root]*/user_projects/domains/*[appserverdomain]*。
1. 输入以下命令：

   * (Windows) `startWebLogic.cmd`
   * (Linux， UNIX)。/ `startWebLogic.sh`

## 停止WebLogic服务器{#stop-weblogic-server}

1. 通过在Web浏览器的URL行中键入`https://[host name]:7001/console`来启动WebLogic服务器管理控制台。
1. 通过键入创建此WebLogic配置时使用的用户名和密码登录，然后单击“登录”。
1. 在“更改中心”(Change Center)下，单击“锁定并编辑”(Lock &amp; Edit)。
1. 在“域结构”下，单击“环境”>“服务器”。
1. 单击AdminServer ，然后在AdminServer的“设置”窗格中，单击“控制”选项卡。
1. 确保在“服务器状态”表中选择了AdminServer ，然后单击“关闭”。
1. 选择“工作完成时”以正常关闭服务器，或选择“立即强制关闭”以立即停止服务器，而不完成正在进行的任务。
1. 在“Server Life Cycle Assistant”窗格上，单击“是”以完成关闭。

WebLogic服务器管理控制台不再可用，并且从中运行start命令的命令提示符可用。

## 启动WebLogic管理控制台{#start-weblogic-administration-console}

1. 如果WebLogic Admin Server尚未运行，请从命令提示符下，转到&#x200B;*[appserver root]\user_projects\domains\[domainname]*&#x200B;目录，然后输入以下命令：

   * (Windows)`startWebLogic.cmd`
   * (Linux， UNIX)。/ `startWebLogic.sh`

1. 通过在Web浏览器的URL行中键入`https://[host name]:[port]/console`访问WebLogic服务器管理控制台，其中&#x200B;*[port]*&#x200B;是非安全监听端口。 默认情况下，此端口值为7001。
1. 在登录屏幕上，键入您的管理员用户名和密码，然后单击登录。

## 启动节点管理器{#start-node-manager}

1. 确保WebLogic服务器正在运行。
1. 在新的命令提示符下，转到&#x200B;*[appserver root]*/server/bin。
1. 输入以下命令：

   * (Windows)`startNodeManager.cmd`
   * (Linux， UNIX)`./startNodeManager.sh`

## 停止节点管理器{#stop-node-manager}

关闭WebLogic服务器后，可以关闭命令提示符，从该提示符中调用节点管理器。

## 启动WebLogic托管服务器{#start-a-weblogic-managed-server}

>[!NOTE]
>
>只有在创建WebLogic域和受管服务器后，才能执行此任务。

1. 确保WebLogic服务器和节点管理器正在运行。
1. 通过在Web浏览器的URL行中键入`https://host name]:[port]`/console`来启动WebLogic服务器管理控制台。
1. 在“域结构”下，单击“环境”>“服务器”。
1. 在右窗格中，单击“Control（控制）”选项卡。
1. 选择要启动的受控服务器。
1. 单击要启动的受控服务器下方的“启动”按钮。

## 停止WebLogic托管服务器{#stop-a-weblogic-managed-server}

1. 在Web浏览器的URL行中键入`https://`*[主机名]:[端口&#x200B;]*`/console`，以启动WebLogic服务器管理控制台。
1. 在“域结构”下，单击“环境”>“服务器”。
1. 在右窗格中，单击“Control（控制）”选项卡。
1. 选择要停止的受控服务器。
1. 单击要停止的受控服务器下方的关闭按钮。
1. 选择“工作完成时”以正常关闭服务器，或选择“立即强制关闭”以立即停止服务器，而不完成正在进行的任务。
1. 在“Server Life Cycle Assistant”窗格上，单击“是”以完成关闭。

