---
title: 封裝權杖支援
seo-title: Encapsulated Token Support
description: 瞭解AEM中的封裝權杖支援。
seo-description: Learn about the Encapsulated Token support in AEM.
uuid: a7c6f269-bb5a-49ba-abef-ea029202ab6d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 2c263c0d-2521-49df-88ba-f304a25af8ab
exl-id: e24d815c-83e2-4639-8273-b4c0a6bb008a
source-git-commit: ed2cb35593780cd627c15f493e58d3b68c55519b
workflow-type: tm+mt
source-wordcount: '801'
ht-degree: 0%

---

# 封裝權杖支援{#encapsulated-token-support}

## 简介 {#introduction}

依預設，AEM會使用權杖驗證處理常式來驗證每個請求。 但是，為了提供驗證請求，「權杖驗證處理常式」需要存取每個請求的存放庫。 發生此情況是因為使用Cookie來維護驗證狀態。 邏輯上，狀態需要持續存在於存放庫中，才能驗證後續請求。 實際上，這表示驗證機制是有狀態的。

這對於水準擴充能力尤其重要。 在像下面描述的發佈伺服器陣列那樣的多重執行個體設定中，無法以最佳方式實現負載平衡。 透過狀態式驗證，持續驗證狀態將只適用於使用者首次驗證的執行個體。

![chlimage_1-33](assets/chlimage_1-33a.png)

以下列案例為例：

使用者可以在發佈執行個體1上進行驗證，但如果後續請求進入發佈執行個體2，則該執行個體沒有該持續驗證狀態，因為該狀態持續保留在發佈執行個體1和發佈執行個體2的存放庫中，且發佈執行個體具有自己的存放庫。

此問題的解決方案是在負載平衡器層級設定粘性連線。 使用粘性連線時，使用者一律會導向相同的發佈執行個體。 因此，不可能實現真正的最佳負載平衡。

如果發佈執行個體無法使用，則所有在該執行個體上驗證的使用者都將失去其工作階段。 這是因為需要存放庫存取權來驗證驗證Cookie。

## 使用封裝權杖的無狀態驗證 {#stateless-authentication-with-the-encapsulated-token}

水準擴充性的解決方案是無狀態驗證，可在AEM中使用新的Encapsulated Token支援。

封裝權杖是一種加密技術，可讓AEM安全地離線建立和驗證驗證資訊，而無需存取存放庫。 如此一來，驗證請求便可在所有發佈執行個體上發生，而不需要粘性連線。 它還有改善驗證效能的優點，因為不需要針對每個驗證請求存取存放庫。

您可以在下方的MongoMK作者和TarMK發佈執行個體中，檢視這如何在地理上分散的部署中運作：

![chlimage_1-34](assets/chlimage_1-34a.png)

>[!NOTE]
>
>請注意，封裝權杖與驗證有關。 這可確保無需存取存放庫即可驗證Cookie。 不過，使用者仍需存在於所有執行個體上，且每個執行個體都能存取該使用者下儲存的資訊。
>
>例如，如果在第一個發佈執行個體上建立了新使用者，則由於封裝Token的運作方式，它將在第二個發佈執行個體上成功驗證。 如果使用者不存在於第二個發佈執行個體上，請求仍不會成功。

## 設定封裝權杖 {#configuring-the-encapsulated-token}

>[!NOTE]
>同步使用者並依賴權杖驗證的所有驗證處理常式（例如SAML和OAuth）僅在以下情況下才能與封裝的權杖搭配使用：
>
>* 已啟用粘性工作階段，或
>
>* 同步啟動時，已在AEM中建立使用者。 這表示在處理常式的情況下，將不支援封裝的權杖 **建立** 同步程式期間的使用者。


設定封裝Token時，您需要考慮一些事項：

1. 由於涉及密碼編譯，所有執行個體都需要有相同的HMAC金鑰。 自AEM 6.3起，主要資料不再儲存在存放庫中，而是儲存在實際的檔案系統上。 考慮到這一點，複製金鑰的最佳方式是將其從來源執行個體的檔案系統複製到您要複製金鑰的目標執行個體的檔案系統。 請參閱下方「複製HMAC金鑰」下的詳細資訊。
1. 需要啟用封裝的Token。 這可透過Web主控台完成。

### 複製HMAC金鑰 {#replicating-the-hmac-key}

若要跨執行個體復寫金鑰，您需要：

1. 存取AEM例項，通常為製作例項，其中包含要複製的關鍵素材；
1. 找到 `com.adobe.granite.crypto.file` 本機檔案系統中的組合。 例如，在此路徑下：

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle25`

   此 `bundle.info` 每個資料夾內的檔案將識別該套件組合名稱。

1. 導覽至資料夾。 例如：

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle25/data`

1. 複製HMAC和主檔案。
1. 然後，前往您要將HMAC金鑰複製到的目標執行個體，並導覽至資料資料夾。 例如：

   * `<publish-aem-install-dir>/crx-quickstart/launchpad/felix/bundle25/data`

1. 貼上您先前複製的兩個檔案。
1. [重新整理加密套件組合](/help/communities/deploy-communities.md#refresh-the-granite-crypto-bundle) 如果目標執行個體已在執行中。

1. 對您要複製金鑰的所有執行個體重複上述步驟。

#### 啟用封裝權杖 {#enabling-the-encapsulated-token}

複製HMAC金鑰後，您可以透過Web主控台啟用封裝權杖：

1. 將瀏覽器指向 `https://serveraddress:port/system/console/configMgr`
1. 尋找名為的專案 **AdobeGranite權杖驗證處理常式** 並按一下。
1. 在下列視窗中，勾選 **啟用封裝權杖支援** 方塊並按 **儲存**.
