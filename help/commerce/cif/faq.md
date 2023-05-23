---
title: AEM — 使用Commerce Integration Framework進行Commerce整合常見問題集
description: AEM — 使用Commerce Integration Framework進行Commerce整合常見問題集
exl-id: d541607f-c4c9-4dd5-aadf-64d4cb5f9f2a
source-git-commit: c96f83b84ed1473aee0ddcca08a0e585ec088aa1
workflow-type: tm+mt
source-wordcount: '960'
ht-degree: 0%

---

# AEM — 使用Commerce Integration Framework進行Commerce整合常見問題集

## 1. CIF GraphQL是否僅用於商務，還是可用於查詢在AEM JCR上編寫的內容？

Adobe已採用Adobe Commerce的GraphQL API作為適用於所有商務相關資料的官方Commerce API。 因此，AEM會使用GraphQL透過I/O Runtime與Adobe Commerce及任何商務引擎交換商務資料。 此GraphQL API獨立於AEM GraphQL API，可存取內容片段。

## 2.能否透過Adobe Commerce管理員從AEM儲存及參考產品資產（影像）？ 如何才能使用Dynamic Media中的資產？

無官方AEM Assets — 提供Adobe Commerce整合。 有一個合作夥伴聯結器可在 [marketplace](https://marketplace.magento.com/partner/bounteous_ecomm).

或者，作為因應措施，您可以在AEM Assets中儲存產品資產（影像），但您必須在Adobe Commerce中手動儲存資產URL。 Dynamic Media是AEM Assets的一部分，且運作方式相同。

## 3.商業解決方案的部署位置重要嗎？ （內部部署或雲端）

否，您的商務解決方案部署在哪裡並不重要。 無論部署模式為何，CIF和AEM店面都能運作。 不過，如果解決方案是使用建議的E2E參考架構進行部署，E2E測試就可以根據代表典型企業客戶個人檔案的效能KPI執行。 此程式提供可作為基準的其他資訊。

## 4.如何在AEM中建立目錄頁面或產品頁面？ 它們如何在AEM中持續存在？

目錄頁面和產品頁面會根據通用目錄和產品頁面範本，在AEM中動態建立及快取。 AEM中未匯入及儲存任何產品或目錄資料。

## 5.當您更新商務解決方案中的產品資料時，這是否即時推送至AEM？ 還是批次流程？

搭配AEM使用的CIF附加元件可讓資料從商務解決方案依需求流向AEM。 因此，當您的商務解決方案中有更新時，此工作流程不是即時推送或批次程式。

## 6. AEM支援CIF的目錄大小多大？

目錄大小支援取決於您必須考慮的其他幾個方面。 您的目錄資料和頁面的快取比率是多少？ 您預期在高峰時段會有多少同時請求？ 您的商務解決方案的API可擴充性如何？

## 7. PIM如何在這個架構中運作？

PIM資料會透過GraphQL請求公開給AEM和使用者端。 Adobe建議將PIM與商務引擎(Adobe Commerce或其他)整合，以便之後可以從商務引擎擷取PIM資料。

## 8.您也會透過Dispatcher快取定價和其他資料嗎？ 這是否會引發頻繁的快取失效挑戰？

Dispatcher上不會快取價格或庫存等動態資料。 動態資料是透過GraphQL API直接使用網頁元件在使用者端擷取。 Dispatcher上只會快取靜態資料（例如產品或類別資料）。 如果產品資料變更，則需要讓快取失效。

## 9. AEM Dispatcher的快取失效如何與AEM和commerce搭配運作？

Adobe建議為Dispatcher上快取的頁面設定TTL型快取失效。 若是價格或庫存等動態資訊，Adobe建議在使用者端轉譯日期。 如需有關TTL型快取失效的詳細資訊，請參閱 [AEM傳送器](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17458.html?lang=zh-Hans)

## 10.對於使用Commerce跨AEM內容進行整合式搜尋是否有任何建議？

已提供產品搜尋參考實作，但沒有提供整合式搜尋與內容。 此功能因客戶而異，專案專屬層級可提供更理想的解決方案。

## 11. Search如何使用CIF搭配AEM和Commerce使用？

CIF提供搜尋列和搜尋結果元件。 搜尋列元件會將包含搜尋字詞的GraphQL請求傳送至商業解決方案，然後傳回包含產品名稱、價格、SLUG等的產品清單。 「搜尋結果」元件接著會在AEM中建立的搜尋結果頁面上，以相簿檢視顯示搜尋結果。 「搜尋」支援基本的全文檢索搜尋。 使用SLUG/url鍵來建置PDP的參考。

## 12.如何在MSM或翻譯中使用產品資料？

產品資料已在PIM或Adobe Commerce中翻譯。 AEM - Adobe Commerce整合支援連線至多個Adobe Commerce商店和商店檢視。 在MSM設定中，通常一個AEM網站會連結至一個Adobe Commerce商店檢視。

## 13.是否有使用商業文字來增強產品資料的方法？ 若有，會在哪裡完成？ 在AEM中還是在商務解決方案中？

Adobe建議在AEM中管理與行銷相關的資料和內容。 使用內容片段的其他屬性裝飾商務解決方案的產品資料，或建立非結構化內容的體驗片段並將其與您的產品連結。

## 14.公司在整個展示層使用AEM時，如何確保PCI相容性？

Adobe建議使用抽象的付款方法。 這麼做會讓瀏覽器使用者端與支付閘道提供者直接通訊，讓Adobe不會保留或傳遞持卡人日期，也不會傳遞商業解決方案。 此方法只需要第3級PCI相容性。 不過，還需要考慮其他完全符合PCI規範的事項，例如員工如何與系統和資料互動。 如需Adobe Commerce PCI相容性的詳細資訊，請參閱 [PCI法規遵循](https://business.adobe.com/products/magento/pci-compliance.html)

## 15.如果我使用AEM和Adobe Commerce雲端版本，此聯合解決方案是否符合PCI規範？

可以，您可以依要求取得自我評估問卷D和合規證明。

## 16.如何要求I/O Runtime試用版授權？

您可以要求試用版授權以使用I/O Runtime [此處](https://adobeio.typeform.com/to/obqgRm).
