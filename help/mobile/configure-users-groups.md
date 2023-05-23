---
title: 設定使用者和使用者群組
description: 請詳閱本頁面，瞭解使用者角色，以及如何設定使用者和群組，以支援行動應用程式的撰寫和管理。
uuid: 55cea2b3-d7e6-4174-92b3-ee97e46b59c4
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
discoiquuid: 167f3bd9-7dbc-4e6b-9868-3ee53935641b
exl-id: 9f814204-8cd4-4ba9-9e25-3ff1b25c1955
source-git-commit: f4b6eb2ded17ec641f23a1fc3b977ce77169c8a1
workflow-type: tm+mt
source-wordcount: '633'
ht-degree: 0%

---

# 設定您的使用者和使用者群組 {#configure-your-users-and-user-groups}

>[!NOTE]
>
>Adobe建議針對需要以單頁應用程式框架為基礎的使用者端轉譯（例如React）專案使用SPA編輯器。 [了解详情](/help/sites-developing/spa-overview.md).

本章說明使用者角色，以及如何設定使用者和群組，以支援行動應用程式的製作和管理。

## AEM Mobile應用程式使用者和群組管理 {#aem-mobile-application-users-and-group-administration}

若要協助組織和管理AEM應用程式的許可權模式，可使用下列兩個群組：

* 適用於應用程式管理員的應用程式管理員
* 應用程式作者的應用程式作者

### AEM Mobile應用程式內容作者（app-author群組） {#aem-mobile-application-content-authors-app-author-group}

應用程式作者群組的成員負責編寫AEM行動應用程式內容，包括頁面、文字、影像和視訊。

#### 群組設定 — 應用程式作者 {#group-configuration-app-authors}

1. 建立名為「app-authors」的新使用者群組：

   導覽至「使用者」Admin Console： [http://localhost:4502/libs/granite/security/content/groupadmin.html](http://localhost:4502/libs/granite/security/content/groupadmin.html)

   從使用者群組主控台中，選取「+」按鈕以建立群組。

   將此群組的ID設為「app-authors」，表示這是特定型別的作者使用者群組，專用於在AEM內編寫行動應用程式。

1. 新增成員至群組：作者

   ![chlimage_1-18](assets/chlimage_1-18.png)

   將應用程式作者新增至「作者」群組

1. 現在您已建立應用程式 — 作者使用者群組，您可以透過以下方式將個別團隊成員新增至此新群組： [使用者Admin console](http://localhost:4502/libs/granite/security/content/useradmin.md).

   ![chlimage_1-19](assets/chlimage_1-19.png)

   編輯使用者群組

1. 導覽至 [許可權主控台](http://localhost:4502/useradmin) 並新增許可權以管理cloudservices

   * /etc/cloudservices上的（讀取）
   >[!NOTE]
   >
   >App Authors會延伸AEM的預設內容作者(Authors)群組，繼承/content/phonegap底下建立內容的能力

### AEM Mobile應用程式管理員群組（app-admins群組） {#aem-mobile-application-administrators-group-app-admins-group}

app-admins群組的成員可以使用與應用程式作者相同的許可權來創作應用程式內容 **和** 此外，還負責：

* 在AEM中設定PhoneGap Build和AdobeMobile Services雲端服務
* 暫存、發佈和清除應用程式Content Sync OTA更新

>[!NOTE]
>
>許可權會決定AEM App Command Center中某些使用者動作的可用性。
>
>您會注意到，某些選項不適用於應用程式作者，而僅適用於應用程式管理員。

#### 群組設定 — 應用程式管理員 {#group-configuration-app-admins}

1. 建立名為app-admins的新群組。
1. 將下列群組新增至新的app-admins群組：

   * content-author
   * workflow-users

   ![chlimage_1-20](assets/chlimage_1-20.png)

1. 導覽至 [許可權主控台](http://localhost:4502/useradmin) 並新增許可權以管理cloudservices

   * （讀取、修改、建立、刪除、復寫） /etc/cloudservices/mobileservices
   * （讀取、修改、建立、刪除、復寫） /etc/cloudservices/phonegap-build

1. 在相同的許可權控制檯上，新增許可權以暫存、發佈和清除應用程式內容更新

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

## 控制面板圖磚許可權 {#dashboard-tile-permissions}

控制面板圖磚可能會根據使用者擁有的許可權公開不同的動作。 以下說明每個圖磚可用的動作。

除了這些許可權，動作也可以根據目前應用程式的設定方式顯示/隱藏。 例如，如果尚未將PhoneGap雲端設定指派給應用程式，則公開「遠端建置」動作就沒有意義。 這些專案將列於下方「**設定條件**&#39;區段。

### 管理應用程式動態磚 {#manage-app-tile}

圖磚目前沒有需要許可權的動作，但應用程式的詳細資訊頁面有下列動作：

* *編輯* 適用於app-author和app-admin （UI觸發器 — jcr：write - on /content/phonegap/{suffix}）
* *下載* 適用於app-author和app-admin （UI觸發器 — /content/phonegap/{suffix}）

下圖顯示應用程式的「下載」和「編輯」選項：

![chlimage_1-21](assets/chlimage_1-21.png)
