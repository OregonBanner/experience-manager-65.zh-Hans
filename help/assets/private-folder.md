---
title: 用于共享资产的专用文件夹
description: 了解如何在中创建专用文件 [!DNL Adobe Experience Manager Assets] 夹并与其他用户共享该文件夹，以及为他们分配各种权限。
contentOwner: AG
translation-type: tm+mt
source-git-commit: ce43c49f8f7d4509e414554b8f4eba368ff66e95
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 3%

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
   >You can assign various roles, such as `Editor`, `Owner`, or `Viewer` to the user with whom you share the folder. 如果您为用 `Owner` 户分配了角色，则用户对该文 `Editor` 件夹具有权限。 此外，用户还可以与他人共享文件夹。 If you assign an `Editor` role, the user can edit the assets in your private folder. 如果您分配了查看器角色，则用户只能视图您的专用文件夹中的资产。

   >[!NOTE]
   >
   >专用文件夹至少有一个具有角色的 `Owner` 成员。 因此，管理员无法从专用文件夹中删除所有所有者成员。 但是，要从专用文件夹中删除现有所有者（以及管理员本身），管理员必须将其他用户添加为所有者。

1. 单击&#x200B;**[!UICONTROL 保存]**。Depending on the role you assign, the user is assigned a set of privileges on your private folder when the user logs in to [!DNL Assets].
1. 单击&#x200B;**[!UICONTROL 确定]**&#x200B;以关闭确认消息。
1. 您向用户共享文件夹时，用户会收到共享通知。使用用 [!DNL Assets] 户的凭据登录以视图通知。

   ![chlimage_1-416](assets/chlimage_1-416.png)

1. 单击 [!UICONTROL “通知] ”以打开通知列表。

   ![通知列表](assets/Assets-Notification.png)

1. 单击管理员共享的专用文件夹条目以打开该文件夹。

>[!NOTE]
>
>要创建专用文件夹，您需要对要创建专用文件夹 [的父级](/help/sites-administering/security.md#permissions-in-aem) 文件夹具有“读取”和“修改”访问控制权限。 如果您不是管理员，则默认情况下不会为您启用这些权限 `/content/dam`。 在这种情况下，首先获得用户ID/组的这些权限，然后再尝试创建专用文件夹。

## 删除专用文件夹 {#delete-private-folder}

您可以通过选择文件夹并从顶部菜单中选择“ [!UICONTROL 删除] ”选项，或使用键盘上的Backspace键来删除文件夹。

![顶部菜单中的删除选项](assets/delete-option.png)

>[!CAUTION]
>
>如果从CRXDE Lite中删除专用文件夹，则会在存储库中保留冗余用户组。

>[!NOTE]
>
>如果使用上述方法从用户界面删除文件夹，则关联的用户组也会被删除。
>
>但是，可以使用创作实例()中JMX中的方法，将现有的冗余、未使 `clean` 用和自动生成的用户组从存储库中`http://[server]:[port]/system/console/jmx/com.day.cq.dam.core.impl.team%3Atype%3DClean+redundant+groups+for+Assets`删除。
