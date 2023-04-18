---
title: 定位您的Adobe Campaign
description: 设置分段后，您可以为Adobe Campaign创建目标体验。
uuid: 8fcc9210-d8c5-44e3-8aa8-6c6db810c98e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
discoiquuid: f1cb5e98-ccd1-4b2c-acca-2b3cc1b7ac5f
exl-id: fc6fccba-41c5-4c13-aac0-b4ef67767abe
source-git-commit: f4b6eb2ded17ec641f23a1fc3b977ce77169c8a1
workflow-type: tm+mt
source-wordcount: '811'
ht-degree: 0%

---

# 定位Adobe Campaign{#targeting-your-adobe-campaign}

要定位Adobe Campaign新闻稿，您需要先设置分段，该分段仅在经典UI中可用（对于客户端上下文）。 之后，您便可以为Adobe Campaign创建定位体验。 本节将介绍这两种方法。

## 在AEM中设置分段 {#setting-up-segmentation-in-aem}

要设置分段，您需要使用经典UI来设置区段。 其余步骤可在标准UI中执行。

设置分段包括创建区段、品牌、营销活动和体验。

>[!NOTE]
>
>区段ID需要映射到Adobe Campaign端的区段ID。

### 创建区段 {#creating-segments}

要创建区段，请执行以下操作：

1. 打开 [分段控制台](http://localhost:4502/miscadmin#/etc/segmentation) at **&lt;host>:&lt;port>/miscadmin#/etc/segmentation**.
1. 创建新页面并输入标题 — 例如， **交流区段** — 并选择 **区段(Adobe Campaign)** 模板。
1. 在左侧的树视图中选择已创建的页面。
1. 通过在您创建的名为Male的区段下创建新页面，然后选择 **区段(Adobe Campaign)** 模板。
1. 打开创建的区段页面，并拖放 **区段ID** 从sidekick转到页面。
1. 双击该特征，输入表示在此示例中定义的男性区段的ID — 例如， **男**  — 单击 **确定**. 应会显示以下消息： *`targetData.segmentCode == "MALE"`*
1. 对另一个区段重复执行这些步骤，例如，针对女性用户的区段。

### 创建品牌 {#creating-a-brand}

要创建品牌，请执行以下操作：

1. 在 **站点**，导航到 **促销活动** 文件夹（例如，在We.Retail中）。
1. 单击 **创建页面** ，然后为页面输入标题（例如We.Retail Brand），然后选择 **品牌** 模板。

### 创建活动 {#creating-a-campaign}

要创建营销活动，请执行以下操作：

1. 打开 **品牌** 页面。
1. 单击 **创建页面** 并为您的页面输入标题（例如， We.Retail Campaign），然后选择 **Campaign** 模板，单击 **创建**.

### 创建体验 {#creating-experiences}

要为区段创建体验，请执行以下操作：

1. 打开 **Campaign** 页面。
1. 通过单击 **创建页面** 并为页面输入标题（例如，当您为“男性”区段创建体验时），然后选择 **体验** 模板。
1. 打开创建的体验页面。
1. 单击 **编辑**，然后在区段下单击 **添加项目**.
1. 例如，输入男区段的路径 **/etc/segmentation/ac-segments/male** 单击 **确定**. 应会显示以下消息： *体验的目标：男*
1. 重复上述步骤以为所有区段（例如女性目标）创建体验。

## 创建包含目标内容的新闻稿 {#creating-a-newsletter-with-targeted-content}

创建区段、品牌、营销活动和体验后，即可创建包含目标内容的新闻稿。 创建体验后，您可以将体验关联到您的区段。

>[!NOTE]
>
>[电子邮件示例仅在Geometrixx中可用](/help/sites-developing/we-retail.md). 请从包共享下载示例Geometrixx内容。

要创建包含目标内容的新闻稿，请执行以下操作：

1. 创建包含目标内容的新闻稿：在Geometrixx Outdoors中的“电子邮件促销活动”下方，单击或点按 **创建** > **页面**，然后选择其中一个Adobe Campaign邮件模板。

   ![chlimage_1-188](assets/chlimage_1-188.png)

1. 在新闻稿中，添加文本和个性化组件。
1. 在文本与个性化组件中添加文本，如“这是默认设置”。
1. 单击旁边的箭头 **编辑** 选择 **定位**.
1. 从“品牌”下拉菜单中选择您的品牌，然后选择您的营销活动。 （这是您之前创建的品牌和营销活动）。
1. 单击 **开始定位**. 您会看到您的区段显示在受众区域。 如果定义的区段均不匹配，则使用默认体验。

   >[!NOTE]
   >
   >默认情况下，AEM随附的电子邮件示例使用Adobe Campaign作为定位引擎。 对于自定义新闻稿，您可能需要选择Adobe Campaign作为定位引擎。 定位时，点按或单击工具栏中的+，为新活动输入标题，然后选择 **Adobe Campaign** 作为定位引擎。

1. 单击 **默认** 然后，再选择添加的文本与个性化组件，您会看到带有箭头的靶心图标。 单击图标以定位此组件。

   ![chlimage_1-189](assets/chlimage_1-189.png)

1. 导航到另一个区段(Male)，然后单击 **添加选件** 并单击加号图标+。 然后编辑选件。
1. 导航到另一个区段(Female)，然后单击 **添加选件** 和加号图标+。 然后编辑此选件。
1. 单击 **下一个** 要查看映射，请单击 **下一个** 要查看不适用于Adobe Campaign的设置，请单击 **保存**.

   当内容用于Adobe Campaign内的投放时，AEM会自动为Adobe Campaign生成正确的定位代码

1. 在Adobe Campaign中，创建投放 — 选择 **包含AEM内容的电子邮件投放** 并选择本地AEM帐户，然后确认更改。

   在“HTML”视图中，目标组件的不同体验都包含在Adobe Campaign定位代码中。

   ![chlimage_1-190](assets/chlimage_1-190.png)

   >[!NOTE]
   >
   >如果还在Adobe Campaign中设置区段，请单击 **预览** 将显示每个区段的体验。
