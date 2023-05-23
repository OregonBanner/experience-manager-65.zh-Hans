---
title: 「教學課程：建立最適化表單」
seo-title: Create an adaptive form
description: 瞭解如何建立、佈局和預覽最適化表單。 另外，瞭解如何設定提交動作。
seo-description: Learn to create, layout, and preview an adaptive form. Also, learn to configure submit actions.
page-status-flag: de-activated
uuid: 0010d274-a683-499e-9fa6-ce355d7898a0
discoiquuid: 55c08940-8c25-4938-8e49-25bce20aaf22
feature: Adaptive Forms
exl-id: c0a2adcd-528a-41af-99b5-d8b423cd6605
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '1376'
ht-degree: 3%

---

# 教學課程：建立最適化表單 {#do-not-publish-tutorial-create-an-adaptive-form}

![02-create-adaptive-form-main-image](assets/02-create-adaptive-form-main-image.png)

本教學課程是 [建立第一個最適化表單](/help/forms/using/create-your-first-adaptive-form.md) 數列。 建議您依照時間順序觀看本系列，以瞭解、執行和示範完整的教學課程使用案例。

## 關於教學課程 {#about-the-tutorial}

調適型表單是新一代的表單，可動態且回應。 您可以使用調適型表單來提供個人化體驗。 您也可以整合最適化表單與 [!DNL Adobe Analytics] 使用狀況統計資料和 [!DNL Adobe Campaign] 用於行銷活動管理。 如需最適化表單功能的詳細資訊，請參閱 [製作調適型表單簡介](/help/forms/using/introduction-forms-authoring.md).

遵循適當的程式後，可更輕鬆建立及管理表單。 在本文章中，您將瞭解如何：

* [建立可讓客戶新增送貨地址的最適化表單](/help/forms/using/create-adaptive-form.md#step-create-the-adaptive-form)

* [用於顯示和接受客戶資訊的最適化表單的版面配置欄位](/help/forms/using/create-adaptive-form.md#step-add-header-and-footer)

* [建立提交動作以傳送包含表單內容的電子郵件](/help/forms/using/create-adaptive-form.md#step-add-components-to-capture-and-display-information)
* [預覽和提交最適化表單](/help/forms/using/create-adaptive-form.md)

在文章結尾處，您的表單將類似於以下內容：\
[![](do-not-localize/form-preview-mobile.gif)](do-not-localize/form-preview-mobile.gif)

## 步驟1：建立最適化表單 {#step-create-the-adaptive-form}

1. 登入AEM編寫執行個體並導覽至 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms與檔案]**. 預設URL為 [http://localhost:4502/aem/forms.html/content/dam/formsanddocuments](http://localhost:4502/aem/forms.html/content/dam/formsanddocuments).
1. 點選 **[!UICONTROL 建立]** 並選取 **[!UICONTROL 最適化表單]**. 隨即顯示選取範本的選項。 點選 **[!UICONTROL 空白]** 範本以選取並點選 **[!UICONTROL 下一個]**.

1. 的選項 **[!UICONTROL 新增屬性]** 出現。 此 **[!UICONTROL 標題]** 和 **[!UICONTROL 名稱]** 欄位為必填欄位：

   * **標題：** 指定 `Add new or update shipping address` 在 **[!UICONTROL 標題]** 欄位。 標題欄位會指定表單的顯示名稱。 標題可協助您識別AEM中的表單 [!DNL Forms] 使用者介面。
   * **名稱：** 指定 `shipping-address-add-update-form` 在 **[!UICONTROL 名稱]** 欄位。 「名稱」欄位指定表單的名稱。 在存放庫中會建立具有指定名稱的節點。 當您開始輸入標題時，會自動產生名稱欄位的值。 您可以變更建議值。 名稱欄位只能包含英數字元、連字型大小和底線。 所有無效輸入都會以連字型大小取代。

1. 點選 **[!UICONTROL 建立]**. 系統隨即會建立最適化表單，並顯示對話方塊以開啟表單進行編輯。 點選 **[!UICONTROL 開啟]** 以在新標籤中開啟新建立的表單。 表單隨即開啟以進行編輯。 它也會顯示側邊欄，以根據需求自訂新建立的表單。

   如需最適化表單製作介面和可用元件的相關資訊，請參閱 [製作調適型表單簡介](/help/forms/using/creating-adaptive-form.md).

   ![新建立的 — adaptive-form](assets/newly-created-adaptive-form.png)

## 步驟2：新增頁首和頁尾 {#step-add-header-and-footer}

AEM [!DNL Forms] 提供許多元件，可在最適化表單上顯示資訊。 頁首和頁尾元件有助於提供一致的外觀和感覺。 頁首通常包含企業的標誌、表單標題和摘要。 頁尾通常包含版權資訊和其他頁面的連結。

1. 點選 ![切換側面板](assets/toggle-side-panel.png) > ![treeexpandall](assets/treeexpandall.png). 元件瀏覽器隨即開啟。 拖曳 **[!UICONTROL 頁首]** 元件從元件瀏覽器變更為最適化表單。
1. 點選 **[!UICONTROL 標誌]**. 工具列隨即顯示。 點選 ![aem_6_3_edit](assets/aem_6_3_edit.png) 在工具列上，輸入 **We.Retail**，然後點選 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

1. 點選「影像」。 工具列隨即顯示。 點選 ![cmppr](assets/cmppr.png). 屬性瀏覽器會在畫面左側開啟。 **[!UICONTROL 瀏覽]** 並上傳標誌影像。 點選 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png). 影像會顯示在頁首上。

   如果您沒有商標，可以點選「取得檔案」下載本文中使用的商標。

[获取文件](assets/logo.png)

1. 拖曳 **[!UICONTROL 頁尾]** 元件來源 ![treeexpandall](assets/treeexpandall.png) 至最適化表單。 在此階段，表單看起來像這樣：

   ![adaptive-form-with-headers-and-footers](assets/adaptive-form-with-headers-and-footers.png)

## 步驟3：新增元件以擷取和顯示資訊 {#step-add-components-to-capture-and-display-information}

元件是適用性表單的建置組塊。 AEM [!DNL Forms] 提供許多元件，可擷取和顯示最適化表單中的資訊。 您可以從下列位置拖曳元件： ![treeexpandall](assets/treeexpandall.png) 至表單。 若要瞭解可用元件和對應功能，請參閱 [製作調適型表單簡介](/help/forms/using/introduction-forms-authoring.md).

1. 拖曳 **[!UICONTROL 數值方塊元件]** 至最適化表單。 放在頁尾元件之前。 開啟元件的屬性，變更 **[!UICONTROL 標題]** 的元件至 **`Customer ID`**，變更 **[!UICONTROL 元素名稱]** 至 **`customer_ID`**，啟用 **[!UICONTROL 必要欄位]** 選項，啟用 **[!UICONTROL 使用HTML5數字輸入型別]** 選項，然後點選 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).
1. 將三個文字方塊元件拖曳至最適化表單。 將這些專案放在頁尾元件之前。 為這些文字方塊設定下列屬性。: 

   <table> 
    <tbody> 
     <tr> 
      <td><b>属性</b></td> 
      <td><b>文字方塊1<br/></b></td> 
      <td><b>文字方塊2<br/></b></td> 
      <td><b>文字方塊3</b></td> 
     </tr> 
     <tr> 
      <td>标题</td> 
      <td>名称<br /> </td> 
      <td>配送地址</td> 
      <td>状态</td> 
     </tr> 
     <tr> 
      <td>元素名称</td> 
      <td>customer_name<br /> </td> 
      <td>customer_Shipping_Address</td> 
      <td>customer_state</td> 
     </tr> 
     <tr> 
      <td>必要欄位</td> 
      <td>启用</td> 
      <td>启用</td> 
      <td>启用</td> 
     </tr> 
     <tr> 
      <td>允許多行<br /> </td> 
      <td>已禁用</td> 
      <td>启用</td> 
      <td>已禁用</td> 
     </tr> 
    </tbody> 
   </table>

1. 拖曳 **[!UICONTROL 數值方塊]** 頁尾元件之前的元件。 開啟元件的屬性，設定下表所列值，點選 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   | 属性 | 价值 |
   |---|---|
   | 标题 | 郵遞區號 |
   | 元素名称 | customer_ZIPCode |
   | 最大数字数量 | 6 |
   | 必要欄位 | 启用 |
   | 顯示圖樣型別 | 無模式 |

1. 拖曳 **[!UICONTROL 電子郵件]** 頁尾元件之前的元件。 開啟元件的屬性、設定下表所列值，然後點選 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   | 属性 | 价值 |
   |---|---|
   | 标题 | 电子邮件 |
   | 元素名称 | customer_Email |
   | 必要欄位 | 启用 |

1. 拖曳 **[!UICONTROL 檔案附件]** 頁尾元件之前的元件。 開啟元件的屬性、設定下表所列值，然後點選 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   <table> 
    <tbody> 
     <tr> 
      <td><b>属性</b></td> 
      <td><b>价值</b></td> 
     </tr> 
     <tr> 
      <td>标题</td> 
      <td>政府核准的地址證明<br /> </td> 
     </tr> 
     <tr> 
      <td>元素名称</td> 
      <td>customer_Address_Proof</td> 
     </tr> 
     <tr> 
      <td>必要欄位</td> 
      <td>启用</td> 
     </tr> 
    </tbody> 
   </table>

1. 拖曳 **[!UICONTROL 提交按鈕]** 最適化表單的元件。 放在頁尾元件之前。 開啟元件的屬性，將元素名稱變更為 `address_addition_update_submit`，點選 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png). 表單版面配置完整，表單如下所示：

   ![adaptive-form-with-all-the-components](assets/adaptive-form-with-all-the-components.png)

## 步驟4：設定最適化表單的提交動作 {#step-configure-submit-action-for-the-adaptive-form}

當使用者點選最適化表單上的提交按鈕時，會觸發提交動作。 您可以使用提交動作將表單資料儲存至本機存放庫、將表單資料傳送至REST端點、以電子郵件傳送表單資料等。 調適型表單提供一些其他立即可用的提交動作。 如需詳細資訊，請參閱 [設定提交動作](/help/forms/using/configuring-submit-actions.md).

使用下列步驟，您可以設定表單的電子郵件提交動作和示範提交動作：

1. 設定電子郵件伺服器。 如需詳細資訊，請參閱 [設定電子郵件通知](/help/sites-administering/notification.md).


1. 點選 **[!UICONTROL 表單容器]** 在內容瀏覽器中點選 ![cmppr](assets/cmppr.png). 屬性瀏覽器會在左側開啟。
1. 前往 **[!UICONTROL 提交]** >  **[!UICONTROL 提交動作]**. 選取 **[!UICONTROL 傳送電子郵件]**. 指定下列值並點選 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   | 属性 | 价值 |
   |--- |--- |
   | 发件人 | `donotreply@weretail.com` |
   | 收件人 | `${customer_Email}` |
   | 主题 | 通知：您已在We.Retail網站上新增運送地址。 |
   | 电子邮件模板 | 嗨 `${customer_Name}`，下列地址會新增為您的帳戶的運送地址： <br>`${customer_Name}`， `${customer_Shipping_Address}`， `${customer_State}`， `${customer_ZIPCode}`<br> 謹祝， We.Retail |
   | 包含附件 | 启用 |

   您的表單已準備就緒。 現在，您可以預覽表單並測試功能。 如果您已使用教學課程中提到的名稱，並在執行AEM的電腦上存取表單 [!DNL Forms] 伺服器，則可在以下位置取得表單： [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html).

## 步驟5：預覽並提交最適化表單 {#step-preview-and-submit-the-adaptive-form}

您可以使用 **[!UICONTROL 預覽選項]** 評估表單的外觀和行為。 您可以在預覽模式中提交表單，也可以檢查表單上套用的驗證。 例如，如果必填欄位留空時顯示錯誤。

調適型表單也提供可模擬各種裝置表單體驗的選項。 例如，iPhone、iPad和案頭。 您可以使用兩者 **[!UICONTROL 預覽]** 和 **[!UICONTROL 模擬器]** ![尺標](assets/ruler.png) 這些選項會相互結合，以預覽不同熒幕大小之裝置的表單。

1. 點選 **[!UICONTROL 預覽]** 選項的位置。 表單會在預覽模式下開啟。 如果您已使用教學課程中提到的名稱，則表單的預覽URL會是 [http://localhost:4502/content/dam/formsanddocuments/shipping-address-add-update-form/jcr:content?wcmmode=disabled](http://localhost:4502/content/dam/formsanddocuments/shipping-address-addition-updation-form/jcr:content?wcmmode=disabled)
1. 使用 ![尺標](assets/ruler.png) 以檢視表單在各種裝置上的外觀。
1. 填寫表單的欄位並點選 **[!UICONTROL 提交]**. 表單已提交，您被重新導向至預設值 **感謝您** 頁面。 您也可以指定自訂感謝頁面。 如需詳細資訊，請參閱 [設定重新導向頁面](/help/forms/using/configuring-redirect-page.md).

新增地址的最適化表單已就緒。 如果您已使用教學課程中提到的名稱，並在執行AEM Forms伺服器的電腦上存取表單，則表單可在 [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html).
