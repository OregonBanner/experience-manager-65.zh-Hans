---
title: 将资产发布到 Brand Portal
seo-title: Publish assets to Brand Portal
description: 瞭解如何將資產發佈和取消發佈到Brand Portal。
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
hide: true
source-git-commit: 3d5e9ad8ee19756b05e5a77a3f748bc647fcf734
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 46%

---

# 将资产发布到 Brand Portal {#publish-assets-to-brand-portal}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/brand-portal/publish-to-brand-portal.html?lang=zh-Hans) |
| AEM 6.5 | 本文 |

身為Adobe Experience Manager (AEM) Assets管理員，您可以將資產和資料夾發佈到AEM Assets Brand Portal執行個體（或將發佈工作流程排程到更晚的日期/時間）。 但是，您必须首先使用 Brand Portal 配置 AEM Assets。有关详细信息，请参阅[使用 Brand Portal 配置 AEM Assets](/help/assets/configure-aem-assets-with-brand-portal.md)。

複製成功後，您可以將資產、資料夾和集合發佈到Brand Portal。 若要將資產發佈至Brand Portal，請遵循下列步驟：

>[!NOTE]
>
>Adobe 建议实施错峰发布，最好在非高峰时段发布，这样 AEM 作者就不会占用过多的资源。

1. 在「資產」控制檯中，選取您要發佈的資產/資料夾，然後按一下 **[!UICONTROL 快速發佈]** 工具列中的選項。

   或者，選取您要發佈至Brand Portal的資產。

   ![publish2bp-2](assets/publish2bp.png)

1. 若要將資產發佈至Brand Portal，可使用下列兩個選項：
   * [立即發佈資產](#publish-to-bp-now)
   * [稍后发布资产](#publish-to-bp-now)

## 立即发布资产 {#publish-to-bp-now}

要将选定资产发布到 Brand Portal，请执行以下任一操作：

* 在工具栏中，选择&#x200B;**[!UICONTROL 快速发布]**。然後從功能表中選取 **[!UICONTROL 發佈至Brand Portal]**.

* 在工具栏中，选择&#x200B;**[!UICONTROL 管理发布]**。

   1. 然後從 **[!UICONTROL 動作]** 選取 **[!UICONTROL 發佈至Brand Portal]**、和從 **[!UICONTROL 排程]** 選取 **[!UICONTROL 現在]**. 单击&#x200B;**[!UICONTROL 下一步]**。

   2. 範圍 **[!UICONTROL 範圍]**，確認您的選取專案並按一下 **[!UICONTROL 發佈至Brand Portal]**.

此时将显示一条消息，表明资产已排队等候发布到 Brand Portal。登录到 Brand Portal 界面可查看已发布的资产。

## 稍后发布资产 {#publish-to-bp-later}

要计划在稍后的日期或时间将资产发布到 Brand Portal，请执行以下操作：

1. 選取要發佈的資產/資料夾後，請選取 **[!UICONTROL 管理發布]** 從頂端的工具列取得。

1. 開啟 **[!UICONTROL 管理發布]** 頁面，選取 **[!UICONTROL 發佈至Brand Portal]** 從 **[!UICONTROL 動作]** 並選取 **[!UICONTROL 稍後]** 從 **[!UICONTROL 排程]**.

   ![publishlaterbp-1](assets/publishlaterbp-1.png)

1. 选择&#x200B;**[!UICONTROL 激活日期]**，并指定时间。单击&#x200B;**[!UICONTROL 下一步]**。

1. 选择&#x200B;**激活日期**，并指定时间。单击&#x200B;**下一步**。

1. 在&#x200B;**[!UICONTROL 工作流]**&#x200B;中指定&#x200B;**[!UICONTROL 工作流标题]**。单击&#x200B;**[!UICONTROL 稍后发布]**。

   ![publishworkflow](assets/publishworkflow.png)

現在，請登入Brand Portal以檢視已發佈的資產是否可在Brand Portal介面上使用。

![bp_landingpage](assets/bp_landingpage.png)
