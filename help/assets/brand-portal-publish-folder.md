---
title: 将文件夹发布到Brand Portal
description: 了解如何将文件夹发布和取消发布到Brand Portal。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: brand-portal
content-type: reference
docset: aem65
feature: Brand Portal
role: User
exl-id: 92a156f0-ce2a-4c83-bd57-0c29efbf784f
source-git-commit: 04050f31742c926b45235595f6318929d3767bd8
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 34%

---

# 将文件夹发布到Brand Portal{#publish-folders-to-brand-portal}

作为Adobe Experience Manager (AEM) Assets管理员，您可以将资产和文件夹发布到AEM Assets Brand Portal实例（或安排在稍后的日期/时间执行发布工作流）。 但是，您必须首先将AEM Assets与Brand Portal集成。 有关详细信息，请参阅[使用 Brand Portal 配置 AEM Assets](/help/assets/configure-aem-assets-with-brand-portal.md)。

发布资源或文件夹后，Brand Portal中的用户即可使用该资源或文件夹。

如果您随后在AEM Assets中对原始资源或文件夹进行了修改，则在重新发布该资源或文件夹之前，这些更改不会反映在Brand Portal中。 此功能可确保在 Brand Portal 中不会出现进行中的更改。只有管理员发布的已批准更改才会出现在 Brand Portal 中。

## 将文件夹发布到Brand Portal {#publish-folders-to-brand-portal-1}

1. 在AEM Assets界面中，将鼠标悬停在所需文件夹上并选择 **Publish** 选项。

   或者，选择所需的文件夹，然后执行其他步骤。

   ![publish2bp](assets/publish2bp.png)

1. **立即发布文件夹**

   要将选定文件夹发布到 Brand Portal，请执行以下任一操作：

   * 在工具栏中，选择&#x200B;**快速发布**。然后从菜单中选择 **发布到Brand Portal**.

   * 在工具栏中，选择&#x200B;**管理发布**。

   1. 从 **操作** 选择 **发布到Brand Portal**，从 **正在计划** 选择 **现在**，然后单击 **下一个。**
   1. 在&#x200B;**范围**&#x200B;中确认您的选择，然后单击&#x200B;**发布到 Brand Portal**。

   此时将显示一条消息，表明文件夹已排队等候发布到 Brand Portal。登录到Brand Portal界面可查看已发布的文件夹。

   **稍后发布文件夹**

   要计划在稍后的日期或时间发布到Brand Portal资源文件夹工作流，请执行以下操作：

   1. 选择要发布的资产/文件夹后，选择 **管理发布** 从顶部的工具栏删除。
   1. 从 **操作** 选择 **发布到Brand Portal**，从 **正在计划** 选择 **稍后**.

      ![publishlaterbp](assets/publishlaterbp.png)

   1. 选择&#x200B;**激活日期**，并指定时间。单击&#x200B;**下一步**。
   1. 在&#x200B;**范围**&#x200B;中确认您的选择。单击&#x200B;**下一步**。
   1. 在&#x200B;**工作流**&#x200B;下指定工作流标题。单击&#x200B;**稍后发布**。

      ![manageschedulepub](assets/manageschedulepub.png)

## 从Brand Portal取消发布文件夹 {#unpublish-folders-from-brand-portal}

您可以通过从AEM创作实例中取消发布已发布到Brand Portal的任何资源文件夹，来删除该文件夹。 取消发布原始文件夹后，Brand Portal 用户将无法再使用其副本。

您可以选择快速从Brand Portal中取消发布文件夹，或安排在以后的日期和时间取消发布。 要从 Brand Portal 取消发布资产文件夹，请执行以下操作：

1. 在AEM Author实例的AEM Assets界面中，选择要取消发布的文件夹。

   ![publish2bp-1](assets/publish2bp.png)

1. 在工具栏中，单击 **管理发布**.

1. **立即从Brand Portal取消发布**

   要快速从Brand Portal中取消发布所需的文件夹，请执行以下操作：

   1. 在工具栏中，选择&#x200B;**管理发布**。
   1. 从 **操作** 选择 **从Brand Portal取消发布**，从 **正在计划** 选择 **现在**，然后单击 **下一个。**
   1. 在&#x200B;**范围**&#x200B;中确认您的选择，然后单击&#x200B;**从 Brand Portal 取消发布**。

   ![confirm-unpublish](assets/confirm-unpublish.png)

   **稍后从Brand Portal取消发布**

   要计划在稍后的日期和时间发布Brand Portal中的文件夹，请执行以下操作：

   1. 在工具栏中，选择&#x200B;**管理发布**。
   1. 从 **操作** 选择 **从Brand Portal取消发布**、和从 **正在计划** 选择 **稍后**.
   1. 选择&#x200B;**激活日期**，并指定时间。单击&#x200B;**下一步**。
   1. 在&#x200B;**范围**&#x200B;中确认您的选择，然后单击&#x200B;**下一步**。
   1. 在&#x200B;**工作流**&#x200B;中指定&#x200B;**工作流标题**。单击 **稍后取消发布。**

      ![unpublishworkflows](assets/unpublishworkflows.png)

>[!NOTE]
>
>将资源发布到Brand Portal以及从取消发布资源的过程与文件夹的相应过程类似。
