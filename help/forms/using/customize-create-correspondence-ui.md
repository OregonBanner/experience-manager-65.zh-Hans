---
title: 自訂建立通訊UI
seo-title: Customize create correspondence UI
description: 瞭解如何自訂建立通訊UI。
seo-description: Learn how to customize create correspondence UI.
uuid: 9dee9b6f-4129-4560-9bf8-db48110b76f7
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 13a93111-c08c-4457-b69a-a6f6eb6da330
docset: aem65
feature: Correspondence Management
exl-id: 9593ca2a-7f9e-4487-a1a5-ca44114bff17
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1088'
ht-degree: 0%

---

# 自訂建立通訊UI{#customize-create-correspondence-ui}

## 概述 {#overview}

通訊管理可讓您重新品牌化其解決方案範本，以獲得更好的品牌價值，並遵守您組織的品牌標準。 將使用者介面品牌化包括變更組織標誌，其顯示在「建立通訊UI」的左上角。

您可以在建立通訊UI中使用您組織的徽標來變更徽標。

![建立通訊UI中的自訂圖示](assets/0_1_introscreenshot.png)

建立通訊UI中的自訂圖示

### 變更建立通訊UI中的標誌 {#changing-the-logo-in-the-create-correspondence-ui}

若要設定您所選擇的標誌影像，請執行下列步驟：

1. 建立適當的 [CRX中的資料夾結構](#creatingfolderstructure).
1. [上傳新的標誌檔案](#uploadlogo) 位於您已在CRX中建立的資料夾中。

1. [設定CSS](#createcss) 在CRX上，以參照新標誌。
1. 清除瀏覽器歷程記錄並 [重新整理建立通訊UI](#refreshccrui).

## 建立所需的資料夾結構 {#creatingfolderstructure}

建立檔案夾結構（如下所述），以託管自訂標誌影像和樣式表。 具有根資料夾/apps的新資料夾結構類似於/libs資料夾的結構。

如有任何自訂內容，請在/apps分支中建立平行資料夾結構，如下所述。

/apps分支（資料夾結構）：

* 在系統更新時，確保檔案的安全。 若是升級、Feature Pack或Hot Fix、/libs分支會更新，而若您在/libs分支中託管變更，則會覆寫這些變更。
* 協助您避免干擾現有的系統/分支，如果您使用預設位置來儲存自訂檔案，可能會錯誤地解除干擾。
* 協助您的資源在AEM搜尋資源時獲得更高的優先順序。 AEM設定為先搜尋/apps分支，然後搜尋/libs分支以尋找資源。 此機制表示系統使用您的覆蓋（以及其中定義的自訂）。

使用以下步驟，在/apps分支中建立所需的資料夾結構：

1. 前往 `https://'[server]:[port]'/[ContextPath]/crx/de` 並以管理員身分登入。
1. 在apps資料夾中，建立名為的資料夾 `css` 路徑/結構類似於css資料夾（位於ccrui資料夾）。

   建立css資料夾的步驟：

   1. 以滑鼠右鍵按一下 **css** 資料夾並選取 **覆蓋節點**： `/libs/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/css`

      ![覆蓋節點](assets/1_overlaynode_css.png)

   1. 確定「覆蓋節點」對話方塊具有下列值：

      **路徑：** /libs/fd/cm/ccr/gui/components/admin/clientlibs/crui/css

      **覆蓋位置：** /apps/

      **符合節點型別：** 已核取

      ![覆蓋節點路徑](assets/0_1_5ioverlaynodedialog.png)

      >[!NOTE]
      >
      >請勿在/libs分支中進行變更。 您所做的任何變更都可能遺失，因為每當您：
      >
      >    
      >    
      >    * 在您的執行個體上升級
      >    * 套用Hot Fix
      >    * 安裝功能套件


   1. 单击&#x200B;**确定**。CSS資料夾是在指定的路徑中建立。

1. 在apps資料夾中，建立名為的資料夾 `imgs` 路徑/結構類似於imgs資料夾（位於ccrui資料夾）。

   1. 以滑鼠右鍵按一下 **影像** 資料夾並選取 **覆蓋節點**： `/libs/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/imgs`
   1. 確定「覆蓋節點」對話方塊具有下列值：

      **路徑：** /libs/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/imgs

      **覆蓋位置：** /apps/

      **符合節點型別：** 已核取

   1. 单击&#x200B;**确定**。

      >[!NOTE]
      >
      >您也可以手動在/apps資料夾中建立資料夾結構。

1. 按一下 **全部儲存** 以將變更儲存在伺服器上。

## 將新標誌上傳至CRX {#uploadlogo}

將自訂標誌檔案上傳至CRX。 標準HTML規則控管標誌的呈現。 支援的影像檔案格式取決於您用來存取AEM Forms的瀏覽器。 所有瀏覽器都支援JPEG、GIF和PNG。 如需詳細資訊，請參閱支援影像格式的瀏覽器專屬檔案。

* 標誌影像的預設尺寸為48畫素 &#42; 48畫素 確保影像與此大小相似或大於48畫素 &#42; 48畫素
* 如果您的標誌影像高度超過50 px，建立通訊使用者介面會將影像縮放到最大50 px高度，因為這是標頭的高度。 縮小影像時，「建立對應」使用者介面會維持影像的外觀比例。
* 建立通訊使用者介面不會將影像放大（如果影像較小），因此請確定您使用至少48畫素的高度和足夠寬度的標誌影像，以清楚明瞭。

使用下列步驟將自訂標誌檔案上傳至CRX：

1. 转到 `https://'[server]:[port]'/[contextpath]/crx/de`. 如有必要，請以管理員身分登入。
1. 在CRXDE中，以滑鼠右鍵按一下 **影像** 資料夾並選取 **「建立」>「建立檔案」**：

   `/apps/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/imgs/`

   ![在imgs資料夾中建立新節點](assets/2_contentexplorernewnode.png)

1. 在「建立檔案」對話方塊中，以CustomLogo.png格式輸入檔案名稱（或您的標誌檔案名稱）。

   ![CustomLogo.png作為新節點](assets/3_contentexplorernewnode_customlogo.png)

1. 按一下 **全部儲存**.

   在您建立的新檔案（此處CustomLogo.png）下，會出現jcr：content屬性。

1. 按一下資料夾結構中的jcr：content。

   jcr：content的屬性會出現。

   ![jcrcontentproperties](assets/jcrcontentproperties.png)

1. 連按兩下 **jcr：data** 屬性。

   「編輯jcr：data」對話方塊隨即顯示。

   現在按一下newlogo.png資料夾，連按兩下jcr：content （dim選項）並設定型別nt：resource。 如果不存在，請建立名為jcr：content的屬性。

1. 在「編輯jcr：data」對話方塊中，按一下 **瀏覽** 並選取您要當作標誌使用的影像檔案（此處CustomLogo.png）。

   支援的影像檔案格式取決於您用來存取AEM Forms的瀏覽器。 所有瀏覽器都支援JPEG、GIF和PNG。 如需詳細資訊，請參閱支援影像格式的瀏覽器專屬檔案。

   ![自訂標誌檔案範例](assets/geometrixx-outdoors.png)

   範例：CustomLogo.png做為自訂標誌

1. 按一下 **全部儲存**.

## 建立CSS以將標誌與UI整合 {#createcss}

自訂標誌影像需要在內容內容內容中載入額外的樣式表。

使用下列步驟來設定呈現標誌的樣式表：

1. 转到 `https://'[server]:[port]'/[contextpath]/crx/de`. 如有必要，請以管理員身分登入。
1. 在下列位置建立名為customcss.css的檔案（不能使用其他檔案名稱）：

   `/apps/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/css/`

   建立customcss.css檔案的步驟：

   1. 以滑鼠右鍵按一下 **css** 資料夾並選取 **「建立」>「建立檔案」**.
   1. 在「新增檔案」對話方塊中，將CSS的名稱指定為 `customcss.css`（不能使用其他檔案名稱），然後按一下 **確定**.
   1. 將下列程式碼新增至新建立的css檔案。 在程式碼的content：url中，指定您已上傳至CRXDE中imgs資料夾的影像名稱。

      ```css
      .logo, .logo:after {
      content:url("../imgs/CustomLogo.png");
      }
      ```

   1. 按一下 **全部儲存**.

## 重新整理建立通訊UI以檢視自訂標誌 {#refreshccrui}

清除瀏覽器快取，然後在瀏覽器中開啟「建立通訊UI」例項。 您應該會看到自訂標誌。

![使用自訂標誌建立通訊使用者介面](assets/0_1_introscreenshot-1.png)

建立通訊UI中的自訂圖示
