---
title: 管理任務的收件匣
description: 使用收件匣管理您的工作。
uuid: ddd48019-ce69-4a47-be2b-5b66ae2fe3c8
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 8b607b55-2412-469f-856b-0a3dea4b0efb
exl-id: 80b7f179-b011-4f90-b5ab-9ef8a669d271
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '1143'
ht-degree: 26%

---

# 您的收件箱{#your-inbox}

您可以從AEM的各個區域接收通知，包括工作流程和專案；例如，關於：

* 任务：

   * 這些也可在AEM UI中的不同時間點建立，例如 **專案**，
   * 這些可以是工作流程的產物 **建立任務** 或 **建立專案任務** 步驟。

* 工作流：

   * 代表您需要對頁面內容執行之動作的工作專案；

      * 這些是工作流程的產物 **參與者** 步驟
   * 失敗專案，以允許管理員重試失敗的步驟。


您會在自己的收件匣中收到這些通知，您可以在其中檢視通知並採取行動。

>[!NOTE]
>
>現成可用的AEM會預先載入指派給管理員使用者群組的管理任務。 另請參閱 [現成可用的管理任務](#out-of-the-box-administrative-tasks) 以取得詳細資訊。

>[!NOTE]
>
>如需有關料號型態的進一步資訊，另請參閱：
>
>* [项目](/help/sites-authoring/touch-ui-managing-projects.md)
>* [專案 — 使用任務](/help/sites-authoring/task-content.md)
>* [工作流](/help/sites-authoring/workflows.md)
>* [Forms](/help/forms/home.md)
>


## 标题中的收件箱 {#inbox-in-the-header}

從任何控制檯中，收件匣中目前的專案數量會顯示在標題中。 指標也可以開啟，以提供對需要動作的頁面的快速存取權或收件匣的存取權：

![wf-80](assets/wf-80.png)

>[!NOTE]
>
>某些動作也會顯示於 [適當資源的卡片檢視](/help/sites-authoring/basic-handling.md#card-view).

## 現成可用的管理任務  {#out-of-the-box-administrative-tasks}

現成可用的AEM預先載入了指派給管理員使用者群組的四個任務。

* [配置分析和定位](/help/sites-administering/opt-in.md)
* [应用 AEM 安全核对清单](/help/sites-administering/security-checklist.md)
* 收集汇总的使用情况统计数据
* [配置 HTTPS](/help/sites-administering/ssl-by-default.md)

## 開啟收件匣 {#opening-the-inbox}

打开 AEM 通知收件箱：

1. 单击/点按工具栏中的指示器。

1. 选择&#x200B;**查看全部**。此时将打开 **AEM 收件箱**。收件箱会显示工作流、项目和任务中的项目。
1. 默认视图为“列 [表视图](#inbox-list-view)”，但您也可以切换到“日历 [视图”](#inbox-calendar-view)。 这是通过视图选择器（工具栏，右上方）完成的。

   對於這兩個檢視，您也可以定義 [檢視設定](#inbox-view-settings)；可用選項取決於目前檢視。

   ![wf-79](assets/inbox-list-view.png)

>[!NOTE]
>
>收件箱作为控制台运行，因此当您完成操作后，可使用[全局导航](/help/sites-authoring/basic-handling.md#global-navigation)或[搜索](/help/sites-authoring/search.md)导航到其他位置。

### 收件箱 – 列表视图 {#inbox-list-view}

此檢視會列出所有專案，以及主要的相關資訊：

![wf-82](assets/wf-82.png)

### 收件箱 – 日历视图 {#inbox-calendar-view}

此檢視會根據專案在行事曆中的位置以及您選取的精確檢視來顯示專案：

![wf-93](assets/wf-93.png)

您可以：

* 選取特定檢視； **時間表**， **欄**， **清單**

* 指定要根據以下條件顯示的任務 **排程**； **全部**， **已計畫**， **進行中**， **即將到期**， **過期**

* 向下追溯料號的詳細資訊
* 選取日期範圍以聚焦檢視：

![wf-91](assets/wf-91.png)

### 收件匣 — 設定 {#inbox-view-settings}

對於這兩個檢視（「清單」和「行事曆」），您可以定義設定：

* **日历视图**

   對象 **行事曆檢視** 您可以設定：

   * **分組依據**
   * **计划**&#x200B;或&#x200B;**无**
   * **卡片大小**

   ![wf-92](assets/wf-92.png)

* **列表视图**

   對象 **清單檢視** 您可以設定排序機制：

   * **排序字段**
   * **排序顺序**

   ![wf-83](assets/inbox-settings.png)

### 收件匣 — 管理員控制 {#inbox-admin-control}

「管理員控制」選項可讓管理員：

* 自訂AEM收件匣欄

* 自訂頁首文字和標誌

* 控制標題中可用導覽連結的顯示

「管理員控制」選項僅對成員可見。 `administrators` 或 `workflow-administrators` 群組。

* **欄自訂**：自訂AEM收件匣以變更欄的預設標題、重新排序欄的位置，以及根據工作流程的資料顯示其他欄。
   * **新增欄**：選取要新增至AEM收件匣的欄。
   * **編輯欄**：將滑鼠停留在欄標題上並點選 ![編輯](assets/edit.svg) 圖示輸入欄顯示名稱。
   * **刪除欄**：點選 ![刪除](assets/delete_updated.svg) 圖示以從AEM收件匣中刪除欄。
   * **移動欄**：拖曳 ![移動](assets/move_updated.svg) 圖示將欄移動到AEM收件匣中的新位置。

   ![admin-control](assets/admin-control-column-customize.png)

* **品牌化自定义**

   * **自訂頁首文字：** 指定要在標題中顯示的文字以取代預設值 **Adobe Experience Manager** 文字。

   * **自訂標誌：** 指定要在頁首中顯示的影像為標誌。 在數位資產管理(DAM)中上傳影像，並在欄位中參照該影像。

* **用户导航**
   * **隱藏導覽選項：** 選取此選項可隱藏標題中可用的導覽選項。 導覽選項包含其他解決方案的連結、說明連結，以及點選Adobe Experience Manager標誌或文字時可用的撰寫選項。
* **儲存：** 點選/按一下此選項以儲存設定。

## 对某个项目执行操作 {#taking-action-on-an-item}

>[!NOTE]
>
>尽管可以选择多个项目，但一次只能对一个项目执行操作。


1. 若要對專案執行動作，請選取適當專案的縮圖。 適用於該專案的動作圖示將顯示在工具列中：

   ![wf-84](assets/wf-84.png)

   这些操作适用于该项目，具体包括：

   * **完成**&#x200B;操作；例如，任務或工作流程專案。
   * **重新指派**/**委派** 專案。
   * **開啟** 料號；視料號型態而定，此動作可以：

      * 顯示專案屬性
      * 開啟適當的儀表板或精靈以進一步操作
      * 開啟相關檔案
   * **回退**&#x200B;到上一步.
   * 查看工作流的有效负荷.
   * 从该项目创建一个项目.

   >[!NOTE]
   >
   >有关更多信息，请参阅：
   >
   >* 工作流程專案 —  [參與工作流程](/help/sites-authoring/workflows-participating.md)


1. 視選取的專案而定，將會啟動動作；例如：

   * 將會開啟適合該動作的對話方塊。
   * 將啟動動作精靈。
   * 將會開啟檔案頁面。

   例如， **重新指派** 將會開啟一個對話方塊：

   ![wf-85](assets/wf-85.png)

   根据是否已打开对话框、向导和文档页面，您可以：

   * 確認適當的動作；例如重新指派。
   * 取消操作.
   * 上一頁箭頭；例如，如果已開啟動作精靈或檔案頁面，您可以返回「收件匣」。


## 创建任务 {#creating-a-task}

您可以從收件匣建立任務：

1. 選取 **建立**，則 **任務**.
1. 填妥中必要的欄位 **基本** 和 **進階** 標籤；僅限 **標題** 為必要專案，其他專案則為選用專案：

   * **基本**:

      * **标题**
      * **项目**
      * **被分派人**
      * **內容**；與「裝載」類似，這是從任務到存放庫中位置的參考
      * **描述**
      * **任务优先级**
      * **开始日期**
      * **到期日期**

   ![wf-86](assets/wf-86.png)

   * **高级**

      * **名称**：這會用來組成URL；如果留空，則會根據 **標題**.

   ![wf-87](assets/wf-87.png)

1. 選取 **提交**.

## 创建项目 {#creating-a-project}

您可以針對特定工作建立 [專案](/help/sites-authoring/projects.md) 根據該任務：

1. 點選/按一下縮圖，選取適當的工作。

   >[!NOTE]
   >
   >只有使用&#x200B;**收件箱**&#x200B;的&#x200B;**创建**&#x200B;选项创建的任务才能用于创建项目。
   >
   >工作專案（來自工作流程）無法用於建立專案。

1. 从工具栏中选择“**创建项目**”以打开向导。
1. 選取適當的範本，然後 **下一個**.
1. 指定必要的屬性：

   * **基本**

      * **标题**
      * **描述**
      * **开始日期**
      * **到期日期**
      * **使用者** 和角色
   * **高级**

      * **名称**
   >[!NOTE]
   >
   >另請參閱 [建立專案](/help/sites-authoring/touch-ui-managing-projects.md#creating-a-project) 以取得完整資訊。

1. 選取 **建立** 以確認動作。

## 筛选 AEM 收件箱中的项目 {#filtering-items-in-the-aem-inbox}

您可以筛选列出的项目：

1. 打开 **AEM 收件箱**。

1. 打开过滤器选择器：

   ![wf-88](assets/wf-88.png)

1. 您可以根據一系列條件篩選列出的專案，其中許多條件可以細化；例如：

   ![wf-89](assets/wf-89.png)

   >[!NOTE]
   >
   >通过[视图设置](#inbox-view-settings)，您还可以在使用[列表视图](#inbox-list-view)时配置排序顺序。
