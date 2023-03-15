---
title: 在HTML5表单中使用涂写签名
seo-title: Using Scribble Signature in HTML5 forms
description: HTML5表单越来越多地用于触控设备，并且通常会要求支持签名。 在移动设备上签署文档正成为在移动设备上签署表单的普遍方式。
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

HTML5表单越来越多地用于触控设备，并且通常会要求支持签名。 涂写（用手写笔或手指书写）正在成为在移动设备上签署表单的一种公认方式。 HTML5表单和Forms Designer现在启用了表单上涂写签名字段的选项。 在浏览器中呈现表单时，可以使用手写笔、鼠标或触摸来登录这些字段。

## 如何使用涂鸦签名字段设计表单 {#how-to-design-a-form-using-scribble-signature-field}

1. 在Forms Designer中打开表单。
1. 将“签名涂鸦”字段拖放到页面上。

   ![designer_scribble](assets/designer_scribble.png)

   >[!NOTE]
   >
   >在Forms Designer中选择的字段的Dimension在呈现该字段时反映出来。 但是，已渲染签名框的尺寸是根据字段的长宽比计算的，而不是根据Forms Designer中指定的尺寸计算的。

1. 配置“签名涂鸦”字段。

   默认情况下，“签名涂鸦”字段在iPad上的签名过程中将地理位置信息标记为必需（对于其他设备而言，该字段是可选的）。 此默认行为可以通过更改 `geoLocMandatoryOnIpad` 属性。 此属性在“签名涂鸦字段”中作为附加项显示。 修改它的步骤如下：

   1. 在表单上，选择签名涂写字段。
   1. 选择 **XML源** 选项卡。

      >[!NOTE]
      >
      >要打开“XML源”选项卡，请单击 **视图** > **XML源**.

   1. 找到 `<ui>` 标记中 `<field>` 标记并修改源代码，使其类似于以下内容：

      ```xml
      <extras name="x-scribble-add-on">
      <boolean name="geoLocMandatoryOnIpad">0</boolean>
      </extras>
      ```

   1. 选择 **设计视图** 选项卡。 在确认框中，单击 **是**.
   1. 保存表单。

1. 在支持的设备/桌面浏览器上渲染表单。

## 与Scribble签名连接 {#interfacing-with-the-scribble-signatures}

### 签名 {#signing}

在将签名涂写字段添加到表单并呈现后，单击或点按该字段会打开一个对话框。 用户可以使用鼠标、手指或手写笔在虚线矩形指定的绘制区域中涂写签名。

![地理位置](assets/geolocation.png)

**答：** 画笔 **B.** 橡皮擦 **C.** 地理位置 **D.** 地理位置信息

### 地理标记 {#geo-tagging}

创建涂鸦时单击地理位置图标会导致地理位置和时间信息嵌入到字段中。

>[!NOTE]
默认情况下，在iPad上，嵌入地理位置信息是必需的。

在iPad上，默认情况下不显示地理位置图标，当您单击时，会自动嵌入地理位置信息 **确定**.

对于iPad，可以通过修改 `geoLocManadatoryOnIpad` 参数至 `0`，在字段的init参数中。

* 当地理位置信息是必填信息时，将为用户显示一个缩小的绘制区域。 用户单击时添加地理位置文本 **确定** 图标。
* 在其他情况下，用户会看到一个完整的可绘制区域。 如果用户选择嵌入地理位置信息，则将调整此区域大小以适应地理位置文本。

### 清除签名 {#clearing-a-signature}

使用此功能时，用户可以单击 **橡皮擦** 图标以清除字段，然后重新开始。 如果添加了地理位置信息，则也会清除该信息。

### 保存签名 {#saving-a-signature}

单击 **确定** 图标将涂鸦另存为字段中的图像。 可将图像和值提交到服务器以供进一步处理。 用户单击后 **确定**，涂写字段被锁定。 无法使用涂鸦构件再次编辑签名。

点击或单击涂写字段以只读模式打开对话框。

![3](assets/3.png)

### 选择钢笔大小 {#selecting-pen-size}

单击 **画笔** 图标，以显示可用钢笔大小的列表。 单击或点按笔大小以使用相应的笔。

### 从表单中删除签名 {#delete-signatures-from-the-form}

要从表单中删除签名，请执行以下操作：

* （移动设备）长按签名字段，然后在确认对话框中，点按 **是**.
* （桌面）将鼠标悬停在签名字段上，单击 **取消** 图标，然后在确认对话框中，单击 **是**.
