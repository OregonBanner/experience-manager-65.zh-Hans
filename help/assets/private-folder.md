---
title: 在中创建和共享专用文件夹 [!DNL Adobe Experience Manager]。
description: 了解如何在中创建专用文件 [!DNL Adobe Experience Manager Assets] 夹并与其他用户共享该文件夹，以及为他们分配各种权限。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 9%

---


# 专用文件夹共享 {#private-folder-sharing}

您可以在用户界面中创 [!DNL Adobe Experience Manager Assets] 建仅供您使用的专用文件夹。 您可以将此专用文件夹共享给其他用户，并为其分配各种权限。 根据您分配的权限级别，用户可以对文件夹执行各种任务，例如，视图文件夹中的资产或编辑资产。

>[!NOTE]
>
>专用文件夹至少有一个具有所有者角色的成员。

1. 在控制 [!DNL Assets] 台中，单 **[!UICONTROL 击工]** 具栏中的创建，然后从菜 **[!UICONTROL 单中选]** 择“文件夹”。

   ![创建资产文件夹](assets/Create-folder.png)

1. 在“创 **[!UICONTROL 建文件夹]** ”对话框中，输入文件夹的标题和名称（可选），然后选择“ **[!UICONTROL 专用]** ”选项。

1. 单击 **[!UICONTROL 创建]**。 将创建专用文件夹。

   ![chlimage_1-413](assets/chlimage_1-413.png)

1. To share the folder with other users and the assign privileges to them, select the folder, and click **[!UICONTROL Properties]** from the toolbar.

   ![info选项](assets/do-not-localize/info-circle-icon.png)

   >[!NOTE]
   >
   >在您共享文件夹之前，该文件夹对任何其他用户都不可见。

1. In the **[!UICONTROL Folder Properties]** page, select a user from the **[!UICONTROL Add User]** list, assign a role to the user on your private folder, and click **[!UICONTROL Add]**.

   ![chlimage_1-415](assets/chlimage_1-415.png)

   >[!NOTE]
   >
   >对于您向其共享文件夹的用户，您可以分配各种角色，例如“编辑者”‘、“所有者”或“查看者”。如果为用户分配了“所有者”角色，则用户对该文件夹具有“编辑者”权限。 此外，用户还可以与他人共享文件夹。 如果您分配了“编辑者”角色，则用户可以编辑您的专用文件夹中的资产。 如果您分配了查看器角色，则用户只能视图您的专用文件夹中的资产。

   >[!NOTE]
   >
   >专用文件夹至少有一个具有所有者角色的成员。 因此，管理员无法从专用文件夹中删除所有所有者成员。 但是，要从专用文件夹中删除现有所有者（以及管理员本身），管理员必须将其他用户添加为所有者。

1. 单击&#x200B;**[!UICONTROL 保存]**。Depending on the role you assign, the user is assigned a set of privileges on your private folder when the user logs in to [!DNL Assets].
1. 单击&#x200B;**[!UICONTROL 确定]**&#x200B;以关闭确认消息。
1. 您向用户共享文件夹时，用户会收到共享通知。使用用 [!DNL Assets] 户的凭据登录以视图通知。

   ![chlimage_1-416](assets/chlimage_1-416.png)

1. 单击“通知”以打开通知列表。

   ![通知列表](assets/Assets-Notification.png)

1. 单击管理员共享的专用文件夹条目以打开该文件夹。

>[!NOTE]
>
>要创建专用文件夹，您需要对要创建专用文件夹的父文件夹具有“读取”和“编辑ACL”权限。 如果您不是管理员，则默认情况下不会为您启用这些权限 `/content/dam`。 在这种情况下，首先获得用户ID/组的这些权限，然后再尝试创建专用文件夹或视图文件夹设置。
