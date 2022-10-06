---
title: 使用隐藏条件
seo-title: Using Hide Conditions
description: 隐藏条件可用于确定是否渲染组件资源。
seo-description: Hide conditions can be used to determine if a component resource is rendered or not.
uuid: 93b4f450-1d94-4222-9199-27b5f295f8e6
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 104d1c64-b9b3-40f5-8f9b-fe92d9daaa1f
exl-id: 65f5d5e1-ac11-4a3c-8a51-ce06a741c264
source-git-commit: baf2c6339a554743b6cc69486fb77b121048ba4b
workflow-type: tm+mt
source-wordcount: '628'
ht-degree: 2%

---

# 使用隐藏条件 {#using-hide-conditions}

隐藏条件可用于确定是否渲染组件资源。 例如，模板作者配置核心组件时 [列表组件](https://helpx.adobe.com/experience-manager/core-components/using/list.html) 在 [模板编辑器](/help/sites-authoring/templates.md) 并决定禁用基于子页面构建列表的选项。 在设计对话框中禁用此选项会设置一个属性，以便在呈现列表组件时，将评估隐藏条件，并且不显示显示子页面的选项。

## 概述 {#overview}

对话框可能会变得非常复杂，用户可能只使用一小部分可供他/她使用的选项，但有许多选项可供他/她使用。 这可能会为用户带来压倒性的用户界面体验。

通过使用隐藏条件，管理员、开发人员和超级用户可以根据一组规则来隐藏资源。 此功能允许他们决定在作者编辑内容时应显示哪些资源。

>[!NOTE]
>
>根据表达式隐藏资源不会替换ACL权限。 内容仍然可编辑，但根本不显示。

## 实施和使用详细信息 {#implementation-and-usage-details}

`com.adobe.granite.ui.components.FilteringResourceWrapper` 负责根据 `granite:hide` 属性，位于要过滤的字段中。 实施 `/libs/cq/gui/components/authoring/dialog/dialog.jsp` 包含的实例 `FilteringResourceWrapper.`

该实施利用了Granite [ELResolver API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/docs/server/el.html) 并添加 `cqDesign` 自定义变量。

以下是位于 `etc/design` 或作为内容策略。

```
${cqDesign.myProperty}
${!cqDesign.myProperty}
${cqDesign.myProperty == 'someText'}
${cqDesign.myProperty != 'someText'}
${cqDesign.myProperty == true}
${cqDesign.myProperty == true}
${cqDesign.property1 == 'someText' && cqDesign.property2 || cqDesign.property3 != 1 || header.myHeader}
```

在定义隐藏表达式时，请记住：

* 要有效，应表示找到属性的范围(如 `cqDesign.myProperty`)。
* 值为只读。
* 函数（如果需要）应限于服务提供的给定集。

## 示例 {#example}

隐藏条件的示例可在AEM和 [核心组件](https://docs.adobe.com/content/help/zh-Hans/experience-manager-core-components/using/introduction.html) 特别是。 例如，请考虑 [列表核心组件](https://helpx.adobe.com/experience-manager/core-components/using/list.html).

[使用模板编辑器](/help/sites-authoring/templates.md)，模板作者可以在设计对话框中定义页面作者可以使用的列表组件的选项。 诸如是否允许列表为静态列表、子页面列表、标记页面列表等选项。 可以启用或禁用。

如果模板作者选择禁用子页面选项，则会设置设计属性并针对该属性评估隐藏条件，这会导致该选项无法呈现给页面作者。

1. 默认情况下，页面作者可以使用列表核心组件通过选择选项来使用子页面构建列表 **子页面**.

   ![chlimage_1-218](assets/chlimage_1-218.png)

1. 在列表核心组件的设计对话框中，模板作者可以选择选项 **禁用子项** 以阻止向页面作者显示用于生成基于子页面的列表的选项。

   ![chlimage_1-219](assets/chlimage_1-219.png)

1. 将在下创建策略节点 `/conf/we-retail/settings/wcm/policies/weretail/components/content/list` 属性 `disableChildren` 设置为 `true`.
1. 隐藏条件定义为 `granite:hide` 对话框属性节点上的属性 `/conf/we-retail/settings/wcm/policies/weretail/components/content/list`

   ![chlimage_1-220](assets/chlimage_1-220.png)

1. 的值 `disableChildren` 是从设计配置和表达式中提取 `${cqDesign.disableChildren}` 评估结果 `false`，这表示选项将不会作为组件的一部分呈现。

   您可以将隐藏表达式视为 `granite:hide` 属性 [在GitHub中](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/blob/master/content/src/content/jcr_root/apps/core/wcm/components/list/v1/list/_cq_dialog/.content.xml#L40).

1. 选项 **子页面** 使用列表组件时，不再为页面作者呈现。

   ![chlimage_1-221](assets/chlimage_1-221.png)
