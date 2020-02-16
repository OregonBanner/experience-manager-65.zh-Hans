---
title: 为组件启用JSON导出
seo-title: 为组件启用JSON导出
description: 组件可以基于建模器框架生成其内容的JSON导出。
seo-description: 组件可以基于建模器框架生成其内容的JSON导出。
uuid: d7cc3347-2adb-4ea5-94a4-a847a2e66d28
contentOwner: User
content-type: reference
topic-tags: components
products: SG_EXPERIENCEMANAGER/6.5/SITES
discoiquuid: 448ad337-d4bb-4603-a27b-77da93feadbd
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 为组件启用JSON导出{#enabling-json-export-for-a-component}

组件可以基于建模器框架生成其内容的JSON导出。

## 概述 {#overview}

JSON导出基于 [Sling Models](https://sling.apache.org/documentation/bundles/models.html)，并基于 [Sling Model Exporter框架(该框架本身依赖](https://sling.apache.org/documentation/bundles/models.html#exporter-framework-since-130) Jackson注释 [](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations))。

这意味着，如果组件需要导出JSON，则必须具有Sling模型。 因此，您需要按照以下两个步骤在任何组件上启用JSON导出。

* [为组件定义Sling模型](/help/sites-developing/json-exporter-components.md#define-a-sling-model-for-the-component)
* [注释Sling model界面](#annotate-the-sling-model-interface)

## 为组件定义Sling模型 {#define-a-sling-model-for-the-component}

首先，必须为组件定义Sling模型。

>[!NOTE]
>
>有关使用Sling模型的示例，请参阅文章在AEM [中开发Sling模型导出器](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/sling-model-exporter-tutorial-develop.html)。

Sling Model实现类必须添加以下注释：

```java
@Model(... adapters = {..., ComponentExporter.class})
@Exporter(name = ExporterConstants.SLING_MODEL_EXPORTER_NAME, extensions = ExporterConstants.SLING_MODEL_EXTENSION)
@JsonSerialize(as = MyComponent.class)
```

这可确保您的组件能够使用选择器和扩展单 `.model` 独导出 `.json` 。

此外，这指定Sling Model类可适应于接口 `ComponentExporter` 中。

>[!NOTE]
>
>Jackson注释通常不在Sling Model类级别指定，而是在Model界面级别指定。 这是为了确保将JSON导出视为组件API的一部分。

>[!NOTE]
>
>和 `ExporterConstants` 课 `ComponentExporter` 程来自捆绑 `com.adobe.cq.export.json` 套件。

## 注释Sling模型界面 {#annotate-the-sling-model-interface}

要在JSON Exporter框架中考虑，模型界面应实 `ComponentExporter` 现该界面( `ContainerExporter`或，对于容器组件)。

然后，相应的Sling model界面( `MyComponent`)将使用 [Jackson注释进行注释](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations) ，以定义如何导出（序列化）它。

需要对“模型”界面进行正确注释以定义哪些方法应进行序列化。 默认情况下，所有符合getter通常命名约定的方法都将进行序列化，并将从getter名称自然派生其JSON属性名称。 使用或重命名JSON属性可以阻止 `@JsonIgnore` 或覆 `@JsonProperty` 盖该属性。

## 示例 {#example}

核心组件自核心组件的 [1.1.0版起就支持JSON导出](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/introduction.html) ，可用作参考。

例如，请参阅图像核心组件及其注释界面的Sling Model实现。

GITHUB上的代码

您可以在GitHub上找到此页面的代码

* [在GitHub上打开aem-core-wcm-components项目](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components)
* 将项目下载为 [ZIP文件](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/archive/master.zip)

## 相关文档 {#related-documentation}

有关更多详细信息，请参阅：

* 资产 [用户指南中的内容片段主题](https://helpx.adobe.com/experience-manager/6-4/assets/user-guide.html?topic=/experience-manager/6-4/assets/morehelp/content-fragments.ug.js)

* [内容片段模型](/help/assets/content-fragments-models.md)
* [使用内容片段进行创作](/help/sites-authoring/content-fragments.md)
* [针对内容服务的JSON导出器](/help/sites-developing/json-exporter.md)
* [核心组件](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/introduction.html) 和内容 [片段组件](https://helpx.adobe.com/experience-manager/core-components/using/content-fragment-component.html)

