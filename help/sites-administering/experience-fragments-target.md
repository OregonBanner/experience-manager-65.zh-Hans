---
title: 将体验片段导出到 Adobe Target
description: 将体验片段导出到 Adobe Target
contentOwner: carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
docset: aem65
exl-id: f2921349-de8f-4bc1-afa2-aeace99cfc5c
source-git-commit: fd937341e26edd0c3edfced8e862066ebc30f9a3
workflow-type: tm+mt
source-wordcount: '1533'
ht-degree: 43%

---

# 将体验片段导出到 Adobe Target{#exporting-experience-fragments-to-adobe-target}

>[!CAUTION]
>
>此页面上的某些功能需要应用AEM 6.5.3.0（或更高版本）。
>
>6.5.3.0:
>
>* **Externalizer域** 现在可以选中。
>  **注意：** 外部化器域仅与发送到Target的体验片段的内容相关，与查看选件内容等元数据无关。
>
>6.5.2.0:
>
>* 体验片段可以导出到：
>
>   * 默认工作区。
>   * 在云配置中指定的命名工作区。
>   * **注意：** 导出到特定工作区需要Adobe Target Premium。
>
>* AEM必须 [使用IMS与Adobe Target集成](/help/sites-administering/integration-target-ims.md).
>
>AEM 6.5.0.0和6.5.1.0：
>
>* AEM 体验片段将导出到 Adobe Target 的默认工作区。
>* 必须按照[与 Adobe Target 集成](/help/sites-administering/target.md)下的说明将 AEM 与 Adobe Target 集成。

您可以导出 [体验片段](/help/sites-authoring/experience-fragments.md)，在Adobe Experience Manager (AEM)中创建的，迁移到Adobe Target (Target)。 然后，可以将它们用作Target活动中的选件，以大规模测试和个性化体验。

有三个格式选项可用于将体验片段导出到Adobe Target：

* HTML（默认）：支持 Web 和混合内容交付
* JSON：支持 Headless 内容交付
* HTML 和 JSON

AEM Experience Fragments可以导出到Adobe Target中的默认工作区，也可以导出到Adobe Target的用户定义工作区。 可使用Adobe Developer控制台完成此操作，对于该控制台，AEM必须 [使用IMS与Adobe Target集成](/help/sites-administering/integration-target-ims.md).

>[!NOTE]
>
>Adobe Target 本身没有 Adobe Target 工作区。它们是在Adobe IMS (Identity Management System)中定义和管理的，然后通过Adobe Developer Console中的集成，选择在解决方案间使用。

>[!NOTE]
>
>Adobe Target 工作区可用于允许组织（组）的成员仅为该组织创建和管理选件和活动；不向其他用户授予访问权限。例如，全球关注的国家/地区特定的组织。

>[!NOTE]
>
>有关更多信息，另请参阅：
>
>* [Adobe Target 开发](http://developers.adobetarget.com/)
>* [核心组件 – 体验片段](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/experience-fragment.html)
>

## 前提条件 {#prerequisites}

>[!CAUTION]
>
>本页上的某些功能需要应用AEM 6.5.3.0。

需要执行各种操作：

1. 你必须要 [使用IMS将AEM与Adobe Target集成](/help/sites-administering/integration-target-ims.md).
2. 体验片段将从AEM创作实例中导出，因此您必须 [配置AEM链接外部化器](/help/sites-administering/target-requirements.md#configuring-the-aem-link-externalizer) 在创作实例上，确保体验片段中的任何引用都外部化以进行Web交付。

   >[!NOTE]
   >
   >对于默认情况下未涵盖的链接重写，可以使用[体验片段链接重写器提供程序](/help/sites-developing/experience-fragments.md#the-experience-fragment-link-rewriter-provider-html)。利用它，可以为您的实例开发自定义规则。

## 添加云配置 {#add-the-cloud-configuration}

在导出片段之前，必须添加 **云配置** 对象 **Adobe Target** 到片段或文件夹。 这也使您能够：

* 指定要用于导出的格式选项
* 选择 Target 工作区作为目标
* 选择外部化器域以重写体验片段中的引用（可选）

可以在所需的文件夹和/或片段的&#x200B;**页面属性**&#x200B;中选择所需的选项；将根据需要继承规范。

1. 导航到&#x200B;**体验片段**&#x200B;控制台。

1. 打开相应的文件夹或片段的&#x200B;**页面属性**。

   >[!NOTE]
   >
   >如果将云配置添加到体验片段父文件夹，则该配置将由所有子级继承。
   >
   >
   >如果将云配置添加到体验片段本身，则该配置将由所有变体继承。

1. 选择&#x200B;**云服务**&#x200B;选项卡。

1. 在&#x200B;**云服务配置**&#x200B;下，从下拉列表中选择 **Adobe Target**。

   >[!NOTE]
   >
   >可以自定义体验片段选件的 JSON 格式。为此，请定义一个客户体验片段组件，然后注释如何在组件Sling模型中导出其属性。
   >
   >请参阅核心组件：
   >
   >[核心组件 – 体验片段](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/experience-fragment.html)

   在 **Adobe Target** 下，选择：

   * 相应的配置
   * 所需的格式选项
   * Adobe Target 工作区
   * 如有必要 — Externalizer域

   >[!CAUTION]
   >
   >Externalizer域是可选的。
   >
   >如果您希望导出的内容指向特定的，可以配置AEM外部化器 *发布* 域。 有关更多详细信息，请参阅 [配置AEM链接外部化器](/help/sites-administering/target-requirements.md#configuring-the-aem-link-externalizer).
   >
   >另请注意，外部化器域仅与发送到 Target 的体验片段的内容相关，与查看选件内容等元数据无关。

   例如，对于文件夹：

   ![文件夹 – 云服务](assets/xf-target-integration-01.png "文件夹 – 云服务")

1. **保存并关闭**。

## 将体验片段导出到 Adobe Target {#exporting-an-experience-fragment-to-adobe-target}

>[!CAUTION]
>
>对于媒体资产（例如图像），仅将引用导出到 Target。资产本身仍存储在 AEM Assets 中，并且从 AEM 发布实例进行交付。
>
>因此，在导出到Target之前，必须发布包含所有相关资产的体验片段。

要将体验片段从AEM导出到Target（在指定云配置后），请执行以下操作：

1. 导航到体验片段控制台。
1. 选择要导出到 Target 的体验片段。

   >[!NOTE]
   >
   >它必须是体验片段 Web 变体。

1. 点按/单击&#x200B;**导出到 Adobe Target**。

   >[!NOTE]
   >
   >如果已导出体验片段，请选择&#x200B;**在 Adobe Target 中更新**。

1. 根据需要点按/单击&#x200B;**导出而不发布**&#x200B;或&#x200B;**发布**。

   >[!NOTE]
   >
   >选择 **Publish** 立即发布体验片段并将其发送到Target。

1. 在“确认”对话框中，点按/单击&#x200B;**确定**。

   您的体验片段现在应位于Target中。

   >[!NOTE]
   >
   >可以在控制台的&#x200B;**列表视图**&#x200B;和&#x200B;**属性**&#x200B;中查看导出的[各种详细信息](/help/sites-authoring/experience-fragments.md#details-of-your-experience-fragment)。

   >[!NOTE]
   >
   >在 Adobe Target 中查看体验片段时，看到的&#x200B;*上次修改*&#x200B;日期是上次在 AEM 中修改片段的日期，而不是上次将片段导出到 Adobe Target 的日期。

>[!NOTE]
>
>或者，您可以使用[页面信息](/help/sites-authoring/author-environment-tools.md#page-information)菜单中的类似命令从页面编辑器执行导出。

## 在 Adobe Target 中使用体验片段 {#using-your-experience-fragments-in-adobe-target}

执行上述任务后，体验片段会显示在Adobe Target的“选件”页面上。 查看 [特定Target文档](https://experienceleague.adobe.com/docs/target/using/experiences/offers/aem-experience-fragments.html?lang=zh-Hans) 了解可以实现的目标。

>[!NOTE]
>
>在 Adobe Target 中查看体验片段时，看到的&#x200B;*上次修改*&#x200B;日期是上次在 AEM 中修改片段的日期，而不是上次将片段导出到 Adobe Target 的日期。

## 删除已导出到 Adobe Target 的体验片段 {#deleting-an-experience-fragment-already-exported-to-adobe-target}

删除已导出到Target的体验片段时，如果该片段已在Adobe Target的选件中使用，则可能会导致出现问题。 由于 AEM 正在交付片段内容，因此，删除片段会导致选件不可用。

避免此类情况：

* 如果体验片段当前未在活动中使用，AEM 将允许用户删除片段而不显示警告消息。
* 如果Adobe Target中的某个活动正在使用体验片段，则会出现一条错误消息，警告AEM用户删除该片段可能会对活动产生的后果。

  AEM 中的错误消息不会禁止用户（强制）删除体验片段。如果删除体验片段：

   * 带有 AEM 体验片段的 Target 选件可能会显示意外行为

      * 该选件可能仍会呈现，因为体验片段 HTML 已推送到 Target
      * 如果也从 AEM 中删除了引用的资产，则体验片段中的任何引用都无法正常工作。

   * 由于体验片段在AEM中不再存在，因此无法对体验片段进行任何进一步修改。


## 从导出到Target的体验片段中删除ClientLibs {#removing-clientlibs-from-fragments-exported-target}

体验片段包含完整的html标记和所有必要的客户端库(CSS/JS)，以便按照体验片段内容作者创建的内容完全呈现片段。 这是精心设计的。

在AEM交付的页面上将体验片段选件与Adobe Target结合使用时，“目标”页面已包含所有必要的客户端库。 此外，也不需要体验片段选件中的无关html(请参阅 [注意事项](#considerations))。

以下是体验片段选件中html的伪示例：

```html
<!DOCTYPE>
<html>
   <head>
      <title>…</title>
      <!-- all of the client libraries (css/js) -->
      …
   </head>
   <body>
        <!--/* Actual XF Offer content would appear here... */-->
   </body>
</html>
```

从较高层面来看，当AEM将体验片段导出到Adobe Target时，它会使用几个额外的Sling选择器执行此操作。 例如，导出的体验片段的URL可能如下所示(注意 `nocloudconfigs.atoffer`)：

* http://www.your-aem-instance.com/content/experience-fragments/my-offers/my-xf-offer.nocloudconfigs.atoffer.html

此 `nocloudconfigs` 选择器通过使用HTL来定义，并且可以通过从以下位置复制来覆盖：

* /libs/cq/experience-fragments/components/xfpage/nocloudconfigs.html

此 `atoffer` 使用以下方式应用选择器的后处理 [Sling重写器](/help/sites-developing/experience-fragments.md#the-experience-fragment-link-rewriter-provider-html). 任一选项都可用于删除客户端库。

### 示例 {#example}

出于此目的，让我们说明如何使用 `nocloudconfigs`.

>[!NOTE]
>
>参见 [可编辑的模板](/help/sites-developing/templates.md#editable-templates) 了解更多详细信息。

#### 叠加 {#overlays}

在此特定示例中， [叠加](/help/sites-developing/overlays.md) 被包含将删除客户端库 *和* 无关的html。 假定您已创建体验片段模板类型。 需要从中复制的必要文件 `/libs/cq/experience-fragments/components/xfpage/` 包括：

* `nocloudconfigs.html`
* `head.nocloudconfigs.html`
* `body.nocloudconfigs.html`

#### 模板类型叠加图 {#template-type-overlays}

在本例中，我们使用如下结构：

![模板类型叠加图](assets/xf-target-integration-02.png "模板类型叠加图")

这些文件内容如下：

* `body.nocloudconfigs.html`

  ![body.nocloudconfigs.html](assets/xf-target-integration-03.png "body.nocloudconfigs.html")

* `head.nocloudconfigs.html`

  ![head.nocloudconfigs.html](assets/xf-target-integration-04.png "head.nocloudconfigs.html")

* `nocloudconfigs.html`

  ![nocloudconfigs.html](assets/xf-target-integration-05.png "nocloudconfigs.html")

>[!NOTE]
>
>使用 `data-sly-unwrap` 要删除body标记，您需要 `nocloudconfigs.html`.

### 注意事项 {#considerations}

如果您需要在Adobe Target中使用“体验片段选件”支持AEM站点和非AEM站点，则必须创建两个体验片段（两种不同的模板类型）：

* 一个带有叠加，用于删除clientlibs/额外的html

* 没有叠加的元素，因此包含所需的clientlibs