---
title: 在We.Retail中试用核心组件
seo-title: Trying out Core Components in We.Retail
description: 在We.Retail中试用核心组件
seo-description: null
uuid: 8d1cea0b-99d9-49b2-b275-41f14864b1ff
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: af3cd818-61cf-4da1-bfb5-87540911ddd5
exl-id: b5f2be67-c93c-4dbc-acc0-3edd8f1a282f
source-git-commit: b886844dc80482ae4aae5fc7ce09e466efecc3bd
workflow-type: tm+mt
source-wordcount: '535'
ht-degree: 1%

---

# 在We.Retail中试用核心组件{#trying-out-core-components-in-we-retail}

核心组件是灵活的新式组件，具有轻松的扩展性，并允许轻松集成到项目中。 核心组件是围绕几个主要设计原则构建的，例如HTL、开箱即用可用性、可配置性、版本控制和可扩展性。 We.Retail构建在核心组件之上。

## 正在尝试 {#trying-it-out}

1. 从We.Retail示例内容开始AEM，然后打开 [组件控制台](/help/sites-authoring/default-components-console.md).

   **全局导航 — >工具 — >组件**

1. 在组件控制台中打开边栏，您可以筛选特定组件组。 核心组件可在中找到

   * `.core-wcm`：标准核心组件
   * `.core-wcm-form`：表单提交核心组件

   选择 `.core-wcm`.

   ![chlimage_1-162](assets/chlimage_1-162.png)

1. 请注意，所有核心组件都已命名 **v1**，反映这是此核心组件的第一个版本。 今后将发布常规版本，这些版本与AEM的版本兼容，并且允许轻松升级，以便您能够利用最新功能。
1. 单击 **文本(v1)**.

   请参见 **资源类型** 组件的 `/apps/core/wcm/components/text/v1/text`. 核心组件位于 `/apps/core/wcm/components` 和是按组件进行版本控制的。

   ![chlimage_1-163](assets/chlimage_1-163.png)

1. 单击 **文档** 选项卡以查看组件的开发人员文档。

   ![chlimage_1-164](assets/chlimage_1-164.png)

1. 返回到组件控制台。 筛选组 **We.Retail** 并选择 **文本** 组件。
1. 请参见 **资源类型** 指向下的预期组件 `/apps/weretail` 但是 **资源超级类型** 指向核心组件 `/apps/core/wcm/components/text/v1/text`.

   ![chlimage_1-165](assets/chlimage_1-165.png)

1. 单击 **实时使用情况** 选项卡，以查看哪些页面当前正在使用此组件。 单击第一个 **谢谢** 页面以编辑该页面。

   ![chlimage_1-166](assets/chlimage_1-166.png)

1. 在感谢页面上，选择文本组件，然后在组件的“编辑”菜单中，单击取消继承图标。

   [We.Retail具有全球化网站结构](/help/sites-developing/we-retail-globalized-site-structure.md) 将内容从语言母版推送到 [通过称为继承的机制创建活动副本](/help/sites-administering/msm.md). 因此，必须取消继承，以便允许用户手动编辑文本。

   ![chlimage_1-167](assets/chlimage_1-167.png)

1. 单击以确认取消 **是**.

   ![chlimage_1-168](assets/chlimage_1-168.png)

1. 取消继承并选择文本组件后，即可使用更多选项。 单击**编辑**。

   ![chlimage_1-169](assets/chlimage_1-169.png)

1. 您现在可以看到文本组件有哪些编辑选项可用。

   ![chlimage_1-170](assets/chlimage_1-170.png)

1. 从 **页面信息** 菜单选择 **编辑模板**.
1. 在页面的模板编辑器中，单击 **策略** 中文本组件的图标 **布局容器** 页面的。

   ![chlimage_1-171](assets/chlimage_1-171.png)

1. 利用核心组件，模板作者可以配置哪些属性可供页面作者使用。 这些功能包括允许的粘贴源、格式选项、可用的段落样式等功能。

   此类设计对话框可用于许多核心组件，并与模板编辑器携手工作。 启用后，作者可以通过组件编辑器使用它们。

   ![chlimage_1-172](assets/chlimage_1-172.png)

## 更多信息 {#further-information}

有关核心组件的更多信息，请参阅创作文档 [核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hans) 有关核心组件和开发人员文档的功能概述 [开发核心组件](https://helpx.adobe.com/experience-manager/core-components/using/developing.html) 了解技术概述。

此外，您可能希望进一步调查 [可编辑的模板](/help/sites-developing/we-retail-editable-templates.md). 请参阅创作文档 [创建页面模板](/help/sites-authoring/templates.md) 或开发人员文档页面 [模板 — 可编辑](/help/sites-developing/page-templates-editable.md) 有关可编辑模板的完整详细信息。
