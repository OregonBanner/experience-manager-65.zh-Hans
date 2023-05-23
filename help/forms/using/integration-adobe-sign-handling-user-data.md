---
title: 與Adobe Sign整合 |處理使用者資料
seo-title: Integration with Adobe Sign | Handling user data
description: 與Adobe Sign整合 |處理使用者資料
uuid: cb3a455d-2e33-44c8-8f71-3a7ecd939cd8
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e9e0d8fb-955e-4021-9e9a-9c95c6ffe88d
feature: Acrobat Sign
role: Admin
exl-id: b43ed9b7-b1ef-4878-ae3b-643b558eed7b
source-git-commit: 28d092a7713438c27213766f0bb702b699305b88
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 0%

---

# 與Adobe Sign整合 |處理使用者資料 {#integration-with-adobe-sign-handling-user-data}

[!DNL AEM Forms] 整合[!DNL  Adobe Sign] 啟用最適化表單中的電子簽章工作流程，以處理法律、銷售、薪資、人力資源管理工作流程的表單或協定。 它允許單一和多使用者簽署、連續和同時簽署工作流程、以匿名或登入使用者身分簽署表單，以及多種驗證使用者的方式。

當一名或多名簽署者簽署並提交最適化表單時， [!DNL Adobe Sign] 會產生包含簽名者相關資訊的合約。

如需有關的詳細資訊 [!DNL AEM Forms] 與整合 [!DNL Adobe Sign]，請參閱 [在最適化表單中使用Adobe Sign](/help/forms/using/working-with-adobe-sign.md).

## 使用者資料和資料存放區 {#data}

[!DNL Adobe Sign] 啟用的最適化表單包含簽名者的相關資訊，並可能包含最適化表單收集的其他使用者資料。 此 [!DNL Adobe Sign] 服務會儲存使用者資料，並在合約中簽名。 合約已儲存於 [!DNL Adobe Sign] 伺服器設定於 [!DNL AEM Forms] 雲端服務。 此外，如果最適化表單設定為使用Forms Portal提交動作，則協定資料會與表單資料一起儲存在Forms Portal資料存放區中。

## 存取和刪除使用者資料 {#access-and-delete-user-data}

使用者資料會在合約中收集，但不會儲存在任何服務表格中。 [!DNL Adobe Sign] 可讓管理員自行選擇管理他們在服務中控制的資料。 隱私權管理員： [!DNL Adobe Sign] 服務可以根據請求者的電子郵件地址列出或移除協定。

[!DNL Adobe Sign] 提供Web應用程式，可依參與者搜尋協定，並視需要刪除協定。 如需詳細資訊，請參閱 [Adobe Sign — 功能：刪除使用者資訊](https://helpx.adobe.com/sign/help/adobesign_gdpr_user_deletion.html).

針對設定為使用Forms Portal提交動作的最適化表單而設定的協定資料也會儲存在Forms Portal資料存放區中。 若要存取和刪除表單入口網站資料存放區的資料，請參閱 [Forms入口網站 |處理使用者資料](/help/forms/using/forms-portal-handling-user-data.md).
