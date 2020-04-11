---
title: 在HTML5表单中使用涂抹签名
seo-title: 在HTML5表单中使用涂抹签名
description: HTML5表单在触控设备上的使用越来越多，一个常见要求是支持签名。 在移动设备上签署文档正成为在移动设备上签署表单的一种可接受方式。
seo-description: HTML5表单在触控设备上的使用越来越多，一个常见要求是支持签名。 在移动设备上签署文档正成为在移动设备上签署表单的一种可接受方式。
uuid: 163dd55a-971a-4dd4-93a7-a14e80184d9b
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: designer
discoiquuid: ecd7f538-9c24-48e7-8450-596851e99cff
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# 在HTML5表单中使用涂抹签名{#using-scribble-signature-in-html-forms}

HTML5表单在触控设备上的使用越来越多，一个常见要求是支持签名。 划线（用手写笔或手指书写）正成为在移动设备上签署表单的一种可接受方式。 HTML5表单和表单设计器现在启用在表单上具有涂抹签名字段的选项。 当表单在浏览器中呈现时，您可以使用手写笔、鼠标或触控在这些字段上签名。

## 如何使用“涂写签名”字段设计表单 {#how-to-design-a-form-using-scribble-signature-field}

1. 在Forms Designer中打开表单。
1. 将“签名涂鸦”字段拖放到页面上。

   ![designer_scribble](assets/designer_scribble.png)

   >[!NOTE]
   >
   >呈现表单设计器中选定字段的尺寸会反映在该字段中。 但是，渲染的签名框的尺寸是根据字段的长宽比计算的，而不是根据Forms Designer中指定的尺寸计算的。

1. 配置“签名涂写”字段。

   默认情况下，“签名涂鸦”字段在iPad上的签名过程中将地理位置信息标记为必填（对于其他设备而言为可选）。 通过更改属性的值可以覆盖此默认行 `geoLocMandatoryOnIpad` 为。 此属性在“签名涂鸦字段”中显示为额外内容。 修改它的步骤有：

   1. 在表单上，选择“签名涂鸦”字段。
   1. 选择“ **XML源** ”选项卡。

      >[!NOTE]
      >
      >要打开“XML源”选项卡，请单击“ **视图** ”>“ **XML源”**。

   1. 在标记 `<ui>` 中找到标记 `<field>` 并修改源代码，使其如下所示：

      ```xml
      <extras name="x-scribble-add-on">
      <boolean name="geoLocMandatoryOnIpad">0</boolean>
      </extras>
      ```

   1. 选择“设 **计视图** ”选项卡。 在确认框中，单击“ **是”**。
   1. 保存表单。

1. 在支持的设备／桌面浏览器上渲染表单。

## 与涂写签名接口 {#interfacing-with-the-scribble-signatures}

### 签名 {#signing}

在将签名涂鸦字段添加到表单并呈现后，单击或点按该字段会打开一个对话框。 用户可以使用鼠标、手指或手写笔在由点线矩形指定的绘制区域中涂抹签名。

![地理位置](assets/geolocation.png)

**答：** 画笔 **B。** 橡皮 **擦C.** 地理位 **置D。** 地理位置信息

### 地理标记 {#geo-tagging}

在创建涂抹图时单击地理位置图标会导致地理位置和时间信息嵌入到字段中。

>[!NOTE]
在iPad上，默认情况下，必须嵌入地理位置信息。

在iPad上，默认情况下不显示geolocation图标，单击“确定”时会自动嵌入geolocation **信息**。

对于iPad，可通过将字段的init参数中的参 `geoLocManadatoryOnIpad` 数值 `0`修改为来更改此设置。

* 当地理位置信息是必需的时候，向用户呈现缩小的绘制区域。 当用户单击其余区域上的“确 **定** ”图标时，将添加地理位置文本。
* 在其他情况下，向用户显示完整的可绘制区域。 如果用户选择嵌入地理位置信息，则会调整该区域的大小以容纳地理位置文本。

### 清除签名 {#clearing-a-signature}

使用此功能时，用户可以单击“橡皮擦 **** ”图标以清除字段并开始。 如果添加了地理位置信息，则也会清除该信息。

### 保存签名 {#saving-a-signature}

单击“确 **定** ”图标，将涂抹内容保存为字段中的图像。 图像和值可提交到服务器以进一步处理。 用户单击“确 **定**”后，涂写字段将被锁定。 无法使用涂抹构件再次编辑签名。

点按或单击“涂抹”字段将以只读模式打开对话框。

![3](assets/3.png)

### 选择钢笔大小 {#selecting-pen-size}

单击“ **画笔** ”图标以显示可用笔大小的列表。 单击或点按钢笔大小以使用相应的钢笔。

### 从表单中删除签名 {#delete-signatures-from-the-form}

要从表单中删除签名，请执行以下操作：

* （移动设备）长按签名字段，然后在确认对话框中点按 **是**。
* （桌面）将指针悬停在签名字段上，单击“取 **消** ”图标，然后在确认对话框中，单击“ **是”**。
