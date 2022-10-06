---
title: 在HTML5表单中使用涂写签名
seo-title: Using Scribble Signature in HTML5 forms
description: HTML5表单在触屏设备上越来越常用，一种常见要求是支持签名。 在移动设备上签署文档已成为在移动设备上签署表单的一种可接受方式。
seo-description: HTML5 forms are increasingly used on touch devices, and one common requirement is to support signatures. Signing documents on mobile devices is becoming an accepted way of signing forms on mobile devices.
uuid: 163dd55a-971a-4dd4-93a7-a14e80184d9b
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: designer
discoiquuid: ecd7f538-9c24-48e7-8450-596851e99cff
docset: aem65
feature: Designer
exl-id: 2025182f-195b-40d0-aee7-67669f55b964
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '658'
ht-degree: 0%

---

# 在HTML5表单中使用涂写签名{#using-scribble-signature-in-html-forms}

HTML5表单在触屏设备上的使用越来越多，一种常见要求是支持签名。 划线（用手写笔或手指书写）正成为在移动设备上签署表格的一种可接受方式。 HTML5表单和Forms Designer现在允许在表单上使用涂写签名字段的选项。 在浏览器中呈现表单后，您可以使用手写笔、鼠标或触摸在这些字段上登录。

## 如何使用潦草签名字段设计表单 {#how-to-design-a-form-using-scribble-signature-field}

1. 在Forms Designer中打开表单。
1. 将签名潦草字段拖放到页面上。

   ![designer_scribble](assets/designer_scribble.png)

   >[!NOTE]
   >
   >在Forms Designer中选择的字段的Dimension在呈现该字段时反映。 但是，渲染的签名框的维度是根据字段的宽高比计算的，而不是根据Forms Designer中指定的维度计算的。

1. 配置签名潦草字段。

   默认情况下，“签名潦草”字段会将地理位置信息标记为iPad上签名过程中的必填项（对于其他设备而言，它是可选项）。 通过更改 `geoLocMandatoryOnIpad` 属性。 此属性在签名潦草字段中作为额外显示。 修改该报表包的步骤如下：

   1. 在窗体上，选择签名潦草字段。
   1. 选择 **XML源** 选项卡。

      >[!NOTE]
      >
      >要打开“XML源”选项卡，请单击 **查看** > **XML源**.

   1. 找到 `<ui>` 标记 `<field>` 标记并修改源代码，使其如下所示：

      ```xml
      <extras name="x-scribble-add-on">
      <boolean name="geoLocMandatoryOnIpad">0</boolean>
      </extras>
      ```

   1. 选择 **设计视图** 选项卡。 在确认框中，单击 **是**.
   1. 保存表单。

1. 在支持的设备/桌面浏览器上渲染表单。

## 与涂写签名连接 {#interfacing-with-the-scribble-signatures}

### 签名 {#signing}

将签名潦草字段添加到表单并渲染后，单击或点按该字段会打开一个对话框。 用户可以使用鼠标、手指或手写笔在由点线矩形指定的绘制区域中涂写签名。

![地理位置](assets/geolocation.png)

**A.** 画笔 **B.** 橡皮擦 **C.** 地理位置 **D.** 地理位置信息

### 地理标记 {#geo-tagging}

在创建涂写时单击地理位置图标会导致地理位置和时间信息嵌入到字段中。

>[!NOTE]
在iPad上，默认情况下必须嵌入地理位置信息。

在iPad上，默认情况下不显示地理位置图标，并且在单击 **确定**.

对于iPad，可通过修改 `geoLocManadatoryOnIpad` 参数 `0`，位于字段的init参数中。

* 当地理位置信息是强制性的时，向用户呈现缩小的绘制区域。 当用户单击时，将添加地理位置文本 **确定** 图标。
* 在其他情况下，向用户显示完整的可绘制区域。 如果用户选择嵌入地理位置信息，则会调整此区域的大小以适应地理位置文本。

### 清除签名 {#clearing-a-signature}

使用此功能时，用户可以单击 **橡皮擦** 图标以清除字段，然后重新开始。 如果添加了地理位置信息，则也会清除该信息。

### 保存签名 {#saving-a-signature}

单击 **确定** 图标会将潦草的文字另存为字段中的图像。 图像和值可提交到服务器以进一步处理。 用户单击后 **确定**，则潦草字段会被锁定。 无法使用涂写小组件再次编辑签名。

点按或单击涂写字段会以只读模式打开对话框。

![3](assets/3.png)

### 选择笔大小 {#selecting-pen-size}

单击 **画笔** 图标以显示可用笔大小列表。 单击或点按笔大小以使用相应的笔。

### 从表单中删除签名 {#delete-signatures-from-the-form}

要从表单中删除签名：

* （移动设备）长按签名字段，然后在确认对话框中，点按 **是**.
* （桌面）将鼠标悬停在签名字段上，单击 **取消** 图标，然后在确认对话框上单击 **是**.
