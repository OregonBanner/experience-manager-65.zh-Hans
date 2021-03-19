---
title: HTML5表单与PDF forms之间的功能区别
seo-title: HTML5表单与PDF forms之间的功能区别
description: HTML5表单和PDF forms中支持的功能
seo-description: HTML5表单和PDF forms中支持的功能
uuid: 6ddee197-d108-4897-9976-77d115a06504
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: bdd97c20-d1f2-4898-9862-1a6a8071be88
docset: aem65
feature: 移动设备表单
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 3%

---


# HTML5表单与PDF forms的功能区别{#feature-differentiation-between-html-forms-and-pdf-forms}

下表指定了对HTML5表单和PDF forms提供的功能支持：

<table>
 <tbody>
  <tr>
   <th>功能</th>
   <th>HTML5 表单</th>
   <th>PDF</th>
  </tr>
  <tr>
   <td>条码<br /> </td>
   <td>用户界面级别不可用。 </td>
   <td>支持</td>
  </tr>
  <tr>
   <td>签名字段<br /> </td>
   <td><strong>不支</strong> 持数字签名，但会为类似签 <strong>名的</strong> 纸质文档添加一个新的Scribble Signaturefield。您可以使用<strong>“涂抹签名</strong>”字段在表单上涂抹其签名。 签名将作为图像保存在表单中。 可以在<strong>“涂抹签名</strong>”字段中保存地理位置信息。</td>
   <td>可用于<strong>数字签名</strong>的签名字段。</td>
  </tr>
  <tr>
   <td>数据合并</td>
   <td>支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>图像</td>
   <td>数据URI方案用于显示图像。 所有现代版本的浏览器都支持此方案，但每个浏览器支持的图像格式范围存在差异。<br /> </td>
   <td>支持.gif、.png、.jpeg、.bmp和.tiff格式。</td>
  </tr>
  <tr>
   <td>分页<br /> </td>
   <td><p>HTML5表单被分为面板和框，使其外观与PDF forms相似。 页面的大小是动态计算的。 如果HTML5表单中页面的所有内容被删除或标记为隐藏，则空白页面将被隐藏，空白页面上方和下方的页面之间不显示空白（空格）。</p> <p>如果数据合并或脚本向页面添加内容，则页面的长度会扩展以容纳新添加的内容。 表单中不会添加新页面以容纳新添加的内容。 </p> <p><strong>注意：</strong> 当HTML5表单中页面的所有内容被删除或标记为隐藏时，空白页面（空格）在第1页和第2页之间保持可见，但在任何其他页面之间不可见。</p> </td>
   <td>PDF中的分页取决于合并的数据内容或用户内容，并且页面计数会据此增加/减少。</td>
  </tr>
  <tr>
   <td>页眉/页脚 </td>
   <td>支持。<br /> <br /> 由于HTML5移动表单不支持分页，因此页眉和页脚只显示一次。但是，您可以在布局中设置它们，使其显示在移动表单预览的多个位置。<br /> </td>
   <td>支持。</td>
  </tr>
  <tr>
   <td>自定义构件</td>
   <td>您可以自定义构件以增强移动设备上的用户体验。<br /> </td>
   <td>所有Widget都处于锁定状态，无法插入自定义Widget。<br /> </td>
  </tr>
  <tr>
   <td>XFA Script API</td>
   <td>支持最常用的XFA脚本构造。 有关所支持构造的详细列表，请参阅<a href="/help/forms/using/scripting-support.md">脚本支持</a>。</td>
   <td>支持所有XFA脚本构造。</td>
  </tr>
  <tr>
   <td>Acrobat Script API </td>
   <td>HTML5表单支持最常用的API。 有关详细信息，请参阅<a href="/help/forms/using/scripting-support.md">脚本支持</a>。</td>
   <td>如果在Acrobat或Reader中打开PDF文件，它还支持Acrobat提供的所有脚本API。</td>
  </tr>
  <tr>
   <td>支持从右到左的语言 </td>
   <td>支持</td>
   <td>支持</td>
  </tr>
 </tbody>
</table>

<!--Follow the best practices to enable a form template for HTML5 renditions and ensure that the behavior and appearance of HTML5 forms and XFA-based PDF is consistent. For detailed list of best practices, see [Best practices to design an HTML5 form.](/help/forms/using/best-practices-design-html5-forms.md)-->
