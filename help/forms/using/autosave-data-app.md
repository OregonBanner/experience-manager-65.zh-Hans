---
title: 在AEM Forms应用程序中使用自动保存
seo-title: 在AEM Forms应用程序中使用自动保存
description: 了解如何在AEM Forms应用程序中使用自动保存功能，以避免数据丢失。
seo-description: 了解如何在AEM Forms应用程序中使用自动保存功能，以避免数据丢失。
uuid: 00fe6a10-1a72-443d-a840-0415dc769199
contentOwner: sashanka
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 2c71cc28-b7c8-4785-9fc2-b47fa80cbd70
docset: aem65
translation-type: tm+mt
source-git-commit: d9975c0dcc02ae71ac64aadb6b4f82f7c993f32c

---


# 在AEM Forms应用程序中使用自动保存{#using-autosave-in-aem-forms-app}

当用户在Adobe Experience Manager Forms应用程序中输入数据时，自动保存功能会定期保存数据。 AEM Forms应用程序中的自动保存功能可帮助您避免意外关闭应用程序时的数据丢失。

您的应用程序可能会意外关闭：

* 如果设备因电池电量不足而关闭
* 如果用户杀死了应用程序
* 如果发生意外崩溃

您可以指定应用程序保存输入数据的间隔。

>[!NOTE]
>
>谨慎选择自动保存频率。 频繁的自动保存操作可能会对设备的性能产生显着影响。

执行以下步骤以在AEM Forms应用程序中使用自动保存功能：

1. 登录到应用程序，然后导航到“设置” **>“常规”**。
1. 在“常规”屏幕中，使用“自 **动保存频率** ”选项选择您希望应用程序保存输入数据的间隔。
   [ 设 ![置自动保存频率](assets/using-autosave-freq-07.png)](assets/using-autosave-freq-07-1.png)

1. 当您重新启动应用程序并使用同一用户登录时，系统会提示您使用“恢复未保存的任务”对话框恢复任务。 在“恢 **复未保存的任务** ”对话框中单击“确定”，以继续处理保存的任务。 单击“取 **消** ”可删除与上次触发的自动保存操作相对应的已保存数据，并开始处理新任务。

   单击“确 **定**”后，将恢复任务，并显示与应用程序崩溃前触发的最新自动保存相对应的数据。 它包括表单数据和与任务关联的所有附件。
   [![](assets/autosave-flow.png)](assets/using-autosave-freq-06.png)****获**&#x200B;得恢复的&#x200B;**任务A。在创作品表** B。应用程序强制关 **闭C.** App，并在“恢复未保存的任务”对话框 **D中重新启动。使用原始数据恢复的表单

