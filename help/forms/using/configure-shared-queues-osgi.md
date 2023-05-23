---
title: 設定共用佇列
seo-title: Configure shared queues
description: 瞭解如何在OSGi上的AEM Forms上將共用佇列用於以Forms為中心的工作流程。
seo-description: Learn how to use shared queues for Forms-centric workflows on AEM Forms on OSGi.
topic-tags: process
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
exl-id: 72cd0594-8b5e-4d14-bc6f-bca26bae50f2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '841'
ht-degree: 1%

---

# 共用和要求存取使用者的收件匣專案 {#share-and-request-access}

佇列是使用者的AEM收件匣中的專案清單。 這些專案可以是指派給使用者的專案，或是共用給使用者所屬群組的專案。 您可以存取收件匣以檢視收件匣專案並對其採取行動。 例如，與其他使用者共用一個專案。

您也可以與其他使用者共用收件匣專案。 一旦其他使用者擁有您收件匣專案的存取權，使用者就可以宣告共用專案並對之採取適當行動。 同樣地，您可以向其他使用者要求收件匣專案的存取權。

## 先決條件 {#pre-requisites}

登入使用者必須是 `workflow-users` 群組。 使用者只能從登入使用者擁有讀取許可權的使用者或已啟用公開設定檔的使用者共用專案或要求專案存取權。

## 與其他使用者共用收件匣的單一或所有專案

AEM收件匣可讓您與其他使用者共用收件匣中的單一或所有專案。

### 共用所有收件匣專案

執行以下步驟，與其他使用者共用收件匣中的所有專案：

1. 登入您的AEM執行個體。 點選 ![收件匣](assets/bell.svg) 圖示並點選 **[!UICONTROL 檢視全部]**. 您的收件匣專案清單隨即顯示。
1. 點選 ![檢視選擇器](assets/viewlist.svg) 或 ![檢視選擇器](assets/calendar.svg) 圖示加以存取 **[!UICONTROL 建立]** 按鈕並點選 **[!UICONTROL 設定]**. 設定對話方塊隨即顯示。
1. 開啟 **[!UICONTROL 共用]** 標籤進行設定。
1. 在中輸入使用者名稱 **[!UICONTROL 授與收件匣專案的存取權]** 文字方塊並點選 **[!UICONTROL 授予]**. 重複此步驟以新增更多使用者。 所有可存取您專案的使用者都會顯示在 **使用者名稱** 區段。
1. 點選 **[!UICONTROL 儲存]**.

>[!NOTE]
>
>(僅適用於Forms中心工作流程專案)啟用 **[允許受分派者透過收件匣共用進行共用](aem-forms-workflow-step-reference.md)** 的選項 **指派任務** 工作流程中的步驟。 只有啟用上述選項的專案才會顯示給其他使用者。

### 共用個別專案

執行以下步驟，與其他使用者共用收件匣專案：

1. 登入您的AEM執行個體。 點選 ![收件匣](assets/bell.svg) 圖示並點選 **[!UICONTROL 檢視全部]**. 您的收件匣專案清單隨即顯示。
1. 選取專案並點選 **[!UICONTROL 共用]**. 将显示一个对话框。
1. 在「新增要共用此專案的使用者」文字方塊中輸入使用者名稱，然後點選 **[!UICONTROL 新增]**. 重複此步驟以新增更多使用者。 所有可存取您專案的使用者都會顯示在 **[!UICONTROL 使用者名稱]** 區段。
1. 點選 **[!UICONTROL 儲存]**.


>[!NOTE]
>
>(僅適用於Forms中心工作流程專案)啟用 **[允許受分派者在收件匣中明確共用](aem-forms-workflow-step-reference.md)** 的選項 **指派任務** 工作流程中的步驟。 只有啟用上述選項的專案才會顯示給其他使用者。

## 请求访问收件箱项目 {#request-access}

您可以要求存取其他使用者的收件匣專案。 授與存取權後，您可以檢視、宣告共用專案並採取適當的動作。 執行以下步驟，要求存取其他使用者的收件匣專案：

1. 登入您的AEM執行個體。 點選 ![檢視選擇器](assets/bell.svg) 圖示並點選 **[!UICONTROL 檢視全部]**.
1. 點選 ![檢視選擇器](assets/viewlist.svg) 或 ![檢視選擇器](assets/calendar.svg) 圖示加以存取 **[!UICONTROL 建立]** 按鈕並點選 **[!UICONTROL 設定]**. 設定對話方塊隨即顯示。
1. 在中輸入使用者名稱 **[!UICONTROL 要求存取使用者的收件匣專案]** 文字方塊並點選 **[!UICONTROL 請求]**. 系統會傳送請求給使用者，並根據使用者名稱來顯示請求狀態。 重複此步驟以新增更多使用者。
1. 點選 **[!UICONTROL 儲存]**. 此請求會以收件匣專案的形式傳送給使用者。 使用者可以選取專案並點選「核准」或「拒絕」以授與或拒絕存取權。


## 其他使用者共用的索賠專案 {#claim-items}

只有在宣告共用專案後，您才能開始處理該專案。 它可防止多位使用者處理單一專案。 執行下列步驟來宣告專案：

1. 登入您的AEM執行個體。 點選「收件匣」 ![收件匣](assets/bell.svg) 圖示並點選 **[!UICONTROL 檢視全部]**.
1. 點選 ![僅內容](assets/railleft.svg) 圖示以開啟篩選選擇器。
1. 點選 **[!UICONTROL 選取被指定者]** 下拉式清單，檢視並選取已與您共用其收件匣專案的使用者。
1. 選取專案並點選 **[!UICONTROL 索賠]**. 專案會新增至您的收件匣。

## 發行宣告的專案 {#release-items}

您必須在宣告共用專案後，才能處理該專案。 其他使用者看不到或無法處理您聲稱的專案。 如果您無法繼續處理某個專案，可以將其釋放回集區。   在您核發料號之後，其他人可以申請並處理料號：

執行下列步驟以核發料號：

1. 登入您的AEM執行個體。 點選「收件匣」 ![收件匣](assets/bell.svg) 圖示並點選 **[!UICONTROL 檢視全部]**. 您的收件匣專案清單隨即顯示。
1. 選取要釋出的專案並點選 **[!UICONTROL 取消宣告]**. 專案會新增回集區。 其他人現在可以申請該專案。

## 限制 {#limitations}

* 不支援與群組共用專案。
* 不支援共用專案任務。
