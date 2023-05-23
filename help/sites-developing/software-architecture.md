---
title: 軟體架構
seo-title: Software Architecture
description: 設計軟體架構的最佳作法
seo-description: Best practices for architecting your software
uuid: a557f6ca-c3f1-486e-a45e-6e1f986fab41
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 92971747-1c74-4917-b5a0-7b79b3ae1e68
exl-id: cd4f3b4c-5488-4ca7-9c1e-b4c819fda8e8
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 0%

---

# 軟體架構{#software-architecture}

## 針對升級而設計 {#design-for-upgrades}

延伸OOTB行為時，請務必牢記升級事項。 請一律在/apps目錄中套用自訂，並覆蓋在/libs目錄中對應節點的頂端，或使用sling：resourceSuperType來擴充現成行為。 雖然支援新AEM版本可能需要一些修改，但若遵循此作法，新版本不應覆寫您的自訂。

### 儘可能重複使用範本和元件 {#reuse-template-and-components-when-possible}

這可讓網站維持一致的外觀和風格，並簡化程式碼維護。 當需要新範本時，請務必從共用基本範本擴充，以便可以在一個位置對clientlib包含等全域需求進行編碼。 需要新元件時，請尋找從現有元件擴充的機會。

### 設計範本設計 {#design-template-designs}

透過定義頁面上每個parsys可包含哪些元件，可以控制網站外觀/感覺的一致性。 透過限制對頁面上設計的存取，可允許「超級作者」修改每頁允許的元件，而不需要開發人員干預，同時確保其他作者遵循企業標準。

### 開發堅固的架構 {#develop-a-solid-architecture}

SOLID是描述應遵守的五個架構原則的縮寫：

* **S**&#x200B;單一職責原則 — 每個模組、類別、方法等應只有一個職責。
* **O**&#x200B;筆型/封閉式原則 — 模組應開啟以供擴充，並關閉以供修改。
* **L** iskov替代原則 — 型別應該由其子型別取代。
* **I**&#x200B;介面分隔原則 — 不應強制任何使用者端依賴其未使用的方法。
* **D**&#x200B;相依性反轉原則 — 高階模組不應依賴低階模組。 兩者都應該依賴抽象。 抽象不應該取決於細節。 詳細資訊應取決於抽象概念。

努力遵守這五項原則應該會導致系統對關注點有嚴格的分離。

>[!TIP]
>
>SOLID是物件導向程式設計中常用的概念，在產業文獻中廣泛討論每個元素。
>
>此為簡短摘要，旨在提升您的認識，建議您更深入地熟悉這些概念。

### 遵循健全性原則 {#follow-the-robustness-principle}

穩健性原則指出我們對於傳送的內容應保持保守，但在接受的內容上應保持開明。 換言之，當傳送訊息給第三方時，我們應完全符合規格，但是當從第三方接收訊息時，只要訊息的含義明確，我們就應接受不符合的訊息。

### 在自己的模組中實作尖峰 {#implement-spikes-in-their-own-modules}

尖峰和測試程式碼是任何Agile軟體實作不可或缺的一部分，但我們想要確保這些程式碼在沒有適當監督的情況下，不會進入我們的生產程式碼庫。 因此，建議在其本身的模組中建立尖峰。

### 在其本身的模組中實作資料移轉指令碼 {#implement-data-migration-scripts-in-their-own-module}

資料移轉指令碼雖然是生產程式碼，但通常只在網站的初始啟動時執行一次。 因此，一旦網站上線，這就會變成廢棄的程式碼。 為了確保我們不建置相依於移轉指令碼的實作程式碼，這些程式碼應在各自的模組中實作。 這也允許我們在啟動後立即移除並淘汰此程式碼，從系統中消除廢棄的程式碼。

### 遵循POM檔案中發佈的Maven慣例 {#follow-published-maven-conventions-in-pom-files}

Apache已發佈樣式慣例 [https://maven.apache.org/developers/conventions/code.html](https://maven.apache.org/developers/conventions/code.html). 最好遵循這些慣例，因為這會使新資源更易於快速上線。
