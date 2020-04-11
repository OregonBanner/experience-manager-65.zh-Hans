---
title: 添加附件
seo-title: 添加附件
description: 在AEM Forms应用程序中将照片和涂鸦附注添加为任务的注释
seo-description: 在AEM Forms应用程序中将照片和涂鸦附注添加为任务的注释
uuid: 3d2738b4-fd43-44ec-8eaf-a2ad4b7e5af5
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: d5976ed2-4482-495c-bf77-6d192379cfef
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# 添加附件{#adding-attachments}

## 在与AEM Forms Workflow服务器同步的表单中添加附件（JEE上的AEM Forms） {#adding-annotations}

通过AEM Forms应用程序，您可以将图像、草图注释和文本注释附加到与AEM Forms JEE服务器同步的表单中。 如果您的表单是从AEM Forms Workflow服务器加载的，则您的附件将添加到表单。 您可以点按附件按钮 ![attachments-app](assets/attachments-app.png) ，一起查看表单中的所有附件。 红色通知指定表单中的附件数。 如果表单中没有附件，则看不到红色通知按钮。 如果表单中没有附件，则点按附件按钮附件时 ![](assets/attch.png)，您可以选择附加照片或涂鸦。

您的选择包括：

* **画廊**:允许您根据保存在设备上的图片添加图片。

* **相机**:允许您拍摄照片并将其添加到表单中。

* **注意**:允许您添加涂鸦或文本注释。 使用 ![涂鸦](assets/scribble.png) ，添加涂鸦， ![使用键盘](assets/keyboard.png) ，添加文本注释。

>[!NOTE]
>
>其他用户添加的附件对其他AEM Forms应用程序用户可见。 其他用户无法删除用户添加的附件。


### “附件”屏幕 {#the-attachments-screen}

要查看某个位置中的所有附件，请点按 ![attachments-app](assets/attachments-app.png)。 您可以在此处添加、重命名和删除附件。

![位置中的所有附件](assets/attachments-screen.png)

可以使用“附 **件”屏** 幕中的+按钮附加另一张图片、涂鸦或文本。

### 添加照片 {#adding-a-photograph}

您可以使用移动设备的相机或设备中保存的图片附加表单中的图片。

1. 点按窗口底 ![部的](assets/attch.png) “附件”按钮。
1. 在显 **示的弹** 出窗口中点按“画廊 **** ”或“摄像机”。
1. 根据您选择的选项，执行以下操作：

   1. 选择“摄 **像机**”。

      拍照。 然后点按 **Use** ![use-pic按钮](assets/use-pic.png) 。

      或点按“重 **拍**![](assets/retake.png) ”按钮以重拍照片。

   1. 如果选择“ **画廊”**。

      弹出设备的图像浏览器。 在设备的图片浏览器中，点按要附加的图片。

### 添加备注 {#adding-a-note}

“备 **注** ”选项允许您在表单中添加手绘脚本和文本附件。

1. 点按窗口底 ![部的](assets/attch.png) “附件”按钮。
1. 点 **按显示** 的弹出窗口中的“附注”。
1. 在启动的“备注”用户界面中，捕获徒手涂鸦。

   ![涂抹界面](assets/scribble-ui.png)

   涂鸦

   您可以在“涂写”界面中使用以下选项：

   * **清除**:清除屏幕。
   * **完成按钮**:附加当前涂鸦。
   * **“取消”按钮**:放弃当前涂鸦，并退出涂鸦用户界面。
   * ![键盘](assets/keyboard.png):清除涂鸦，并允许您添加文本注释。
   ![AEM Forms应用程序涂鸦式中的键盘](assets/keyboard-inapp.png)

## 与AEM Forms服务器同步的表单中的附件，但不带AEM Forms Workflow（OSGi上的AEM Forms） {#attachments-in-forms-synced-with-the-aem-forms-servers-without-aem-forms-workflow-aem-forms-on-osgi}

与AEM Forms OSGi服务器同步的移动表单附件的工作方式与AEM Forms JEE服务器类似。

从AEM Forms OSGi服务器加载到应用程序中的自适应表单不支持表单级别附件。 要附加图像或文本附注，请在创作表单时启用表单中的字段级附件。 将文件附件组件从组件浏览器拖放到字段上。

对于自适应表单，您可以在记录文档(DoR)中视图附加的文件。 请参 [阅为非XFA自适应表单生成记录文档](../../forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)。
