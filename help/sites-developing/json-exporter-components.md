---
title: 为组件启用 JSON 导出
seo-title: Enabling JSON Export for a Component
description: 组件可以基于建模器框架进行修改，以生成其内容的JSON导出。
seo-description: Components can be adapted to generate JSON export of their content based on a modeler framework.
uuid: d7cc3347-2adb-4ea5-94a4-a847a2e66d28
contentOwner: User
content-type: reference
topic-tags: components
products: SG_EXPERIENCEMANAGER/6.5/SITES
discoiquuid: 448ad337-d4bb-4603-a27b-77da93feadbd
exl-id: 6d127e14-767e-46ad-aaeb-0ce9dd14d553
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 9%

---

# 为组件启用 JSON 导出{#enabling-json-export-for-a-component}

组件可以基于建模器框架进行修改，以生成其内容的JSON导出。

## 概述 {#overview}

JSON导出基于 [Sling模型](https://sling.apache.org/documentation/bundles/models.html)、和 [Sling模型导出程序](https://sling.apache.org/documentation/bundles/models.html#exporter-framework-since-130) 框架(它本身依赖 [Jackson批注](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations))。

这意味着如果组件需要导出JSON，则必须具有Sling模型。 因此，您需要按照以下两个步骤在任何组件上启用JSON导出。

* [为组件定义Sling模型](/help/sites-developing/json-exporter-components.md#define-a-sling-model-for-the-component)
* [在Sling模型界面中添加批注](#annotate-the-sling-model-interface)

## 为组件定义Sling模型 {#define-a-sling-model-for-the-component}

首先，必须为组件定义Sling模型。

>[!NOTE]
>
>有关使用Sling模型的示例，请参阅文章 [在AEM中开发Sling模型导出程序](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/sling-model-exporter-tutorial-develop.html).

Sling模型实施类必须使用以下内容添加注释：

```java
@Model(... adapters = {..., ComponentExporter.class})
@Exporter(name = ExporterConstants.SLING_MODEL_EXPORTER_NAME, extensions = ExporterConstants.SLING_MODEL_EXTENSION)
@JsonSerialize(as = MyComponent.class)
```

这可确保您的组件可以使用 `.model` 选择器和 `.json` 扩展。

此外，这还指定Sling Model类可以适应于 `ComponentExporter` 界面。

>[!NOTE]
>
>Jackson批注通常不是在Sling模型类级别指定，而是在模型界面级别指定。 这是为了确保将JSON导出视为组件API的一部分。

>[!NOTE]
>
>的 `ExporterConstants` 和 `ComponentExporter` 课程来自 `com.adobe.cq.export.json` 捆绑。

### 使用多个选择器 {#multiple-selectors}

除了 `model` 选择器。

```
https://<server>:<port>/content/page.model.selector1.selector2.json
```

但是，在这种情况下， `model` 选择器必须是第一个选择器，并且扩展必须是 `.json`.

## 在Sling模型界面中添加批注 {#annotate-the-sling-model-interface}

要由JSON导出程序框架考虑，模型界面应实施 `ComponentExporter` 界面(或 `ContainerExporter`，对于容器组件)。

相应的Sling模型界面( `MyComponent`)，则将使用 [Jackson批注](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations) 定义应如何导出（序列化）。

需要对“模型”(Model)界面进行适当的注释，以定义应序列化哪些方法。 默认情况下，所有遵循getter通用命名约定的方法都将进行序列化，并将从getter名称中自然派生其JSON属性名称。 可以使用阻止或覆盖此功能 `@JsonIgnore` 或 `@JsonProperty` 重命名JSON属性。

## 示例 {#example}

核心组件自发布以来一直支持JSON导出 [核心组件的1.1.0](https://docs.adobe.com/content/help/zh-Hans/experience-manager-core-components/using/introduction.html) 和可用作参考。

有关示例，请参阅图像核心组件及其注释界面的Sling模型实施。

GITHUB上的代码

您可以在GitHub上找到此页面的代码

* [在GitHub上打开aem-core-wcm-components项目](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components)
* 将项目下载为 [ZIP文件](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/archive/master.zip)

## 相关文档 {#related-documentation}

有关更多详细信息，请参阅：

* 的 [Assets用户指南中的内容片段主题](https://helpx.adobe.com/experience-manager/6-4/assets/user-guide.html?topic=/experience-manager/6-4/assets/morehelp/content-fragments.ug.js)

* [内容片段模型](/help/assets/content-fragments/content-fragments-models.md)
* [使用内容片段创作](/help/sites-authoring/content-fragments.md)
* [内容服务的 JSON 导出器](/help/sites-developing/json-exporter.md)
* [核心组件](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/introduction.html) 和 [内容片段组件](https://helpx.adobe.com/experience-manager/core-components/using/content-fragment-component.html)
