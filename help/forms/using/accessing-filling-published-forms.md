---
title: 存取和填寫已發佈的表單
seo-title: Accessing and filling published forms
description: Forms入口網站為網頁開發人員配備元件，以便在使用Adobe Experience Manager (AEM)編寫的網站上建立和自訂表單入口網站。
seo-description: Forms Portal equips Web Developers with components to create and customize a forms portal on websites authored using Adobe Experience Manager (AEM).
uuid: 44731604-5d97-46fa-baa9-0c020c634fa7
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 88dc8ef2-95ce-4906-ac28-eecc3a32a64e
docset: aem65
exl-id: aedf890c-a2f1-412f-8897-2492ffab335a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '935'
ht-degree: 0%

---

# 存取和填寫已發佈的表單{#accessing-and-filling-published-forms}

在以表單為中心的入口網站部署設定中，表單開發和入口網站開發是兩個不同的活動。 當表單設計人員將表單設計和儲存在存放庫時，網頁開發人員會建立一個Web應用程式到該清單表單並處理提交。 Forms接著會複製到Web層，因為Forms存放庫和Web應用程式之間沒有通訊。

這通常會導致管理設定和生產延遲的問題。 例如，如果儲存庫中有較新版本的表單，則表單設計人員會取代Web層上的表單、修改Web應用程式，以及在公共網站上重新部署表單。 重新部署Web應用程式可能會造成伺服器停機。 由於伺服器停機時間是計畫的活動，因此變更無法立即推送至公用網站。

Forms Portal可減少管理開銷和生產延遲。 它為網頁開發人員配備元件，以便在使用Adobe Experience Manager (AEM)編寫的網站上建立和自訂表單入口網站。

如需有關表單入口網站及其功能的詳細資訊，請參閱 [在入口網站上發佈表單的簡介](/help/forms/using/introduction-publishing-forms.md).

## 表單入口網站快速入門 {#getting-started-with-forms-portal}

導覽至已發佈的表單入口網站頁面。 如需建立表單入口網站頁面的詳細資訊，請參閱 [建立表單入口網站頁面](../../forms/using/creating-form-portal-page.md).

Roms入口網站的搜尋和製表器元件會顯示AEM伺服器Publish執行個體上可用的表單。 此清單包含製作表單入口網站頁面時在篩選器中定義的所有表單或表單。 Forms入口網站頁面看起來類似，如下圖所示：

![範例表單入口網站頁面 ](assets/forms-portal-page.png)

範例表單入口網站頁面

### 搜尋和製表人 {#search-and-lister}

「搜尋並製表器」元件可讓您將下列功能新增至表單入口網站：

* 在面板、卡片或格線檢視中列出現成可用的表單。 它也支援自訂範本列出Forms Manager中特定資料夾的表單。
* 指定表單的呈現方式 — HTML5、PDF或兩者。
* 指定PDF和XFA表單的呈現方式 — HTML5、PDF或兩者。 HTML5的非XFA表單。
* 啟用根據條件搜尋表單，例如表單屬性、中繼資料和標籤。
* 將表單資料提交至servlet。
* 使用自訂樣式表(CSS)來自訂入口網站的外觀。
* 建立表單連結。

您可以使用下列選項，在Forms Portal頁面中搜尋表單：

* 全文檢索搜尋
* 高级搜索

全文檢索搜尋可讓您根據指定的關鍵字尋找及列出表單。

![進階搜尋對話方塊](assets/search-panel.png)

進階搜尋對話方塊

進階搜尋可讓您根據指定的表單屬性來搜尋表單。 這比全文檢索搜尋提供更具體的結果。 進階搜尋包括根據標籤、屬性（例如作者、說明和標題）、修改日期和全文檢索進行的搜尋。

清單產生器會根據搜尋引數顯示表單。 搜尋結果中的每個表單都會顯示一個圖示，該圖示會以超連結方式連結到關聯的表單。 您可以按一下圖示以開啟及使用相關表單。

### 填寫表單 {#filling-a-form}

![最適化表單範例](assets/filling_a_form.png)

最適化表單範例

可從隨頁面的「搜尋和製表器」元件中的表單提供的連結存取表單。

每個表單都包含使用者填寫表單的說明資訊。

#### 草稿與提交 {#drafts-and-submission}

使用者可以選擇按一下儲存按鈕來儲存表單草稿。 這可讓使用者在提交表單前的一段時間內處理表單。

填入表單（包括附件）的資料會儲存為伺服器上的草稿。 表單的草稿可以儲存任意次數。 已儲存的表單會顯示在頁面的「草稿和提交」元件的「草稿」標籤中。

填寫完表單後，使用者按一下表單上的提交按鈕即可提交表單。 提交的表單會顯示在該頁面「草稿和提交」元件的「提交」標籤中。

>[!NOTE]
>
>只有當最適化表單的提交動作設定為Forms Portal提交動作時，提交的表單才會顯示在已提交的Forms標籤中。 如需提交動作的詳細資訊，請參閱 [設定提交動作](../../forms/using/configuring-submit-actions.md).

![草稿和提交元件](assets/draft-submission.png)

草稿和提交元件

## 使用提交的表單資料開始新表單 {#start-a-new-form-using-submitted-form-data}

有些表格您經常需要填寫和提交。 例如，每年都會提交個人報稅表。 在這種情況下，雖然有些資訊會在您每次填寫表單時有所變更，但大部分如個人和家庭詳細資料一樣不會變更。 不過，您仍須從頭開始再次填寫整個表單。

AEM Forms可協助最佳化表單填寫體驗，並大幅縮短再次填寫和提交表單的時間。 一般使用者可使用提交的表單中的資料來開始新表單。 此功能內建於 [草稿和提交元件](../../forms/using/draft-submission-component.md). 當您新增草稿和提交元件至表單入口網站頁面並發佈時，終端使用者可在已提交的Forms和草稿Forms標籤中尋找選項，使用已提交表單中的資料建立新表單。 下圖會反白顯示該選項。

![開始新表單](assets/start-a-new-form.png)

當您按一下按鈕以啟動新表單時，它會開啟一個新表單，其中包含來自對應提交表單的資料。 您現在可以視需要檢閱和更新資訊，並提交表單。
