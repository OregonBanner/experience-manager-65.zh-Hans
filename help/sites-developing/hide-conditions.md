---
title: 使用隐藏条件
description: 隐藏条件可用于确定是否呈现组件资源。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
exl-id: 65f5d5e1-ac11-4a3c-8a51-ce06a741c264
source-git-commit: 69346a710708ee659ee97e9fdc193c8ea2658fe6
workflow-type: tm+mt
source-wordcount: '633'
ht-degree: 2%

---

# 使用隐藏条件 {#using-hide-conditions}

隐藏条件可用于确定是否呈现组件资源。 例如，模板作者配置核心组件时 [列表组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/list.html?lang=en) 在 [模板编辑器](/help/sites-authoring/templates.md) 并决定禁用基于子页面构建列表的选项。 在“设计”对话框中禁用此选项可设置属性，以便在呈现列表组件时，会计算隐藏条件，并且不会显示显示子页面的选项。

## 概述 {#overview}

对于用户而言，对话框可能会变得复杂，并包含许多选项，用户只能使用自己可以使用的选项的一部分。 这可能会导致用户获得难以承受的用户界面体验。

通过使用隐藏条件，管理员、开发人员和超级用户可以根据一组规则来隐藏资源。 利用此功能，他们可以决定在作者编辑内容时应该显示哪些资源。

>[!NOTE]
>
>基于表达式隐藏资源不会替换ACL权限。 内容保持可编辑状态，但不会显示。

## 实施和使用详细信息 {#implementation-and-usage-details}

`com.adobe.granite.ui.components.FilteringResourceWrapper` 负责根据资源的存在性和价值筛选资源 `granite:hide` 属性，位于要筛选的字段中。 实施 `/libs/cq/gui/components/authoring/dialog/dialog.jsp` 包含实例 `FilteringResourceWrapper.`

实施利用Granite [ELResolver API](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/docs/server/el.html) 并添加 `cqDesign` 自定义变量。

以下是位于以下位置的设计节点上的几个隐藏条件示例 `etc/design` 或作为内容策略。

```
${cqDesign.myProperty}
${!cqDesign.myProperty}
${cqDesign.myProperty == 'someText'}
${cqDesign.myProperty != 'someText'}
${cqDesign.myProperty == true}
${cqDesign.myProperty == true}
${cqDesign.property1 == 'someText' && cqDesign.property2 || cqDesign.property3 != 1 || header.myHeader}
```

定义隐藏表达式时，请记住以下事项：

* 要使其有效，应表示在其中找到属性的范围(例如， `cqDesign.myProperty`)。
* 值为只读。
* 功能（如有必要）应仅限于该服务提供的给定集合。

## 示例 {#example}

隐藏条件的示例可在整个AEM和 [核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) 尤其是。 例如，考虑 [列出核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/list.html?lang=en).

[使用模板编辑器](/help/sites-authoring/templates.md)，模板作者可以在“设计”对话框中定义列表组件的哪些选项可供页面作者使用。 可以启用或禁用此类选项，例如是否允许列表作为静态列表、子页面列表、标记页面列表等。

如果模板作者选择禁用子页面选项，则会设置设计属性，并根据该属性评估隐藏条件，从而导致不为页面作者呈现该选项。

1. 默认情况下，页面作者可以通过选择选项，使用列表核心组件使用子页面构建列表 **子页面**.

   ![chlimage_1-218](assets/chlimage_1-218.png)

1. 在列表核心组件的“设计”对话框中，模板作者可以选择选项 **禁用子项** 以防止向页面作者显示基于子页面生成列表的选项。

   ![chlimage_1-219](assets/chlimage_1-219.png)

1. 策略节点创建于 `/conf/we-retail/settings/wcm/policies/weretail/components/content/list` 具有属性 `disableChildren` 设置为 `true`.
1. 隐藏条件被定义为 `granite:hide` 对话框属性节点上的属性 `/conf/we-retail/settings/wcm/policies/weretail/components/content/list`

   ![chlimage_1-220](assets/chlimage_1-220.png)

1. 的值 `disableChildren` 从设计配置和表达式中提取 `${cqDesign.disableChildren}` 评估为 `false`，这意味着该选项将不会作为组件的一部分渲染。

   您可以查看隐藏表达式，它是 `granite:hide` 属性 [在此处GitHub中](https://github.com/adobe/aem-core-wcm-components/blob/main/content/src/content/jcr_root/apps/core/wcm/components/list/v1/list/_cq_dialog/.content.xml#L40).

1. 选项 **子页面** 使用列表组件时，不再为页面作者渲染。

   ![chlimage_1-221](assets/chlimage_1-221.png)
