---
title: 測試和追蹤工具
seo-title: Testing and Tracking Tools
description: AEM提供測試元件UI的架構，以及測試和偵錯元件的機制
seo-description: AEM provides a framework for testing component UI and a mechanism for testing and debugging components
uuid: 12abedb5-4ee7-4389-9340-e628adbbc053
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: 3cf0fd8d-7fc8-468a-bb1e-1debb68a82a5
docset: aem65
exl-id: bb5d1c7c-56ce-4d1e-a3cb-4e74d6922137
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 1%

---

# 測試和追蹤工具{#testing-and-tracking-tools}

## 测试 {#testing}

AEM 提供：

* [測試元件UI的架構](/help/sites-developing/hobbes.md).
* [用於測試和偵錯元件的機制](/help/sites-developing/developer-mode.md).

以下是兩種開放原始碼測試工具：

**Selenium**

Selenium可用於瀏覽器中的功能測試，每個活動有一個使用者。 測試步驟（點按）會記錄為HTML表格或Java類別。

如需詳細資訊，請參閱 [https://www.seleniumhq.org/](https://www.seleniumhq.org/).

**Jmeter**

JMeter可用來追蹤要求，也可用於功能、效能和壓力測試。

如需詳細資訊，請參閱 [https://jakarta.apache.org/jmeter/](https://jakarta.apache.org/jmeter).

還有許多自動化測試和管理測試計畫的專有工具。

### 追蹤 {#tracking}

您可輕鬆使用下列工具。 不過，所有案例中的關鍵問題是專案團隊的所有成員（合作夥伴和客戶）都能取得資料。

**Bugzilla**

可依您自己的需求設定的錯誤追蹤系統。

**电子表格**

雖然不是專門用於追蹤錯誤的工具，但試算表通常 *mis*&#x200B;用於此目的，因為它們容易理解，且大多數使用者對其功能有體驗。

如果這些是用於追蹤，則：

* 應該儘量保持簡單。
* 個別試算表的數量應維持在最低限度。
* 必須定期更新。
* 只應維護一個主版副本，而且每個人都應知道主版副本的位置。
* 所有專案成員都應該可存取這些檔案。
* 如果安全性是個問題（通常發生在大公司）且無法共同存取，只要每個人都知道這些是復本且無法更新，就可以發佈復本。

同樣地，也有許多追蹤錯誤和功能要求的專有工具。
