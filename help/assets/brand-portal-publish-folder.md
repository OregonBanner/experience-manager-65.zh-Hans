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
feature: Brand Portal
role: Business Practitioner
exl-id: 92a156f0-ce2a-4c83-bd57-0c29efbf784f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 38%

---

# 将文件夹发布到 Brand Portal{#publish-folders-to-brand-portal}

作为Adobe Experience Manager(AEM)Assets管理员，您可以将资产和文件夹发布到您组织的AEM Assets Brand Portal实例（或将发布工作流安排到稍后的日期/时间）。 但是，您必须先将AEM Assets与Brand Portal集成。 有关详细信息，请参阅[使用 Brand Portal 配置 AEM Assets](/help/assets/configure-aem-assets-with-brand-portal.md)。

发布资产或文件夹后，Brand Portal中的用户便可以使用该资产或文件夹。

如果您随后在AEM Assets中对原始资产或文件夹进行了修改，则在重新发布该资产或文件夹之前，所做的更改不会反映在Brand Portal中。 此功能可确保在 Brand Portal 中不会出现进行中的更改。只有管理员发布的已批准更改才会出现在 Brand Portal 中。

## 将文件夹发布到 Brand Portal{#publish-folders-to-brand-portal-1}

1. 在AEM Assets界面中，将鼠标悬停在所需的文件夹上，然后从快速操作中选择&#x200B;**发布**&#x200B;选项。

   或者，选择所需的文件夹并执行进一步的步骤。

   ![publish2bp](assets/publish2bp.png)

1. **立即发布文件夹**

   要将选定文件夹发布到 Brand Portal，请执行以下任一操作：

   * 在工具栏中，选择&#x200B;**快速发布**。然后，从菜单中选择&#x200B;**发布到Brand Portal**。

   * 在工具栏中，选择&#x200B;**管理发布**。
   1. 从&#x200B;**Action**&#x200B;中，选择&#x200B;**发布到Brand Portal**，从&#x200B;**Scheduling**&#x200B;中，选择&#x200B;**Now**，然后单击&#x200B;**Next。**
   1. 在&#x200B;**范围**&#x200B;中确认您的选择，然后单击&#x200B;**发布到 Brand Portal**。

   此时将显示一条消息，表明文件夹已排队等候发布到 Brand Portal。登录到Brand Portal界面以查看已发布的文件夹。

   **稍后发布文件夹**

   要计划在稍后的日期或时间将资产文件夹发布到Brand Portal工作流，请执行以下操作：

   1. 选择要发布的资产/文件夹后，从顶部工具栏中选择&#x200B;**管理发布** 。
   1. 从&#x200B;**Action**&#x200B;中，选择&#x200B;**发布到Brand Portal**，从&#x200B;**Scheduling**&#x200B;中，选择&#x200B;**Later**。

      ![publishlaterbp](assets/publishlaterbp.png)

   1. 选择&#x200B;**激活日期**，并指定时间。单击&#x200B;**下一步**。
   1. 在&#x200B;**范围**&#x200B;中确认您的选择。单击&#x200B;**下一步**。
   1. 在&#x200B;**工作流**&#x200B;下指定工作流标题。单击&#x200B;**稍后发布**。

      ![manageschedulepub](assets/manageschedulepub.png)



## 从 Brand Portal 取消发布文件夹{#unpublish-folders-from-brand-portal}

您可以通过从AEM创作实例中取消发布已发布到Brand Portal的任何资产文件夹，来删除该文件夹。 取消发布原始文件夹后，Brand Portal 用户将无法再使用其副本。

您可以选择快速从Brand Portal中取消发布文件夹，或安排在稍后的日期和时间取消发布文件夹。 要从 Brand Portal 取消发布资产文件夹，请执行以下操作：

1. 从AEM创作实例的AEM Assets界面中，选择要取消发布的文件夹。

   ![publish2bp-1](assets/publish2bp.png)

1. 在工具栏中，单击&#x200B;**管理发布**。

1. **立即从Brand Portal取消发布**

   要快速从Brand Portal中取消发布所需的文件夹，请执行以下操作：

   1. 在工具栏中，选择&#x200B;**管理发布**。
   1. 从&#x200B;**Action**&#x200B;中，选择&#x200B;**从Brand Portal取消发布**，从&#x200B;**Scheduling**&#x200B;中，选择&#x200B;**Now**，然后单击&#x200B;**Next.**
   1. 在&#x200B;**范围**&#x200B;中确认您的选择，然后单击&#x200B;**从 Brand Portal 取消发布**。

   ![confirm-unpublish](assets/confirm-unpublish.png)

   **稍后从Brand Portal取消发布**

   要计划将文件夹从Brand Portal发布到稍后的日期和时间，请执行以下操作：

   1. 在工具栏中，选择&#x200B;**管理发布**。
   1. 从&#x200B;**Action**&#x200B;中，选择&#x200B;**从Brand Portal**&#x200B;取消发布，从&#x200B;**Scheduling**&#x200B;中，选择&#x200B;**Later**。
   1. 选择&#x200B;**激活日期**，并指定时间。单击&#x200B;**下一步**。
   1. 在&#x200B;**范围**&#x200B;中确认您的选择，然后单击&#x200B;**下一步**。
   1. 在&#x200B;**工作流**&#x200B;中指定&#x200B;**工作流标题**。单击&#x200B;**稍后取消发布。**

      ![unpublishworkflows](assets/unpublishworkflows.png)


>[!NOTE]
>
>向Brand Portal发布/取消发布资产的过程与文件夹的相应过程类似。
