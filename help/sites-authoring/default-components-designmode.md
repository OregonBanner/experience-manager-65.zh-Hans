---
title: 在设计模式中配置组件
seo-title: 在设计模式中配置组件
description: 'null'
seo-description: 'null'
uuid: b9c9792d-4398-446d-8767-44d4e7ce9a2e
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 8ae6817a-16d3-4740-b67a-498e75adf350
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '907'
ht-degree: 80%

---


# 在设计模式中配置组件{#configuring-components-in-design-mode}

安装现成 AEM 实例后，组件浏览器中会提供一些可立即使用的组件。

除了这些组件，还有各种其他组件可用。您可以使用设计模式[启用／禁用此类组件](#enable-disable-components)。启用组件并位于页面上后，您便可以使用设计模式通过编辑属性参数来[配置组件设计的各个方面。](#configuring-the-design-of-a-component)

>[!NOTE]
>
>编辑这些组件时必须要谨慎。设计设置通常是整个网站设计中不可缺少的部分，因此只应由具有相应权限和经验丰富的人员更改设置，这些人员通常是管理员或开发人员。有关详细信息，请参阅[开发组件](/help/sites-developing/components.md)。

>[!NOTE]
>
>设计模式仅适用于静态模板。使用可编辑的模板创建的模板应使用[模板编辑器](/help/sites-authoring/templates.md)进行编辑。

>[!NOTE]
>
>设计模式仅适用于存储为(`/etc`)下的内容的设计配置。
>
>从AEM 6.4开始，建议将设计作为配置数据存储在`/apps`下，以支持连续部署方案。 存储在`/apps`下的设计在运行时不可编辑，非管理员用户将无法使用此类模板的设计模式。

这涉及到添加或删除在页面的段落系统中允许使用的组件。段落系统 (`parsys`) 本身是一个复合组件，其中包含其他段落组件。段落系统允许作者向页面中添加不同类型的组件，并包含所有其他段落组件。每个段落类型表示为一个组件。

例如，产品页面的内容可能包含带有以下各项的段落系统：

* 产品的图像（以图像或文本图像段落的形式）
* 产品说明（作为文本段落）
* 包含技术数据的表（作为表段落）
* 用户填写的表单（作为表单开始、表单元素和表单结束段落）

>[!NOTE]
>
>有关 [](/help/sites-developing/components.md) 的详细信息，请参阅[开发组件](/help/sites-developing/dev-guidelines-bestpractices.md#guidelines-for-using-templates-and-components)和`parsys`模板使用指南。

>[!CAUTION]
>
>定义静态模板设计的建议方式是按照本文中所述使用“设计模式”编辑设计
>
>例如，在 CRX DE 中修改设计不是最佳实践，并且此类设计的应用程序可能与预期不同。请参阅开发人员文档[页面模板 - 静态](/help/sites-developing/page-templates-static.md#how-template-designs-are-applied)以获取更多信息。

## 启用/禁用组件 {#enable-disable-components}

要启用或禁用组件，请执行以下操作：

1. 选择&#x200B;**设计**&#x200B;模式。

   ![screen_shot_2018-03-22at103113](assets/screen_shot_2018-03-22at103113.png)

1. 点按或单击某个组件。选中组件后，组件将带有一个蓝色边框。

   ![screen_shot_2018-03-22at103204](assets/screen_shot_2018-03-22at103204.png)

1. 单击或点按&#x200B;**父项**&#x200B;图标。

   ![](do-not-localize/screen_shot_2018-03-22at103204.png)

   此操作将选中包含当前组件的段落系统。

1. 段落系统的&#x200B;**配置**&#x200B;图标将显示在父项的操作栏中。

   ![](do-not-localize/screen_shot_2018-03-22at103256.png)

   选择此图标以显示对话框。

1. 使用该对话框定义在编辑当前页面时组件浏览器中可供使用的组件。

   ![screen_shot_2018-03-22at103329](assets/screen_shot_2018-03-22at103329.png)

   该对话框包含两个选项卡：

   * 允许的组件
   * 设置

   **允许的组件**

   在&#x200B;**允许的组件**&#x200B;选项卡上，定义可用于parsys的组件。

   * 这些组件按其组件组分组，各组可以展开和折叠。
   * 可以通过选中组名称选择整个组，通过取消选中全部取消选择。
   * 减号表示至少选中了组中的一个而并非所有项目。
   * 可按名称进行搜索来筛选组件。
   * 无论是否应用了筛选器，组件组名称右侧列出的数字都表示这些组中选定组件的总数。

   此配置是按页面组件来定义。如果子页面也使用相同的模板和/或页面组件（通常一致），那么会将相同的配置应用到相应的段落系统。

   >[!NOTE]
   >
   >自适应表单组件专门用于在自适应表单容器内使用，以便利用表单生态系统。因此，这些组件只能在自适应表单编辑器中使用，而不能在站点页面编辑器中使用。

   **设置**

   在&#x200B;**设置**&#x200B;选项卡上，您可以定义其他选项，例如为每个组件绘制锚点，以及定义每个容器的单元格边距。

1. 选择&#x200B;**完成**&#x200B;以保存配置。

## 配置组件的设计 {#configuring-the-design-of-a-component}

1. 选择&#x200B;**设计**&#x200B;模式。

   ![screen_shot_2018-03-22at103113-1](assets/screen_shot_2018-03-22at103113-1.png)

1. 点按或单击某个带蓝色边框的组件。在此示例中，已选中一个主页横幅组件。

   ![screen_shot_2018-03-22at103434](assets/screen_shot_2018-03-22at103434.png)

1. 使用&#x200B;**配置**&#x200B;图标打开对话框。

   ![](do-not-localize/screen_shot_2018-03-22at103256-1.png)

   在设计对话框中，可以根据可用的设计参数配置组件。

   ![screen_shot_2018-03-22at103530](assets/screen_shot_2018-03-22at103530.png)

   该对话框包含三个选项卡：

   * 主要
   * 功能
   * 样式

   **属性**

   **属性**&#x200B;选项卡允许您配置组件的重要设计参数。例如，对于图像组件，您可以定义允许的图像最大和最小大小。

   **功能**

   **功能**&#x200B;选项卡允许您启用或禁用组件的其他功能。例如，对于图像组件，您可以定义图像的方向、可用的裁剪选项以及是否可以上传图像。

   **样式**

   **样式**&#x200B;选项卡允许您定义要与组件一起使用的 CSS 类和样式。

   ![screen_shot_2018-03-22at103741](assets/screen_shot_2018-03-22at103741.png)

   使用&#x200B;**添加**&#x200B;按钮可将其他条目添加到多条目对话框列表中。

   ![chlimage_1-94](assets/chlimage_1-94.png)

   使用**删除**图标从多条目对话框列表中删除条目。

   ![](do-not-localize/screen_shot_2018-03-22at103809.png)

   使用&#x200B;**移动**&#x200B;图标可重新排列多条目对话框列表中的条目顺序。

   ![](do-not-localize/screen_shot_2018-03-22at103816.png)

1. 单击或点按&#x200B;**完成**&#x200B;图标以保存并关闭对话框。

