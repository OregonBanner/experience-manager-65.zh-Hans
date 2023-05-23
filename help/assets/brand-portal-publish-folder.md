---
title: 将文件夹发布到 Brand Portal
seo-title: Publish folders to Brand Portal
description: 瞭解如何將資料夾發佈和取消發佈至Brand Portal。
seo-description: Learn how to publish and unpublish folders to Brand Portal.
uuid: 350beb85-c0fb-4a1c-8597-c03592c02d3d
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: brand-portal
content-type: reference
discoiquuid: 39b8cf9b-afec-4c9a-8a5d-7fc87e643f26
docset: aem65
feature: Brand Portal
role: User
exl-id: 92a156f0-ce2a-4c83-bd57-0c29efbf784f
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '566'
ht-degree: 38%

---

# 将文件夹发布到 Brand Portal{#publish-folders-to-brand-portal}

身為Adobe Experience Manager (AEM) Assets管理員，您可以將資產和資料夾發佈到AEM Assets Brand Portal執行個體（或將發佈工作流程排程到更晚的日期/時間）。 不過，您必須先整合AEM Assets與Brand Portal。 有关详细信息，请参阅[使用 Brand Portal 配置 AEM Assets](/help/assets/configure-aem-assets-with-brand-portal.md)。

發佈資產或資料夾後，Brand Portal中的使用者即可使用該資產或資料夾。

如果您後續修改AEM Assets中的原始資產或資料夾，則在您重新發佈資產或資料夾之前，這些變更不會反映在Brand Portal中。 此功能可确保在 Brand Portal 中不会出现进行中的更改。只有管理员发布的已批准更改才会出现在 Brand Portal 中。

## 将文件夹发布到 Brand Portal {#publish-folders-to-brand-portal-1}

1. 在AEM Assets介面中，暫留在所需的資料夾上並選取 **發佈** 快速動作中的選項。

   或者，選取所需的資料夾，然後遵循進一步的步驟操作。

   ![publish2bp](assets/publish2bp.png)

1. **立即发布文件夹**

   要将选定文件夹发布到 Brand Portal，请执行以下任一操作：

   * 在工具栏中，选择&#x200B;**快速发布**。然後從功能表中選取 **發佈至Brand Portal**.

   * 在工具栏中，选择&#x200B;**管理发布**。
   1. 從 **動作** 選取 **發佈至Brand Portal**，從 **排程** 選取 **現在**，然後按一下 **下一個。**
   1. 在&#x200B;**范围**&#x200B;中确认您的选择，然后单击&#x200B;**发布到 Brand Portal**。

   此时将显示一条消息，表明文件夹已排队等候发布到 Brand Portal。登入Brand Portal介面可檢視已發佈的資料夾。

   **稍后发布文件夹**

   若要將資產資料夾的發佈至Brand Portal工作流程排程在之後的日期或時間：

   1. 選取要發佈的資產/資料夾後，請選取 **管理發布** 從頂端的工具列取得。
   1. 從 **動作** 選取 **發佈至Brand Portal**，從 **排程** 選取 **稍後**.

      ![publishlaterbp](assets/publishlaterbp.png)

   1. 选择&#x200B;**激活日期**，并指定时间。单击&#x200B;**下一步**。
   1. 在&#x200B;**范围**&#x200B;中确认您的选择。单击&#x200B;**下一步**。
   1. 在&#x200B;**工作流**&#x200B;下指定工作流标题。单击&#x200B;**稍后发布**。

      ![manageschedulepub](assets/manageschedulepub.png)



## 从 Brand Portal 取消发布文件夹 {#unpublish-folders-from-brand-portal}

您可以從AEM作者例項中透過取消發佈來移除任何已發佈至Brand Portal的資產資料夾。 取消发布原始文件夹后，Brand Portal 用户将无法再使用其副本。

您可以選擇快速從Brand Portal取消發佈資料夾，或將其排程在之後的日期和時間。 要从 Brand Portal 取消发布资产文件夹，请执行以下操作：

1. 從AEM Author例項的AEM Assets介面中，選取您要取消發佈的資料夾。

   ![publish2bp-1](assets/publish2bp.png)

1. 在工具列中，按一下 **管理發布**.

1. **立即從Brand Portal取消發佈**

   若要從Brand Portal快速取消發佈所需的資料夾：

   1. 在工具栏中，选择&#x200B;**管理发布**。
   1. 從 **動作** 選取 **從Brand Portal取消發佈**，從 **排程** 選取 **現在**，然後按一下 **下一個。**
   1. 在&#x200B;**范围**&#x200B;中确认您的选择，然后单击&#x200B;**从 Brand Portal 取消发布**。

   ![confirm-unpublish](assets/confirm-unpublish.png)

   **稍後從Brand Portal取消發佈**

   若要將資料夾從Brand Portal發佈到更晚的日期和時間，請執行下列動作：

   1. 在工具栏中，选择&#x200B;**管理发布**。
   1. 從 **動作** 選取 **從Brand Portal取消發佈**、和從 **排程** 選取 **稍後**.
   1. 选择&#x200B;**激活日期**，并指定时间。单击&#x200B;**下一步**。
   1. 在&#x200B;**范围**&#x200B;中确认您的选择，然后单击&#x200B;**下一步**。
   1. 在&#x200B;**工作流**&#x200B;中指定&#x200B;**工作流标题**。按一下 **稍後取消發佈。**

      ![unpublishworkflows](assets/unpublishworkflows.png)


>[!NOTE]
>
>將資產發佈/取消發佈至/自Brand Portal的程式，與資料夾的對應程式類似。
