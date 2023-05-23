---
title: Granite作業 — 使用者和群組管理
seo-title: Granite Operations - User and Group Administration
description: 瞭解Granite使用者和群組管理。
seo-description: Learn about Granite user and group administration.
uuid: 7b6b7767-712c-4cc8-8d90-36f26280d6e3
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 95ab2e54-0f8d-49e0-ad20-774875f6f80a
exl-id: f3477d21-7e9a-4588-94e8-496bc42434a8
feature: Security
source-git-commit: 9134130f349c6c7a06ad9658a87f78a86b7dbf9c
workflow-type: tm+mt
source-wordcount: '923'
ht-degree: 4%

---

# Granite作業 — 使用者和群組管理{#granite-operations-user-and-group-administration}

由於Granite納入JCR API規格的CRX Repository實作，因此擁有自己的使用者和群組管理。

這些帳戶是 [AEM帳戶](/help/sites-administering/security.md) 而且如果存取帳號，則會反映對Granite管理所做的任何帳號變更。 [AEM使用者主控台](/help/sites-administering/security.md#accessing-user-administration-with-the-security-console) (例如： `http://localhost:4502/useradmin`)。 您也可以從AEM使用者主控台管理許可權和其他AEM細節。

Granite使用者和群組管理主控台都可從 **[工具](/help/sites-administering/tools-consoles.md)** 觸控最佳化UI的控制檯：

![chlimage_1-72](assets/chlimage_1-72a.png)

選擇其中一項 **使用者** 或 **群組** 從「工具」主控台將開啟適當的主控台。 在這兩種模式中，您都可從工具列使用點按方塊然後動作，或透過下方的連結開啟帳戶詳細資訊，以採取動作 **名稱**.

* [使用者管理](#user-administration)

   ![chlimage_1-73](assets/chlimage_1-73a.png)

   此 **使用者** 主控台清單：

   * 使用者名稱
   * 使用者登入名稱（帳戶名稱）
   * 已指定帳戶的任何標題

* [群組管理](#group-administration)

   ![chlimage_1-74](assets/chlimage_1-74a.png)

   此 **群組** 主控台清單：

   * 群組名稱
   * 群組說明
   * 群組中的使用者/群組數量

## 使用者管理 {#user-administration}

### 新增使用者 {#adding-a-new-user}

1. 使用 **新增使用者** 圖示：

   ![](do-not-localize/chlimage_1-1.png)

1. 此 **建立使用者** 表單將會開啟：

   ![chlimage_1-75](assets/chlimage_1-75a.png)

   您可以在此處輸入帳戶的使用者詳細資訊（大部分為標準且易於說明）：

   * **ID**

      這是使用者帳戶的唯一識別碼。 此為必填欄位，不得包含空格。

   * **电子邮件地址**
   * **密码**

      密碼為必填。

   * **重新键入密码**

      這是強制性的，因為確認密碼需要它。

   * **名字**
   * **姓氏**
   * **电话号码**
   * **职务**
   * **街道**
   * **移动设备**
   * **城市**
   * **邮政编码**
   * **国家/地区**
   * **状态**
   * **标题**
   * **性别**
   * **关于**
   * **帐户设置**

      * **狀態**
您可以將帳戶標幟為 
**作用中** 或 **非使用中**.
   * **照片**

      您可以在此處上傳像片以用作頭像。

      接受的文件类型: `.jpg .png .tif .gif`

      偏好大小： `240x240px`

   * **将用户添加到组**

      使用選擇下拉式清單來選取使用者應成為其成員的群組。 選取後，使用 **X** 儲存前取消選取的名稱。

   * **组**

      使用者目前所屬的群組清單。 使用 **X** 儲存前取消選取的名稱。


1. 當您已定義使用者帳戶時，請使用：

   * **取消** 以中止註冊。
   * **儲存** 以完成註冊。 將使用訊息確認使用者帳戶的建立。

### 編輯現有使用者 {#editing-an-existing-user}

1. 從使用者控制檯使用者名稱下的連結存取使用者詳細資訊。

1. 您現在可以編輯詳細資訊，如下所示 [新增使用者](#adding-a-new-user).

1. 從使用者控制檯使用者名稱下的連結存取使用者詳細資訊。

1. 您現在可以編輯詳細資訊，如下所示 [新增使用者](#adding-a-new-user).

### 變更現有使用者的密碼 {#changing-the-password-for-an-existing-user}

1. 從使用者控制檯使用者名稱下的連結存取使用者詳細資訊。

1. 您現在可以編輯詳細資訊，如下所示 [新增使用者](#adding-a-new-user). 下 **帳戶設定** 有一個連結 **變更密碼**.

   ![chlimage_1-76](assets/chlimage_1-76a.png)

1. 此 **變更密碼** 對話方塊將會開啟。 輸入並重新輸入新密碼以及您的密碼。 使用 **確定** 以確認變更。

   ![chlimage_1-77](assets/chlimage_1-77a.png)

   訊息會確認密碼已變更。

### 快速群組指派 {#quick-group-assignment}

1. 使用點按方塊標示一或多個使用者。
1. 使用 **群組** 圖示：

   ![](do-not-localize/chlimage_1-2.png)

   若要開啟群組選擇下拉式清單：

   ![chlimage_1-78](assets/chlimage_1-78a.png)

1. 在選取方塊中，您可以選取或取消選取使用者帳戶應屬於的群組。

1. 當您已指派或未指派群組時，視需要使用：

   * **取消** 中止變更
   * **儲存** 確認變更

### 刪除現有使用者詳細資訊 {#deleting-existing-user-details}

1. 使用點按方塊標示一或多個使用者。
1. 使用 **刪除** 圖示可刪除使用者詳細資訊：

   ![](do-not-localize/chlimage_1-3.png)

1. 系統會要求您確認刪除，然後訊息會確認已實際刪除。

## 群組管理 {#group-administration}

### 新增群組 {#adding-a-new-group}

1. 使用「新增群組」圖示：

   ![](do-not-localize/chlimage_1-4.png)

1. 此 **建立群組** 表單將會開啟：

   ![chlimage_1-79](assets/chlimage_1-79a.png)

   您可以在此處輸入群組詳細資料：

   * **ID**

      這是群組的唯一識別碼。 此為必填欄位，不得包含空格。

   * **名称**

      群組的名稱；將顯示在群組主控台中。

   * **描述**

      群組的說明。

   * **将成员添加到组**

      使用選取下拉式清單來選取要新增至群組的使用者。 選取後，使用 **X** 儲存前取消選取的名稱。

   * **组成员**

      群組中的使用者清單。 使用 **X** 儲存前取消選取的名稱。

1. 定義群組後，請使用：

   * **取消** 以中止註冊。
   * **儲存** 以完成註冊。 將使用訊息確認群組的建立。

### 編輯現有群組 {#editing-an-existing-group}

1. 從「群組」主控台中群組名稱下方的連結存取群組詳細資料。

1. 您現在可以在中編輯並儲存詳細資料 [新增群組](#adding-a-new-group).

### 複製現有群組 {#copying-an-existing-group}

1. 使用點按方塊標示群組。
1. 使用 **複製** 圖示以複製群組詳細資訊：

   ![](do-not-localize/chlimage_1-5.png)

1. 此 **編輯群組設定** 將開啟表單。

   群組ID將與原始的相同，但首碼為 `Copy of`. 您必須編輯此專案，因為ID不可包含空格。 所有其他詳細資料將與原始資料相同。

   您現在可以在中編輯並儲存詳細資料 [新增群組](#adding-a-new-group).

### 刪除現有群組 {#deleting-an-existing-group}

1. 使用點按方塊標示一或多個群組。
1. 使用 **刪除** 圖示可刪除群組詳細資訊：

   ![](do-not-localize/chlimage_1-6.png)

1. 系統會要求您確認刪除，然後訊息會確認已實際刪除。
