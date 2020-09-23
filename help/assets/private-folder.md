---
title: 中的专用文件夹 [!DNL Adobe Experience Manager Assets]
description: 了解如何在中创建专用文件 [!DNL Adobe Experience Manager Assets] 夹并与其他用户共享该文件夹，以及为他们分配各种权限。
contentOwner: AG
translation-type: tm+mt
source-git-commit: b676f73a800c45be12de70b8ba57a332563a49a4
workflow-type: tm+mt
source-wordcount: '642'
ht-degree: 6%

---


# 中的专用文件夹 [!DNL Adobe Experience Manager Assets] {#private-folder}

您可以在用户界面中创 [!DNL Adobe Experience Manager Assets] 建仅供您使用的专用文件夹。 您可以将此专用文件夹共享给其他用户，并为其分配各种权限。 根据您分配的权限级别，用户可以对文件夹执行各种任务，例如，视图文件夹中的资产或编辑资产。

>[!NOTE]
>
>专用文件夹至少有一个具有所有者角色的成员。

## 专用文件夹创建和共享 {#create-share-private-folder}

要创建和共享专用文件夹，请执行以下操作：

1. 在控制 [!DNL Assets] 台中，单 **[!UICONTROL 击工]** 具栏中的创建，然后从菜 **[!UICONTROL 单中选]** 择“文件夹”。

   ![创建资产文件夹](assets/Create-folder.png)

1. 在“创 **[!UICONTROL 建文件夹]** ”对话框中，输入文件夹的标题和名称（可选），然后选择“ **[!UICONTROL 专用]** ”选项。

1. 单击 **[!UICONTROL 创建]**。将创建专用文件夹。

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
>要创建专用文件夹，您需要对要创建专用文件夹的父文件夹具有读取和编辑ACL权限。 如果您不是管理员，则默认情况下不会为您启用这些权限 `/content/dam`。 在这种情况下，首先获得用户ID/组的这些权限，然后再尝试创建专用文件夹或视图文件夹设置。

## 删除专用文件夹 {#delete-private-folder}

您可以通过选择文件夹并从顶部菜单中选择“ [!UICONTROL 删除] ”选项，或使用键盘上的Backspace键来删除专用文件夹。

### 删除文件夹时删除用户组 {#group-removal-on-folder-deletion}

如果使用上述方法从用户界面删除专用文件夹，则关联的用户组也会被删除。 但是，可以使用JMX从存储库中清理现有的冗余、未使用和自动生 [成的用户组](#group-clean-up-jmx)。

>[!CAUTION]
>
>如果从CRXDE Lite中删除专用文件夹，则会在存储库中保留冗余用户组。

### 使用JMX清除未使用的用户组 {#group-clean-up-jmx}

要清理未使用的用户组的存储库，请执行以下操作：

1. 打开JMX以清除Assets的冗余组 `http://[server]:[port]/system/console/jmx/com.day.cq.dam.core.impl.team%3Atype%3DClean+redundant+groups+for+Assets`。

1. 从此 `clean` JMX调用方法。

您可以看到，所有冗余用户组或自动生成的用户组（创建与先前删除的用户组同名的专用文件夹时创建的用户组）都从路径中删除 `/home/groups/mac/default/<user_name>/<folder_name>`。
