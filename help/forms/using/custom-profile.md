---
title: 建立HTML5表單的自訂設定檔
seo-title: Creating a custom profile for HTML5 forms
description: HTML5表單設定檔是Apache Sling中的資源節點。 它代表HTML5表單轉譯器服務的自訂版本。
seo-description: A HTML5 forms profile is a resource node in Apache Sling. It represents a customized version of HTML5 forms Render service.
uuid: b9938280-a92c-4dde-b465-04372db3ca8d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 9cd22244-9aa6-4b5f-96cf-c9cb3d6f9c8a
feature: Mobile Forms
exl-id: cf86c810-c466-4894-acc2-d4faf49754cc
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '660'
ht-degree: 0%

---

# 建立HTML5表單的自訂設定檔 {#creating-a-custom-profile-for-html-forms}

設定檔是中的資源節點 [Apache Sling](https://sling.apache.org/). 它代表HTML5表單轉譯服務的自訂版本。 您可以使用HTML5表單轉譯服務來自訂HTML5表單的外觀、行為和互動。 設定檔節點存在於中 `/content` JCR存放庫中的資料夾。 您可以將節點直接放在 `/content` 資料夾或任何子資料夾 `/content` 資料夾。

設定檔節點具有 **sling：resourceSuperType** 屬性且預設值為 **xfaforms/profile**. 節點的轉譯器指令碼位於/libs/xfaforms/profile。

Sling指令碼是JSP指令碼。 這些JSP指令碼可當作容器，用來將請求表單的HTML與必要的JS/CSS成品放在一起。 這些Sling指令碼也稱為 **設定檔轉譯器指令碼**. 設定檔轉譯器會呼叫Forms OSGi服務來轉譯請求的表單。

針對GET和POST請求，設定檔指令碼位於html.jsp和html.POST.jsp中。 您可以複製和修改一個或多個檔案，以覆蓋和新增自訂。 不要進行任何就地變更，修補程式更新會覆寫此類變更。

設定檔包含各種模組。 這些模組是formRuntime.jsp、config.jsp、toolbar.jsp、formBody.jsp、nav_footer.jsp和footer.jsp。

## formRuntime.jsp {#formruntime-jsp-br}

formRuntime.jsp模組包含使用者端程式庫的參照。 此外也說明如何從要求擷取地區設定資訊，並在要求中包含當地語系化的訊息。 您可以在formRuntime.jsp中包含自己的customJavaScript程式庫或樣式。

## config.jsp {#config-jsp}

config.jsp模組包含各種設定，例如記錄、Proxy服務和行為版本。 您可以將自己的設定和Widget自訂新增到config.jsp模組中。 您也可以將自訂Widget註冊等設定新增到config.jsp模組。

## toolbar.jsp {#toolbar-jsp}

toolbar.jsp包含建立彩色工具列的程式碼。 若要移除工具列，請從HTML.jsp中移除toolbar.jsp

## formBody.jsp {#formbody-jsp}

formBody.jsp模組用於XFA表單的HTML表示。

## nav_footer.jsp {#nav-footer-jsp}

最初，HTML5表單只會轉譯表單的第一頁。 當使用者捲動表單時，則會載入其餘表單。 這可讓載入體驗更快。 nav_footer.jsp元件包含所有樣式和必要元素，以便在捲動時載入頁面。

## footer.jsp {#footer-jsp}

footer.jsp模組是空的。 它可讓您新增僅用於使用者互動的指令碼。

## 建立自訂設定檔 {#creating-custom-profiles}

若要建立自訂設定檔，請執行下列步驟：

### 建立設定檔節點 {#create-profile-node}

1. 在URL導覽至CRX DE介面： `https://'[server]:[port]'/crx/de` 並使用管理員認證登入介面。

1. 在左窗格中，導覽至該位置 */content/xfaforms/profiles*.

1. 複製節點預設值，並將節點貼到不同的資料夾(*/content/profiles*)，並加上名稱 *hrform*.

1. 選取新節點， *hrform*，並新增字串屬性： *sling：resourceType* 含值： *表單/示範*.

1. 按一下工具列選單中的「儲存全部」以儲存變更。

### 建立設定檔轉譯器指令碼 {#create-the-profile-renderer-script}

建立自訂設定檔後，將轉譯資訊新增至此設定檔。 在收到新設定檔的請求時，CRX會驗證要轉譯的JSP頁面的/apps資料夾是否存在。 在/apps資料夾中建立JSP頁面。

1. 在左窗格中，導覽至 `/apps` 資料夾。
1. 以右鍵按一下 `/apps` 資料夾並選擇以名稱建立資料夾 **hrform**.
1. 內部人員 **hrform** 資料夾建立名為的資料夾 **示範**.
1. 按一下 **全部儲存** 按鈕。
1. 導覽至 `/libs/xfaforms/profile/html.jsp` 並複製節點 **html.jsp**.
1. 貼上 **html.jsp** 節點進入 `/apps/hrform/demo` 以上建立的相同名稱資料夾 **html.jsp** 並按一下 **儲存**.
1. 如果您有設定檔指令碼的任何其他元件，請依照步驟1-6複製/apps/hrform/demo資料夾中的元件。

1. 若要確認設定檔已建立，請開啟URL `https://'[server]:[port]'/content/xfaforms/profiles/hrform.html`

若要驗證您的表單， [匯入您的表單](/help/forms/using/get-xdp-pdf-documents-aem.md) 從您的本機檔案系統移至AEM Forms和 [預覽表單](/help/forms/using/previewing-forms.md) 在AEM伺服器作者執行個體上。
