---
title: 内容服务的 JSON 导出器
seo-title: JSON Exporter for Content Services
description: AEM 内容服务旨在概括 AEM 中/来自 AEM 的内容的描述和投放，而不只是关注网页。它们使用可供任何客户使用的标准化方法，将内容投放到非传统 AEM 网页的渠道。
seo-description: AEM Content Services are designed to generalize the description and delivery of content in/from AEM beyond a focus on web pages. They provide the delivery of content to channels that are not traditional AEM web pages, using standardized methods that can be consumed by any client.
uuid: be6457b1-fa9c-4f3b-b219-01a4afc239e7
contentOwner: User
content-type: reference
topic-tags: components
products: SG_EXPERIENCEMANAGER/6.5/SITES
discoiquuid: 4c7e33ea-f2d3-4d69-b676-aeb50c610d70
exl-id: 647395c0-f392-427d-a998-e9ddf722b9f9
source-git-commit: 4fa868f3ae4778d3a637e90b91f7c5909fe5f8aa
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 35%

---

# 内容服务的 JSON 导出器{#json-exporter-for-content-services}

AEM 内容服务旨在概括 AEM 中/来自 AEM 的内容的描述和投放，而不只是关注网页。

它们使用可供任何客户使用的标准化方法，将内容投放到非传统 AEM 网页的渠道。 这些渠道可以包括：

* [单页面应用程序](spa-walkthrough.md)
* 本机移动设备应用程序
* AEM 外部的其他渠道和接触点

对于使用结构化内容的内容片段，您可以使用JSON导出程序以JSON数据模型格式交付任何AEM页面的内容，从而提供内容服务。 然后，您自己的应用程序可以使用此方法。

>[!NOTE]
>
>此处描述的功能适用于以下所有核心组件： [核心组件版本1.1.0](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hans).

## 包含内容片段核心组件的JSON导出程序 {#json-exporter-with-content-fragment-core-components}

使用AEM JSON导出程序，您可以以JSON数据模型格式交付任何AEM页面的内容。 然后，您自己的应用程序可以使用此方法。

在AEM中，使用选择器实现投放 `model` 和 `.json` 扩展。

`.model.json`

1. 例如，URL，如：

   ```shell
   http://localhost:4502/content/we-retail/language-masters/en.model.json
   ```

1. 提供以下内容：

   ![chlimage_1-192](assets/chlimage_1-192.png)

您也可以通过专门定位结构化内容片段来交付其内容。

使用片段的整个路径(通过 `jcr:content`);例如，带有后缀（如）。

`.../jcr:content/root/responsivegrid/contentfragment.model.json`

您的页面可以包含一个内容片段或多种类型的多个组件。 您还可以使用列表组件等机制自动搜索相关内容。

* 例如，URL，如：

   ```shell
   http://localhost:4502/content/we-retail/language-masters/en/manchester-airport/jcr:content/root/responsivegrid/contentfragment.model.json
   ```

* 提供以下内容：

   ![chlimage_1-193](assets/chlimage_1-193.png)

   >[!NOTE]
   >
   >您可以 [调整您自己的组件](/help/sites-developing/json-exporter-components.md) 以访问和使用此数据。

   >[!NOTE]
   >
   >尽管不是标准实施， [支持多个选择器，](json-exporter-components.md#multiple-selectors) 但 `model` 必须是第一个。

### 更多信息 {#further-information}

另请参阅：

* Assets HTTP API

   * [Assets HTTP API](/help/assets/mac-api-assets.md)

* Sling 模型:

   * [Sling模型 — 自130年起将模型类与资源类型关联](https://sling.apache.org/documentation/bundles/models.html#associating-a-model-class-with-a-resource-type-since-130)

* 包含JSON的AEM:

   * [以JSON格式获取页面信息](/help/sites-developing/pageinfo.md)

## 相关文档 {#related-documentation}

有关更多详细信息，请参阅：

* 的 [Assets用户指南中的内容片段主题](https://experienceleague.adobe.com/docs/experience-manager-64/assets/home.html?lang=en&amp;topic=/experience-manager/6-4/assets/morehelp/content-fragments.ug.js)

* [内容片段模型](/help/assets/content-fragments/content-fragments-models.md)
* [使用内容片段创作](/help/sites-authoring/content-fragments.md)
* [为组件启用 JSON 导出](/help/sites-developing/json-exporter-components.md)

* [核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hans) 和 [内容片段组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html?lang=en)
