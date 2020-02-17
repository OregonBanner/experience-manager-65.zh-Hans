---
title: 创建启动项
seo-title: 创建启动项
description: 可创建启动项，以允许更新现有网页的新版本，以便将来激活。在创建启动项时，需要指定标题和源页面。
seo-description: 可创建启动项，以允许更新现有网页的新版本，以便将来激活。在创建启动项时，需要指定标题和源页面。
uuid: e67608a9-e6c9-42f3-bd1d-63a5fa87ae18
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 48826f03-6731-49c5-a6c5-6e2fb718f912
legacypath: /content/docs/en/aem/6-0/author/site-page-features/launches
translation-type: tm+mt
source-git-commit: 016c705230dffec052c200b058a36cdbe0520fc4

---


# 创建启动项{#creating-launches}

可创建启动项，以允许更新现有网页的新版本，以便将来激活。创建启动项时，需要指定标题和源页面：

* The title appears in the **Sidekick**, from where authors can access them to work on them.
* 默认情况下，源页面的子页面包含在启动项中。必要时，可只使用源页面。
* 默认情况下，[Live Copy](/help/sites-administering/msm.md) 会在源页面发生更改时自动更新启动页面。您可以指定创建一个静态副本，以防止自动更改。

或者，您可以选择指定&#x200B;**启动日期**（和时间），以便定义何时提升和激活启动页面。However the **Launch Date** only operates in combination with the **Production Ready** flag (see [Editing a Launch Configuration](/help/sites-classic-ui-authoring/classic-launches-editing.md#editing-a-launch-configuration)); for the actions to actually occur automatically, both must be set.

## 创建启动项 {#creating-a-launch}

可按照以下过程创建启动项。

1. Open the Website administration page ([http://localhost:4502/siteadmin](http://localhost:4502/siteadmin)).
1. 单击&#x200B;**新建...**，然后单击&#x200B;**新建启动项...**。
1. 在&#x200B;**创建启动项**&#x200B;对话框中，指定以下属性的值：

   * **启动项标题**：启动项的名称。该名称应当体现出作者的相关信息。
   * **源页面**：创建启动项的页面路径。默认情况下，包含所有子页面。
   * **不包括子页面**：选中此选项，可只为源页面（而非子页面）创建启动项。默认情况下，此选项处于未选中状态。
   * **保持同步**：选中此选项，可在源页面发生更改时自动更新启动页面的内容。此功能可通过将启动项设为 [Live Copy](/help/sites-administering/msm.md) 来实现。
   * **启动日期**：激活启动副本的日期和时间（取决于&#x200B;**生产就绪**&#x200B;标记；请参阅[启动项 - 事件的顺序](/help/sites-authoring/launches.md#launches-the-order-of-events)）。
   ![chlimage_1-99](assets/chlimage_1-99a.png)

1. 单击&#x200B;**创建**。

## 删除启动项 {#deleting-a-launch}

您还可以删除启动项。

1. 在[启动项控制台](/help/sites-classic-ui-authoring/classic-launches.md)中，选择所需的启动项。
1. 单击&#x200B;**删除** - 需要进行确认：

   ![chlimage_1-100](assets/chlimage_1-100a.png)

   >[!CAUTION]
   >
   >在删除嵌套启动项时，应先删除较低的级别。

