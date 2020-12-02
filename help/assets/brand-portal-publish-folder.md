---
title: 将文件夹发布到 Brand Portal
seo-title: 将文件夹发布到 Brand Portal
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
source-git-commit: 9f923782d3d0a7bdf45b18e8025bd2d083acf77c
workflow-type: tm+mt
source-wordcount: '581'
ht-degree: 38%

---


# 将文件夹发布到 Brand Portal{#publish-folders-to-brand-portal}

作为Adobe Experience Manager(AEM)资产管理员，您可以将资产和文件夹发布到您组织的AEM Assets品牌门户实例(或将发布工作流计划到以后的日期／时间)。 但是，您必须首先将AEM Assets与Brand Portal集成。 有关详细信息，请参阅[使用 Brand Portal 配置 AEM Assets](/help/assets/configure-aem-assets-with-brand-portal.md)。

发布资产或文件夹后，Brand Portal中的用户便可使用该资产或文件夹。

如果您随后对AEM Assets的原始资产或文件夹进行了修改，则在您重新发布资产或文件夹之前，这些更改不会反映在Brand Portal中。 此功能可确保在 Brand Portal 中不会出现进行中的更改。只有管理员发布的已批准更改才会出现在 Brand Portal 中。

## 将文件夹发布到 Brand Portal{#publish-folders-to-brand-portal-1}

1. 从AEM Assets界面，将指针悬停在所需的文件夹上，然后从快速操作中选择&#x200B;**发布**&#x200B;选项。

   或者，选择所需的文件夹，然后执行后续步骤。

   ![publish2bp](assets/publish2bp.png)

1. **立即发布文件夹**

   要将选定文件夹发布到 Brand Portal，请执行以下任一操作：

   * 在工具栏中，选择&#x200B;**快速发布**。然后，从菜单中选择&#x200B;**发布到品牌门户**。

   * 在工具栏中，选择&#x200B;**管理发布**。
   1. 从&#x200B;**操作**&#x200B;选择&#x200B;**发布到品牌门户**，从&#x200B;**计划**&#x200B;选择&#x200B;**Now**，然后单击&#x200B;**下一步。**
   1. 在&#x200B;**范围**&#x200B;中确认您的选择，然后单击&#x200B;**发布到 Brand Portal**。

   此时将显示一条消息，表明文件夹已排队等候发布到 Brand Portal。登录到Brand Portal界面，查看已发布的文件夹。

   **稍后发布文件夹**

   要将资产文件夹的发布计划到Brand Portal工作流，请在以后的日期或时间执行以下操作：

   1. 选择要发布的资产／文件夹后，从顶部的工具栏中选择&#x200B;**管理发布**。
   1. 从&#x200B;**操作**&#x200B;选择&#x200B;**发布到品牌门户**，从&#x200B;**计划**&#x200B;选择&#x200B;**稍后**。

      ![publishlaterbp](assets/publishlaterbp.png)

   1. 选择&#x200B;**激活日期**，并指定时间。单击&#x200B;**下一步**。
   1. 在&#x200B;**范围**&#x200B;中确认您的选择。单击&#x200B;**下一步**。
   1. 在&#x200B;**工作流**&#x200B;下指定工作流标题。单击&#x200B;**稍后发布**。

      ![manageschedulepub](assets/manageschedulepub.png)



## 从 Brand Portal 取消发布文件夹{#unpublish-folders-from-brand-portal}

您可以通过从AEM作者实例中取消发布已发布到Brand Portal的任何资产文件夹，来删除该资产文件夹。 取消发布原始文件夹后，Brand Portal 用户将无法再使用其副本。

您可以选择快速从Brand Portal中取消发布文件夹，或在以后的日期和时间计划它。 要从 Brand Portal 取消发布资产文件夹，请执行以下操作：

1. 从AEM作者实例的AEM Assets界面中，选择要取消发布的文件夹。

   ![publish2bp-1](assets/publish2bp.png)

1. 在工具栏中，单击&#x200B;**管理发布**。

1. **立即从Brand Portal中取消发布**

   要快速从Brand Portal中取消发布所需的文件夹，请执行以下操作：

   1. 在工具栏中，选择&#x200B;**管理发布**。
   1. 从&#x200B;**操作**&#x200B;选择&#x200B;**从品牌门户**&#x200B;取消发布，从&#x200B;**计划**&#x200B;选择&#x200B;**现在**，然后单击&#x200B;**下一步。**
   1. 在&#x200B;**范围**&#x200B;中确认您的选择，然后单击&#x200B;**从 Brand Portal 取消发布**。

   ![confirm-unpublish](assets/confirm-unpublish.png)

   **稍后从Brand Portal中取消发布**

   要将文件夹从Brand Portal发布计划到以后的日期和时间，请执行以下操作：

   1. 在工具栏中，选择&#x200B;**管理发布**。
   1. 从&#x200B;**操作**&#x200B;中，选择&#x200B;**从品牌门户**&#x200B;取消发布，从&#x200B;**计划**&#x200B;中选择&#x200B;**稍后**。
   1. 选择&#x200B;**激活日期**，并指定时间。单击&#x200B;**下一步**。
   1. 在&#x200B;**范围**&#x200B;中确认您的选择，然后单击&#x200B;**下一步**。
   1. 在&#x200B;**工作流**&#x200B;中指定&#x200B;**工作流标题**。单击&#x200B;**稍后取消发布。**

      ![unpublishworkflows](assets/unpublishworkflows.png)


>[!NOTE]
>
>将资产发布／取消发布到／从Brand Portal的过程与文件夹的相应过程类似。

