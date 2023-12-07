---
title: 在设计器中更改零页内容
description: 在非Adobe PDF查看器中查看XFAPDF时，您知道如何更改在该页面的第0页上显示的消息吗？
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
docset: aem65
feature: Adaptive Forms
exl-id: 466b7e85-a2f8-4e1e-8afc-1566b0ccb84c
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 0%

---

# 在设计器中更改零页内容 {#changing-page-zero-content-in-designer}

当非Adobe PDF查看器(如中的默认PDF查看器)时，默认显示零页内容 [!DNL Chrome] 或 [!DNL Firefox]，无法读取PDF/XFA表单的内容。 默认的Page Zero消息如下所示。

![defaultpage0message](assets/defaultpage0message.png)

[!DNL AEM Forms] Designer的版本允许您更改显示在第0页上的消息。 要更改Page Zero消息，请执行以下步骤：

1. 确保您拥有 [!DNL AEM Forms] 已安装设计器版本。 您可以从设计器的“关于”屏幕中检查版本。

1. 打开要为其更改“页面零”内容的表单。

1. 单击 **[!UICONTROL 文件]** > **[!UICONTROL 表单属性]**.

1. 在 [!UICONTROL 表单属性] 对话框，请单击 ![加](assets/plus.png) （加号图标）以添加自定义属性。

1. 指定 **_pagezerocontent** 作为资产的名称。
1. 以富文本格式添加新的“页面零”消息作为值。 例如：


   `<body xmlns="https://www.w3.org/1999/xhtml" xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/"><p style="font-family:'Times';font-size:12pt;letter-spacing:0in"><span style="xfa-spacerun:yes"> </code></p><p style="font-family:'Times';font-size:12pt;letter-spacing:0in">You are seeing this message maybe because you are using a non Adobe PDF Viewer or an Old version of Adobe Reader. You can upgrade to the latest version of Adobe Reader for Windows, Mac, or Linux by visiting <span style="xfa-spacerun:yes"> </code>https://www.adobe.com/go/reader_download.</p><p style="font-family:'Times';font-size:12pt;letter-spacing:0in"><span style="xfa-spacerun:yes"> </code></p><p style="font-family:'Times';font-size:12pt;letter-spacing:0in">For more assistance with Adobe Reader visit <span style="xfa-spacerun:yes"> </code>https://www.adobe.com/go/acrreader.</p></body>`

1. 将表单另存为PDF。

1. 在浏览器中查看PDF表单，确认消息已更新。 上面的示例值如下所示：

   ![更改消息](assets/changedmessage.png)

>[!NOTE]
>
>重新打开表单时，您创建的自定义属性可能无法正确显示在表单属性对话框中。 但是，它可正常使用，并且表单会显示更新的零页消息。
