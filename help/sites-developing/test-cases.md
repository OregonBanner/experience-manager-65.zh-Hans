---
title: 定義測試案例
seo-title: Defining your Test Cases
description: 您的測試案例應以使用案例和詳細需求規格為基礎
seo-description: Your test cases should be based upon the use cases and the detailed requirements specification
uuid: daaa5370-bcd3-45a6-9974-f9b5af6a1529
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: f01eb2aa-6891-4f5d-8a4a-43fc1534c222
docset: aem65
exl-id: c09cde0d-401c-437f-9ec8-a0530c1312d5
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 0%

---

# 定義測試案例{#defining-your-test-cases}

您的測試案例應該以下列專案為基礎：

**使用案例**

* 這些會根據參與者（啟動特定動作的角色）與系統之間的互動來定義所需的功能。
* 使用案例應由客戶定義。

**詳細需求規格**

* 所有功能和效能需求都應進行測試。

測試應清楚定義：

* 先決條件；這些可能涵蓋特定系統、設定或測試者體驗。
* 應遵循的步驟；在適當的詳細資訊層級。
* 預期結果。
* 清除通過或失敗的准則。

自動化測試案例的前景顯然很有吸引力，因為它可以消除重複性的任務。

## 手動與自動化測試 {#manual-versus-automated-tests}

然而，自動化測試案例是一項重大投資，因此應考慮某些方面：

* 需要時間、精力和經驗才能進行設定和設定。
* 如果以瀏覽器為基礎，安裝瀏覽器更新時問題的風險會增加；需要更多時間才能更正。
* 只適用於大型專案。
* 當針對測試或長期發行計畫產生多個發行時良好。

## 測試特定方面 {#testing-specific-aspects}

在測試AEM時，有一些特別令人感興趣的特定細節：

**製作和發佈環境**

不過，涵蓋在 [環境](/help/sites-developing/the-basics.md#environments) 在測試方面，值得強調AEM的決定因素。

您必須將AEM視為兩個應用程式：

* 此 *作者* 環境此例項可讓作者輸入及發佈內容。
這擁有一小部分可預測的使用者，對他們來說，特定的功能和效能至關重要。

* 此 *發佈* 環境此例項會以已發佈的形式顯示網站，以供訪客存取。
這通常會有較多的使用者集，其流量並不總是100%可預測。 效能仍然至關重要 — 在回應請求時。 快取和負載平衡也必須考量。

雖然是相同的軟體，但：

* 用途不同
* 對功能與效能有不同的需求
* 設定方式不同
* 已分別調整
* 各自將擁有自己的驗收測試集

換言之，必須分別使用不同測試案例進行測試。

**个性化**

測試個人化時，每個個別使用案例應使用多個使用者帳戶重複以證明行為。

快取也必須檢查是否有正確行為。

**排程程式**

大部分專案都會安裝Dispatcher以進行快取和負載平衡。

測試很困難（快取會發生在不同的層級和位置），並且必須以黑匣子方式進行。 要測試的主要方面包括：

* **準確度**
確保網站訪客看到內容更新。

* **連續性**
確保關閉一台伺服器時，網站仍然可用。

* **叢集**
叢集用於提供：

   * **容錯移轉**
如果一個伺服器發生故障，則叢集中的其他伺服器將會接管處理作業。

   * **效能**
使用完整容錯移轉的負載平衡可提升叢集的效能。
用於客戶專案時，必須測試叢集以確認設定的正確操作。

## 測試協力廠商軟體 {#testing-third-party-software}

任何連線至AEM的協力廠商軟體，均可在「詳細需求規格」中參照。

必須分析所需的任何測試（取決於定義的範圍），並取得乾淨測試。
