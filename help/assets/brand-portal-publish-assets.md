---
title: 将资产发布到 Brand Portal
seo-title: Publish assets to Brand Portal
description: 了解如何将资产发布和取消发布到Brand Portal。
seo-description: Learn how to publish and unpublish assets to Brand Portal.
uuid: 350beb85-c0fb-4a1c-8597-c03592c02d3d
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: brand-portal
content-type: reference
discoiquuid: 39b8cf9b-afec-4c9a-8a5d-7fc87e643f26
docset: aem65
feature: Brand Portal
role: User
exl-id: 76652a16-cad6-4e95-9e66-41efec452b03
source-git-commit: 9d5440747428830a3aae732bec47d42375777efd
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 42%

---

# 将资产发布到 Brand Portal {#publish-assets-to-brand-portal}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/brand-portal/publish-to-brand-portal.html?lang=en) |
| AEM 6.5 | 本文 |
| AEM 6.4 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-64/assets/brandportal/brand-portal-publish-assets.html?lang=en) |

作为Adobe Experience Manager(AEM)Assets管理员，您可以将资产和文件夹发布到您组织的AEM Assets Brand Portal实例（或将发布工作流安排到稍后的日期/时间）。 但是，您必须首先使用 Brand Portal 配置 AEM Assets。有关详细信息，请参阅[使用 Brand Portal 配置 AEM Assets](/help/assets/configure-aem-assets-with-brand-portal.md)。

复制成功后，您可以将资产、文件夹和收藏集发布到Brand Portal。 要将资产发布到Brand Portal，请执行以下步骤：

>[!NOTE]
>
>Adobe 建议实施错峰发布，最好在非高峰时段发布，这样 AEM 作者就不会占用过多的资源。

1. 从资产控制台中，选择要发布的资产/文件夹，然后单击 **[!UICONTROL 快速发布]** 选项。

   或者，选择要发布到Brand Portal的资产。

   ![publish2bp-2](assets/publish2bp.png)

1. 要将资产发布到Brand Portal，可使用以下两个选项：
   * [立即发布资产](#publish-to-bp-now)
   * [稍后发布资产](#publish-to-bp-now)

## 立即发布资产 {#publish-to-bp-now}

要将选定资产发布到 Brand Portal，请执行以下任一操作：

* 在工具栏中，选择&#x200B;**[!UICONTROL 快速发布]**。然后，从菜单中，选择 **[!UICONTROL 发布到Brand Portal]**.

* 在工具栏中，选择&#x200B;**[!UICONTROL 管理发布]**。

   1. 然后，从 **[!UICONTROL 操作]** 选择 **[!UICONTROL 发布到Brand Portal]**，从 **[!UICONTROL 计划]** 选择 **[!UICONTROL 现在]**. 单击&#x200B;**[!UICONTROL 下一步]**。

   2. 在 **[!UICONTROL 范围]**，确认您的选择，然后单击 **[!UICONTROL 发布到Brand Portal]**.

此时将显示一条消息，表明资产已排队等候发布到 Brand Portal。登录到 Brand Portal 界面可查看已发布的资产。

## 稍后发布资产 {#publish-to-bp-later}

要计划在稍后的日期或时间将资产发布到 Brand Portal，请执行以下操作：

1. 选择要发布的资产/文件夹后，请选择 **[!UICONTROL 管理发布]** 工具栏。

1. 开 **[!UICONTROL 管理发布]** 页面，选择 **[!UICONTROL 发布到Brand Portal]** 从 **[!UICONTROL 操作]** 选择 **[!UICONTROL 稍后]** 从 **[!UICONTROL 计划]**.

   ![publishlaterbp-1](assets/publishlaterbp-1.png)

1. 选择&#x200B;**[!UICONTROL 激活日期]**，并指定时间。单击&#x200B;**[!UICONTROL 下一步]**。

1. 选择&#x200B;**激活日期**，并指定时间。单击&#x200B;**下一步**。

1. 在&#x200B;**[!UICONTROL 工作流]**&#x200B;中指定&#x200B;**[!UICONTROL 工作流标题]**。单击&#x200B;**[!UICONTROL 稍后发布]**。

   ![publishworkflow](assets/publishworkflow.png)

现在，登录Brand Portal ，查看已发布的资产在Brand Portal界面上是否可用。

![bp_landingpage](assets/bp_landingpage.png)
