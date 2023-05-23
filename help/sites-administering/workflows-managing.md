---
title: 管理对工作流的访问权限
seo-title: Managing Access to Workflows
description: 瞭解如何管理工作流程存取許可權。
seo-description: Learn how to manage access to Workflows.
uuid: 58f79b89-fe56-4565-a869-8179c1ac68de
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 5150867a-02a9-45c9-b2fd-e536b60ffa8c
exl-id: cc54d637-d66c-49d2-99ee-00d96f1a74e0
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 2%

---

# 管理对工作流的访问权限{#managing-access-to-workflows}

根據使用者帳戶設定ACL，以允許（或停用）啟動和參與工作流程。

## 工作流程所需的使用者許可權 {#required-user-permissions-for-workflows}

在下列情況下，可以對工作流程採取行動：

* 您正在使用 `admin` 帳戶
* 已將帳戶指派給預設群組 `workflow-users`：

   * 此群組擁有您的使用者執行工作流程動作所需的所有許可權。
   * 當帳戶在此群組中時，它只能存取它啟動的工作流程。

* 已將帳戶指派給預設群組 `workflow-administrators`：

   * 此群組擁有您的有特殊許可權使用者監視和管理工作流程所需的所有許可權。
   * 當帳戶在此群組中時，它可以存取所有工作流程。

>[!NOTE]
>
>這些是最低需求。 您的帳戶也必須是指派的參與者或已指派群組的成員，才能執行特定步驟。

## 設定工作流程的存取權 {#configuring-access-to-workflows}

工作流程模型會繼承預設存取控制清單(ACL)，以控制使用者與工作流程互動的方式。 若要自訂工作流程的使用者存取，請修改包含工作流程模型節點之資料夾的存放庫中的「存取控制清單(ACL)」：

* [將特定工作流程模型的ACL套用至/var/workflow/models](/help/sites-administering/workflows-managing.md#apply-an-acl-for-the-specific-workflow-model-to-var-workflow-models)
* [在/var/workflow/models中建立子資料夾，並將ACL套用至該資料夾](/help/sites-administering/workflows-managing.md#create-a-subfolder-in-var-workflow-models-and-apply-the-acl-to-that)

>[!NOTE]
>
>如需有關使用CRXDE Lite來設定ACL的資訊，請參閱 [存取許可權管理](/help/sites-administering/user-group-ac-admin.md#access-right-management).

### 將特定工作流程模型的ACL套用至/var/workflow/models {#apply-an-acl-for-the-specific-workflow-model-to-var-workflow-models}

如果工作流程模型儲存在 `/var/workflow/models` 然後，您可以在資料夾上指派特定的ACL （僅與該工作流程相關）：

1. 在網頁瀏覽器中開啟CRXDE Lite(例如， [http://localhost:4502/crx/de](http://localhost:4502/crx/de))。
1. 在節點樹狀結構中，選取工作流程模型資料夾的節點：

   `/var/workflow/models`

1. 按一下 **存取控制** 標籤。
1. 在 **本機存取控制原則** (**存取控制清單**)表格中，按一下加號圖示以 **新增專案**.
1. 在 **新增專案** 對話方塊新增具有下列屬性的新ACE：

   * **主體**： `content-authors`
   * **类型**: `Deny`
   * **許可權**： `jcr:read`
   * **rep：glob**：參考特定工作流程

   ![wf-108](assets/wf-108.png)

   此 **存取控制清單** 表格現在包含 `content-authors` 於 `prototype-wfm-01` 工作流程模型。

   ![wf-109](assets/wf-109.png)

1. 按一下 **全部儲存**.

   此 `prototype-wfm-01` 工作流程不再適用於的會員 `content-authors` 群組。

### 在/var/workflow/models中建立子資料夾，並將ACL套用至該資料夾 {#create-a-subfolder-in-var-workflow-models-and-apply-the-acl-to-that}

您的 [開發團隊可以在子資料夾中建立工作流程](/help/sites-developing/workflows-models.md#creating-a-new-workflow) 之

`/var/workflow/models`

與以下儲存的DAM工作流程比較：

`/var/workflow/models/dam/`

然後，您可以將ACL新增至資料夾本身。

1. 在網頁瀏覽器中開啟CRXDE Lite(例如， [http://localhost:4502/crx/de](http://localhost:4502/crx/de))。
1. 在節點樹狀結構中，選取工作流程模型資料夾中個別資料夾的節點；例如：

   `/var/workflow/models/prototypes`

1. 按一下 **存取控制** 標籤。
1. 在 **適用的存取控制原則** 表格中，按一下加號圖示以 **新增** 一個專案。
1. 在 **本機存取控制原則** (**存取控制清單**)表格中，按一下加號圖示以 **新增專案**.
1. 在 **新增專案** 對話方塊新增具有下列屬性的新ACE：

   * **主體**： `content-authors`
   * **类型**: `Deny`
   * **許可權**： `jcr:read`

   >[!NOTE]
   >
   >與 [將特定工作流程模型的ACL套用至/var/workflow/models](/help/sites-administering/workflows-managing.md#apply-an-acl-for-the-specific-workflow-model-to-var-workflow-models) 您可以加入rep：glob來限制對特定工作流程的存取。

   ![wf-110](assets/wf-110.png)

   此 **存取控制清單** 表格現在包含 `content-authors` 於 `prototypes` 資料夾。

   ![wf-111](assets/wf-111.png)

1. 按一下 **全部儲存**.

   中的模型 `prototypes` 資料夾不再可供的成員使用。 `content-authors` 群組。
