---
title: AEM Communities中的使用者和UGC管理服務
seo-title: User and UGC Management Service in AEM Communities
description: 使用API來大量刪除和大量匯出使用者產生的內容，並停用使用者帳戶。
seo-description: Use APIs to bulk delete and bulk export user generated content, and disable user account.
uuid: 91180659-617d-4f6c-9a07-e680770d0d8f
contentOwner: mgulati
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
discoiquuid: d305821d-1371-4e4a-8b28-8eee8fafa43b
docset: aem65
role: Admin
exl-id: 526ef0fa-3f20-4de4-8bc5-f435c60df0d0
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 1%

---

# AEM Communities中的使用者和UGC管理服務 {#user-and-ugc-management-service-in-aem-communities}

>[!IMPORTANT]
>
>以下各節以GDPR為例，但說明的詳細資料適用於所有資料保護和隱私權法規，例如GDPR、CCPA等。

AEM Communities會公開現成可用的API，以管理使用者設定檔和大量管理使用者產生的內容(UGC)。 啟用後， **UserUgcManagement** 此服務可讓有特殊許可權的使用者（社群管理員和版主）停用使用者設定檔，以及大量刪除或大量匯出特定使用者的UGC。 這些API也讓客戶資料的控管者和處理者能夠遵守歐盟一般資料保護規範(GDPR)和其他受GDPR啟發的隱私權法令。

如需進一步資訊，請參閱 [Adobe隱私權中心的GDPR頁面](https://www.adobe.com/privacy/general-data-protection-regulation.html).

>[!NOTE]
>
>若您已設定 [AEM Communities中的Adobe Analytics](/help/communities/analytics.md) 之後，擷取的使用者資料會傳送至Adobe Analytics伺服器。 Adobe Analytics提供的API可讓您存取、匯出和刪除使用者資料，以及遵守GDPR。 如需詳細資訊，請參閱 [提交存取與刪除請求](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/gdpr-submit-access-delete.html).

若要使用這些API，您必須啟用 `/services/social/ugcmanagement` 端點（透過啟動UserUgcManagement服務）。 若要啟用此服務，請安裝 [範例servlet](https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/main/bundles/communities-ugc-management-servlet) 可用日期 [GitHub.com](https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/main/bundles/communities-ugc-management-servlet). 接著，使用http要求，以適當的引數點選Communities網站之發佈執行個體上的端點，如下所示：

`https://localhost:port/services/social/ugcmanagement?user=<authorizable ID>&operation=<getUgc>`. 不過，您也可以建置UI （使用者介面）來管理系統中的使用者設定檔和使用者產生的內容。

這些API可執行以下功能。

## 擷取使用者的UGC {#retrieve-the-ugc-of-a-user}

**getUserUgc(ResourceResolver resourceResolver， String user， OutputStream outputStream)** 協助從系統匯出使用者的所有UGC。

* **使用者**：使用者的可授權識別碼。
* **outputstream**：結果會以輸出資料流傳回，其為zip檔案，包含使用者產生的內容（以json檔案形式）和附件（包含使用者上傳的影像或影片）。

例如，若要匯出名為Weston McCall的使用者(使用weston.mccall@dodgit.com作為可授權ID登入communities網站)的UGC，您可以傳送類似以下的httpGET請求：

`https://localhost:port/services/social/ugcmanagement?user=weston.mccall@dodgit.com&operation=getUgc`

## 刪除使用者的UGC {#delete-the-ugc-of-a-user}

**deleteUserUgc(ResourceResolver resourceResolver， String user)** 協助從系統中刪除使用者的所有UGC。

* **使用者**：使用者的可授權識別碼。

例如，若要透過http-POST請求刪除具有可授權ID weston.mccall@dodgit.com之使用者的UGC，請使用以下引數：

* 用户 = `weston.mccall@dodgit.com`
* 操作 = `deleteUgc`

### 從Adobe Analytics刪除UGC {#delete-ugc-from-adobe-analytics}

若要從Adobe Analytics刪除使用者資料，請遵循 [GDPR分析工作流程](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/an-gdpr-workflow.html)；因為API不會從Adobe Analytics刪除使用者資料。

如需AEM Communities使用的Adobe Analytics變數對應，請參閱下列影像：

![Adobe Analytics的AEM社群變數對應](assets/analytics-communities-mapping.png)

## 停用使用者帳戶 {#disable-a-user-account}

**deleteUserAccount(ResourceResolver resourceResolver， String user)** 協助停用使用者帳戶。

* **使用者**：使用者的可授權識別碼。

>[!NOTE]
>
>停用使用者將會刪除使用者在伺服器上產生的所有內容。

例如，刪除具有可授權ID之使用者的設定檔 `weston.mccall@dodgit.com` 透過httpPOST要求，使用以下引數：

* 用户 = `weston.mccall@dodgit.com`
* 操作 = `deleteUser`

>[!NOTE]
>
>deleteUserAccount() API只會停用系統中的使用者設定檔，並移除UGC。 不過，若要從系統刪除使用者設定檔，請瀏覽至 **CRXDE Lite**： [https://&lt;server>/crx/de](https://localhost:4502/crx/de)，找出使用者節點並將其刪除。
