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
exl-id: 1603eef1-d7c8-47d3-8cfa-55ec3eaadd64
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 0%

---

# 在AEM Forms应用程序中使用自动保存{#using-autosave-in-aem-forms-app}

当用户在Adobe Experience Manager Forms应用程序中输入数据时，自动保存功能会定期保存数据。 AEM Forms应用程序中的自动保存功能可帮助您避免在应用程序意外关闭时丢失数据。

您的应用程序可能会意外关闭：

* 如果设备因电池不足而关闭
* 如果用户杀死应用程序
* 如果发生意外崩溃

您可以指定应用程序保存输入数据的间隔。

>[!NOTE]
>
>谨慎选择自动保存频率。 频繁的自动保存操作可能会对设备的性能产生显着影响。

执行以下步骤以使用AEM Forms应用程序中的自动保存功能：

1. 登录应用程序，然后导航到&#x200B;**设置>常规**。
1. 在“常规”屏幕中，使用&#x200B;**自动保存频率**选项选择您希望应用程序保存输入数据的间隔。
   [ ![设置自动保存频率](assets/using-autosave-freq-07.png)](assets/using-autosave-freq-07-1.png)

1. 重新启动应用程序并使用同一用户登录时，系统会提示您使用恢复未保存的任务对话框还原任务。 在恢复未保存的任务对话框中单击&#x200B;**确定**&#x200B;以恢复已保存的任务。 单击&#x200B;**取消**&#x200B;可删除与上次触发的自动保存对应的已保存数据，并开始处理新任务。

   单击&#x200B;**确定**后，将恢复任务，并在应用程序崩溃之前触发与最新自动保存对应的数据。 它包括表单数据以及与任务关联的所有附件。
   [ ![正在恢复&#x200B;](assets/autosave-flow.png)](assets/using-autosave-freq-06.png)**任务A。** 正在进行的表单B。 **应用程序已强制关闭C.** 应用程序，并 **在恢复未保存的任务对话框D.** 中 **** 恢复了原始数据的表单
