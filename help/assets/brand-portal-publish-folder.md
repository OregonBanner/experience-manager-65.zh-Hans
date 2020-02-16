---
title: 将文件夹发布到Brand Portal
seo-title: 将文件夹发布到Brand Portal
description: 了解如何将文件夹发布和取消发布到Brand Portal。
seo-description: 了解如何将文件夹发布和取消发布到Brand Portal。
uuid: 350beb85-c0fb-4a1c-8597-c03592c02d3d
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: brand-portal
content-type: reference
discoiquuid: 39b8cf9b-afec-4c9a-8a5d-7fc87e643f26
docset: aem65
translation-type: tm+mt
source-git-commit: 9c73abc3291f2847c705cb649d2993fb186b0993

---


# Publish folders to Brand Portal{#publish-folders-to-brand-portal}

作为Adobe Experience Manager(AEM)资产管理员，您可以将资产和文件夹发布到AEM Assets Brand Portal实例（或将发布工作流计划到以后的日期／时间）。 但是，您必须先将AEM资产与Brand Portal集成。 有关详细信息，请参 [阅配置AEM资产与Brand Portal的集成](/help/assets/brand-portal-configuring-integration.md)。

发布资产或文件夹后，该资产或文件夹便可供Brand Portal中的用户使用。

如果您随后在AEM资产中对原始资产或文件夹进行了修改，则在重新发布资产或文件夹之前，这些更改不会反映在Brand Portal中。 此功能可确保在Brand Portal中不提供进行中的更改。 只有管理员发布的已批准更改才可在Brand Portal中使用。

## Publish folders to Brand Portal {#publish-folders-to-brand-portal-1}

1. 在AEM资产界面中，将指针悬停在所需的文件夹上，然后从快速操 **作中选择** “发布”选项。

   或者，选择所需的文件夹，然后执行后续步骤。

   ![publish2bp](assets/publish2bp.png)

1. **立即发布文件夹**

   要将选定文件夹发布到Brand Portal，请执行以下任一操作：

   * 从工具栏中，选择“快 **速发布”**。 然后从菜单中，选择 **发布到Brand Portal**。

   * 从工具栏中，选择管 **理发布**。
   1. 从“ **From** **Sect** Publish to Brand Portal **”中，从“Scheduling** Now **”中选择“发布到****Brand Portal”，然后单击“下一步”。**
   1. 在范围中确认您的 **选择** ，然后单 **击发布到Brand Portal**。
   将显示一条消息，指明文件夹已排队等候发布到Brand Portal。 登录到Brand Portal界面，查看已发布的文件夹。

   **稍后发布文件夹**

   要将资产文件夹的发布计划到Brand Portal工作流程，请在以后的日期或时间执行以下操作：

   1. 选择要发布的资产／文件夹后，从顶 **部的工具栏中选择** “管理发布”。
   1. 从“操 **作** ”中，选 **择“发布到品牌门户**”，从“计划” **中选择** “ ****&#x200B;稍后发布”。

      ![publishlaterbp](assets/publishlaterbp.png)

   1. 选择激 **活日期** ，然后指定时间。 单击&#x200B;**下一步**。
   1. 在范围中确认您 **的选择**。 单击&#x200B;**下一步**。
   1. 在“工作流”下指定工作流 **标题**。 单击“ **稍后发布**”。

      ![manageschedulepub](assets/manageschedulepub.png)



## Unpublish folders from Brand Portal {#unpublish-folders-from-brand-portal}

您可以通过从AEM作者实例中取消发布已发布到Brand Portal的任何资产文件夹，来删除该文件夹。 取消发布原始文件夹后，Brand Portal用户将无法再使用其副本。

您可以选择快速从Brand Portal中取消发布文件夹，或将其安排在以后的日期和时间。 要从Brand Portal取消发布资产文件夹，请执行以下操作：

1. 从AEM作者实例的AEM资产界面中，选择要取消发布的文件夹。

   ![publish2bp-1](assets/publish2bp.png)

1. 在工具栏中，单击“管 **理发布”**。

1. **立即从Brand Portal中取消发布**

   要从Brand Portal快速取消发布所需的文件夹，请执行以下操作：

   1. 从工具栏中，选择管 **理发布**。
   1. 从“ **操作** ”中，选 **择“从Brand Portal取消发布**”，从“计划”中， **现在选择Action** ******And Portal单击Next Portal。**
   1. 在范围中确认您的选 **择** ，然后单 **击从Brand Portal取消发布**。
   ![确认——取消发布](assets/confirm-unpublish.png)

   **稍后从Brand Portal中取消发布**

   要将文件夹从Brand Portal发布到以后的日期和时间，请执行以下操作：

   1. 从工具栏中，选择管 **理发布**。
   1. 从“ **From** Brand **Portal**”中选择“Unpublish” **，从“Scheduling** ”中选择“ **** LaterAler”。
   1. 选择激 **活日期** ，然后指定时间。 单击&#x200B;**下一步**。
   1. 在范围中确认您的选 **择** ，然后单击 **下一步**。
   1. 在工作流 **中指定工作流****标题**。 单击“ **稍后取消发布”。**

      ![取消发布工作流](assets/unpublishworkflows.png)


>[!NOTE]
>
>将资产发布到／从Brand Portal取消发布的过程与文件夹的相应过程类似。

