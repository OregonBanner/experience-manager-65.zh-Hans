---
title: 配置共享队列
seo-title: Configuring Shared Queues
description: 共享队列允许您有效地配置和管理用户队列。 了解如何配置共享队列。
seo-description: Shared Queues allow you to configure and manage user queues effectively. Learn how to configure shared queues.
uuid: 69ab611d-334b-40a5-bd2d-533d4cb25eda
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: fc403a60-b635-4334-9bf8-2f3d2036b2f3
exl-id: 5f4467c1-0f3f-4dc6-9bd5-98259f327295
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '652'
ht-degree: 0%

---

# 配置共享队列{#configuring-shared-queues}

共享队列允许您有效地配置和管理用户队列。 用户队列只是分配给用户的所有任务，请参阅 [待办事项列表](https://help.adobe.com/en_US/livecycle/11.0/WorkspaceHelp/WS92d06802c76abadb-2b6ab502126beb6ba2f-7ffc.2.html) 了解更多信息。 您可以根据组织需求分配、取消分配和重新分配用户队列。 您可以通过两种方式管理共享队列：

**管理对用户的访问**

您可以使用此选项管理对所选用户队列的访问权限。

**按用户管理访问权限**

您可以使用此选项管理分配给选定用户的共享队列。

## 管理对所选用户队列的访问权限 {#managing-access-to-a-selected-user-queue}

“管理对用户的访问”功能允许您管理对选定用户队列的访问。 您可以将所选用户队列的访问权限授予或撤销给组织中的其他用户。 比如，卡拉·鲍曼不在办公室。 使用“管理对用户的访问权限”功能，可以与Akira Tanaka和John Jacobs共享她的队列以填写。 之后，当Kara Bowman返回办公室时，您可以撤销田中昭和约翰·雅各布斯对她的队列的访问权限。

共享后，这些任务可以由用户使用工作区完成并对队列具有访问权限。

>[!NOTE]
>
>AEM Forms版本弃用Flex工作区。

### 配置对选定用户队列的访问权限 {#configuring-access-to-a-selected-user-queue}

1. 使用管理员帐户登录到管理控制台。
1. 选择 **服务** > **表单工作流** > **共享队列**.

1. 在管理对用户的访问选项卡上，查找并选择您要共享其队列的用户。 在任何时候，右下方窗格都会显示有权访问所选用户队列的用户列表。
1. 在左下方的窗格中，查找并选择用户。 单击共享。
1. 单击“保存”以完成。

### 撤销对选定用户队列的访问权限 {#revoking-access-to-a-selected-user-queue}

1. 使用管理员帐户登录到管理控制台。
1. 选择 **服务** > **表单工作流** > **共享队列**.

1. 在管理对用户的访问选项卡上，查找并选择您要管理其队列的用户。
1. 右下方窗格显示有权访问所选用户队列的用户列表。 选择用户，然后单击撤销。
1. 单击“保存”以完成。

## 管理分配给用户的队列 {#managing-queues-assigned-to-a-user}

“按用户管理访问”功能允许您管理分配给选定用户的队列。 您可以单独授予或撤销所选用户访问用户队列的权限。 例如，您希望将Akira Tanaka和John Jacobs用户队列分配给Kara Bowman。 使用“按用户管理访问权限”功能，您可以搜索Kara Bowman并授予对分配给Akira Tanaka和John Jacobs的任务的访问权限。 之后，您可以撤消Kara Bowman对这些用户队列的访问权限。

分配后，用户可以使用工作区完成这些任务。

>[!NOTE]
>
>AEM Forms版本弃用Flex工作区。

### 授予对选定用户队列的访问权限 {#granting-access-to-a-selected-user-queue}

1. 使用管理员帐户登录到管理控制台。
1. 选择 **服务** > **表单工作流** > **共享队列**.

1. 在管理对用户的访问权限选项卡上，查找并选择您要共享其队列的用户。 在任何时候，右下方窗格都会显示有权访问所选用户队列的用户列表。
1. 在左下方的窗格中，查找并选择您希望与选定用户共享的用户队列。 单击共享。
1. 单击“保存”以完成。

### 撤销对选定用户队列的访问权限 {#revoking_access_to_a_selected_user_queue-1}

1. 使用管理员帐户登录到管理控制台。
1. 选择 **服务** > **表单工作流** > **共享队列**.

1. 在按用户管理访问选项卡上，查找并选择您要管理其队列的用户。
1. 右下窗格显示分配给选定用户的用户队列列表。 选择用户队列并单击撤消。
1. 单击“保存”以完成。
