---
title: 使用启动项为将来的版本开发内容
description: 通过启动项，您可以有效地为未来版本开发内容。 它们允许您进行更改，以便将来发布，同时保持当前页面。
uuid: 4bbd9865-735d-4232-b69c-b64193ac5d83
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: e145afd8-7391-47aa-b389-16fb303749d0
docset: aem65
exl-id: b25d3f8e-5687-49ab-95e1-19ec75c87f6e
source-git-commit: f4b6eb2ded17ec641f23a1fc3b977ce77169c8a1
workflow-type: tm+mt
source-wordcount: '833'
ht-degree: 27%

---

# 启动项{#launches}

通过启动项，您可以有效地为将来的版本开发内容。

将创建一个启动项，以便进行更改以准备将来发布（同时维护当前页面）。 编辑和更新启动页面后，您可以将其提升回源，然后激活源页面（顶级）。 提升会将启动项内容复制回源页面，并且可以手动或自动完成（具体取决于创建和编辑启动项时设置的字段）。

例如，您的在线商店的季节性产品页面会每季更新一次，以便特色产品与当季产品保持一致。 要为下一季度的更新做好准备，您可以创建相应网页的启动项。 在整个季度中，启动项副本中会累计以下更改：

* 对由于正常维护任务而发生的源页面所做的更改。 这些更改会在启动页面中自动复制。
* 直接在启动页面上执行的编辑，以便为下一季度做准备。

当下一季度到来时，您需要提升启动页面，以便发布源页面（包含更新的内容）。您可以提升所有页面，也可以仅提升已修改的页面。

启动项也可以是：

* 为多个根分支创建。 虽然您可以为整个网站创建启动项（并在此进行更改），但由于需要复制整个网站，因此创建启动项可能不现实。 当涉及数百甚至数千个页面时，复制操作以及以后的升级任务所需的比较都会影响系统要求和性能。
* 嵌套（启动项中的启动项），让您能够从现有启动项创建启动项，以便作者可以利用已做的更改，而不必对每个启动项多次进行相同的更改。

本节介绍如何创建、编辑和提升（如有必要） [删除](/help/sites-authoring/launches-creating.md#deleting-a-launch))从站点控制台中启动页面，或 [启动项控制台](#the-launches-console):

* [创建启动项](/help/sites-authoring/launches-creating.md)
* [编辑启动项](/help/sites-authoring/launches-editing.md)
* [提升启动项](/help/sites-authoring/launches-promoting.md)

## 启动项 — 事件的顺序 {#launches-the-order-of-events}

通过启动项，您可以为一个或多个已激活网页的未来版本高效地开发内容。

启动项允许您：

* 创建源页面的副本：

   * 副本是您的启动项。
   * 顶级源页面称为&#x200B;**生产**。

      * 源页面可以从多个（单独的）分支中获取。

   ![chlimage_1-111](assets/chlimage_1-111.png)

* 编辑启动项配置：

   * 在启动项中添加或删除页面和/或分支。
   * 编辑启动项属性；例如&#x200B;**标题**、**启动日期**、**生产就绪**&#x200B;标记。

* 您可以手动或自动提升和发布内容：

   * 手动:

      * 将启动项内容提升回 **Target** （源页面）。
      * 从源（向后提升后）页面发布内容。
      * 提升所有页面，或仅提升已修改的页面。
   * 自动 – 这涉及以下各项：

      * **启动**（**起始**）**日期**&#x200B;字段：可在创建或编辑启动项时设置此字段。

      * 的 **生产就绪** 标记：只有在编辑启动项时才能设置此设置。
      * 如果 **生产就绪** 标记设置后，启动项将自动提升到指定的生产页面 **Launch**(**实时**) **日期**. 提升后，生产页面会自动发布。\
         如果未设置日期，该标记将不起作用。


* 并行更新源页面和启动页面：

   * 对源页面所做的更改会自动体现在启动副本中（如果进行了继承设置，即设置为 Live Copy）。
   * 可以在不中断这些自动更新或源页面的情况下对启动副本进行更改。

   ![chlimage_1-112](assets/chlimage_1-112.png)

* [创建嵌套启动项](/help/sites-authoring/launches-creating.md#creating-a-nested-launch)  — 启动项中的启动项：

   * 源是现有的启动项。
   * 您可以 [提升嵌套启动项](/help/sites-authoring/launches-promoting.md#promoting-a-nested-launch) 对任何目标；这可以是父启动项，也可以是顶级源页面（生产）。

   ![chlimage_1-113](assets/chlimage_1-113.png)

   >[!CAUTION]
   >
   >删除启动项时，将会删除该启动项本身及其所有下级嵌套启动项。

>[!NOTE]
>
>要创建和编辑启动项，需要拥有 `/content/launches` 的访问权限 – 与默认组 `content-authors` 的权限相同。
>
>如果您遇到任何问题，请联系您的系统管理员。

>[!CAUTION]
>
>不支持在Launch页面上对组件进行重新排序。
>
>提升页面时，将反映任何内容更改，但组件位置不会发生更改。


### 启动项控制台 {#the-launches-console}

启动项控制台提供了启动项的概述，并允许您对列出的启动项执行操作。 可以通过以下方式访问该控制台：

* **工具**&#x200B;控制台：**工具**、**站点**、**启动项**。

* 或直接使用 [https://localhost:4502/libs/launches/content/launches.html](https://localhost:4502/libs/launches/content/launches.html)

## 引用中的启动项（站点控制台） {#launches-in-references-sites-console}

1. 在 **站点** 控制台中，导航到启动项的源。
1. 打开 **引用** 边栏并选择源页面。
1. 选择 **启动项**，则会列出现有的启动项：

   ![screenshot_2019-03-05at121901-1](assets/screen-shot_2019-03-05at121901-1.png)

1. 点按/单击相应的启动项，此时将显示可执行的操作列表：

   ![screenshot_2019-03-05at121952-1](assets/screen-shot_2019-03-05at121952-1.png)
