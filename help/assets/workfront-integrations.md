---
title: '[!DNL Experience Manager Assets] 與整合 [!DNL Adobe Workfront]'
description: 以下專案之間的整合簡介： [!DNL Assets] 和 [!DNL Workfront]
role: Admin,Leader,Architect
feature: Integrations
exl-id: 57e2bffe-8094-4557-99c8-7b482681687e
hide: true
source-git-commit: 3d5e9ad8ee19756b05e5a77a3f748bc647fcf734
workflow-type: tm+mt
source-wordcount: '1158'
ht-degree: 5%

---

# [!DNL Adobe Experience Manager Assets] 與整合 [!DNL Adobe Workfront] {#assets-integration-overview}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/integrations/workfront-integrations.html?lang=en) |
| AEM 6.5 | 本文 |

[!DNL Adobe Workfront] 是一个工作管理应用程序，它帮助您集中在一处管理工作的整个生命周期。以下兩者的整合： [!DNL Workfront] 和 [!DNL Adobe Experience Manager Assets] 可讓組織在本質上連線工作和數位資產管理，藉以改善內容速度和上市時間。 在Workfront中管理其工作的情況下，使用者可以存取所需的檔案和影像。

此 [!DNL Workfront for Experience Manager enhanced connector] 透過端對端工作流程實現增強的業務流程，並提供個人化的端對端使用者端體驗和中央儲存。 Adobe提供標準聯結器和增強型聯結器，可整合這兩個解決方案。 如需比較，請參閱下列支援的功能，並參閱 [的新增功能 [!DNL enhanced connector]](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience).

[!DNL Workfront for Experience Manage enhanced connector] 可讓您的組織：

* 在Workfront中自動建立連結的Experience Manager資料夾，並根據WorkfrontPortfolio、計畫和專案組織資料夾。
* 將Workfront專案中繼資料與連結的Experience Manager資料夾同步。
* 以新版本Experience Manager中繼資料更新。
* 使用Experience Manager工作流程，根據可設定的條件設定Workfront物件狀態。
* 將資產發佈到Experience Manager發佈環境或Brand Portal。

請參閱平台支援和 [增強型聯結器的先決條件](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience).

>[!IMPORTANT]
>
>* Adobe需要部署和設定 [!DNL Adobe Workfront for Experience Manager enhanced connector] 僅透過認證合作夥伴或 [!DNL Adobe Professional Services]. 如果部署與設定沒有認證合作夥伴或 [!DNL Adobe Professional Services]，Adobe不支援。
>
>* Adobe可能會將更新發行至 [!DNL Adobe Workfront] 和 [!DNL Adobe Experience Manager] 讓此聯結器成為備援；如果發生這種情況，客戶可能需要從使用此聯結器進行轉換。
>
>* Adobe支援增強型聯結器1.7.4版及更新版本。 不支援舊版發行前版本和自訂版本。 若要檢查增強型聯結器版本，請導覽至 `digital.hoodoo` 群組可在左側窗格中找到，位置為 [封裝管理員](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=zh-Hans).
>
>* 另請參閱 [適用於Experience Manager Assets增強型聯結器的Workfront合作夥伴認證考試](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html). 如需有關考試的資訊，請參閱 [考試指南](https://express.adobe.com/page/Tc7Mq6zLbPFy8/).


## 比較以下專案之間的不同整合： [!DNL Assets] 和 [!DNL Workfront] {#feature-parity-matrix}

以下為透過以下各種整合型別所提供的功能細節： [!DNL Assets] 和 [!DNL Workfront].

| 专题 | 描述 | [!DNL Workfront] 和 [!DNL Assets Essentials] *無聯結器(OOTB)* | [!DNL Workfront for Experience Manager enhanced connector] *需要聯結器* | Workfront和 [!DNL Experience Manager as a Cloud Service] *無聯結器(OOTB)* |
|----|----|----|-----|-----|
| 部署方法 | 適合的 [!DNL Assets] 方案。 | Assets Essentials | Adobe Managed Services，內部部署 | 云服务 |
| **常规** |
| 傳送數位檔案來源 [!DNL Workfront] 至 [!DNL Assets] | WF檔案的最新版本可上傳至AEM Assets，這會連結為檔案的新版本。 | ✓ | ✓ | ✓ |
| 手動將AEM資料夾連結至Workfront物件 | 現有的AEM資料夾可連結為Workfront資料夾，其子資產可連結為新的Workfront檔案。 | ✓ | ✓ | ✓ |
| 連結 [!DNL Assets] Workfront物件 | AEM中的現有資產可以連結到新的Workfront檔案，或作為現有檔案的新版本。 | ✓ | ✓ | ✓ |
| 新增至連結資料夾的資產會自動傳送至AEM | 如果將檔案新增至連結的資料夾，則會自動將關聯的資產作為新資產上傳到AEM Assets。 | ✓ | ✓ | ✓ |
| 從Workfront下載連結的AEM Assets | 在Workfront中連結資產時，使用者可以下載資產的位元組。 | ✓ | ✓ | ✓ |
| 在Workfront中搜尋AEM Assets | Workfront中的AEM Assets選擇器可讓您以全文搜尋資產。 | ✓ | ✓ | ✓ |
| 在Workfront中搜尋AEM資料夾 | Workfront中的AEM Assets選擇器允許對資料夾進行全文搜尋。 | ✓ | ✓ | ✓ |
| 從Workfront檢視和導覽AEM資料夾階層 | Workfront中的AEM Assets選擇器可讓您瀏覽受使用者在AEM中設定的相關存取控制項和許可權限制的AEM Assets階層。 | ✓ | ✓ | ✓ |
| 在AEM時間軸中追蹤資產版本 | 維護Workfront和AEM之間的檔案版本記錄。 | ✓ | ✓ | ✓ |
| 在Workfront中取消資產與AEM Assets的連結 | 從AEM連結的現有資產可以從關聯的Workfront檔案中取消連結。 這不會刪除AEM內的原始資產。 | ✓ | ✓ | ✓ |
| 從Workfront將新版本的資產新增至AEM Assets | 在Workfront的檔案中新增新版本時，使用者可以將新版本傳送至AEM以取代現有版本。 | ✓ | ✓ | ✓ |
| 按一下時在Workfront中連結的資產(直接使用者連結至AEM) | 系統會將使用者導向至AEM，以從Workfront預覽連結的資產。 | ✓ | ✓ | 近期 |
| 在Workfront中自動建立連結的AEM資料夾 | 使用專案狀態在Workfront中自動建立連結的AEM資料夾。 根據WorkfrontPortfolio、計畫和專案自動設定AEM資料夾。 | 否 | ✓ | 否 |
| 從Workfront直接導覽至AEM存放庫 | 允許使用者導覽至Workfront中設定的可用AEM存放庫。 | ✓ | 否 | ✓ |
| 在Workfront中建立連結的AEM資料夾 | 使用「檔案」標籤中的選項，在Workfront中手動建立連結的AEM資料夾。 | ✓ | 否 | ✓ |
| 評論同步 | 從自動同步資產的註解 [!DNL Workfront] 至 [!DNL Assets] | 否 | ✓ | 否 |
| 支援連線至單一AEM環境的多個Workfront環境 | 來自多個Workfront環境的使用者可以連線至單一AEM環境。 | ✓ | 否 | ✓ |
| 支援連線至單一Workfront環境的多個AEM環境 | 單一Workfront環境內的使用者可以在多個AEM環境之間傳送或連結資產。 | ✓ | ✓ | ✓ |
| **元数据** |
| 將Workfront資產中繼資料對應至AEM Assets | Workfront物件和自訂表單屬性可能會對應至AEM資產中繼資料屬性。 值將在初始上傳/連結時推送。 | ✓ | ✓ | ✓ |
| 在Workfront中自動建立檔案自訂Forms | 使用AEM工作流程將自訂表單附加至Workfront檔案、任務和問題。 | 否 | ✓ | 否 |
| 在AEM Assets和Workfront之間雙向自動更新中繼資料 | 在AEM Assets和Workfront之間自動更新中繼資料。 資產必須先從Workfront推送至AEM，且Workfront資產中繼資料必須對應至AEM資產，才能正確進行雙向中繼資料更新。 | 否 | ✓ | 否 |
| 在Workfront中即時檢視對應至AEM的中繼資料 | 在「Workfront檔案詳細資訊」和「檔案摘要」面板中，檢視更新後對應至AEM的中繼資料。 | ✓ | 否 | ✓ |
| 將更新的Workfront中繼資料即時推送到AEM | 自動將對應的Workfront中繼資料更新為AEM，無需重新推送資產或資產的新版本。 | ✓ | 否 | ✓ |
| 將Workfront中繼資料對應至AEM Assets資料夾 | 將Workfront專案中繼資料與連結的AEM資料夾同步。 | 否 | ✓ | ✓ |
| 新版本的AEM中繼資料更新 | AEM中的設定可決定Workfront中新版本的資產是否也會推動對其中繼資料所做的任何變更。 | 否 | ✓ | 否 |
| 在Workfront中自訂Forms變更時自動更新AEM中繼資料 | AEM可讓您訂閱Workfront中檔案表單的更新。 因此，Workfront檔案自訂表單中繼資料的任何更新都會修改對應AEM中繼資料欄位的值。 | 否 | ✓ | 否 |
| **工作流程（現成可用）** |
| 在連結的資產上建立新校訂版本 | 在Workfront中連結資產時，會自動產生校訂。 | 否 | 自定义 | 否 |
| 在Workfront物件上設定狀態 | 使用AEM工作流程根據可設定的條件設定Workfront物件狀態 | 否 | ✓ | 近期 |
| 將資產發佈至AEM發佈環境或Brand Portal | 為Workfront使用者提供自動將連結的資產發佈至AEM發佈環境或Brand Portal的選項。 | 否 | ✓ | 近期 |
