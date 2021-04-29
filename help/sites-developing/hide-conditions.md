---
title: 使用隐藏条件
seo-title: 使用隐藏条件
description: 隐藏条件可用于确定是否渲染组件资源。
seo-description: 隐藏条件可用于确定是否渲染组件资源。
uuid: 93b4f450-1d94-4222-9199-27b5f295f8e6
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 104d1c64-b9b3-40f5-8f9b-fe92d9daaa1f
exl-id: 65f5d5e1-ac11-4a3c-8a51-ce06a741c264
translation-type: tm+mt
source-git-commit: baf2c6339a554743b6cc69486fb77b121048ba4b
workflow-type: tm+mt
source-wordcount: '646'
ht-degree: 1%

---

# 使用隐藏条件{#using-hide-conditions}

隐藏条件可用于确定是否渲染组件资源。 例如，当模板作者在[模板编辑器](/help/sites-authoring/templates.md)中配置核心组件[列表组件](https://helpx.adobe.com/experience-manager/core-components/using/list.html)并决定禁用选项以基于子页面构建列表时，就会出现这种情况。 在设计对话框中禁用此选项会设置一个属性，以便在渲染列表组件时，将评估隐藏条件，而不显示显示子页面的选项。

## 概述 {#overview}

对话框可能会变得非常复杂，用户可能只使用一小部分可供自己使用的选项。 这会为用户带来压倒性的用户界面体验。

通过使用隐藏条件，管理员、开发人员和超级用户可以根据一组规则隐藏资源。 此功能允许他们决定在作者编辑内容时应显示哪些资源。

>[!NOTE]
>
>根据表达式隐藏资源不会替换ACL权限。 内容仍然可编辑，但不显示。

## 实施和使用详细信息{#implementation-and-usage-details}

`com.adobe.granite.ui.components.FilteringResourceWrapper` 负责根据要筛选的字段上属性的存在 `granite:hide` 和值来筛选资源。`/libs/cq/gui/components/authoring/dialog/dialog.jsp`的实现包括`FilteringResourceWrapper.`的实例

该实现利用Granite [ELResolver API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/docs/server/el.html)并通过ExpressionCustomizer添加`cqDesign`自定义变量。

以下是设计节点上隐藏条件的几个示例，该节点位于`etc/design`下或作为内容策略。

```
${cqDesign.myProperty}
${!cqDesign.myProperty}
${cqDesign.myProperty == 'someText'}
${cqDesign.myProperty != 'someText'}
${cqDesign.myProperty == true}
${cqDesign.myProperty == true}
${cqDesign.property1 == 'someText' && cqDesign.property2 || cqDesign.property3 != 1 || header.myHeader}
```

定义隐藏表达式时请牢记：

* 要有效，应表示找到属性的范围(例如，`cqDesign.myProperty`)。
* 值为只读。
* 职能（如果需要）应限于服务提供的给定集。

## 示例 {#example}

隐藏条件的示例可在AEM中找到，特别是[核心组件](https://docs.adobe.com/content/help/zh-Hans/experience-manager-core-components/using/introduction.html)。 例如，考虑[列表核心组件](https://helpx.adobe.com/experience-manager/core-components/using/list.html)。

[使用模板编辑器](/help/sites-authoring/templates.md)，模板作者可以在设计对话框中定义页面作者可以使用的列表组件选项。诸如是否允许列表为静态列表、子页面列表、标记页面列表等选项。 可以启用或禁用。

如果模板作者选择禁用子页面选项，则会设置设计属性并针对该属性评估隐藏条件，这会导致选项不为页面作者呈现。

1. 默认情况下，页面作者可以通过选择选项&#x200B;**子页面**&#x200B;来使用子页面使用列表核心组件构建列表。

   ![chlimage_1-218](assets/chlimage_1-218.png)

1. 在列表核心组件的设计对话框中，模板作者可以选择选项&#x200B;**禁用子项**，以阻止将基于子页面生成列表的选项显示给页面作者。

   ![chlimage_1-219](assets/chlimage_1-219.png)

1. 在`/conf/we-retail/settings/wcm/policies/weretail/components/content/list`下创建策略节点，其属性`disableChildren`设置为`true`。
1. 隐藏条件定义为对话框属性节点`/conf/we-retail/settings/wcm/policies/weretail/components/content/list`上`granite:hide`属性的值

   ![chlimage_1-220](assets/chlimage_1-220.png)

1. `disableChildren`的值从设计配置中提取，表达式`${cqDesign.disableChildren}`的计算结果为`false`，这意味着选项不会作为组件的一部分呈现。

   您可以将隐藏表达式视图为GitHub中`granite:hide`属性[的值，此处为](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/blob/master/content/src/content/jcr_root/apps/core/wcm/components/list/v1/list/_cq_dialog/.content.xml#L40)。

1. 使用列表组件时，不再为页面作者呈现选项&#x200B;**子页面**。

   ![chlimage_1-221](assets/chlimage_1-221.png)
