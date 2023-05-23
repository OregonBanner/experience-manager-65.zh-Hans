---
title: 編碼提示
seo-title: Coding Tips
description: AEM的編碼秘訣
seo-description: Tips for coding for AEM
uuid: 1bb1cc6a-3606-4ef4-a8dd-7c08a7cf5189
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 4adce3b4-f209-4a01-b116-a5e01c4cc123
exl-id: 85ca35e5-6e2b-447a-9711-b12601beacdd
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '867'
ht-degree: 0%

---

# 編碼提示{#coding-tips}

## 儘可能使用taglibs或HTL {#use-taglibs-or-htl-as-much-as-possible}

在JSP中加入Scriptlet會使得在程式碼中偵錯問題變得困難。 此外，若在JSP中加入指令碼，就很難將商業邏輯與檢視層分離，這違反了單一職責原則和MVC設計模式。

### 寫入可讀取的程式碼 {#write-readable-code}

程式碼只會寫入一次，但會讀取許多次。 花點時間提前清理我們撰寫的程式碼，日後將可獲得回報，因為我們和其他開發人員日後需要閱讀此程式碼。

### 選擇意向顯露的名稱 {#choose-intention-revealing-names}

理想情況下，另一位程式設計師不必開啟模組來瞭解其功能。 同樣地，他們應該能夠在不閱讀方法的情況下判斷方法的作用。 我們訂閱這些創意的效果越好，閱讀程式碼就會越容易，就能越快撰寫和變更程式碼。

在AEM程式碼基底中，會使用下列慣例：


* 介面的單一實作已命名 `<Interface>Impl`，即 `ReaderImpl`.
* 已命名介面的多個實作 `<Variant><Interface>`，即 `JcrReader` 和 `FileSystemReader`.
* 抽象基底類別已命名 `Abstract<Interface>` 或 `Abstract<Variant><Interface>`.
* 封裝已命名 `com.adobe.product.module`.  每個Maven成品或OSGi套件組合都必須有自己的套件。
* Java實作會放置在其API下方的實作套件中。


請注意，這些慣例不一定需要套用至客戶實作，但請務必定義並遵守慣例，這樣程式碼才能持續可供維護。

理想情況下，名稱應會顯示其意圖。 當名稱不如應有的清楚時，的常見程式碼測試是存在解釋變數或方法的用途的註釋：

<table>
 <tbody>
  <tr>
   <td><p><strong>不清楚</strong></p> </td>
   <td><p><strong>清除</strong></p> </td>
  </tr>
  <tr>
   <td><p>int d； //經過的時間（以天為單位）</p> </td>
   <td><p>int elapsedTimeInDays；</p> </td>
  </tr>
  <tr>
   <td><p>//取得標籤影像<br /> 公用清單getItems() {}</p> </td>
   <td><p>公用清單getTaggedImages() {}</p> </td>
  </tr>
 </tbody>
</table>

### 不要重複您自己  {#don-t-repeat-yourself}

DRY指出同一組程式碼絕不應重複。 這也適用於字串常值等。 程式碼複製會在任何必須變更的內容時開啟瑕疵之門，並應加以尋找和消除。

### 避免使用裸露的CSS規則 {#avoid-naked-css-rules}

CSS規則應該專屬於應用程式內容中的目標元素。 例如，套用至以下專案的CSS規則： *.content .center* 過於廣泛，可能會影響您系統中的許多內容，未來需要其他人覆寫此風格。 *.myapp-centertext* 將會是更具體的規則，因為它會指定「置中」 *文字* 在應用程式內容中。

### 避免使用過時的API {#eliminate-usage-of-deprecated-apis}

棄用API時，最好尋找新的建議方法，而不是依賴已棄用的API。 這將確保未來升級更順暢。

### 撰寫可本地化的程式碼 {#write-localizable-code}

任何不是由作者提供的字串，都應包裝在AEM i18n字典的呼叫中，透過 *I18n.get()* 在JSP/Java和 *CQ.I18n.get()* 在JavaScript中。 如果找不到實作，此實作會傳回傳遞至它的字串，因此這樣就能靈活地在主要語言中實作功能後實作本地化。

### 為安全起見逸出資源路徑 {#escape-resource-paths-for-safety}

雖然JCR中的路徑不應包含空格，但它們的存在不應導致程式碼中斷。 Jackrabbit提供文字公用程式類別，包含 *escape()* 和 *escapePath()* 方法。 若為JSP，Granite UI會公開 *granite：encodeURIPath() EL* 函式。

### 使用XSS API和/或HTL來抵禦跨網站指令碼攻擊 {#use-the-xss-api-and-or-htl-to-protect-against-cross-site-scripting-attacks}

AEM提供XSS API來輕鬆清除引數，並確保安全性不受跨網站指令碼攻擊。 此外，HTL也直接在範本語言中內建這些保護。 API速查表可在以下網址下載： [開發 — 指引和最佳作法](/help/sites-developing/dev-guidelines-bestpractices.md).

### 實作適當的記錄 {#implement-appropriate-logging}

對於Java程式碼，AEM支援slf4j作為記錄訊息的標準API，並且應該與透過OSGi控制檯提供的設定結合使用，以確保管理的一致性。 Slf4j會公開五個不同的記錄層級。 選擇要在哪個層級記錄訊息時，我們建議使用下列准則：

* 錯誤：當程式碼中的某些專案損毀，且處理無法繼續時。 這通常會發生於非預期的例外狀況。 在這些情況下包含棧疊追蹤通常會有幫助。
* 警告：當某些專案未正確運作時，可以繼續處理。 這通常是因為我們預期的例外狀況，例如 *PathNotFoundException*.
* INFO：監視系統時有用的資訊。 請記住，這是預設值，並且大多數客戶會在他們的環境中保留此設定。 因此，請勿過度使用。
* DEBUG：有關處理的較低層級資訊。 對支援問題進行偵錯時很有用。
* TRACE：最低層級的資訊，例如輸入/結束方法。 這通常僅供開發人員使用。

若是JavaScript， *console.log* 應僅在開發期間使用，且應在發行之前移除所有log陳述式。

### 避免貨運崇拜程式設計 {#avoid-cargo-cult-programming}

避免復製程式碼而不瞭解其用途。 如有疑問，最好總是詢問對模組或API有較多經驗，但您未明確說明的人。
