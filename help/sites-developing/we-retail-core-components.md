---
title: 在We.Retail中试用核心组件
seo-title: 在We.Retail中试用核心组件
description: 'null'
seo-description: 'null'
uuid: 8d1cea0b-99d9-49b2-b275-41f14864b1ff
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: af3cd818-61cf-4da1-bfb5-87540911ddd5
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 在We.Retail中试用核心组件{#trying-out-core-components-in-we-retail}

核心组件是现代、灵活的组件，它们具有轻松的可扩展性，并且允许与项目进行简单集成。 核心组件围绕几个主要设计原则构建而成，如HTL、开箱即用、可配置性、版本控制和可扩展性。 We.Retail已构建在核心组件上。

## 试用 {#trying-it-out}

1. 使用We.Retail示例内容启动AEM，然后打开组件 [控制台](/help/sites-authoring/default-components-console.md)。

   **全局导航->工具->组件**

1. 在组件控制台中打开边栏，可以过滤特定组件组。 核心组件位于

   * `.core-wcm`:标准核心组件
   * `.core-wcm-form`:表单提交核心组件
   选择 `.core-wcm`。

   ![chlimage_1-162](assets/chlimage_1-162.png)

1. 请注意，所有核心组件均命 **名为v1**，这反映出这是此核心组件的第一个版本。 将在以后发布常规版本，该版本与AEM兼容，并可轻松升级，以便您利用最新功能。
1. 单 **击文本(v1)**。

   请参阅组 **件的资源类** 型是 `/apps/core/wcm/components/text/v1/text`。 核心组件位于下面， `/apps/core/wcm/components` 并按组件进行版本控制。

   ![chlimage_1-163](assets/chlimage_1-163.png)

1. 单击“文 **档** ”选项卡，查看组件的开发人员文档。

   ![chlimage_1-164](assets/chlimage_1-164.png)

1. 返回到组件控制台。 筛选组 **We.Retail** ，然后选择 **Text组件** 。
1. 请参阅 **资源类型** (Resource Type `/apps/weretail` )按照预期指向组件，但资源超级类型(Resource Super Type **)指向核心组件**`/apps/core/wcm/components/text/v1/text`。

   ![chlimage_1-165](assets/chlimage_1-165.png)

1. 单击“ **实时使用** ”选项卡可查看当前使用该组件的页面。 单击第一个 **感谢页面** ，以编辑该页面。

   ![chlimage_1-166](assets/chlimage_1-166.png)

1. 在感谢页面上，选择文本组件，然后在组件的编辑菜单中单击取消继承图标。

   [We.Retail的站点结构是全球化的](/help/sites-developing/we-retail-globalized-site-structure.md) ，内容通过称为继承的机制从语 [言母版推送到Live Copy](/help/sites-administering/msm.md)。 因此，必须取消继承才能允许用户手动编辑文本。

   ![chlimage_1-167](assets/chlimage_1-167.png)

1. 单击是以确认取 **消**。

   ![chlimage_1-168](assets/chlimage_1-168.png)

1. 取消继承并选择文本组件后，将有更多选项可用。 单击**编辑**。

   ![chlimage_1-169](assets/chlimage_1-169.png)

1. 您现在可以看到文本组件可用的编辑选项。

   ![chlimage_1-170](assets/chlimage_1-170.png)

1. 从页面信 **息菜单中** ，选择 **编辑模板**。
1. 在页面的模板编辑器中，单击页面布 **局容器中** “文本”组件的 **策略图标** 。

   ![chlimage_1-171](assets/chlimage_1-171.png)

1. 核心组件允许模板作者配置哪些属性可供页面作者使用。 这些功能包括允许的粘贴源、格式选项、可用的段落样式等。

   此类设计对话框可用于许多核心组件，并与模板编辑器协同工作。 启用后，作者可通过组件编辑器访问这些组件。

   ![chlimage_1-172](assets/chlimage_1-172.png)

## 更多信息 {#further-information}

有关核心组件的详细信息，请参阅创作文档 [Core Components](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/introduction.html) （核心组件） [，以获取核心组件功能的概述；有关技术概述，请参阅开发人员文档](https://helpx.adobe.com/experience-manager/core-components/using/developing.html) Developing Core Components（开发核心组件）。

此外，您可能希望进一步调查可编 [辑的模板](/help/sites-developing/we-retail-editable-templates.md)。 有关可编辑模板的完整 [详细信息，请参阅创作文档](/help/sites-authoring/templates.md) “创建页面模板”或开发人 [员文档页面模板——可编辑](/help/sites-developing/page-templates-editable.md) 。
