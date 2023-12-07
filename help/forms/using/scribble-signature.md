---
title: 在HTML5表单中使用涂写签名
description: HTML5表单越来越多地用于触摸设备，并且通常会要求支持签名。 在移动设备上签署文档已成为一种可接受的在移动设备上签署表单的方式。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: designer
docset: aem65
feature: Designer
exl-id: 2025182f-195b-40d0-aee7-67669f55b964
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 0%

---

# 在HTML5表单中使用涂写签名{#using-scribble-signature-in-html-forms}

HTML5表单越来越多地用于触摸设备，并且通常会要求支持签名。 脚本编写（使用手写笔或手指书写）正在成为在移动设备上签名表单的一种可接受的方式。 HTML5表单和Forms Designer现在启用了表单上涂写签名字段的选项。 在浏览器中呈现表单时，可以使用手写笔、鼠标或触摸登录这些字段。

## 如何使用涂鸦签名字段设计表单 {#how-to-design-a-form-using-scribble-signature-field}

1. 在Forms Designer中打开表单。
1. 将签名涂写字段拖放到页面上。

   ![designer_scribble](assets/designer_scribble.png)

   >[!NOTE]
   >
   >呈现字段时，将反映在Forms Designer中选择的字段的Dimension。 但是，呈现的签名框的尺寸是根据字段的长宽比计算的，而不是根据Forms Designer中指定的尺寸计算的。

1. 配置签名涂写字段。

   默认情况下，签名涂写字段将地理位置信息标记为在iPad上的签名过程中必需（对于其他设备而言，该字段是可选的）。 此默认行为可以通过更改 `geoLocMandatoryOnIpad` 属性。 此属性在签名涂写字段中作为附加项显示。 修改它的步骤如下：

   1. 在表单上，选择签名涂写字段。
   1. 选择 **XML源** 选项卡。

      >[!NOTE]
      >
      >要打开“XML源”选项卡，请单击 **视图** > **XML源**.

   1. 找到 `<ui>` 标记中 `<field>` 标记并修改源代码，使其如下所示：

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
>
默认情况下，iPad上的嵌入地理位置信息是必需的。

在iPad上，默认情况下，不显示地理位置图标，当您单击时，会自动嵌入地理位置信息 **确定**.

对于iPad，可以通过修改 `geoLocManadatoryOnIpad` 参数至 `0`、字段的初始化参数中的。

* 当地理位置信息是强制性的时，用户会看到一个缩小的绘制区域。 用户单击时添加地理位置文本 **确定** 图标。
* 在其他情况下，用户会看到一个完整的可绘制区域。 如果用户选择嵌入地理位置信息，则将调整此区域大小以适应地理位置文本。

### 清除签名 {#clearing-a-signature}

使用此功能时，用户可以单击 **橡皮擦** 图标以清除字段，然后重新开始。 如果添加了地理位置信息，则也会清除该信息。

### 保存签名 {#saving-a-signature}

单击 **确定** 图标将涂鸦另存为字段中的图像。 图像和值可以提交到服务器以供进一步处理。 用户单击后 **确定**，涂鸦字段被锁定。 无法使用涂写构件再次编辑签名。

点击或单击涂写字段会以只读模式打开对话框。

![3](assets/3.png)

### 选择钢笔大小 {#selecting-pen-size}

单击 **画笔** 图标，以显示可用钢笔大小的列表。 单击笔大小以使用相应的笔。

### 从表单中删除签名 {#delete-signatures-from-the-form}

要从表单中删除签名，请执行以下操作：

* （移动设备）长按签名字段，然后在确认对话框上选择 **是**.
* （桌面）将鼠标悬停在签名字段上，单击 **取消** 图标，然后在确认对话框中，单击 **是**.
