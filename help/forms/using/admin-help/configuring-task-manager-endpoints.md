---
title: 配置任务管理器端点
description: 了解如何配置Task Manager端点以调用服务。 配置Task Manager端点需要不同的设置。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 8495a3d7-6ac9-41f5-b1f9-31decaba118a
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---

# 配置任务管理器端点 {#configuring-task-manager-endpoints}

任务管理器端点使Workspace用户能够调用服务。

**任务管理器端点设置**

使用以下设置配置任务管理器端点。

**名称：** （必需）标识端点。 该名称显示在工作区中的卡片视图中。 不要包含&lt;字符，因为它将截断工作区中显示的名称。 如果您输入URL作为端点的名称，请确保它符合RFC1738中指定的语法规则。

**描述：** 端点的描述。 不要包含&lt;字符，因为它将截断工作区中显示的描述。

**任务说明：** 启动此工作流的用户的说明。

**进程所有者：** 负责流程的人员的姓名。

**用户可以转发任务：** 允许用户转发初始任务。

**显示附件窗口：** 允许用户查看附件窗口。

**允许添加附件：** 允许用户添加附件和注释。

**最初锁定的任务：** 锁定初始任务。

**为共享队列添加ACL：** 初始任务是为共享队列用户创建的ACL。

**分类：** （必需）用户将在工作区中看到表单的类别。 从列表中选择一个类别，或选择“新建类别”以添加类别。

**操作名称：** （必需）可分配给端点的操作列表。
