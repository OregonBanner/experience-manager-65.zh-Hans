---
title: 配置共享队列
seo-title: 配置共享队列
description: 通过共享队列，您可以有效地配置和管理用户队列。 了解如何配置共享队列。
seo-description: 通过共享队列，您可以有效地配置和管理用户队列。 了解如何配置共享队列。
uuid: 69ab611d-334b-40a5-bd2d-533d4cb25eda
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: fc403a60-b635-4334-9bf8-2f3d2036b2f3
exl-id: 5f4467c1-0f3f-4dc6-9bd5-98259f327295
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '672'
ht-degree: 0%

---

# 配置共享队列{#configuring-shared-queues}

通过共享队列，您可以有效地配置和管理用户队列。 用户队列只是分配给用户的所有任务，有关详细信息，请参阅[要执行的列表](https://help.adobe.com/en_US/livecycle/11.0/WorkspaceHelp/WS92d06802c76abadb-2b6ab502126beb6ba2f-7ffc.2.html)。 您可以根据组织需求分配、取消分配和重新分配用户队列。 您可以通过两种方式管理共享队列：

**管理用户访问权限**

您可以使用此选项管理对选定用户队列的访问权限。

**管理用户的访问权限**

您可以使用此选项管理分配给选定用户的共享队列。

## 管理对选定用户队列{#managing-access-to-a-selected-user-queue}的访问

通过“管理对用户的访问”功能，您可以管理对选定用户队列的访问。 您可以向组织中的其他用户授予或撤消对选定用户队列的访问权限。 比如，卡拉·鲍曼不在办公室。 使用“管理对用户的访问”功能，可以与Akira Tanaka和John Jacobs共享她的队列，以便完成。 之后，当卡拉·鲍曼回到办公室时，你可以撤销对田中明和约翰·雅各布斯排队的访问权。

共享后，用户可以使用工作区完成这些任务，并有权访问队列。

>[!NOTE]
>
>AEM Forms版本已弃用Flex Workspace。

### 配置对选定用户队列{#configuring-access-to-a-selected-user-queue}的访问

1. 使用管理员帐户登录到管理控制台。
1. 选择&#x200B;**服务** > **表单工作流** > **共享队列**。

1. 在管理对用户的访问权限选项卡上，查找并选择要共享其队列的用户。 在任意位置，右下方的窗格都会显示有权访问所选用户队列的用户列表。
1. 在左下窗格中，查找并选择用户。 单击共享。
1. 单击保存以完成。

### 撤消对选定用户队列{#revoking-access-to-a-selected-user-queue}的访问

1. 使用管理员帐户登录到管理控制台。
1. 选择&#x200B;**服务** > **表单工作流** > **共享队列**。

1. 在管理对用户的访问权限选项卡上，查找并选择要管理其队列的用户。
1. 右下方的窗格显示有权访问选定用户队列的用户列表。 选择用户，然后单击“撤消”。
1. 单击保存以完成。

## 管理分配给用户{#managing-queues-assigned-to-a-user}的队列

通过“按用户管理访问权限”功能，您可以管理分配给选定用户的队列。 您可以单独授予或撤消对选定用户的用户队列的访问权限。 例如，您希望将Akira Tanaka和John Jacobs用户队列分配给Kara Bowman。 使用“按用户管理访问”功能，您可以搜索Kara Bowman并授予对分配给Akira Tanaka和John Jacobs的任务的访问权限。 稍后，您可以撤消Kara Bowman对这些用户队列的访问权限。

分配后，用户即可使用工作区完成这些任务。

>[!NOTE]
>
>AEM Forms版本已弃用Flex Workspace。

### 授予对选定用户队列{#granting-access-to-a-selected-user-queue}的访问权限

1. 使用管理员帐户登录到管理控制台。
1. 选择&#x200B;**服务** > **表单工作流** > **共享队列**。

1. 在管理对用户的访问权限选项卡上，查找并选择要共享其队列的用户。 在任意位置，右下方的窗格都会显示有权访问所选用户队列的用户列表。
1. 在左下窗格中，查找并选择您希望与选定用户共享的用户队列。 单击共享。
1. 单击保存以完成。

### 撤消对选定用户队列{#revoking_access_to_a_selected_user_queue-1}的访问

1. 使用管理员帐户登录到管理控制台。
1. 选择&#x200B;**服务** > **表单工作流** > **共享队列**。

1. 在“按用户管理访问”选项卡上，查找并选择要管理其队列的用户。
1. 右下方的窗格显示分配给选定用户的用户队列列表。 选择用户队列，然后单击“撤消”。
1. 单击保存以完成。
