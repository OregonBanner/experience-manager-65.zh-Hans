---
title: 编辑启动项
description: 为某个页面（或一组页面）创建启动项后，您可以编辑该页面的启动项副本中的内容。
uuid: 3a310eeb-553d-4d2b-98b5-c5bc523b2aca
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 666b967a-e94b-4f94-a676-00adf150580f
legacypath: /content/docs/en/aem/6-0/author/site-page-features/launches
exl-id: 21776f42-cd81-459d-b4b9-1d92e0aec164
source-git-commit: f4b6eb2ded17ec641f23a1fc3b977ce77169c8a1
workflow-type: tm+mt
source-wordcount: '291'
ht-degree: 3%

---

# 编辑启动项{#editing-launches}

## 编辑启动页面 {#editing-launch-pages}

为某个页面（或一组页面）创建启动项后，您可以编辑该页面的启动项副本中的内容。

1. 打开页面进行编辑。
1. 在Sidekick中，选择 **版本控制** 选项卡，然后展开 **启动次数** 组。 当前正在编辑的启动项的标题使用粗体字体。

   ![chlimage_1-13](assets/chlimage_1-13.jpeg)

1. 选择要处理的启动项，然后单击 **切换**.
1. 开始编辑。

   >[!NOTE]
   >
   >您可以使用 **页面** tab of sidekick以执行操作，例如 **创建子页面**，等等。

## 编辑Launch配置 {#editing-a-launch-configuration}

创建启动项后，您可以更改启动项名称和启动项日期。 您还可以指定要与启动项关联的图像。

1. 打开启动项管理页面([http://localhost:4502/libs/launches/content/admin.html](http://localhost:4502/libs/launches/content/admin.html))。

1. 选择所需的启动项，然后单击 **编辑** 要打开对话框：

   * 在 **常规** 选项卡，您可以编辑：

      * **标题**
      * **上线日期**：这相当于启动日期
      * **生产就绪**

      参见 [启动次数 — 事件的顺序](/help/sites-authoring/launches.md#launches-the-order-of-events) 以了解这些字段的用途和交互信息。

   * 在 **图像** 选项卡，您可以上传图像文件。


1. 单击“**保存**”。

## 发现页面的启动项状态 {#discovering-the-launch-status-of-a-page}

编辑页面的启动项时，有关该启动项的信息将显示在页面的底部。 **版本控制** Sidekick选项卡：

* 启动项的名称。
* 自上次更改以来的时间。
* 执行上次更改的用户。
* 的状态 **生产就绪** 标志（橙色=未设置；绿色=设置）。

![chlimage_1-186](assets/chlimage_1-186.png)
