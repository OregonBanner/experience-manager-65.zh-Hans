---
title: 在HTML5表单中使用涂写签名
seo-title: 在HTML5表单中使用涂写签名
description: HTML5表单在触控设备上的使用越来越多，一个常见要求是支持签名。 在移动设备上对文档进行签名正成为在移动设备上对表单进行签名的公认方式。
seo-description: HTML5表单在触控设备上的使用越来越多，一个常见要求是支持签名。 在移动设备上对文档进行签名正成为在移动设备上对表单进行签名的公认方式。
uuid: 163dd55a-971a-4dd4-93a7-a14e80184d9b
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: designer
discoiquuid: ecd7f538-9c24-48e7-8450-596851e99cff
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 0%

---


# 在HTML5表单中使用涂写签名{#using-scribble-signature-in-html-forms}

HTML5表单在触控设备上的使用越来越多，一个常见要求是支持签名。 划片（用手写笔或手指书写）正成为在移动设备上签署表单的一种公认方式。 HTML5表单和Forms设计器现在支持在表单上设置徒手签名字段的选项。 在浏览器中呈现表单时，您可以使用手写笔、鼠标或触摸在这些字段上签名。

## 如何使用“涂写签名”字段{#how-to-design-a-form-using-scribble-signature-field}设计表单

1. 在Forms设计师中打开表单。
1. 在页面上拖放“签名涂抹”字段。

   ![designer_scribble](assets/designer_scribble.png)

   >[!NOTE]
   >
   >在Forms设计器中选择的字段的Dimension会在渲染该字段时反映出来。 但是，渲染的签名框的尺寸是根据字段的长宽比计算的，而不是根据Forms设计器中指定的尺寸计算的。

1. 配置签名涂写字段。

   默认情况下，“签名涂抹”字段在iPad上的签名过程中将地理位置信息标记为必填（对于其他设备是可选的）。 更改`geoLocMandatoryOnIpad`属性的值可以覆盖此默认行为。 此属性在“签名涂写”字段中显示为额外内容。 修改它的步骤有：

   1. 在表单上，选择“签名涂写”字段。
   1. 选择&#x200B;**XML源**&#x200B;选项卡。

      >[!NOTE]
      >
      >要打开“XML源”选项卡，请单击&#x200B;**视图** > **XML源**。

   1. 在`<field>`标记中找到`<ui>`标记，并修改源代码，使其如下所示：

      ```xml
      <extras name="x-scribble-add-on">
      <boolean name="geoLocMandatoryOnIpad">0</boolean>
      </extras>
      ```

   1. 选择&#x200B;**设计视图**&#x200B;选项卡。 在确认框中，单击&#x200B;**是**。
   1. 保存表单。

1. 在支持的设备／桌面浏览器上渲染表单。

## 与涂写签名{#interfacing-with-the-scribble-signatures}接口

### 签名{#signing}

在将签名涂抹字段添加到表单并呈现后，单击或点按该字段会打开一个对话框。 用户可以使用鼠标、手指或手写笔在由虚线矩形指定的绘图区域中涂抹签名。

![地理位置](assets/geolocation.png)

**A.** 画 **笔B.** 橡皮 **擦** C.地 **理位** 置D.地理位置信息

### 地理标记{#geo-tagging}

在创建涂鸦时单击地理位置图标会导致地理位置和时间信息嵌入到字段中。

>[!NOTE]
在iPad上，默认情况下，必须嵌入地理位置信息。

在iPad上，默认情况下不显示地理位置图标，并且当您单击&#x200B;**确定**&#x200B;时，将自动嵌入地理位置信息。

对于iPad，可通过在字段的init参数中将`geoLocManadatoryOnIpad`参数的值修改为`0`来更改此设置。

* 当地理位置信息是强制的时候，向用户呈现减小的绘图区域。 当用户单击其余区域上的&#x200B;**OK**&#x200B;图标时，将添加地理位置文本。
* 在其他情况下，向用户显示一个完全可绘制区域。 如果用户选择嵌入地理位置信息，则调整该区域的大小以适应地理位置文本。

### 清除签名{#clearing-a-signature}

使用此功能时，用户可以单击&#x200B;**橡皮擦**&#x200B;图标以清除字段并开始。 如果添加了地理位置信息，也会清除该信息。

### 保存签名{#saving-a-signature}

单击&#x200B;**OK**&#x200B;图标，将涂写内容保存为字段中的图像。 图像和值可提交到服务器以进一步处理。 用户单击&#x200B;**OK**&#x200B;后，涂抹字段将被锁定。 无法使用涂写构件再次编辑签名。

点按或单击“涂抹”字段将以只读模式打开对话框。

![3](assets/3.png)

### 选择笔大小{#selecting-pen-size}

单击&#x200B;**画笔**&#x200B;图标以显示可用笔大小的列表。 单击或点按笔大小以使用相应的笔。

### 从表单{#delete-signatures-from-the-form}中删除签名

要从表单中删除签名：

* （移动设备）长按签名字段，在确认对话框中，点按&#x200B;**是**。
* （桌面）将指针悬停在签名字段上方，单击&#x200B;**取消**&#x200B;图标，在确认对话框中，单击&#x200B;**是**。
