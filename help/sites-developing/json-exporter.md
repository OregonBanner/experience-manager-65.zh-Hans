---
title: 内容服务的JSON导出程序
seo-title: 内容服务的JSON导出程序
description: AEM Content Services旨在将AEM中／来自内容的描述和投放概括到网页之外。 他们使用可供任何客户使用的标准化方法，向非传统AEM网页的渠道提供内容投放。
seo-description: AEM Content Services旨在将AEM中／来自内容的描述和投放概括到网页之外。 他们使用可供任何客户使用的标准化方法，向非传统AEM网页的渠道提供内容投放。
uuid: be6457b1-fa9c-4f3b-b219-01a4afc239e7
contentOwner: User
content-type: reference
topic-tags: components
products: SG_EXPERIENCEMANAGER/6.5/SITES
discoiquuid: 4c7e33ea-f2d3-4d69-b676-aeb50c610d70
translation-type: tm+mt
source-git-commit: a430c4de89bde3b907d342106465d3b5a7c75cc8
workflow-type: tm+mt
source-wordcount: '495'
ht-degree: 4%

---


# 内容服务的JSON导出程序{#json-exporter-for-content-services}

AEM Content Services旨在将AEM中／来自内容的描述和投放概括到网页之外。

他们使用可供任何客户使用的标准化方法，向非传统AEM网页的渠道提供内容投放。 这些渠道可以包括：

* [单页应用程序](spa-walkthrough.md)
* 本机移动应用程序
* AEM外部的其他渠道和触点

对于使用结构化内容的内容片段，您可以通过使用JSON导出器以JSON数据模型格式交付(y)AEM页面的内容，来提供内容服务。 然后，您自己的应用程序可以使用它。

>[!NOTE]
>
>自核心组件1.1.0版以来，所 [有核心组件均可使用此处描述的功能](https://docs.adobe.com/content/docs/en/core-components/v1.html)。

## 包含内容片段核心组件的JSON导出程序 {#json-exporter-with-content-fragment-core-components}

使用AEM JSON导出器，您可以以JSON数据模型格式提供(y)AEM页面的内容。 然后，您自己的应用程序可以使用它。

在AEM中，投放是使用选择器和扩 `model` 展功 `.json` 能实现的。

`.model.json`

1. 例如，URL，如：

   ```shell
   http://localhost:4502/content/we-retail/language-masters/en.model.json
   ```

1. 将提供以下内容：

   ![chlimage_1-192](assets/chlimage_1-192.png)

您也可以通过专门定位结构化内容片段来提供其内容。

这是使用片段的整个路径(通过 `jcr:content`); 例如，带有后缀（如）。

`.../jcr:content/root/responsivegrid/contentfragment.model.json`

您的页面可以包含单个内容片段或多种类型的组件。 您还可以使用列表组件等机制自动搜索相关内容。

* 例如，URL，如：

   ```shell
   http://localhost:4502/content/we-retail/language-masters/en/manchester-airport/jcr:content/root/responsivegrid/contentfragment.model.json
   ```

* 将提供以下内容：

   ![chlimage_1-193](assets/chlimage_1-193.png)

   >[!NOTE]
   >
   >您可以 [调整自己的组件](/help/sites-developing/json-exporter-components.md) ，以访问和使用这些数据。

   >[!NOTE]
   >
   >虽然不是标准实现， [但支持多个选择器](json-exporter-components.md#multiple-selectors) , `model` 但必须是第一个选择器。

### 更多信息 {#further-information}

另请参阅：

* 资产 HTTP API

   * [资产 HTTP API](/help/assets/mac-api-assets.md)

* Sling Models:

   * [Sling模型——自130年起将模型类与资源类型关联](https://sling.apache.org/documentation/bundles/models.html#associating-a-model-class-with-a-resource-type-since-130)

* AEM with JSON:

   * [以JSON格式获取页面信息](/help/sites-developing/pageinfo.md)

## 相关文档 {#related-documentation}

有关更多详细信息，请参阅：

* 资产 [用户指南中的内容片段主题](https://helpx.adobe.com/experience-manager/6-4/assets/user-guide.html?topic=/experience-manager/6-4/assets/morehelp/content-fragments.ug.js)

* [内容片段模型](/help/assets/content-fragments/content-fragments-models.md)
* [使用内容片段进行创作](/help/sites-authoring/content-fragments.md)
* [为组件启用JSON导出](/help/sites-developing/json-exporter-components.md)

* [核心组件](https://docs.adobe.com/content/help/zh-Hans/experience-manager-core-components/using/introduction.html) 和内容 [片段组件](https://helpx.adobe.com/experience-manager/core-components/using/content-fragment-component.html)

