---
title: 添加附件
seo-title: 添加附件
description: 在AEM Forms应用程序中，将照片和笔记作为批注添加到任务中
seo-description: 在AEM Forms应用程序中，将照片和笔记作为批注添加到任务中
uuid: 3d2738b4-fd43-44ec-8eaf-a2ad4b7e5af5
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: d5976ed2-4482-495c-bf77-6d192379cfef
docset: aem65
exl-id: 82282e2d-63a1-47e9-b2ec-f50a4bd32bd3
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '579'
ht-degree: 0%

---

# 添加附件{#adding-attachments}

## 在与AEM Forms工作流服务器(JEE上的AEM Forms)同步的表单中添加附件{#adding-annotations}

AEM Forms应用程序允许您将图像、潦草的注释和文本注释附加到与AEM Forms JEE服务器同步的表单中。 如果您的表单是从AEM Forms工作流服务器加载的，则附件会添加到表单中。 您可以点按附件按钮![attachments-app](assets/attachments-app.png) ，以一起查看表单中的所有附件。 红色通知指定表单中的附件数。 如果表单中没有附件，则看不到红色通知按钮。 如果表单中没有附件，则点按“附件”按钮![attch](assets/attch.png)时，您可以选择附加照片或涂写。

您的选项包括：

* **图库**:用于根据设备上保存的图片添加图片。

* **相机**:允许您拍摄照片并将其添加到表单中。

* **注意**:允许您添加涂写或文本注释。使用![scribble](assets/scribble.png)添加潦草文字，使用![keyboard](assets/keyboard.png)添加文本注释。

>[!NOTE]
>
>一个用户添加的附件对其他AEM Forms应用程序用户可见。 其他用户无法删除用户添加的附件。


### “附件”屏幕{#the-attachments-screen}

要查看某个位置的所有附件，请点按![attachments-app](assets/attachments-app.png)。 您可以在此处添加、重命名和删除附件。

![所有附件都在一个位置](assets/attachments-screen.png)

您可以使用“附件”屏幕中的&#x200B;**+**&#x200B;按钮附加其他图片、涂写或文本。

### 添加照片{#adding-a-photograph}

您可以使用移动设备的相机或设备中保存的图片来附加表单中的图片。

1. 点按窗口底部的附件按钮![attch](assets/attch.png)。
1. 在显示的弹出窗口中，点按&#x200B;**图库**&#x200B;或&#x200B;**Camera**。
1. 根据您选择的选项，执行以下操作：

   1. 如果选择&#x200B;**Camera**。

      拍照。 然后点按&#x200B;**Use** ![use-pic](assets/use-pic.png)按钮。

      或点按&#x200B;**Retake** ![retake](assets/retake.png)按钮以重拍照片。

   1. 如果选择&#x200B;**Gallery**。

      此时会弹出设备的图像浏览器。 在设备的图片浏览器中，点按要附加的图片。

### 添加注释{#adding-a-note}

使用&#x200B;**Notes**&#x200B;选项，可在表单中添加手绘脚本和文本附件。

1. 点按窗口底部的附件按钮![attch](assets/attch.png)。
1. 在显示的弹出窗口中点按&#x200B;**注释**。
1. 在启动的“注释”用户界面中，捕获手绘。

   ![涂写界面](assets/scribble-ui.png)

   涂写

   您可以在涂写界面中使用以下选项：

   * **清除**:清除屏幕。
   * **“完成”按钮**:附加当前涂写。
   * **“取消”按钮**:放弃当前涂写并退出涂写用户界面。
   * ![键盘](assets/keyboard.png):清除涂写，并允许您添加文本注释。

   ![AEM Forms应用程序中的键盘涂写](assets/keyboard-inapp.png)

## 表单中的附件与AEM Forms服务器同步，但没有AEM Forms工作流(OSGi上的AEM Forms){#attachments-in-forms-synced-with-the-aem-forms-servers-without-aem-forms-workflow-aem-forms-on-osgi}

与AEM Forms OSGi服务器同步的移动表单的附件与AEM Forms JEE服务器类似。

从AEM Forms OSGi服务器在应用程序中加载的自适应表单不支持表单级别附件。 要附加图像或文本注释，请在创作表单时启用表单中的字段级附件。 将文件附件组件从组件浏览器拖放到字段上。

如果是自适应表单，则可以查看记录文档(DoR)中的附加文件。 请参阅[为非XFA自适应表单生成记录文档](../../forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)。
