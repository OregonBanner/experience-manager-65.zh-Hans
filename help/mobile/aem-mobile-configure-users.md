---
title: 設定您的使用者和使用者群組
description: 請詳閱本頁面，瞭解使用者角色，以及如何設定使用者和群組，以支援Mobile On-Demand Services應用程式的撰寫和管理。
uuid: 461e1725-41dd-4883-92b9-a7e175660401
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-on-demand-services-app
discoiquuid: c3c73e67-7f85-4308-b4cd-1b42d4f3f2d9
exl-id: 58b7d1b9-a851-442a-9d02-212cad8abbed
source-git-commit: f4b6eb2ded17ec641f23a1fc3b977ce77169c8a1
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 0%

---

# 設定您的使用者和使用者群組 {#configure-your-users-and-user-groups}

>[!NOTE]
>
>Adobe建議針對需要以單頁應用程式框架為基礎的使用者端轉譯（例如React）專案使用SPA編輯器。 [了解详情](/help/sites-developing/spa-overview.md).

本章說明使用者角色，以及如何設定使用者和群組，以支援行動應用程式的編寫和管理。

## AEM Mobile應用程式使用者和群組管理 {#aem-mobile-application-users-and-group-administration}

### AEM Mobile應用程式內容作者（app-author群組） {#aem-mobile-application-content-authors-app-author-group}

應用程式作者群組的成員負責編寫AEM行動應用程式內容，包括頁面、文字、影像和視訊。

#### 群組設定 — 應用程式作者 {#group-configuration-app-authors}

1. 建立名為「app-authors」的新使用者群組：

   導覽至「使用者」Admin Console： [http://localhost:4502/libs/granite/security/content/groupadmin.html](http://localhost:4502/libs/granite/security/content/groupadmin.html)

   從使用者群組主控台中，選取「+」按鈕以建立群組。

   將此群組的ID設為「app-authors」，表示這是特定型別的作者使用者群組，專用於在AEM內編寫行動應用程式。

1. 新增成員至群組：作者

   ![chlimage_1-167](assets/chlimage_1-167.png)

1. 現在您已建立應用程式 — 作者使用者群組，您可以透過以下方式將個別團隊成員新增至此新群組： [使用者Admin console](http://localhost:4502/libs/granite/security/content/useradmin.md).

   ![chlimage_1-168](assets/chlimage_1-168.png)

1. 下列專案可讓您新增至AEM內容作者群組：

   （讀取）於

   * /app
   * /etc/clientlibs
   * /etc/designs
   * /etc/cloudservices/dps2015

### AEM Mobile應用程式管理員群組（app-admins群組） {#aem-mobile-application-administrators-group-app-admins-group}

app-admins群組的成員可以使用與應用程式作者相同的許可權來創作應用程式內容 **和** 此外，還負責：

* 暫存、發佈和清除應用程式ContentSync OTA更新

>[!NOTE]
>
>許可權會決定AEM App Command Center中某些使用者動作的可用性。
>
>您會注意到，某些選項不適用於應用程式作者，而僅適用於應用程式管理員。

### 群組設定 — 應用程式管理員 {#group-configuration-app-admins}

1. 建立名為app-admins的新群組。
1. 將下列群組新增至新的app-admins群組：

   * content-author
   * workflow-users

   ![chlimage_1-169](assets/chlimage_1-169.png)

   >[!NOTE]
   >
   >使用PhoneGap Build服務進行遠端建置需要工作流程使用者

1. 導覽至 [許可權主控台](http://localhost:4502/useradmin) 並新增許可權以管理cloudservices

   * （讀取、修改、建立、刪除、復寫） /etc/cloudservices/mobileservices

1. 在相同的「許可權」控制檯上，新增許可權以暫存、發佈和清除應用程式內容更新；

   * （讀取、修改、建立、刪除、復寫） /etc/packages/mobileapp
   * （讀取） /var/contentsync

   >[!NOTE]
   >
   >套件復寫用於將應用程式更新從製作執行個體發佈到發佈執行個體

   >[!CAUTION]
   >
   >/var/contentsync存取遭拒(OOTB)。
   >
   >省略READ許可權可能會導致建置和復寫空白的更新套件。

1. 視需要新增成員到此群組
1. 匯出內容或上傳

   * （讀取） /etc/contentsync以存取匯出範本
   * （讀取） /var上的，路徑在讀取時周遊
   * （讀取、寫入、修改、刪除） /var/contentsync上的，以寫入、讀取和清除ContentSync快取匯出內容

### 其他资源 {#additional-resources}

若要進一步瞭解建立AEM Mobile On-demand Services應用程式的其他兩個角色和責任，請參閱下列資源：

* [針對AEM Mobile On-demand Services開發AEM內容](/help/mobile/aem-mobile-on-demand.md)
* [為AEM Mobile On-demand Services應用程式編寫AEM內容](/help/mobile/mobile-apps-ondemand.md)
