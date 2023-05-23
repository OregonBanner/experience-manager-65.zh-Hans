---
title: 可持续升级
seo-title: Sustainable Upgrades
description: 瞭解AEM 6.4中的永續升級。
seo-description: Learn about sustainable upgrades in AEM 6.4.
uuid: 80673076-624b-4308-8233-129cb4422bd5
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
discoiquuid: e35c9352-f0d5-4db5-b88f-0720af8f6883
docset: aem65
feature: Upgrading
exl-id: b777fdca-e7a5-427a-9e86-688dd7cac636
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '851'
ht-degree: 0%

---

# 可持续升级{#sustainable-upgrades}

## 自訂架構 {#customization-framework}

### 架構（功能/基礎架構/內容/應用程式）  {#architecture-functional-infrastructure-content-application}

Customization Framework功能的設計目的，是為了協助減少程式碼（如API）或內容（如覆蓋圖）不可延伸區域中無法升級支援的違規。

自訂架構有兩個元件： **API表面** 和 **內容分類**.

#### API表面 {#api-surface}

在舊版AEM中，許多API是透過Uber Jar公開。 其中一些API並非旨在供客戶使用，但會以跨套件提供的方式支援AEM功能。 今後，Java API將標示為「公用」或「私用」，以向客戶指出哪些API在升級環境中可以安全使用。 其他細節包括：

* Java API標示為 `Public` 可供自訂實作套件使用和參考。

* 公用API會回溯相容性套件的安裝。
* 相容性套件將包含相容性Uber JAR，以確保回溯相容性
* Java API標示為 `Private` 僅供AEM內部套件組合使用，不應用於自訂套件。

>[!NOTE]
>
>的概念 `Private` 和 `Public` 在此情況下，不應與公用和私有類別的Java概念混淆。

![image2018-2-12_23-52-48](assets/image2018-2-12_23-52-48.png)

#### 內容分類 {#content-classifications}

AEM一直以來都使用覆蓋和Sling資源合併器的原則，讓客戶可以擴充和自訂AEM功能。 支援AEM主控台和UI的預先定義功能儲存在 **/libs**. 客戶絕不可修改底下的任何專案 **/libs** 但可以在下方新增其他內容 **/apps** 以覆蓋和延伸中定義的功能 **/libs** （如需詳細資訊，請參閱使用覆蓋圖開發）。 當升級AEM作為中的內容時，這仍會導致許多問題 **/libs** 可能會變更，導致覆蓋功能以非預期的方式中斷。 客戶也可以透過繼承來擴充AEM元件 `sling:resourceSuperType`，或只是參照中的元件 **/libs** 直接透過sling：resourceType。 參考和覆寫使用案例可能會發生類似的升級問題。

為了讓客戶更安全、更輕鬆地瞭解 **/libs** 可以安全地使用和覆蓋中的內容 **/libs** 已經過分類，包含下列mixin：

* **公用(granite：PublicArea)**  — 將節點定義為公開，以便覆蓋、繼承( `sling:resourceSuperType`)或直接使用( `sling:resourceType`)。 標示為Public的/libs底下的節點可以安全升級，並額外新增相容性套件。 一般來說，客戶應該只利用標示為「公用」的節點。

* **摘要(granite：AbstractArea)**  — 將節點定義為抽象。 節點可以覆蓋或繼承( `sling:resourceSupertype`)，但不能直接使用( `sling:resourceType`)。

* **最後(granite：FinalArea)**  — 將節點定義為最終節點。 分類為最終理想的節點不應覆蓋或繼承。 可直接透過以下方式使用最終節點： `sling:resourceType`. 依預設，最終節點下的子節點會視為內部。

* ***內部(granite：InternalArea)*** *- *將節點定義為內部節點。 分類為內部理想的節點不應重疊、繼承或直接使用。 這些節點僅適用於AEM的內部功能

* **無註解**  — 節點會根據樹狀結構階層繼承分類。 /根預設為Public。 **父項分類為「內部」或「最終」的節點也將被視為「內部」。**

>[!NOTE]
>
>這些原則僅針對Sling搜尋路徑型機制執行。 其他領域 **/libs** like a client-side library可能會標籤為 `Internal`，但仍可與標準clientlib包含搭配使用。 在這些情況下，客戶必須繼續遵守內部分類。

#### CRXDE Lite內容型別指標 {#crxde-lite-content-type-indicators}

CRXDE Lite中套用的Mixin將顯示標籤為的內容節點和樹狀結構 `INTERNAL` 顯示為灰色。 對象 `FINAL` 只有圖示會呈現灰色。 這些節點的子項也會顯示為灰色。 在這兩種情況下，「覆蓋節點」功能都會停用。

**公共**

![image2018-2-8_23-34-5](assets/image2018-2-8_23-34-5.png)

**最後**

![image2018-2-8_23-34-56](assets/image2018-2-8_23-34-56.png)

**內部**

![image2018-2-8_23-38-23](assets/image2018-2-8_23-38-23.png)

**內容健康情況檢查**

>[!NOTE]
>
>自AEM 6.5起，Adobe建議使用模式偵測器來偵測內容存取違規。 模式偵測器報告更詳細，可偵測更多問題並降低誤報的可能性。
>
>如需詳細資訊，請參閱 [使用模式偵測器評估升級複雜性](/help/sites-deploying/pattern-detector.md).

AEM 6.5將隨附健康情況檢查，以在重疊或參考內容的使用方式與內容分類不一致時提醒客戶。

** Sling/Granite Content Access Check**是新的健康情況檢查，可監視存放庫，以檢視客戶程式碼是否不適當地存取AEM中受保護的節點。

這將會掃描 **/apps** 通常需要幾秒鐘才能完成。

若要存取這項新的健康情況檢查，您需要執行下列動作：

1. 從AEM首頁，瀏覽至 **工具>作業>健康情況報表**
1. 按一下 **Sling/Granite內容存取檢查** 如下所示：

   ![screen_shot_2017-12-14at55648pm](assets/screen_shot_2017-12-14at55648pm.png)

掃描完成後，會出現警告清單，通知終端使用者受保護節點被不當參考：

![熒幕擷圖–2018-2-5健康報告](assets/screenshot-2018-2-5healthreports.png)

修正違規後，它會恢復為綠色狀態：

![熒幕擷圖–2018-2-5healthreports-violations](assets/screenshot-2018-2-5healthreports-violations.png)

健康狀態檢查會顯示背景服務收集的資訊，當覆蓋或資源型別用於所有Sling搜尋路徑時，這些資訊會進行非同步檢查。 如果內容Mixin使用不正確，它會報告違規。
