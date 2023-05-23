---
title: 將資料庫成長減至最低的秘訣
seo-title: Tips for minimizing database growth
description: 長期處理程式會將處理程式資料儲存在AEM表單資料庫中。 使用一些簡單的程式設計和產品設定策略，可以將AEM表單資料庫的成長減到最少。
seo-description: Long-lived processes store process data in the AEM forms database. The growth of the AEM forms database can be minimized using a few easy process design and product configuration strategies.
uuid: 13f99d4f-848e-451e-90d9-55e202dc0bdb
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 89441336-babc-4d1f-9053-d1566cd42d22
exl-id: f64efb06-815a-4608-ba1c-39e22f344ebb
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 0%

---

# 將資料庫成長減至最低的秘訣 {#tips-for-minimizing-database-growth}

長期處理程式會將處理程式資料儲存在AEM表單資料庫中。 使用一些簡單的程式設計和產品設定策略，可以將AEM表單資料庫的成長減到最少。

## 程式設計提示 {#process-design-tips}

儘可能使用短期程式。 短期處理程式不會將處理程式資料儲存在資料庫中。 使用短期程式的缺點在於，其狀態和狀態不會在管理控制檯中進行追蹤，並且沒有程式的歷史記錄。

有些服務作業(例如「指派任務」作業（使用者服務）)需要用於長期處理程式中。 在此情況下，您可以將程式分成數個子程式，並儘可能縮短其存留期。 如果您使用此策略，短期子流程應該處理大型資料專案，例如檔案值。

請謹慎使用變數。 使用長效處理序時，會針對每個處理序執行個體，在資料庫上為處理序中的每個變數分配空間。 策略性使用變數可節省大量空間。 例如，您可以在程式不再需要舊值時，覆寫變數值。 並刪除您建立且未使用的任何變數。 您可以驗證程式以尋找未使用的變數。

使用簡單的變數型別（例如string或int），並儘可能避免使用複雜的變數型別。 即使變數不包含值，資料庫空間也會分配給變數。 複雜變數通常比簡單變數需要更多空間。

## 產品管理秘訣 {#product-administration-tips}

有效使用全球檔案儲存(GDS)。 表單伺服器上的GDS目錄可用來儲存傳遞至處理程式中AEM表單一部分的服務的檔案。 為了改善效能，較小的檔案會儲存在記憶體中，並儲存在資料庫中。

管理主控台會公開Default Document Max Inline Size屬性，以設定儲存在記憶體中並儲存在資料庫中之檔案的大小上限。 (請參閱 [設定一般AEM表單設定](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings).) 如果您將此屬性設定為低值，大部分檔案都會儲存在GDS目錄中，而不是資料庫中。 優點在於，當檔案儲存在GDS目錄中時，不再需要這些檔案時，可以更輕鬆地刪除它們。
