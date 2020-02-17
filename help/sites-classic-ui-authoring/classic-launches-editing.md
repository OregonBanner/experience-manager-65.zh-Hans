---
title: 编辑启动项
seo-title: 编辑启动项
description: 在为一个页面（或一组页面）创建启动项后，您可以编辑页面启动副本中的内容。
seo-description: 在为一个页面（或一组页面）创建启动项后，您可以编辑页面启动副本中的内容。
uuid: 3a310eeb-553d-4d2b-98b5-c5bc523b2aca
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 666b967a-e94b-4f94-a676-00adf150580f
legacypath: /content/docs/en/aem/6-0/author/site-page-features/launches
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 编辑启动项{#editing-launches}

## 编辑启动页面 {#editing-launch-pages}

在为一个页面（或一组页面）创建启动项后，您可以编辑页面启动副本中的内容。

1. 打开要编辑的页面。
1. 在 Sidekick 中，选择&#x200B;**版本控制**&#x200B;选项卡，然后展开&#x200B;**启动项**&#x200B;组。当前正在编辑的启动项标题采用粗体字体。

   ![chlimage_1-13](assets/chlimage_1-13.jpeg)

1. 选择要处理的启动项，然后单击&#x200B;**切换**。
1. 开始编辑。

   >[!NOTE]
   >
   >您可以使用 Sidekick 的&#x200B;**页面**&#x200B;选项卡执行诸如&#x200B;**创建子页面**&#x200B;等操作。

## 编辑启动项配置 {#editing-a-launch-configuration}

在创建启动项之后，您可以更改启动项名称和启动项的日期。您还可以指定一个与启动项关联的图像。

1. 打开启动项管理页面 ([http://localhost:4502/libs/launches/content/admin.html](http://localhost:4502/libs/launches/content/admin.html))。

1. 选择所需的启动项，然后单击&#x200B;**编辑**&#x200B;以打开对话框：

   * 在&#x200B;**常规**&#x200B;选项卡中，您可以编辑：

      * **标题**
      * **起始日期**：这相当于启动日期
      * **生产就绪**
      有关这些字段的用途和交互的信息，请参阅[启动项 - 事件的顺序](/help/sites-authoring/launches.md#launches-the-order-of-events)。

   * 在&#x200B;**图像**&#x200B;选项卡中，您可以上传图像文件。


1. 单击&#x200B;**保存**。

## 发现页面的启动状态 {#discovering-the-launch-status-of-a-page}

编辑页面的启动项时，有关该启动项的信息会显示在 Sidekick 的&#x200B;**版本控制**&#x200B;选项卡底部：

* 启动项的名称。
* 上次更改之后的时间。
* 执行上次更改的用户。
* **生产就绪**&#x200B;标记的状态（橙色=未设置；绿色=已设置）。

![chlimage_1-186](assets/chlimage_1-186.png)

