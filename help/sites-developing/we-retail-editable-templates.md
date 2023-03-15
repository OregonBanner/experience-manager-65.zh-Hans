---
title: 在We.Retail中尝试可编辑模板
seo-title: Trying out Editable Templates in We.Retail
description: 在We.Retail中尝试可编辑模板
seo-description: null
uuid: 0d4b97cb-efcc-4312-a783-eae3ecd6f889
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 3cc8ac23-98ff-449f-bd76-1203c7cbbed7
exl-id: efebe66d-3d30-4033-9c4c-ae347e134f2f
source-git-commit: b886844dc80482ae4aae5fc7ce09e466efecc3bd
workflow-type: tm+mt
source-wordcount: '481'
ht-degree: 11%

---

# 在We.Retail中尝试可编辑模板{#trying-out-editable-templates-in-we-retail}

使用可编辑模板，创建和维护模板不再只是开发人员的任务。 高级用户（称为模板作者）现在可以创建模板。 开发人员仍需要设置环境、创建客户端库和创建要使用的组件，但是，在这些基础知识到位后，模板作者就可以灵活地创建和配置模板，而无需开发项目。 

We.Retail中的所有页面都基于可编辑的模板，允许非开发人员调整和自定义模板。

## 正在尝试 {#trying-it-out}

1. 编辑语言主控分支的“设备”页。

   http://localhost:4502/editor.html/content/we-retail/language-masters/en/equipment.html

1. 请注意，模式选择器不再提供设计模式。 We.Retail的所有页面都基于可编辑模板，要更改可编辑模板的设计，必须在模板编辑器中编辑这些页面。
1. 从 **页面信息** 菜单选择 **编辑模板**.
1. 您现在正在编辑主页模板。

   利用页面的结构模式，可修改模板的结构。 例如，这包括布局容器中允许的组件。

   ![chlimage_1-138](assets/chlimage_1-138.png)

1. 配置布局容器的策略以定义容器中允许哪些组件。

   策略等同于设计配置。

   ![chlimage_1-139](assets/chlimage_1-139.png)

1. 在布局容器的“设计”对话框中，可以

   * 选择现有策略或为容器创建新策略
   * 选择容器中允许的组件
   * 定义将资产拖到容器时要放置的默认组件

   ![chlimage_1-140](assets/chlimage_1-140.png)

1. 返回模板编辑器，您可以在布局容器中编辑文本组件的策略。

   这允许您：

   * 选择现有策略或为容器创建新策略
   * 定义使用此组件时页面作者可用的功能，例如

      * 允许的粘贴源
      * 格式选项
      * 允许的段落样式
      * 允许的特殊字符

   许多基于核心组件的组件允许通过可编辑的模板在组件级别配置选项，从而无需由开发人员进行自定义。

   ![chlimage_1-141](assets/chlimage_1-141.png)

1. 返回模板编辑器，您可以使用模式选择器更改为 **初始内容** 模式，以定义页面上所需的内容。

   **版面** 模式可在普通页面上使用，以定义模板的布局。

## 更多信息 {#more-information}

有关详细信息，请参阅创作文档 [创建页面模板](/help/sites-authoring/templates.md) 或开发人员文档页面 [模板 — 可编辑](/help/sites-developing/page-templates-editable.md) 有关可编辑模板的完整技术详细信息。

您可能还希望调查 [核心组件](/help/sites-developing/we-retail-core-components.md). 请参阅创作文档 [核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hans) 有关核心组件和开发人员文档的功能概述 [开发核心组件](https://helpx.adobe.com/experience-manager/core-components/using/developing.html) 了解技术概述。
