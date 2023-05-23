---
title: HTML5表單與PDF forms之間的功能差異
seo-title: Feature differentiation between HTML5 forms and PDF forms
description: HTML5表單和PDF forms支援的功能
seo-description: Feature supported in HTML5 forms and PDF forms
uuid: 6ddee197-d108-4897-9976-77d115a06504
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: bdd97c20-d1f2-4898-9862-1a6a8071be88
docset: aem65
feature: Mobile Forms
exl-id: 3150f95f-7150-4eee-b5a9-121422dec2a1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 2%

---

# HTML5表單與PDF forms之間的功能差異 {#feature-differentiation-between-html-forms-and-pdf-forms}

下表指定為HTML5表單和PDF forms提供的功能支援：

<table>
 <tbody>
  <tr>
   <th>专题</th>
   <th>HTML5 表单</th>
   <th>PDF</th>
  </tr>
  <tr>
   <td>條碼<br /> </td>
   <td>無法在使用者介面層級使用。 </td>
   <td>支持</td>
  </tr>
  <tr>
   <td>簽章欄位<br /> </td>
   <td><strong>數位簽名</strong> 不支援此功能，但新增 <strong>手寫簽名</strong> 欄位會新增為類似紙本簽章的欄位。 使用者可以使用在表單上塗寫簽名 <strong>手寫簽名</strong> 欄位。 簽名會以影像形式儲存在表單上。 您可以將地理位置資訊儲存在 <strong>手寫簽名</strong> 欄位。</td>
   <td>簽名欄位可用於 <strong>數位簽名</strong>.</td>
  </tr>
  <tr>
   <td>資料合併</td>
   <td>支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>图像</td>
   <td>資料URI配置用於顯示影像。 所有現代版的瀏覽器都支援此配置，但每個瀏覽器支援的影像格式範圍有所不同。<br /> </td>
   <td>支援.gif、.png、.jpeg、.bmp和.tiff格式。</td>
  </tr>
  <tr>
   <td>分页<br /> </td>
   <td><p>HTML5表單會分成面板和方塊，以提供類似於PDF forms的外觀。 頁面大小會以動態方式計算。 如果HTML5表單中頁面的所有內容都已刪除或標籤為隱藏，則會隱藏空白頁面，且空白頁面上方與下方的頁面之間不會顯示空白空間（空格）。</p> <p>如果資料合併或指令碼新增內容至頁面，則頁面長度會展開以容納新新增的內容。 表單中不會新增任何新頁面，以容納新新增的內容。 </p> <p><strong>注意：</strong> 刪除HTML5表單中頁面的所有內容或將其標籤為隱藏時，空白頁面（空格）在第1頁和第2頁之間保持可見，但在任何其他頁面之間不顯示。</p> </td>
   <td>PDF中的分頁取決於合併的資料內容或使用者內容，而頁面計數會據此增加/減少。</td>
  </tr>
  <tr>
   <td>頁首/頁尾 </td>
   <td>支持. <br /> <br /> 由於HTML5行動表單不支援分頁符號，頁首和頁尾只會出現一次。 不過，您可以將其設定在版面中，以顯示在行動表單預覽中的多個位置。<br /> </td>
   <td>支持。</td>
  </tr>
  <tr>
   <td>自訂Widget</td>
   <td>您可以自訂Widget來增強行動裝置上的使用者體驗。<br /> </td>
   <td>所有Widget都已鎖定，無法插入自訂Widget。<br /> </td>
  </tr>
  <tr>
   <td>XFA指令碼API</td>
   <td>支援最常用的XFA指令碼建構。 如需支援的建構詳細資訊清單，請參閱 <a href="/help/forms/using/scripting-support.md">指令碼支援</a>.</td>
   <td>支援所有XFA指令碼建構。</td>
  </tr>
  <tr>
   <td>Acrobat指令碼API </td>
   <td>HTML5表單支援最常用的API。 如需詳細資訊，請參閱 <a href="/help/forms/using/scripting-support.md">指令碼支援</a>.</td>
   <td>如果PDF檔案是在Acrobat或Reader中開啟，它也會支援Acrobat提供的所有指令碼API。</td>
  </tr>
  <tr>
   <td>支援由右至左語言 </td>
   <td>支持</td>
   <td>支持</td>
  </tr>
 </tbody>
</table>

<!--Follow the best practices to enable a form template for HTML5 renditions and ensure that the behavior and appearance of HTML5 forms and XFA-based PDF is consistent. For detailed list of best practices, see [Best practices to design an HTML5 form.](/help/forms/using/best-practices-design-html5-forms.md)-->
