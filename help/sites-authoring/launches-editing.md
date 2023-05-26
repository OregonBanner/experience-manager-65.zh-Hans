---
title: 编辑启动项
description: 在为您的页面（或页面集）创建启动项后，您可以在页面的启动项副本中编辑内容。
uuid: 1f2c2e53-73a3-4bd7-b2c7-425491bc0118
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 30aa3177-bcf4-4260-8f64-e73bc907942a
docset: aem65
legacypath: /content/docs/en/aem/6-0/author/site-page-features/launches
exl-id: 2d441820-b394-47c8-b4ca-a8aede590937
source-git-commit: f4b6eb2ded17ec641f23a1fc3b977ce77169c8a1
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 38%

---

# 编辑启动项{#editing-launches}

## 编辑启动页面 {#editing-launch-pages}

为某个页面（或一组页面）创建启动项后，您可以编辑该页面的启动项副本中的内容。

1. [从“引用”（站点控制台）中访问启动项](/help/sites-authoring/launches.md#launches-in-references-sites-console)以显示可用的操作。
1. 选择 **转到页面** 以打开页面进行编辑。

>[!NOTE]
>
>您不能在启动项中移动页面。尝试此操作将触发警告消息：
>
>* 警告：此页面是启动项的源。不允许移动此页面。


### 编辑基于 Live Copy 的启动页面 {#editing-launch-pages-subject-to-a-live-copy}

如果您的启动项基于 [live copy](/help/sites-administering/msm.md) 然后，您将：

* 在编辑组件（内容和/或属性）时，请参阅锁定符号（小挂锁）。
* 请参见 **Live Copy** 按Tab键进入 **页面属性**

Live Copy 用于将&#x200B;**&#x200B;源分支&#x200B;**&#x200B;中的内容同步到启动分支（以使启动项与源中所做的更改保持最新）。

您可以使用与编辑标准Live Copy相同的方式进行更改；例如：

* 单击已关闭的挂锁将破坏此同步，并允许您对启动项中的内容进行新的更新。 一旦解锁（打开挂锁），您的更改不会被在源分支内的同一位置所做的任何更改覆盖。
* 特定页面的&#x200B;**暂停**（和&#x200B;**继续**）继承。

参见 [更改Live Copy内容](/help/sites-administering/msm-livecopy.md#changing-live-copy-content) 以进一步了解。

## 将启动页面与其源页面进行比较 {#comparing-a-launch-page-to-its-source-page}

要跟踪您所做的更改，您可以在&#x200B;**引用**&#x200B;中查看启动项，并将启动页面与其源页面进行比较：

1. 在 **站点** 控制台， [导航到启动项的源页面并将其选定](/help/sites-authoring/basic-handling.md#viewingandselectingyourresources).
1. 打开 **[引用](/help/sites-authoring/basic-handling.md#references)** 面板并选择 **启动次数**.
1. 选择您的特定启动项，然后 **与源比较**：

   ![screen-shot_2019-03-05at121952](assets/screen-shot_2019-03-05at121952.png)

1. 两个页面（启动项和源）将并排打开。

   有关使用此功能的完整信息，请参阅 [页面差异](/help/sites-authoring/page-diff.md).

## 更改使用的源页面 {#changing-the-source-pages-used}

您可以随时向启动项的源页面范围中添加页面或从中删除页面：

1. 从以下任一位置访问并选择启动项：

   * 此 [启动项控制台](/help/sites-authoring/launches.md#the-launches-console)：

      * 选择&#x200B;**编辑**。
   * [引用（站点控制台）](/help/sites-authoring/launches.md#launches-in-references-sites-console) 要显示可用的操作，请执行以下操作：

      * 选择&#x200B;**编辑启动项**。

   将显示源页面。

1. 进行所需的更改，然后使用&#x200B;**保存**&#x200B;进行确认。

   >[!NOTE]
   >
   >要将页面添加到启动项，这些页面必须位于公共语言根之下；即位于单个站点中。

## 编辑Launch配置 {#editing-a-launch-configuration}

您可以随时编辑启动项的属性：

1. 从以下任一位置访问并选择启动项：

   * 此 [启动项控制台](/help/sites-authoring/launches.md#the-launches-console)：

      * 选择 **属性**.
   * [引用（站点控制台）](/help/sites-authoring/launches.md#launches-in-references-sites-console) 要显示可用的操作，请执行以下操作：

      * 选择&#x200B;**编辑属性**。

   将显示详细信息。

1. 进行所需的更改，然后使用&#x200B;**保存**&#x200B;进行确认。

   有关启 [动日期和生产就绪字段的用途和交互的信息](/help/sites-authoring/launches.md#launches-the-order-of-events)******** ，请参阅启动项——事件的顺序。

## 发现页面的启动项状态 {#discovering-the-launch-status-of-a-page}

当您从“引用”选项卡中选择特定启动项时，将显示状态(请参阅 [引用中的启动项（站点控制台）](/help/sites-authoring/launches.md#launches-in-references-sites-console))。

![screen-shot_2019-03-05at121901](assets/screen-shot_2019-03-05at121901.png)
