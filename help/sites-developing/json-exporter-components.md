---
title: 为组件启用 JSON 导出
description: 组件可以适用于基于建模器框架生成其内容的JSON导出。
contentOwner: User
content-type: reference
topic-tags: components
products: SG_EXPERIENCEMANAGER/6.5/SITES
exl-id: 6d127e14-767e-46ad-aaeb-0ce9dd14d553
source-git-commit: a56d5121a6ce11b42a6c30dae9e479564d16af27
workflow-type: tm+mt
source-wordcount: '528'
ht-degree: 9%

---

# 为组件启用 JSON 导出{#enabling-json-export-for-a-component}

组件可以适用于基于建模器框架生成其内容的JSON导出。

## 概述 {#overview}

JSON导出基于 [Sling模型](https://sling.apache.org/documentation/bundles/models.html)，并且位于 [Sling模型导出程序](https://sling.apache.org/documentation/bundles/models.html#exporter-framework-since-130) 框架(它本身依赖于 [Jackson注释](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations))。

这意味着组件必须具有Sling模型（如果它必须导出JSON）。 因此，请按照以下两个步骤对任何组件启用JSON导出。

* [为组件定义Sling模型](/help/sites-developing/json-exporter-components.md#define-a-sling-model-for-the-component)
* [在Sling模型界面中添加批注](#annotate-the-sling-model-interface)

## 为组件定义Sling模型 {#define-a-sling-model-for-the-component}

首先，必须为组件定义Sling模型。

>[!NOTE]
>
>有关使用Sling模型的示例，请参见 [在AEM中开发Sling模型导出程序](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/develop-sling-model-exporter.html?lang=en).

Sling模型实现类必须使用以下内容进行注释：

```java
@Model(... adapters = {..., ComponentExporter.class})
@Exporter(name = ExporterConstants.SLING_MODEL_EXPORTER_NAME, extensions = ExporterConstants.SLING_MODEL_EXTENSION)
@JsonSerialize(as = MyComponent.class)
```

这可确保可以使用单独导出组件 `.model` 选择器和 `.json` 扩展。

此外，这会指定Sling模型类可以调整到 `ComponentExporter` 界面。

>[!NOTE]
>
>Jackson注释不是在Sling模型类级别指定的，而是在Model界面级别指定的。 这是为了确保将JSON导出视为组件API的一部分。

>[!NOTE]
>
>此 `ExporterConstants` 和 `ComponentExporter` 课程来自 `com.adobe.cq.export.json` 捆绑。

### 使用多个选择器 {#multiple-selectors}

虽然这不是标准用例，但除了标准用例之外，还可以配置多个选择器 `model` 选择器。

```
https://<server>:<port>/content/page.model.selector1.selector2.json
```

然而，在此情况下， `model` 选择器必须是第一个选择器，扩展必须是 `.json`.

## 在Sling模型界面中添加批注 {#annotate-the-sling-model-interface}

要供JSON导出程序框架考虑，模型接口应实现 `ComponentExporter` 界面(或 `ContainerExporter`，如果存在容器组件)。

相应的Sling模型界面( `MyComponent`)，然后使用进行注释 [Jackson注释](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations) 以定义应如何导出（序列化）。

必须正确注释模型接口，以定义应序列化的方法。 默认情况下，所有遵守getter的常规命名约定的方法都会被序列化，并且它们的JSON属性名称自然地从getter名称中派生。 可以使用阻止或覆盖此项 `@JsonIgnore` 或 `@JsonProperty` 以重命名JSON属性。

## 示例 {#example}

自发布以来，核心组件一直支持JSON导出 [核心组件的1.1.0](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) 和可以用作参考。

有关示例，请参阅图像核心组件的Sling模型实施及其注释界面。

GITHUB上的代码

您可以在GitHub上找到此页面的代码

* [在GitHub上打开aem-core-wcm-components项目](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components)
* 将项目下载为 [ZIP文件](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/archive/master.zip)

## 相关文档 {#related-documentation}

有关更多详细信息，请参阅以下内容：

* 此 [资产用户指南中的内容片段主题](https://helpx.adobe.com/experience-manager/6-4/assets/user-guide.html?topic=/experience-manager/6-4/assets/morehelp/content-fragments.ug.js)

* [内容片段模型](/help/assets/content-fragments/content-fragments-models.md)
* [使用内容片段创作](/help/sites-authoring/content-fragments.md)
* [内容服务的 JSON 导出器](/help/sites-developing/json-exporter.md)
* [核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) 和 [内容片段组件](https://helpx.adobe.com/experience-manager/core-components/using/content-fragment-component.html)
