---
title: 配置任务管理器端点
seo-title: 配置任务管理器端点
description: 了解如何配置任务管理器端点。
seo-description: 了解如何配置任务管理器端点。
uuid: 07604b10-0bd7-4bce-9624-7ebac4754f56
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9c55feb9-23d8-4798-a3c5-70ec736df3ad
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---


# 配置任务管理器端点{#configuring-task-manager-endpoints}

任务管理器端点使Workspace用户能够调用服务。

**任务管理器端点设置**

使用以下设置配置任务管理器端点。

**名称：** （强制）标识端点。名称显示在Workspace的卡视图中。 不要包含&lt;字符，因为它将截断Workspace中显示的名称。 如果要输入URL作为端点的名称，请确保它符合RFC1738中指定的语法规则。

**描述：** 端点的描述。不要包含&lt;字符，因为它将截断Workspace中显示的描述。

**任务说** 明：开始此工作流的用户的说明。

**流程所** 有者：负责流程的人员的姓名。

**用户可以转发任务** ：允许用户转发初始任务。

**显示附件窗** 口：允许用户查看附件窗口。

**允许添加附** 件：允许用户添加附件和附注。

**任务初始锁定：** 锁定初始任务。

**为共享队列添加ACL:** 初始任务是使用共享队列用户的ACL创建的。

**分类：** （必填）用户在Workspace中查看表单的类别。从类别中选择一个列表，或选择新建类别以添加类别。

**操作名称** :（必选）可分配给端点的操作列表。
