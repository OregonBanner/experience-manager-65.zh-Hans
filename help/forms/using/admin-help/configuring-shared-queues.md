---
title: 設定共用佇列
seo-title: Configuring Shared Queues
description: 共用佇列可讓您有效地設定和管理使用者佇列。 瞭解如何設定共用佇列。
seo-description: Shared Queues allow you to configure and manage user queues effectively. Learn how to configure shared queues.
uuid: 69ab611d-334b-40a5-bd2d-533d4cb25eda
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: fc403a60-b635-4334-9bf8-2f3d2036b2f3
exl-id: 5f4467c1-0f3f-4dc6-9bd5-98259f327295
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '652'
ht-degree: 0%

---

# 設定共用佇列{#configuring-shared-queues}

共用佇列可讓您有效地設定和管理使用者佇列。 使用者佇列只是指派給使用者的所有任務，請參閱 [待辦事項清單](https://help.adobe.com/en_US/livecycle/11.0/WorkspaceHelp/WS92d06802c76abadb-2b6ab502126beb6ba2f-7ffc.2.html) 以取得詳細資訊。 您可以根據您的組織需求，指派、取消指派和重新指派使用者佇列。 您可以透過兩種方式管理共用佇列：

**管理使用者的存取權**

您可以使用此選項管理對所選使用者佇列的存取權。

**按使用者管理存取許可權**

您可以使用此選項管理指派給所選使用者的共用佇列。

## 管理所選使用者佇列的存取權 {#managing-access-to-a-selected-user-queue}

管理使用者的存取權功能可讓您管理所選使用者佇列的存取權。 您可以將選取使用者佇列的存取權授與或撤銷給組織中的其他使用者。 例如，Kara Bowman不在辦公室。 使用「管理使用者的存取權」功能，可與Akira Tanaka和John Jacobs共用其佇列以完成。 稍後，當Kara Bowman返回辦公室時，您可以撤銷Akira Tanaka和John Jacobs對其佇列的存取權。

共用後，使用者即可使用工作區完成這些工作，並可存取佇列。

>[!NOTE]
>
>AEM Forms版本已棄用Flex Workspace。

### 設定選取使用者佇列的存取權 {#configuring-access-to-a-selected-user-queue}

1. 使用管理員帳戶登入管理主控台。
1. 選取 **服務** > **表單工作流程** > **共用佇列**.

1. 在管理使用者的存取權索引標籤上，尋找並選取您要共用其佇列的使用者。 在任何時候，右下方窗格都會顯示可存取所選使用者佇列的使用者清單。
1. 在左下方的窗格中，尋找並選取使用者。 按一下「共用」。
1. 按一下「儲存」以完成。

### 撤銷對所選使用者佇列的存取權 {#revoking-access-to-a-selected-user-queue}

1. 使用管理員帳戶登入管理主控台。
1. 選取 **服務** > **表單工作流程** > **共用佇列**.

1. 在管理使用者的存取權索引標籤上，尋找並選取您要管理其佇列的使用者。
1. 右下方窗格顯示可存取所選使用者佇列的使用者清單。 選取使用者，然後按一下撤銷。
1. 按一下「儲存」以完成。

## 管理指派給使用者的佇列 {#managing-queues-assigned-to-a-user}

「依使用者管理存取」功能可讓您管理指派給所選使用者的佇列。 您可以將使用者佇列的存取權個別授予或撤銷給選取的使用者。 例如，您希望將Akira Tanaka和John Jacobs使用者佇列指派給Kara Bowman。 使用「依使用者管理存取權」功能，您可以搜尋Kara Bowman並授予指派給Akira Tanaka和John Jacobs的工作存取權。 您稍後可以撤銷Kara Bowman對這些使用者佇列的存取權。

指派後，這些工作可以由使用者使用工作區完成。

>[!NOTE]
>
>AEM Forms版本已棄用Flex Workspace。

### 授與所選使用者佇列的存取權 {#granting-access-to-a-selected-user-queue}

1. 使用管理員帳戶登入管理主控台。
1. 選取 **服務** > **表單工作流程** > **共用佇列**.

1. 在管理使用者的存取權索引標籤上，尋找並選取您要共用其佇列的使用者。 在任何時候，右下方窗格都會顯示可存取所選使用者佇列的使用者清單。
1. 在左下方的窗格中，尋找並選取您要與所選使用者共用的使用者佇列。 按一下「共用」。
1. 按一下「儲存」以完成。

### 撤銷對所選使用者佇列的存取權 {#revoking_access_to_a_selected_user_queue-1}

1. 使用管理員帳戶登入管理主控台。
1. 選取 **服務** > **表單工作流程** > **共用佇列**.

1. 在依使用者管理存取權索引標籤中，尋找並選取您要管理其佇列的使用者。
1. 右下方窗格顯示指派給所選使用者的使用者佇列清單。 選取使用者佇列，然後按一下撤銷。
1. 按一下「儲存」以完成。
