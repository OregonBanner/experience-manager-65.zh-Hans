---
title: 在AEM中创建和共享专用文件夹
description: 了解如何在Adobe Experience Manager(AEM)资产中创建专用文件夹并与其他用户共享该文件夹，以及为其分配各种权限。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 23d19d9656d61874cd00a9a2473092be0c53b8f8
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 14%

---


# 专用文件夹共享 {#private-folder-sharing}

您可以在Adobe Experience Manager(AEM)资产用户界面中创建仅供您使用的专用文件夹。 您可以将此专用文件夹共享给其他用户，并为其分配各种权限。 根据您分配的权限级别，用户可以对文件夹执行各种任务，例如，视图文件夹中的资产或编辑资产。

>[!NOTE]
>
> 专用文件夹至少有一个具有所有者角色的成员。


1. 在“资产”控制台中，单 **[!UICONTROL 击工]** 具栏中的创建，然后从 **[!UICONTROL 菜单中选]** 择“文件夹”。

   ![创建资产文件夹](assets/Create-folder.png)

1. 在“创 **[!UICONTROL 建文件夹]** ”对话框中，输入文件夹的标题和名称（可选），然后选择“专 **[!UICONTROL 用”]**。

   ![选中“专用”复选框，将文件夹设为专用](assets/private-folder.png)

1. 单击&#x200B;**[!UICONTROL 创建]**。将在UI中创建专用文件夹。

   ![chlimage_1-413](assets/chlimage_1-413.png)

1. To share the folder with other users and the assign privileges to them, select the folder, and click the **[!UICONTROL Properties]** icon from the toolbar.

   ![chlimage_1-414](assets/chlimage_1-414.png)

   >[!NOTE]
   >
   >在您共享文件夹之前，该文件夹对任何其他用户都不可见。

1. In the **[!UICONTROL Folder Properties]** page, select a user from the **[!UICONTROL Add User]** list, assign a role to the user on your private folder, and click **[!UICONTROL Add]**.

   ![chlimage_1-415](assets/chlimage_1-415.png)

   >[!NOTE]
   >
   >对于您向其共享文件夹的用户，您可以分配各种角色，例如“编辑者”‘、“所有者”或“查看者”。如果为用户分配了“所有者”角色，则用户对该文件夹具有“编辑者”权限。 此外，用户还可以与他人共享文件夹。 如果您分配了“编辑者”角色，则用户可以编辑您的专用文件夹中的资产。 如果您分配了“查看器”角色，则用户只能视图您的专用文件夹中的资产。

   >[!NOTE]
   >
   > 专用文件夹至少有一个具有所有者角色的成员。 因此，管理员无法从专用文件夹中删除所有所有者成员。 但是，要从专用文件夹中删除现有所有者（以及管理员本身），管理员必须将其他用户添加为所有者。

1. 单击&#x200B;**[!UICONTROL 保存]**。根据您分配的角色，用户在登录 AEM 资产时便会被分配一组针对您的专用文件夹所拥有的权限。
1. 单击&#x200B;**[!UICONTROL 确定]**&#x200B;以关闭确认消息。
1. 您向用户共享文件夹时，用户会收到共享通知。使用用户的凭据登录AEM资产以视图通知。

   ![chlimage_1-416](assets/chlimage_1-416.png)

1. 单击通知图标以打开通知列表。

   ![通知列表](assets/Assets-Notification.png)

1. 单击管理员共享的专用文件夹条目以打开该文件夹。

>[!NOTE]
>
>要创建专用文件夹，您需要对要创建专用文件夹的父文件夹具有“读取”和“编辑ACL”权限。 如果您不是管理员，则默认情况下不会为您启用这些权限 `/content/dam`。 在这种情况下，首先获得用户ID/组的这些权限，然后再尝试创建专用文件夹或视图文件夹设置。
