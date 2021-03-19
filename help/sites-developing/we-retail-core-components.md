---
title: 在We.Retail中试用核心组件
seo-title: 在We.Retail中试用核心组件
description: 在We.Retail中试用核心组件
seo-description: 'null'
uuid: 8d1cea0b-99d9-49b2-b275-41f14864b1ff
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: af3cd818-61cf-4da1-bfb5-87540911ddd5
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '544'
ht-degree: 2%

---


# 在We.Retail{#trying-out-core-components-in-we-retail}中试用核心组件

核心组件是现代、灵活的组件，具有轻松的可扩展性并允许轻松集成到您的项目中。 核心组件围绕几个主要设计原则构建而成，如HTL、现成可用性、可配置性、版本控制和可扩展性。 We.Retail已构建在核心组件上。

## 正在尝试{#trying-it-out}

1. 将AEM与We.Retail示例内容开始，然后打开[组件控制台](/help/sites-authoring/default-components-console.md)。

   **全局导航 — >工具 — >组件**

1. 在组件控制台中打开边栏后，您可以过滤特定组件组。 核心组件位于

   * `.core-wcm`:标准核心组件
   * `.core-wcm-form`:表单提交核心组件

   选择`.core-wcm`。

   ![chlimage_1-162](assets/chlimage_1-162.png)

1. 请注意，所有核心组件均名为&#x200B;**v1**，表明这是此核心组件的第一个版本。 以后将发布常规版本，它与AEM版本兼容，并允许轻松升级，以便您充分利用最新功能。
1. 单击&#x200B;**文本(v1)**。

   请参阅组件的&#x200B;**资源类型**&#x200B;是`/apps/core/wcm/components/text/v1/text`。 核心组件位于`/apps/core/wcm/components`下，并按组件进行版本控制。

   ![chlimage_1-163](assets/chlimage_1-163.png)

1. 单击&#x200B;**文档**&#x200B;选项卡，查看组件的开发人员文档。

   ![chlimage_1-164](assets/chlimage_1-164.png)

1. 返回到组件控制台。 对组&#x200B;**We.Retail**&#x200B;进行筛选，然后选择&#x200B;**Text**&#x200B;组件。
1. 请参阅&#x200B;**资源类型**&#x200B;按照`/apps/weretail`下的预期指向组件，但&#x200B;**资源超级类型**&#x200B;指回核心组件`/apps/core/wcm/components/text/v1/text`。

   ![chlimage_1-165](assets/chlimage_1-165.png)

1. 单击&#x200B;**Live Usage**&#x200B;选项卡，查看当前正在使用此组件的页面。 单击第一个&#x200B;**感谢**&#x200B;页面以编辑页面。

   ![chlimage_1-166](assets/chlimage_1-166.png)

1. 在感谢页面上，选择文本组件，然后在组件的编辑菜单中单击取消继承图标。

   [We.Retail拥有一个全球化的站](/help/sites-developing/we-retail-globalized-site-structure.md) 点结构，其中内容通过一种称为继承 [的机制从语言主页推送到Live Copy](/help/sites-administering/msm.md)。因此，必须取消继承，以便允许用户手动编辑文本。

   ![chlimage_1-167](assets/chlimage_1-167.png)

1. 单击&#x200B;**是**&#x200B;确认取消。

   ![chlimage_1-168](assets/chlimage_1-168.png)

1. 取消继承并选择文本组件后，可使用更多选项。 单击**编辑**。

   ![chlimage_1-169](assets/chlimage_1-169.png)

1. 您现在可以看到文本组件可以使用哪些编辑选项。

   ![chlimage_1-170](assets/chlimage_1-170.png)

1. 从&#x200B;**页面信息**&#x200B;菜单中，选择&#x200B;**编辑模板**。
1. 在页面的模板编辑器中，单击页面的&#x200B;**布局容器**&#x200B;中文本组件的&#x200B;**策略**&#x200B;图标。

   ![chlimage_1-171](assets/chlimage_1-171.png)

1. 核心组件允许模板作者配置页面作者可使用的属性。 这些功能包括允许粘贴源、格式选项、可用的段落样式等。

   此类设计对话框可用于许多核心组件，并可与模板编辑器手动工作。 启用后，作者可通过组件编辑器使用这些组件。

   ![chlimage_1-172](assets/chlimage_1-172.png)

## 更多信息 {#further-information}

有关核心组件的更多信息，请参见创作文档[核心组件](https://docs.adobe.com/content/help/zh-Hans/experience-manager-core-components/using/introduction.html)，了解核心组件功能的概述，以及开发者文档[开发核心组件](https://helpx.adobe.com/experience-manager/core-components/using/developing.html)以获取技术概述。

此外，您可能希望进一步调查[可编辑的模板](/help/sites-developing/we-retail-editable-templates.md)。 有关可编辑模板的完整详细信息，请参阅创作文档[创建页面模板](/help/sites-authoring/templates.md)或开发人员文档页面[模板 — 可编辑](/help/sites-developing/page-templates-editable.md)。
