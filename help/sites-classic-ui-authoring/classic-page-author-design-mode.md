---
title: 在设计模式中配置组件
seo-title: 在设计模式中配置组件
description: 安装现成 AEM 实例后，Sidekick 中会提供一些可立即使用的组件。除了这些组件以外，还有其他一些组件可用。您可以使用设计模式启用/禁用这类组件。
seo-description: 安装现成 AEM 实例后，Sidekick 中会提供一些可立即使用的组件。除了这些组件以外，还有其他一些组件可用。您可以使用设计模式启用/禁用这类组件。
uuid: 2cd5dad0-2f9c-4f34-aae8-1638d1445eb3
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 10466b49-f8bd-4c2c-8106-b0c7ba054989
docset: aem65
translation-type: tm+mt
source-git-commit: bcb1840d23ae538c183eecb0678b6a75d346aa50

---


# 在设计模式中配置组件{#configuring-components-in-design-mode}

安装现成 AEM 实例后，Sidekick 中会提供一些可立即使用的组件。

除了这些组件以外，还有其他一些组件可用。您可以使用设计模式[启用/禁用这类组件](#enabledisablecomponentsusingdesignmode)。When enabled and located on your page you can then use Design mode to [configure aspects of the component design](#configuringcomponentsusingdesignmode) by editing the attribute parameters.

>[!NOTE]
>
>编辑这些组件时必须要谨慎。设计设置通常是整个网站设计中不可缺少的部分，因此只应由具有相应权限（及经验）的人更改设置，通常是管理员或开发人员。有关详细信息，请参阅[开发组件](/help/sites-developing/components.md)。

这涉及到添加或删除在页面的段落系统中允许使用的组件。段落系统 (`parsys`) 本身是一个复合组件，其中包含其他段落组件。段落系统允许作者向页面中添加不同类型的组件，并包含所有其他段落组件。每个段落类型表示为一个组件。

例如，产品页面的内容可能包含带有以下各项的段落系统：

* 产品的图像（以图像或文本图像段落的形式）
* 产品说明（作为文本段落）
* 包含技术数据的表（作为表段落）
* 用户填写的表单（作为表单开始、表单元素和表单结束段落）

>[!NOTE]
>
>有关 [](/help/sites-developing/components.md#paragraphsystem) 的详细信息，请参阅[开发组件](/help/sites-developing/dev-guidelines-bestpractices.md#guidelines-for-using-templates-and-components)和`parsys`模板使用指南。

## 启用/禁用组件 {#enable-disable-components}

在设计模式中，Sidekick 将最小化，您可以配置可供创作使用的组件：

1. 要进入设计模式，请打开要编辑的页面，然后使用 Sidekick 图标：

   ![](do-not-localize/chlimage_1.png)

1. Click **Edit** on the Paragraph system (**Design of par**).

   ![screen_shot_2012-02-08at102726am](assets/screen_shot_2012-02-08at102726am.png)

1. 此时将打开一个对话框，列出 Sidekick 中显示的组件组及其包含的单个组件。

   根据需要选择添加或删除可在 Sidekick 中使用的组件。

   ![screen_shot_2012-02-08at103407am](assets/screen_shot_2012-02-08at103407am.png)

1. 在设计模式下，Sidekick 会最小化。通过单击箭头，可以最大化 Sidekick 并返回编辑模式：

   ![](do-not-localize/sidekick-collapsed.png)

## 配置组件的设计 {#configuring-the-design-of-a-component}

在设计模式中，还可以配置单个组件的属性。每个组件都有其自身的参数，下面的示例说明了&#x200B;**图像**&#x200B;组件的配置方法：

1. 要进入设计模式，请打开要编辑的页面，然后使用 Sidekick 图标：

   ![](do-not-localize/chlimage_1-1.png)

1. 您可以配置组件的设计。

   For example, if you click **Edit** on the Image component (**Design of image**) you can configure the component specific parameters:

   ![chlimage_1-5](assets/chlimage_1-5.png)

1. 单击&#x200B;**确定**&#x200B;以保存您的更改。

1. 在设计模式下，Sidekick 会最小化。通过单击箭头，可以最大化 Sidekick 并返回编辑模式：

   ![](do-not-localize/sidekick-collapsed-1.png)
