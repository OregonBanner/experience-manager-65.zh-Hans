---
title: 管理憑證
seo-title: Managing certificates
description: 瞭解如何匯入和匯出憑證，並編輯其信任設定。
seo-description: Learn how to import and export a certificate and edit its trust settings.
uuid: 46b1dbe5-517c-4294-bb52-cc6700a768e8
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9fd531c0-5206-4be0-a450-13e0dc806068
exl-id: 1fe0e7b4-6109-4f7a-8858-8237a1c5c93b
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '641'
ht-degree: 0%

---

# 管理憑證 {#managing-certificates}

使用「信任存放區管理」，您可以匯入、編輯和刪除您信任在伺服器上的憑證，以驗證數位簽名和憑證驗證。 您可以匯入和匯出任意數量的憑證。 匯入憑證後，您可以編輯信任設定和信任存放區型別。 合併信任存放區型別時，請考慮下列選項：

* **信任使用CA的憑證驗證：** 若為CRL驗證，請同時選取「信任身分」。
* **信任使用ICA的憑證驗證：** 選取「僅信任身分」。 不應將ICA信任為憑證驗證。 如果您信任ICA進行憑證驗證，則ICA會成為路徑建立的CA。 如果ICA同時受到憑證驗證和身分識別的信任，則會忽略CA廠商憑證，因為ICA會成為CA。
* **信任具有HTTP的OCSP伺服器：** 如果OSCP回應伺服器位在HTTPs位置，您也必須選取「信任SSL連線」。 如果OSCP回應者需要CRL驗證，請確定您也選取「信任身分」。
* **Adobe根目錄：** 請勿選取SSL連線或OCSP伺服器信任存放區型別。 SSL連線和OCSP伺服器不信任Adobe根目錄。 Adobe不會核發OCSP和SSL憑證。 Adobe根目錄以別名=&quot;ADOBEROOT&quot;隱含信任。

僅支援X509v3憑證。 此憑證型別可在二進位DER編碼檔案（.cer檔案）或包含相同DER編碼憑證的Base64編碼版本的文字檔案中提供(包括隱私權增強型郵件(PEM)格式的X509憑證)。

完成簽章驗證所需的憑證必須位於相同的存放區（HSM或資料庫）。

您也可以使用Trust Manager API匯入和刪除憑證。 如需詳細資訊，請參閱中的「使用信任管理員API匯入憑證」和「使用信任管理員API刪除憑證」。 [使用AEM表單程式設計](https://www.adobe.com/go/learn_aemforms_programming_63).

## 匯入憑證 {#import-a-certificate}

1. 在管理控制檯中，按一下 **[!UICONTROL 設定>信任存放區管理>憑證]**.
1. 按一下「匯入」，然後在「信任存放區型別」下方，選取下列其中一個選項：

   * **信任SSL連線：** 指定AEM表單可使用憑證透過SSL連線至外部系統。
   * **信任憑證簽名：** 指定在檔案簽署操作中信任憑證以證明作者數位簽名。
   * **信任簽名：** 指定在非作者數位簽章的檔案簽署作業中信任憑證。
   * **信任憑證驗證：** 指定AEM Forms使用憑證來驗證使用憑證或智慧卡驗證的使用者。
   * **OCSP伺服器的信任：** 指定AEM表單可以使用憑證來連線到外部OCSP回應程式
   * **信任身分：** 指定可以使用憑證來信任以上指定型別以外的資訊。

   >[!NOTE]
   >
   >信任存放區會隱含信任Adobe根憑證以進行憑證驗證、簽章、憑證簽章和身分。

1. 在「別名」方塊中，輸入憑證的識別碼。
1. 按一下 **[!UICONTROL 瀏覽]** 以尋找憑證，然後按一下 **[!UICONTROL 確定]**.

## 匯出憑證 {#export-a-certificate}

1. 在管理控制檯中，按一下 **[!UICONTROL 設定>信任存放區管理>憑證]**.
1. 按一下要匯出的憑證別名。 此 **[!UICONTROL 憑證詳細資料]** 頁面隨即顯示。
1. 按一下 **[!UICONTROL 匯出]**，依照指示匯出憑證，然後按一下 **[!UICONTROL 確定]**.

## 編輯憑證的信任設定和信任存放區型別 {#edit-a-certificate-s-trust-settings-and-trust-store-type}

1. 在管理控制檯中，按一下 **[!UICONTROL 設定>信任存放區管理>憑證]**.
1. 按一下要編輯的憑證別名。
1. 按一下 **[!UICONTROL 更新憑證]**.
1. 若要變更憑證的別名，請在「別名」方塊中鍵入新名稱。
1. 若要更新憑證的信任存放區型別，請選取適當的信任存放區型別。
1. 若要更新原則限制，請在[憑證原則]方塊中輸入原則資訊，然後按一下 **[!UICONTROL 確定]**.

## 刪除憑證 {#delete-a-certificate}

1. 在管理控制檯中，按一下 **[!UICONTROL 設定>信任存放區管理>憑證]**.
1. 選取要刪除之憑證的核取方塊，按一下 **[!UICONTROL 刪除]**，然後按一下 **[!UICONTROL 確定]**.
