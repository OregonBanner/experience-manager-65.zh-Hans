---
title: 建立啟動
description: 您可以建立啟動，以更新現有網頁的新版本，以供日後啟用。
uuid: c1a32710-8189-4a2e-bf2f-428ab30d48c8
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 4ec6b408-a165-4617-8d90-e89d8a415bb3
legacypath: /content/docs/en/aem/6-0/author/site-page-features/launches
exl-id: bc7897da-15f6-4de4-a9fd-9dd84e6c7eed
source-git-commit: 7f595bec8ea138d5a73a17d0548320a31544dcd1
workflow-type: tm+mt
source-wordcount: '1018'
ht-degree: 49%

---

# 建立啟動{#creating-launches}

建立啟動項，以更新現有網頁的新版本，以供日後啟用。 在创建启动项时，需要指定标题和源页面：

* 标题会显示在[“引用”](/help/sites-authoring/author-environment-tools.md#references)边栏中，作者可以从中访问启动项，从而对其进行处理。
* 來源頁面的子頁面預設會包含在啟動中。 您可以視需要只使用來源頁面。
* 依預設， [即時副本](/help/sites-administering/msm.md) 當來源頁面變更時，會自動更新啟動頁面。 您可以指定建立靜態副本以防止自動變更。

（可选）您可以指定启 **动日期** （和时间）以定义何时提升和激活启动页面。 但是，启 **动日期仅与生产就绪标** 志结合使用(请 **参阅编辑启动配置**[](/help/sites-authoring/launches-editing.md#editing-a-launch-configuration));要使动作实际自动发生，必须同时设置这两个操作。

## 建立啟動 {#creating-a-launch}

您可以從「網站」或「啟動」主控台建立啟動：

1. 打开&#x200B;**“站点”**&#x200B;或&#x200B;**“启动项”**&#x200B;控制台。

   >[!NOTE]
   >
   >使用時 **網站** console通常是導覽至來源頁面的位置，但這並非必要操作，因為您可以選取 **啟動來源** 在精靈中。

1. 根據您使用的主控台：

   * **启动项**：

      1. 選取 **建立啟動項** 以開啟精靈。
   * **站点**：

      1. 从工具栏中选择&#x200B;**“创建”**&#x200B;以打开选择框。
      1. 從此選取 **建立啟動項** 以開啟精靈。

   >[!NOTE]
   >
   >在&#x200B;**“站点”**&#x200B;控制台中，您还可以使用[选择模式](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)，在选择&#x200B;**“创建”**&#x200B;之前选择页面。
   >
   >这将使用选定的页面作为初始源页面。

1. 在&#x200B;**“选择源”**&#x200B;步骤中，您需要&#x200B;**“添加页面”**。您可以通过指定每个页面的路径来选择多个页面：

   * 导航到所需的位置。
   * 選取來源頁面並確認（核取記號）。

   根据需要重复执行上述步骤。

   ![chlimage_1-225](assets/chlimage_1-225.png)

   >[!NOTE]
   >
   >若要將頁面和/或分支新增至啟動項，這些頁面和/或分支必須位於網站內，即位於通用頂層根目錄下。
   >
   >如果網站在頂層之下包含語言根，則啟動項的頁面和分支必須在共同語言根之下。
   >
   >如果您嘗試在來源路徑中使用父頁面或子頁面來建立啟動，則會失敗並傳回錯誤「目標已存在於：path中的頁面。」

1. 對於每個專案，您可以指定是否：

   * **包括子页面**:

      * 指定您希望创建的启动项包括还是不包括子页面。  默认情况下，将包括这些子页面。

   继续&#x200B;**“下一步”**。

   ![chlimage_1-226](assets/chlimage_1-226.png)

1. 在向导的&#x200B;**“属性”**&#x200B;步骤中，您可以指定：

   * **啟動項標題**：啟動項的名稱。 此名稱對作者應有意義。
   * **包含现有内容**：将使用原始内容创建启动项。
   * **使用新模板替换页面**：有关更多详细信息，请参阅[使用新模板创建启动项](#create-launch-with-new-template)。
   * **继承源页面活动数据**：选中此选项，可在源页面发生更改时自动更新启动页面的内容。此選項可讓啟動成為 [即時副本](/help/sites-administering/msm.md).

      依預設，會選取此選項。

   * **启动日期**：激活启动副本的日期和时间（取决于&#x200B;**生产就绪**&#x200B;标记；请参阅[启动项 – 事件的顺序](/help/sites-authoring/launches.md#launches-the-order-of-events)）。

   ![chlimage_1-227](assets/chlimage_1-227.png)

1. 使用&#x200B;**“创建”**&#x200B;完成该过程并创建新启动项。確認對話方塊會詢問您是否要立即開啟啟動項。

   如果您傳回主控台(包含 **完成**)您可以透過以下任一方式檢視（和存取）您的啟動項：

   * 此 [**啟動** 主控台](/help/sites-authoring/launches.md#the-launches-console)
   * 此 [**引用** 在 **網站** 主控台](/help/sites-authoring/launches.md#launches-in-references-sites-console)

### 使用新模板创建启动项 {#create-launch-with-new-template}

時間 [建立啟動](/help/sites-authoring/launches-creating.md#create-launch-with-new-template) 您可以選取是否使用新範本：

**使用新模板替换页面**

>[!CAUTION]
>
>此选项仅在从&#x200B;**站点**&#x200B;控制台中创建启动项时可用。在从&#x200B;**启动项**&#x200B;控制台中创建启动项时，此选项不可用。

![chlimage_1-228](assets/chlimage_1-228.png)

如果选中此选项，则将会：

* 更新其他可用選項，
* 包括一個新步驟，您可在其中選取所需的範本。

![chlimage_1-229](assets/chlimage_1-229.png)

>[!CAUTION]
>
>當使用不同的範本時，新頁面將是空的。 由於頁面結構不同，將不會複製任何內容。
>
>此機制可用於變更 [現有頁面](/help/sites-authoring/managing-pages.md#creating-a-new-page)  — 雖然必須考量內容遺失。

### 建立巢狀啟動 {#creating-a-nested-launch}

建立巢狀啟動（在啟動中啟動）可讓您從現有啟動建立啟動，讓作者能夠利用已進行的變更，而不必針對每個啟動多次進行相同的變更。

>[!NOTE]
>
>另请参阅[提升嵌套启动项](/help/sites-authoring/launches-promoting.md#promoting-a-nested-launch)。

#### 创建嵌套启动项 – 启动项控制台 {#creating-a-nested-launch-launches-console}

从&#x200B;**启动项**&#x200B;控制台中创建嵌套启动项的步骤与创建任何其他形式的启动项的步骤基本相同，只是需要导航到启动项分支 `/content/launches`：

1. 在&#x200B;**启动项**&#x200B;控制台中，选择&#x200B;**“创建”**。
1. 选择 **添加页面**，然后通过在筛选器中指定来导航到启动 `/content/launches` 项分支。 选择所需的启动项，并通过&#x200B;**“选择”**&#x200B;进行确认：

   ![chlimage_1-230](assets/chlimage_1-230.png)

1. 繼續進行 **下一個** 並完成 **屬性** 和任何其他啟動項一樣。

   ![chlimage_1-231](assets/chlimage_1-231.png)

#### 创建嵌套启动项 – 站点控制台 {#creating-a-nested-launch-sites-console}

要从&#x200B;**站点**&#x200B;控制台中基于现有的启动项创建嵌套启动项，请执行以下操作：

1. [从“引用”（站点控制台）中访问启动项](/help/sites-authoring/launches.md#launches-in-references-sites-console)以显示可用的操作。
1. 选择&#x200B;**“创建启动项”**&#x200B;打开向导（由于已选择源，因此它将跳过&#x200B;**“选择源”**&#x200B;步骤）。

1. 输入&#x200B;**“启动项标题”**&#x200B;和任何其他所需的详细信息（与常规启动项一样）。

1. 使用&#x200B;**“创建”**&#x200B;完成该过程并创建新启动项。確認對話方塊會詢問您是否要立即開啟啟動項。

   如果选择&#x200B;**“完成”**，您将返回到&#x200B;**站点**&#x200B;控制台的&#x200B;**引用**&#x200B;边栏，如果您选择了相应的页面，则会显示新的启动项。

### 刪除啟動項 {#deleting-a-launch}

您可以從以下位置刪除啟動： [啟動主控台](/help/sites-authoring/launches.md#the-launches-console)：

* 點選/按一下縮圖，以選取啟動。
* 工具列隨即顯示 — 選取「刪除」。
* 確認動作。

>[!CAUTION]
>
>删除启动项时，将会删除该启动项本身及其所有下级嵌套启动项。
