---
title: AEM Forms工作區快速入門
seo-title: Getting started with AEM Forms workspace
description: 如何開始使用LiveCycleAEM Forms工作區來管理您的業務自動化流程。
seo-description: How to get started with using the LiveCycle AEM Forms workspace to manage your business automation processes.
uuid: 35ca1a51-92c3-40d8-8de3-604be8704752
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: fa6e0246-6bd2-4ffb-b54c-15eda605f213
exl-id: d2a962b6-16be-4866-a856-5064f81c9610
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '993'
ht-degree: 0%

---

# AEM Forms工作區快速入門 {#getting-started-with-aem-forms-workspace}

您可以使用AEM Forms工作區執行下列工作：

* 啟動業務流程
* 檢視指派給您或您有權存取之其他待辦事項清單的任務並對其執行動作
* 追蹤屬於您開始或參與之程式一部分的任務

## 瀏覽AEM Forms工作區 {#navigating-html-workspace}

AEM Forms工作區使用者介面中會顯示不同的專案，具體取決於您正在處理的程式與工作。 您不一定能看到「摘要」、「Forms」、「詳細資訊」、「歷史記錄」、「附件」或「附註」標籤，或本說明中說明的所有按鈕。

您可以使用下列任何一種方法，導覽至AEM Forms工作區主使用者介面：

* 按一下頂端導覽列中的專案，即可存取「開始程式」、「待辦事項清單」、「偏好設定」、「追蹤」、「說明」和「登出」選項。
* 按一下「開始程式」、「待辦事項」或「追蹤」標籤，以存取三個主要工作區域。
* 在「開始程式」、「待辦事項」和「追蹤」標籤上，按一下左側面板中清單上的專案以存取我的最愛、程式類別、搜尋範本、草稿或指派的任務。 使用卷軸檢視清單中的其他專案。
* 所有動作按鈕（「核准」、「拒絕」、「前進」、「諮詢」、「鎖定」和「共用」）都會顯示在檔案和「擁有權」中。
* 按一下頁面底部導覽列中的「所有選項」圖示，即可將工作轉送給其他使用者、與其他使用者共用工作、與其他使用者諮詢工作或鎖定工作。
* 在「歷史記錄」頁標上，選取要顯示該任務之「附件」與「工作總攬」頁標的工作。
* 使用Tab鍵、方向鍵和空白鍵導覽AEM Forms工作區，而不需使用滑鼠。

## 搭配熒幕助讀程式使用AEM Forms工作區 {#using-html-workspace-with-screen-readers}

AEM Forms workspace是網頁式HTML應用程式，與熒幕朗讀程式相容。 您可以使用鍵盤導覽AEM Forms工作區介面。

若要搭配熒幕助讀程式使用AEM Forms工作區，請記住以下幾點：

* AEM Forms工作區是標準的HTML應用程式，符合任何標準熒幕助讀程式工具。 您不需要任何特定指令碼即可執行熒幕助讀程式工具。
* AEM Forms工作區中的所有導覽都是透過錨點標籤進行，您可以透過索引標籤輕鬆存取。
* 載入Forms可能需要幾秒鐘的時間。 熒幕助讀程式不會以聲音通知您表單正在載入，您必須等待。

## 使用鍵盤導覽AEM Forms工作區 {#navigating-html-workspace-using-a-keyboard}

使用鍵盤導覽AEM Forms工作區時，導覽會遵循HTML協助工具慣例。 在某些情況下，Tab鍵瀏覽順序不會遵循典型的傳統順序。 下列提示可協助您導覽介面：

* 如果您在瀏覽器頂端的工具列上執行Tab鍵定位時發生問題，請按下Ctrl+Tab鍵以進入瀏覽器視窗的內容。
* AEM Forms工作區說明會在個別的瀏覽器視窗中開啟。 檢視「說明」後，焦點會回到包含AEM Forms工作區的瀏覽器視窗。 當焦點返回時，「說明」功能表仍會保持焦點。
* 當您開啟表單以開始流程或完成任務時，焦點會保留在現有元素中，而不會變更為表單。 使用Tab鍵將焦點移動到表單並在表單中瀏覽。 透過表單的Tab鍵瀏覽順序取決於表單的型別和設計。

   針對PDF forms，當您以Tab鍵瀏覽至表單結尾或提交表單時，游標焦點會跳至瀏覽器位址列。 您必須再次Tab鍵瀏覽功能表（但不是整個表單），才能移至表單動作按鈕，例如「另存為草稿」和「完成」。 如果表單仍處於開啟狀態，您也可以使用Tab鍵越過按鈕並返回表單。

## 管理偏好設定 {#managing-preferences}

您可以在下列類別中設定各種AEM Forms工作區偏好設定：

**外出：** 設定偏好設定以控制在您外出時如何將任務指派給其他人。 另請參閱 [設定休假偏好設定](todo-lists.md#setting-out-of-office-preferences).

**佇列：** 設定與其他使用者共用您的待辦事項清單或請求存取其他使用者清單的偏好設定。 另請參閱 [使用來自群組和共用佇列的任務](todo-lists.md#working-with-tasks-from-group-and-shared-queues).

**UI設定：** 設定與AEM Forms工作區互動方式的偏好設定。 另請參閱 [設定使用者介面偏好設定](#set-user-interface-preferences).

### 設定使用者介面偏好設定 {#set-user-interface-preferences}

在「偏好設定> UI設定」標籤中設定使用者介面偏好設定。 下列偏好設定可供使用。

* **開始位置：** 指定登入AEM Forms工作區時顯示的頁面。 四個可用選項為「開始程式」、「待辦事項」、「追蹤」和「我的最愛」。
* **登出提示：** 指定在您按一下「登出」後，是否提示您確認是否要登出。
* **日期格式：** 指定在AEM Forms工作區中使用的日期顯示格式。
* **時間格式**：指定在AEM Forms工作區中使用的時間顯示格式。
* **透過電子郵件通知任務事件：** 指定您是否收到任務事件的電子郵件通知，包括任務指派、提醒，以及您所屬的待辦事項清單和群組待辦事項清單中任務的截止日期。
* **在電子郵件中附加Forms：** 指定是否要將表單復本附加至電子郵件通知訊息。 只有PDF和XDP表單支援附件。
* **定期儲存草稿：** 指定是否定期自動儲存表單草稿。 若要定期儲存草稿，請啟用此選項，並將自動儲存持續時間從1分鐘設定為30分鐘。 當啟用自動儲存且使用者正在處理草稿時，草稿會在指定的分鐘數後定期儲存。 僅當自上次儲存或自動儲存後草稿中有變更時，才會自動儲存草稿。 儲存草稿時，畫面上會顯示警告訊息。
