---
title: 資料模型 — David Nuescheler模型
seo-title: Data Modeling - David Nuescheler's Model
description: David Nuescheler的內容模型建議
seo-description: David Nuescheler's content modelling recommendations
uuid: acb27e81-9143-4e0d-a37a-ba26491a841f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 39546c0a-b72f-42df-859b-98428ee0d5fb
exl-id: 6ce6a204-db59-4ed2-8383-00c6afba82b4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1818'
ht-degree: 0%

---

# 資料模型 — David Nuescheler模型{#data-modeling-david-nuescheler-s-model}

## 源 {#source}

以下是David Nuescheler所表達的構想和意見。

David是Day Software AG的聯合創始人兼技術長，該公司是全球內容管理和內容基礎架構軟體的領先供應商，於2010年由Adobe收購。 他現在是Adobe的企業技術副總裁，並領導開發JSR-170，Java Content Repository (JCR)應用程式設計介面(API)，這是內容管理的技術標準。

進一步更新可見於 [https://wiki.apache.org/jackrabbit/DavidsModel](https://wiki.apache.org/jackrabbit/DavidsModel).

## 來自David的簡介 {#introduction-from-david}

在各種討論中，我發現開發人員對JCR在內容模型方面呈現的特性和功能有點不安。 關於如何為存放庫中的內容建立模型，以及為什麼一種內容模型優於另一種內容模型，目前尚無指南，也鮮有經驗。

雖然在關聯式世界中，軟體產業在如何建立資料模型方面有很多經驗，但我們仍然處於內容存放庫空間的早期階段。

我想透過表達我個人對如何設定內容模型的意見，來開始填補這個空白，希望這有一天能發展成為對開發人員社群更有意義的東西，不僅是「我的意見」，而是更普遍適用的東西。 因此，請將此視為我快速進化的第一招。

>[!NOTE]
>
>免責宣告：這些准則表達了我個人有時有爭議的觀點。 我期待就這些准則進行辯論並加以完善。

## 七個簡單規則 {#seven-simple-rules}

### 規則#1：資料優先，結構稍後。 可能會。 {#rule-data-first-structure-later-maybe}

#### 解释 {#explanation-1}

我建議不要擔心ERD意義上的宣告資料結構。 最初。

瞭解如何在開發中喜歡nt：unstructured (&amp; friends)。

我覺得Stefano差不多是這個的概括。

我的基本原則：結構昂貴，而且在許多情況下，完全不需要明確宣告結構給基礎儲存體。

您的應用程式本身使用的結構有隱含合約。 假設我把部落格的修改日期儲存在lastModified屬性中。 我的應用程式會自動知道要再次從相同屬性讀取修改日期，實際上不需要明確宣告。

其他資料限制（如強制或型別和值限制）只應在資料完整性原因需要時套用。

#### 示例 {#example-1}

上述使用 `lastModified` 上的日期屬性（例如「部落格」節點），並不表示需要特殊的節點型別。 我一定會使用 `nt:unstructured` 至少是在最初，針對我的部落格節點。 由於在我的部落格應用程式中，我所要做的就是顯示lastModified日期（可能為「order by」），因此我一點也不在乎它是否為Date。 由於我含蓄地信任我的部落格撰寫應用程式會將「日期」放在那裡，因此確實不需要宣告存在 `lastModified` 日期，格式為a節點型別。

### 規則#2：驅動內容階層，不要讓它發生。 {#rule-drive-the-content-hierarchy-don-t-let-it-happen}

#### 解释 {#explanation-2}

內容階層是非常有價值的資產。 因此，不要任其發生，請加以設計。 如果您沒有節點的「良好」、人類看得懂的名稱，您可能需要重新考慮。 任意數字幾乎算不上是「好名稱」。

雖然快速將現有的關聯式模型放入階層式模型可能非常容易，但在此過程中應該多加思考。

根據我的經驗，如果考慮存取控制和內含機制，通常對內容階層來說是很好的驅動因素。 將其視為您的檔案系統。 甚至可能使用檔案和資料夾在您的本機磁碟上進行模型化。

就我個人而言，起初在許多情況下，我偏好使用階層慣例，而非節點輸入系統，之後會介紹輸入法。

>[!CAUTION]
>
>內容存放庫的結構方式也會影響效能。 為獲得最佳效能，附加至內容存放庫中個別節點的子節點數量通常不應超過1,000。
>
>另請參閱 [CRX可以處理多少資料？](https://helpx.adobe.com/experience-manager/kb/CrxLimitation.html) 以取得詳細資訊。

#### 示例 {#example-2}

我會建立一個簡單的部落格系統模型，如下所示。 請注意，一開始我甚至不在乎目前使用的個別節點型別。

```xml
/content/myblog
/content/myblog/posts
/content/myblog/posts/what_i_learned_today
/content/myblog/posts/iphone_shipping

/content/myblog/comments/iphone_shipping/i_like_it_too
/content/myblog/comments/iphone_shipping/i_like_it_too/i_hate_it
```

我認為其中一個顯而易見的事實是，我們都根據範例理解了內容的結構，沒有任何進一步的解釋。

最初可能會出乎意料的是，為什麼我不用「貼文」儲存「註解」，這是由於存取控制，我希望以合理的分層方式套用存取控制。

使用上述內容模型，我可以輕鬆地允許「匿名」使用者「建立」評論，但讓匿名使用者在工作區的其餘部分以唯讀方式進行。

### 規則#3：工作區適用於clone()、merge()和update()。 {#rule-workspaces-are-for-clone-merge-and-update}

#### 解释 {#explanation-3}

如果您不使用 `clone()`， `merge()` 或 `update()` 應用程式中的方法單一工作區可能是可行的方式。

「對應節點」是JCR規格中定義的概念。 基本上，這會歸結為代表相同內容的節點，位於不同的所謂工作區中。

JCR引進了工作區非常抽象的概念，讓許多開發人員不清楚如何處理它們。 我建議您將工作區的使用提交到以下專案進行測試。

如果您在多個工作區中的「對應」節點（本質上是具有相同UUID的節點）有大量重疊，您可能會善用工作區。

如果具有相同UUID的節點沒有重疊，則表示您可能正在濫用工作區。

工作區不應用於存取控制。 特定使用者群組的內容可見度並非將專案分隔至不同工作區的好引數。 JCR在內容存放庫中提供「存取控制」功能，可提供該功能。

工作區是參照和查詢的邊界。

#### 示例 {#example-3}

將工作區用於下列事項：

* 專案的v1.2與專案的v1.3
* 「開發」、「QA」和內容的「已發佈」狀態

請勿將工作區用於下列事項：

* 使用者首頁目錄
* 不同目標對象的不同內容，例如公開、私人、本機……
* 不同使用者的郵件收件匣

### 規則#4：注意同名的同層級。 {#rule-beware-of-same-name-siblings}

#### 解释 {#explanation-4}

雖然規格中引入了相同名稱同層級(SNS)，以允許與專為XML設計並透過XML表達的資料結構相容，因此對JCR非常有價值，但SNS對存放庫而言具有相當大的開銷和複雜性。

如果內容存放庫的任何路徑在其其中一個路徑區段中包含SNS，則其穩定性會大幅降低，如果SNS被移除或重新排序，則會影響所有其他的SNS及其子項的路徑。

為了匯入XML或與現有XML SNS互動，可能是必要且有用的，但我從未使用SNS，也永遠不會在我的「綠色欄位」資料模型中使用。

#### 示例 {#example-4}

使用

```xml
/content/myblog/posts/what_i_learned_today
/content/myblog/posts/iphone_shipping
```

而非

```xml
/content/blog[1]/post[1]
/content/blog[1]/post[2]
```

### 規則#5：被視為有害的參考。 {#rule-references-considered-harmful}

#### 解释 {#explanation-5}

參照表示參照完整性。 我認為重要的是要瞭解，參考不僅會為存放庫管理參考完整性增加額外成本，而且從內容彈性的角度來看，成本也很高昂。

我個人會確保只有在我真的無法處理懸置參照且使用路徑、名稱或字串UUID參照其他節點時，才會使用參照。

#### 示例 {#example-5}

假設我允許從檔案(a)到另一個檔案(b)的「參考」。 如果我使用參照屬性來模型化此關係，這表示這兩個檔案是在存放庫層級上連結的。 我無法個別匯出/匯入檔案(a)，因為參考屬性的目標可能不存在。 合併、更新、還原或複製等其他操作也會受到影響。

因此，我會將這些參考建模為「weak-references」（在JCR v1.0中，這基本上歸結為包含目標節點uuid的字串屬性），或只是使用路徑。 有時候，路徑開始時會更有意義。

我認為有些使用案例中，如果參考是懸掛的，系統就真的無法運作，但我無法從我的直接體驗中得出一個好的「真實」但簡單的範例。

### 規則#6：檔案是檔案。 {#rule-files-are-files}

#### 解释 {#explanation-6}

如果內容模型公開某些內容，即使是在遠端 *氣味* 如我嘗試使用（或延伸）的檔案或資料夾 `nt:file`， `nt:folder` 和 `nt:resource`.

根據我的經驗，許多通用應用程式允許與nt：folder和nt：files進行隱含的互動，並且知道如果事件富含其他中繼資訊，該如何處理和顯示。 例如，與CIFS或WebDAV等檔案伺服器實作（位於JCR上方）的直接互動會變成隱含。

我認為根據經驗法則，您可以使用以下內容：如果您需要儲存檔案名稱和mime型別，則 `nt:file`/ `nt:resource` 非常符合。 如果您可以有多個「檔案」，則nt：folder是儲存這些檔案的好地方。

如果您需要為資源新增中繼資訊，假設「author」或「description」屬性，請擴展 `nt:resource` 不是 `nt:file`. 我很少擴充nt：file，而且經常擴充 `nt:resource`.

#### 示例 {#example-6}

假設有人想要上傳影像至部落格專案：

```xml
/content/myblog/posts/iphone_shipping
```

而最初的gut反應可能是新增包含圖片的二進位屬性。

雖然在此情況下，確實有良好使用案例可以只使用二進位屬性（假設名稱不相關且mime型別為隱含），但我會為我的部落格範例建議下列結構。

```xml
/content/myblog/posts/iphone_shipping/attachments [nt:folder]
/content/myblog/posts/iphone_shipping/attachments/front.jpg [nt:file]
/content/myblog/posts/iphone_shipping/attachments/front.jpg/jcr:content [nt:resource]
```

### 規則#7：ID是邪惡的。 {#rule-ids-are-evil}

#### 解释 {#explanation-7}

在關聯式資料庫中，ID是表達關係的必要方式，因此人們也傾向於在內容模型中使用它們。 大部分是出於錯誤的原因。

如果您的內容模型包含許多以「Id」結尾的屬性，表示您可能未正確運用階層。

誠然，某些節點在其整個即時週期中都需要穩定的身分識別。 但比您想像的要少得多。 mix：referenceable提供了這樣的內建於存放庫中的機制，因此確實不需要提出以穩定方式識別節點的額外方法。

同時請記住，專案可透過路徑識別，對於大多數使用者而言，雖然「符號連結」比unix檔案系統中的硬式連結更有意義，但路徑對於大多數應用程式而言，都是指目標節點。

更重要的是，它可以 **mix**：referenceable，這表示它可以在您實際需要參考節點的時間點套用至節點。

假設您想要可能參照「檔案」型別的節點，並不表示您的「檔案」節點型別必須以靜態方式從mix：referenceable延伸，因為它可以動態新增到「檔案」的任何執行個體。

#### 示例 {#example-7}

使用:

```xml
/content/myblog/posts/iphone_shipping/attachments/front.jpg
```

而非：

```xml
[Blog]
-- blogId
-- author
[Post]
-- postId
-- blogId
-- title
-- text
-- date
[Attachment]
-- attachmentId
-- postId
-- filename
+ resource (nt:resource)
```
