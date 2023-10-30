---
title: HTML5表单与PDF forms之间的功能区别
description: 了解HTML5表单与PDF forms之间的差异。
uuid: 6ddee197-d108-4897-9976-77d115a06504
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: bdd97c20-d1f2-4898-9862-1a6a8071be88
docset: aem65
feature: Mobile Forms
exl-id: 3150f95f-7150-4eee-b5a9-121422dec2a1
source-git-commit: 0e5b89617d481c69882ec5d4658e76855aa9b691
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 2%

---

# HTML5表单与PDF forms之间的功能区别 {#feature-differentiation-between-html-forms-and-pdf-forms}

下表指定为HTML5表单和PDF forms提供的功能支持：

<table>
 <tbody>
  <tr>
   <th>专题</th>
   <th>HTML5 表单</th>
   <th>PDF</th>
  </tr>
  <tr>
   <td>条形码<br /> </td>
   <td>在用户界面级别不可用。 </td>
   <td>支持</td>
  </tr>
  <tr>
   <td>签名字段<br /> </td>
   <td><strong>数字签名</strong> 不受支持，但支持新的 <strong>潦草签名</strong> 为类似于纸的签名添加了字段。 人们可以在表格上用手写签名 <strong>潦草签名</strong> 字段。 签名将作为图像保存在表单上。 可将地理位置信息保存在 <strong>潦草签名</strong> 字段。</td>
   <td>签名字段可用于 <strong>数字签名</strong>.</td>
  </tr>
  <tr>
   <td>数据合并</td>
   <td>支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>图像</td>
   <td>数据URI方案用于显示图像。 所有现代版本的浏览器都支持此方案，但每个浏览器支持的图像格式范围有所不同。<br /> </td>
   <td>支持.gif、.png、.jpeg、.bmp和.tiff格式。</td>
  </tr>
  <tr>
   <td>分页<br /> </td>
   <td><p>HTML5窗体被分成多个面板和框，以使其外观类似于PDF forms。 页面大小会动态计算。 如果HTML5表单中页面的所有内容被删除或标记为隐藏，则空白页面将被隐藏，并且空白页面上方和下方页面之间不显示空格（空格）。</p> <p>如果数据合并或脚本向页面添加内容，则页面长度将展开以容纳新添加的内容。 表单中不会添加任何新页面，以适应新添加的内容。 </p> <p><strong>注意：</strong> 删除HTML5表单中页面的所有内容或将其标记为隐藏时，在第1页和第2页之间仍可看到空白页（空格），但在任何其他页面之间不可见。</p> </td>
   <td>PDF中的分页取决于合并的数据内容或用户内容，并且页面计数会因此而增加/减少。</td>
  </tr>
  <tr>
   <td>页眉/页脚 </td>
   <td>支持. <br /> <br /> 由于HTML5移动设备表单不支持分页符，因此页眉和页脚仅出现一次。 但是，您可以将它们设置为在移动设备表单预览中的多个位置显示。<br /> </td>
   <td>支持。</td>
  </tr>
  <tr>
   <td>自定义构件</td>
   <td>可以自定义小组件以增强移动设备的用户体验。<br /> </td>
   <td>所有构件都已锁定，无法插入自定义构件。<br /> </td>
  </tr>
  <tr>
   <td>XFA脚本API</td>
   <td>支持最常用的XFA脚本结构。 有关支持的构造的详细信息列表，请参见 <a href="/help/forms/using/scripting-support.md">脚本支持</a>.</td>
   <td>支持所有XFA脚本结构。</td>
  </tr>
  <tr>
   <td>Acrobat脚本API </td>
   <td>HTML5表单支持最常用的API。 有关详细信息，请参阅 <a href="/help/forms/using/scripting-support.md">脚本支持</a>.</td>
   <td>如果PDF文件在Acrobat或Reader中打开，则它还支持Acrobat提供的所有脚本API。</td>
  </tr>
  <tr>
   <td>支持从右至左的语言 </td>
   <td>支持</td>
   <td>支持</td>
  </tr>
 </tbody>
</table>

<!--Follow the best practices to enable a form template for HTML5 renditions and ensure that the behavior and appearance of HTML5 forms and XFA-based PDF is consistent. For detailed list of best practices, see [Best practices to design an HTML5 form.](/help/forms/using/best-practices-design-html5-forms.md)-->
