---
title: 建立已關閉的使用者群組
seo-title: Creating a Closed User Group
description: 瞭解如何建立封閉式使用者群組。
seo-description: Learn how to create a Closed User Group.
uuid: dc3c7dbd-2e86-43f9-9377-3b75053203b3
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 6ae57874-a9a1-4208-9001-7f44a1f57cbe
docset: aem65
exl-id: 9efba91d-45e8-42e1-9db6-490d21bf7412
source-git-commit: 64d174cc824c8bf200cece4e29f60f946ee5560e
workflow-type: tm+mt
source-wordcount: '753'
ht-degree: 1%

---

# 建立已關閉的使用者群組{#creating-a-closed-user-group}

封閉式使用者群組(CUG)可用來限制對已發佈網際網路網站中特定頁面的存取。 這類頁面需要指派的成員登入並提供安全性認證。

若要在您的網站中設定這類區域，請：

* [建立實際已關閉的使用者群組並指派成員](#creating-the-user-group-to-be-used).

* [將此群組套用至所需的頁面](#applying-your-closed-user-group-to-content-pages) 並選取（或建立）登入頁面，以供CUG的成員使用；也會在將CUG套用至內容頁面時指定。

* [建立連結，以某種形式至少連結到保護區內的一個頁面](#linking-to-the-cug-pages)，否則不會顯示。

* [設定Dispatcher](#configure-dispatcher-for-cugs) 若正在使用中。

>[!CAUTION]
>
>在建立封閉式使用者群組(CUG)時，應一律考慮效能。
>
>雖然CUG中的使用者和群組數量沒有限制，但頁面上大量的CUG可能會減慢轉譯效能。
>
>進行效能測試時，應一律考量CUG的影響。

## 建立要使用的使用者群組 {#creating-the-user-group-to-be-used}

若要建立已關閉的使用者群組，請執行下列動作：

1. 前往 **工具 — 安全性** 從AEM homescreen取得。

   >[!NOTE]
   >
   >另請參閱 [管理使用者和群組](/help/sites-administering/security.md#managing-users-and-groups) 以取得建立和設定使用者和群組的完整資訊。

1. 選取 **群組** 卡片。

   ![screenshot_2018-10-30at145502](assets/screenshot_2018-10-30at145502.png)

1. 按下 **建立** 按鈕來建立新群組。
1. 命名您的新群組；例如， `cug_access`.

   ![screenshot_2018-10-30at151459](assets/screenshot_2018-10-30at151459.png)

1. 前往 **成員** 標籤並將所需的使用者指派給此群組。

   ![screenshot_2018-10-30at151808](assets/screenshot_2018-10-30at151808.png)

1. 啟動您指派給您的CUG的任何使用者；在此情況下，則是 `cug_access`.
1. 啟動封閉式使用者群組，使其可在發佈環境中使用；在此範例中， `cug_access`.

## 將封閉式使用者群組套用至內容頁面 {#applying-your-closed-user-group-to-content-pages}

若要將CUG套用至一或多個頁面，請執行下列動作：

1. 導覽至您要指派給CUG之受限制區段的根頁面。
1. 按一下頁面的縮圖，然後選取 **屬性** 在頂端工具列上。

   ![screenshot_2018-10-30at162632](assets/screenshot_2018-10-30at162632.png)

1. 在下列視窗中，開啟 **進階** 標籤。

1. 向下捲動至 **驗證需求** 區段。

   1. 啟動 **啟用** 勾選方塊。

   1. 將路徑新增至 **登入頁面**.
這是選擇性的，如果保留為空白，將會使用標準登入頁面。

   ![已新增CUG](assets/cug-authentication-requirement.png)

1. 接下來，前往 **許可權** 標籤並選取 **編輯已關閉的使用者群組**.

   ![screenshot_2018-10-30at163003](assets/screenshot_2018-10-30at163003.png)

   >[!NOTE]
   >
   >「許可權」標籤中的CUG無法從Blueprint轉出至即時副本。 请在配置 Live Copy 时对此进行规划。
   >
   >如需詳細資訊，請參閱 [此頁面](closed-user-groups.md#aem-livecopy).

1. 此 **編輯已關閉的使用者群組** 對話方塊將會開啟。 您可以在此處搜尋並選取您的CUG，然後確認群組選取範圍 **儲存**.

   群組將被新增至清單中；例如，群組 **cug_access**.

   ![已新增CUG](assets/cug-added.png)

1. 確認變更，透過 **儲存並關閉**.

>[!NOTE]
>
>另請參閱 [Identity Management](/help/sites-administering/identity-management.md) 瞭解發佈環境中的設定檔以及提供登入和登出表單的相關資訊。

## 連結至CUG頁面 {#linking-to-the-cug-pages}

由於匿名使用者看不到任何連至CUG頁面的連結目標，因此linkchecker會移除這類連結。

若要避免此問題，建議您建立指向CUG區域中頁面的非受保護重新導向頁面。 然後轉譯導覽專案，而不會導致linkchecker任何問題。 只有在實際存取重新導向頁面時，使用者才會在CUG區域中重新導向 — 在成功提供其登入認證後。

## 設定CUG的Dispatcher {#configure-dispatcher-for-cugs}

如果您使用Dispatcher，則需要使用以下屬性定義Dispatcher陣列：

* [virtualhost](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#identifying-virtual-hosts-virtualhosts)：比對CUG套用至的頁面路徑。
* \sessionmanagement：請參閱下文。
* [快取](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#configuring-the-dispatcher-cache-cache)：專屬於CUG套用之檔案的快取目錄。

### 為CUG設定Dispatcher工作階段管理 {#configuring-dispatcher-session-management-for-cugs}

設定 [dispatcher.any檔案中的工作階段管理](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#enabling-secure-sessions-sessionmanagement) 用於CUG。 要求CUG頁面的存取權時使用的驗證處理常式，會決定您設定工作階段管理的方式。

```xml
/sessionmanagement
    ...
    /header "Cookie:login-token"
    ...
```

>[!NOTE]
>
>當Dispatcher陣列啟用工作階段管理時，不會快取陣列處理的所有頁面。 若要快取CUG以外的頁面，請在dispatcher.any中建立第二個陣列
>可處理非CUG頁面。

1. 設定 [/sessionmanagement](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#enabling-secure-sessions-sessionmanagement) 透過定義 `/directory`；例如：

   ```xml
   /sessionmanagement
     {
     /directory "/usr/local/apache/.sessions"
     ...
     }
   ```

1. 設定 [/allowAuthorized](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#caching-when-authentication-is-used) 至 `0`.
