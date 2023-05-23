---
title: 创建并同步 Live Copy
description: 瞭解如何建立和同步即時副本。
feature: Multi Site Manager
exl-id: 896b35dd-4510-4c94-8615-03d9649c2f64
source-git-commit: 05dc73448d6902ccdbc92782fff39ef1a6339056
workflow-type: tm+mt
source-wordcount: '4171'
ht-degree: 46%

---

# 创建并同步 Live Copy{#creating-and-synchronizing-live-copies}

您可以從頁面或Blueprint設定建立即時副本，然後可以管理繼承和同步。

## 管理 Blueprint 配置 {#managing-blueprint-configurations}

Blueprint設定會識別您想要用作一或多個即時副本頁面來源的現有網站。

>[!NOTE]
>
>Blueprint設定可讓您將內容變更推送至即時副本。 请参阅 [Live Copy – 源、Blueprint 和 Blueprint 配置](/help/sites-administering/msm.md#source-blueprints-and-blueprint-configurations)。

创建 Blueprint 配置时，可以选择定义 Blueprint 的内部结构的模板。默认 Blueprint 模板假定源网站具有以下特征：

* 网站具有根页面。
* 根的直接子页面是网站的语言分支。建立即時副本時，語言會顯示為可選內容，以便包含在副本中。
* 每个语言分支的根均有一个或多个子页面。建立即時副本時，子頁面會顯示為可包含在即時副本中的章節。

>[!NOTE]
>
>不同的結構需要另一個Blueprint範本。

创建 Blueprint 配置后，可以配置以下属性：

* **名称**：Blueprint 配置的名称。
* **源路径**：您用作源的站点根页面的路径 (Blueprint).
* **描述**。（選用）Blueprint設定的說明。 說明會顯示在建立網站時可選用的Blueprint設定清單中。

使用您的Blueprint設定時，您可以將其與轉出設定相關聯，以決定來源/Blueprint的即時副本同步的方式。 请参阅[指定要使用的转出配置](/help/sites-administering/msm-sync.md#specifying-the-rollout-configurations-to-use)。

### 建立Blueprint設定 {#creating-a-blueprint-configuration}

要创建 Blueprint 配置，请执行以下操作：

1. [导航](/help/sites-authoring/basic-handling.md#global-navigation)到&#x200B;**工具**&#x200B;菜单，然后选择&#x200B;**站点**&#x200B;菜单。
1. 选择 **Blueprint** 以打开 **Blueprint 配置**&#x200B;控制台：

   ![chlimage_1-209](assets/blueprint-configurations.png)

1. 选择&#x200B;**创建**。
1. 选择 Blueprint 模板，然后选择&#x200B;**下一步**&#x200B;以继续。
1. 选择要用作 Blueprint 的源页面；然后选择&#x200B;**下一步**&#x200B;以继续。
1. 定义：

   * **标题**：Blueprint 的强制性标题
   * **描述**：用于提供更多详细信息的可选描述。

1. **创建**&#x200B;将根据您的规范创建 Blueprint 配置。

### 編輯或刪除Blueprint設定 {#editing-or-deleting-a-blueprint-configuration}

您可以编辑或删除现有 Blueprint 配置：

1. [导航](/help/sites-authoring/basic-handling.md#global-navigation)到&#x200B;**工具**&#x200B;菜单，然后选择&#x200B;**站点**&#x200B;菜单。
1. 选择 **Blueprint** 以打开 **Blueprint 配置**&#x200B;控制台：

   ![chlimage_1-210](assets/blueprint-configurations.png)

1. 选择所需的 Blueprint 配置 – 可在工具栏中使用相应的操作：

   * **属性**；可以使用此项查看并编辑配置的属性。
   * **删除**

## 创建 Live Copy {#creating-a-live-copy}

### 创建页面的 Live Copy {#creating-a-live-copy-of-a-page}

您可以建立任何頁面或分支的即時副本。 建立即時副本時，您可以指定用於同步內容的轉出設定：

* 所選的轉出設定會套用至即時副本頁面及其子頁面。
* 如果您未指定任何转出配置，MSM 将确定要使用的转出配置。请参阅[指定要使用的转出配置](/help/sites-administering/msm-sync.md#specifying-the-rollout-configurations-to-use)。

您可以建立任何頁面的即時副本：

* 由參照的頁面 [Blueprint設定](#creating-a-blueprint-configuration).
* 以及与配置无关联的页面.
* AEM也支援在另一個即時副本的頁面中建立即時副本。

唯一的区别是，**转出**&#x200B;命令在源/Blueprint 页面上的可用性取决于 Blueprint 配置是否引用了源：

* 如果您從來源頁面建立即時副本， **是** 在Blueprint設定中參照，則轉出命令將可在來源/Blueprint頁面上使用。
* 如果您從來源頁面建立即時副本， **不是** 在Blueprint設定中參照，則轉出命令將無法在來源/Blueprint頁面上使用。

若要建立即時副本：

1. 在&#x200B;**站点**&#x200B;控制台中，依次选择&#x200B;**创建**&#x200B;和 **Live Copy**。

   ![chlimage_1-212](assets/chlimage_1-212.png)

1. 选择源页面，然后单击或点按&#x200B;**下一步**。例如：

   ![chlimage_1-213](assets/chlimage_1-213.png)

1. 指定即時副本的目的地路徑（開啟即時副本的父資料夾/頁面），然後按一下或點選 **下一個**.

   ![chlimage_1-214](assets/chlimage_1-214.png)

   >[!NOTE]
   >
   >目标路径不能在源路径内。

1. 输入：

   * 页面的&#x200B;**标题**。
   * URL 中使用的&#x200B;**名称**。

   ![chlimage_1-215](assets/chlimage_1-215.png)

1. 使用&#x200B;**排除子页面**&#x200B;复选框：

   * 選取：僅建立所選頁面的即時副本（淺層即時副本）
   * 未選取：建立包含所選頁面所有子系的即時副本（深層即時副本）

1. （可選）若要指定一個或多個轉出設定以用於LiveCopy，請使用 **轉出設定** 下拉式清單加以選取；選取的設定將顯示在下拉式選取器下方。
1. 单击或点按&#x200B;**创建**。这将显示一条确认消息，可在其中选择&#x200B;**打开**&#x200B;或&#x200B;**完成**。

### 从 Blueprint 配置创建站点的 Live Copy {#creating-a-live-copy-of-a-site-from-a-blueprint-configuration}

使用Blueprint設定建立即時副本，以根據Blueprint （來源）內容建立網站。 從Blueprint設定建立即時副本時，選取要複製的Blueprint來源的一或多個語言分支，然後從語言分支選取要複製的章節。 请参阅[创建 Blueprint 配置](/help/sites-administering/msm-livecopy.md#creating-a-blueprint-configuration)。

如果您從即時副本中省略了一些語言分支或章節，可以稍後新增；請參閱 [在即時副本中建立即時副本（Blueprint設定）](#creating-a-live-copy-inside-a-live-copy-blueprint-configuration).

>[!CAUTION]
>
>當Blueprint來源包含以不同分支中的段落為目標的連結和參考時，即時副本頁面中的目標不會更新，而是保持指向原始目的地。

创建站点时，请提供以下属性的值：

* **初始語言**：要包含在即時副本中的Blueprint來源的語言分支。
* **初始章節**：要包含在即時副本中的Blueprint語言分支的子頁面。
* **目的地路徑**：即時副本網站的根頁面位置。
* **標題**：即時副本網站的根頁面標題。
* **名稱**：（選用）儲存即時副本根頁面的JCR節點名稱。預設值是根據標題。
* **網站擁有者**：（選擇性）
* **Live Copy**：选择此选项可与源站点建立实时关系。如果不选择此选项，则尽管会创建 Blueprint 的副本，但该副本随后不会与源同步。
* **轉出設定**：（選用）選取一或多個轉出設定以用於同步即時副本。 依預設，轉出設定繼承自Blueprint；請參閱 [指定要使用的轉出設定](/help/sites-administering/msm-sync.md#specifying-the-rollout-configurations-to-use) 以取得更多詳細資料。

若要從Blueprint設定建立網站的即時副本：

1. 在&#x200B;**站点**&#x200B;控制台中，选择&#x200B;**创建**，然后从下拉选择器中选择&#x200B;**站点**。
1. 選取要用作即時副本來源的Blueprint設定，並繼續 **下一個**：

   ![chlimage_1-216](assets/blueprint-configuration-select.png)

1. 使用 **初始語言** 選擇器，以指定要用於即時副本的Blueprint網站的語言。

   默认选择所有可用语言。要删除某种语言，请单击或点按该语言旁边显示的 **X**。

   例如：

   ![chlimage_1-217](assets/chlimage_1-217.png)

1. 使用 **初始章節** 下拉式清單，以選取要納入即時副本中的Blueprint區段。 同樣地，所有可用的章節預設都會包含在內，但可移除。
1. 提供剩余属性的值，然后选择&#x200B;**创建**。在确认对话框中，选择&#x200B;**完成**&#x200B;以返回&#x200B;**站点**&#x200B;控制台，或选择&#x200B;**打开站点**&#x200B;以打开站点的根页面。

### 在 Live Copy（Blueprint 配置）中创建 Live Copy {#creating-a-live-copy-inside-a-live-copy-blueprint-configuration}

當您在現有即時副本（使用Blueprint設定建立）中建立即時副本時，可以插入最初建立即時副本時未包含的任何語言副本或章節。

## 监控您的 Live Copy {#monitoring-your-live-copy}

### 查看 Live Copy 的状态 {#seeing-the-status-of-a-live-copy}

即時副本頁面的屬性會顯示下列有關即時副本的資訊：

* **來源**：即時副本頁面的來源頁面。
* **狀態**：即時副本的同步狀態。 狀態包括即時副本是否與來源保持同步、上次同步的時間以及同步的執行者。
* **配置**：

   * 頁面是否仍受即時副本繼承的約束。
   * 配置是否继承自父页面.
   * 即時副本使用的任何轉出設定。

要查看属性，请执行以下操作：

1. 在 **網站** 控制檯中，選取即時副本頁面並開啟屬性。
1. 选择 **Live Copy** 选项卡。

   例如：

   ![chlimage_1-218](assets/chlimage_1-218.png)

   >[!NOTE]
   >
   >如需詳細資訊，另請參閱知識庫文章 [即時副本狀態訊息 — 最新/綠色/同步中](https://helpx.adobe.com/experience-manager/kb/livecopy-status-message---up-to-date-green-in-sync.html).

### 查看 Blueprint 页面的 Live Copy {#seeing-the-live-copies-of-a-blueprint-page}

Blueprint頁面（在Blueprint設定中參照）會為您提供使用目前(Blueprint)頁面作為來源的即時副本頁面清單。 使用此清單來追蹤即時副本。 此列表显示在[页面属性](/help/sites-authoring/editing-page-properties.md)的 **Blueprint** 选项卡上。

![chlimage_1-219](assets/chlimage_1-219.png)

## 同步您的 Live Copy {#synchronizing-your-live-copy}

### 转出 Blueprint {#rolling-out-a-blueprint}

轉出Blueprint頁面以將內容變更推送至即時副本。 **转出**&#x200B;操作执行使用[转出](/help/sites-administering/msm-sync.md#rollout-triggers)触发器的转出配置。

>[!NOTE]
>
>如果在Blueprint分支和相依的即時副本分支中同時建立具有相同頁面名稱的新頁面，則可能會發生衝突。
>
>[转出时需要处理和解决此类冲突](/help/sites-administering/msm-rollout-conflicts.md)。

#### 从页面属性转出 Blueprint {#rolling-out-a-blueprint-from-page-properties}

1. 在&#x200B;**站点**&#x200B;控制台中，选择 Blueprint 中的页面并打开属性。
1. 打开 **Blueprint** 选项卡。
1. 选择&#x200B;**转出**。

   ![chlimage_1-220](assets/chlimage_1-220.png)

1. 指定页面和任何子页面，然后通过复选标记进行确认：

   ![chlimage_1-221](assets/chlimage_1-221.png)

1. 指定转出作业是应立即执行（**现在**）还是在其他日期/时间执行（**稍后**）。

   ![轉出Blueprint](assets/rollout-blueprint.png)

轉出會以非同步工作方式處理，並可在 [**非同步工作狀態** 儀表板](asynchronous-jobs.md#monitor-the-status-of-asynchronous-operations) 於 **全域導覽** -> **工具** -> **作業** -> **工作**

>[!NOTE]
>
>非同步轉出處理需要AEM 6.5.3.0或更新版本。 在舊版中，會立即同步處理頁面。

#### 从引用边栏转出 Blueprint {#roll-out-a-blueprint-from-the-reference-rail}

1. 在&#x200B;**站点**&#x200B;控制台中，从 Live Copy 中选择此页面，然后从工具栏中打开&#x200B;**[引用](/help/sites-authoring/basic-handling.md#references)**&#x200B;面板。
1. 从列表中选择 **Blueprint** 选项以查看与此页面关联的 Blueprint。
1. 从列表中选择所需的 Blueprint。
1. 单击或点按&#x200B;**转出**。
1. 系统会要求您确认转出的详细信息：

   * **转出范围**：

      指定范围是仅针对所选页面，还是应包括子页面。

   * **计划**：

      指定转出作业是应立即执行（**现在**）还是在某个将来日期/时间执行（**稍后**）。

      ![chlimage_1-222](assets/rollout-live-copy.png)

1. 确认这些详细信息后，选择&#x200B;**转出**&#x200B;以执行此操作。

轉出會以非同步工作方式處理，並可在 [**非同步工作狀態** 儀表板](asynchronous-jobs.md#monitor-the-status-of-asynchronous-operations) 於 **全域導覽** -> **工具** -> **作業** -> **工作**

>[!NOTE]
>
>非同步轉出處理需要AEM 6.5.3.0或更新版本。 在舊版中，會立即同步處理頁面，除非 **背景轉出** 選項已核取。

#### 从 Live Copy 概述转出 Blueprint {#roll-out-a-blueprint-from-the-live-copy-overview}

在选择 Blueprint 页面时，[也可以从 Live Copy 概述执行](/help/sites-administering/msm-livecopy-overview.md#using-the-live-copy-overview)转出操作。

1. 打开 [Live Copy 概述](/help/sites-administering/msm-livecopy-overview.md#using-the-live-copy-overview)并选择 Blueprint 页面。
1. 从工具栏中选择&#x200B;**转出**。
1. 指定页面和任何子页面，然后通过复选标记进行确认：

   ![chlimage_1-223](assets/chlimage_1-223.png)

1. 指定转出作业是应立即执行（**现在**）还是在其他日期/时间执行（**稍后**）。

   ![轉出Blueprint](assets/rollout-blueprint.png)

轉出會以非同步工作方式處理，並可在 [**非同步工作狀態** 儀表板](asynchronous-jobs.md#monitor-the-status-of-asynchronous-operations) 於 **全域導覽** -> **工具** -> **作業** -> **工作**

>[!NOTE]
>
>非同步轉出處理需要AEM 6.5.3.0或更新版本。 在舊版中，會立即同步處理頁面。

### 同步 Live Copy {#synchronizing-a-live-copy}

同步即時副本頁面，以將內容變更從來源提取到即時副本。

#### 从页面属性同步 Live Copy {#synchronize-a-live-copy-from-page-properties}

同步即時副本，以將變更從來源提取到即時副本。

>[!NOTE]
>
>同步执行使用[转出](/help/sites-administering/msm-sync.md#rollout-triggers)触发器的转出配置。

1. 在 **網站** 控制檯中，選取即時副本頁面並開啟屬性。
1. 打开 **Live Copy** 选项卡。
1. 单击或点按&#x200B;**同步**。

   ![chlimage_1-224](assets/chlimage_1-224.png)

   将请求确认，并使用&#x200B;**同步**&#x200B;以继续。

#### 从 Live Copy 概述同步 Live Copy {#synchronize-a-live-copy-from-the-live-copy-overview}

在选择 Live Copy 页面时，[也可以从 Live Copy 概述执行同步操作](/help/sites-administering/msm-livecopy-overview.md#using-the-live-copy-overview)。

1. 打开 [Live Copy 概述](/help/sites-administering/msm-livecopy-overview.md#using-the-live-copy-overview)并选择 Live Copy 页面。
1. 从工具栏中选择&#x200B;**同步**。
1. 在指定是否要包含以下项后，在对话框中确认&#x200B;**转出**&#x200B;操作：

   * **页面和子页面**
   * **仅页面**

   ![chlimage_1-225](assets/chlimage_1-225.png)

## 更改 Live Copy 内容 {#changing-live-copy-content}

若要變更即時副本內容，您可以：

* 将段落添加到页面。
* 透過中斷任何頁面或元件的即時副本繼承來更新現有內容。

>[!NOTE]
>
>如果您在即時副本中手動建立新頁面，則它是即時副本的本機頁面，這表示它沒有要附加到的對應來源頁面。
>
>建立屬於關係一部分的本機頁面的最佳作法是在來源中建立它，並進行（深）轉出。 這會將頁面在本機建立為即時副本。

>[!NOTE]
>
>如果在Blueprint分支和相依的即時副本分支中同時建立具有相同頁面名稱的新頁面，則可能會發生衝突。
>
>[转出时需要处理和解决此类冲突](/help/sites-administering/msm-rollout-conflicts.md)。

### 向 Live Copy 页面添加组件 {#adding-components-to-a-live-copy-page}

隨時新增元件至即時副本頁面。 即時副本及其段落系統的繼承狀態不會控制您新增元件的能力。

當即時副本頁面與來源頁面同步時，新增的元件保持不變。 另請參閱 [變更即時副本頁面上的元件順序](#changing-the-order-of-components-on-a-live-copy-page).

>[!NOTE]
>
>在本地对标记为容器的组件所做的更改不会由转出时的 Blueprint 内容覆盖。请参阅 [MSM 最佳实践](/help/sites-administering/msm-best-practices.md#components-and-container-synchronization)以了解更多信息。

### 暂停页面的继承 {#suspending-inheritance-for-a-page}

當您建立即時副本時，即時副本設定會儲存在已複製頁面的根頁面上。 根頁面的所有子頁面都會繼承即時副本設定。 live copy頁面上的元件也會繼承即時副本設定。

您可以暫停即時副本頁面的即時副本繼承，以便變更頁面屬性和元件。 当您暂停继承时，页面属性和组件不再与源同步。

>[!NOTE]
>
>您也可以 [分離即時副本](#detaching-a-live-copy) 從其Blueprint移除所有連線。 分离操作是永久性且不可逆的。

>[!NOTE]
>
>如果元件標示為容器，則取消和暫停動作不會套用至其子元件。 另請參閱 [MSM最佳作法](/help/sites-administering/msm-best-practices.md#components-and-container-synchronization) 以取得其他資訊。

#### 暂停来自页面属性的继承 {#suspending-inheritance-from-page-properties}

要暂停页面上的继承，请执行以下操作：

1. 使用「 」開啟Live Copy頁面的屬性 **檢視屬性** 命令 **網站** 主控台或使用 **頁面資訊** （在頁面工具列上）。
1. 单击或点按 **Live Copy** 选项卡。
1. 从工具栏中选择&#x200B;**暂停**。之后，您可以选择：

   * **暫停**：僅目前頁面
   * **與子項一起暫停**：目前頁面連同任何子頁面

1. 在确认对话框上选择&#x200B;**暂停**。

#### 暂停来自 Live Copy 概述的继承 {#suspending-inheritance-from-the-live-copy-overview}

在选择 Live Copy 页面时，[也可以从 Live Copy 概述执行暂停操作](/help/sites-administering/msm-livecopy-overview.md#using-the-live-copy-overview)。

1. 打开 [Live Copy 概述](/help/sites-administering/msm-livecopy-overview.md#using-the-live-copy-overview)并选择 Live Copy 页面。
1. 从工具栏中选择&#x200B;**暂停**。
1. 从以下项中选择适当的选项：

   * **暂停**
   * **与子项一起暂停**

   ![chlimage_1-226](assets/chlimage_1-226.png)

1. 在&#x200B;**暂停 Live Copy** 对话框中确认&#x200B;**暂停**&#x200B;操作：

   ![chlimage_1-227](assets/chlimage_1-227.png)

### 恢复页面的继承 {#resuming-inheritance-for-a-page}

暫停頁面的即時副本繼承是暫時動作。 在暂停后，**恢复**&#x200B;操作将可用，可让您恢复实时关系。

当您重新启用继承时，页面不会自动与源同步。如果需要，您可以通过以下方式请求同步：

* 在&#x200B;**恢复**/**还原**&#x200B;对话框中；例如：

   ![chlimage_1-228](assets/chlimage_1-228.png)

* 在稍后阶段，通过手动选择同步操作。

>[!CAUTION]
>
>当您重新启用继承时，页面不会自动与源同步。如果需要，您可以在恢復時或稍後手動要求同步。

#### 恢复来自页面属性的继承 {#resuming-inheritance-from-page-properties}

在[暂停](#suspending-inheritance-from-page-properties)后，**恢复**&#x200B;操作将在页面属性的工具栏中变得可用：

![chlimage_1-229](assets/chlimage_1-229.png)

选中后，该对话框将出现。如果需要，您可以选择同步，然后确认操作。

#### 从 Live Copy 概述恢复 Live Copy 页面 {#resume-a-live-copy-page-from-the-live-copy-overview}

在选择 Live Copy 页面时，[也可以从 Live Copy 概述执行恢复操作](/help/sites-administering/msm-livecopy-overview.md#using-the-live-copy-overview)。

1. 開啟 [即時副本概觀](/help/sites-administering/msm-livecopy-overview.md#using-the-live-copy-overview) 並選取已暫停的即時副本頁面；將顯示為 **已取消繼承**.
1. 从工具栏中选择&#x200B;**恢复**。
1. 指示是否要在恢复继承后同步页面，然后在&#x200B;**恢复 Live Copy** 对话框中确认&#x200B;**恢复**&#x200B;操作。

### 更改继承深度（浅/深） {#changing-inheritance-depth-shallow-deep}

您可以在現有的即時副本上變更頁面的深度，也就是是否包含子頁面。

* 切換到淺層即時副本：

   * 将立即生效且不可逆。

      * 子頁面會明確從即時副本中分離。 如果撤消，则无法保留对子项所做的进一步修改。

      * 将删除任何下级 `LiveRelationships`，即使存在嵌套式 `LiveCopies` 也是如此。

* 切換到深層即時副本：

   * 子頁面保持不變。
   * 要查看切换的效果，您可以进行转出，将根据转出配置应用任何内容修改。

* 切換至淺層即時副本，然後返回深層：

   * （先前的）淺層即時副本的所有子項都會被視為是手動建立的，因此會使用將其移開 `[oldname]_msm_moved name`.

要指定或更改深度，请执行以下操作：

1. 使用「 」開啟Live Copy頁面的屬性 **檢視屬性** 命令 **網站** 主控台或使用 **頁面資訊** （在頁面工具列上）。
1. 单击或点按 **Live Copy** 选项卡。
1. 在&#x200B;**配置**&#x200B;部分中，根据是否包含子页面来设置或清除 **Live Copy 继承**&#x200B;选项：

   * 勾選 — 深層即時副本（包含子頁面）
   * 清除 — 淺層即時副本（排除子頁面）

   >[!CAUTION]
   >
   >切換到淺層即時副本將立即生效且不可逆。
   >
   >有关更多信息，请参阅 [Live Copy – 构图](/help/sites-administering/msm.md#live-copies-composition)。

1. 单击或点按&#x200B;**保存**&#x200B;以持久存储您的更新。

### 取消组件的继承 {#cancelling-inheritance-for-a-component}

取消元件的即時副本繼承，使元件不再與來源元件同步。 如果需要，您可以稍后启用继承。

>[!NOTE]
>
>如果元件標示為容器，則取消和暫停動作不會套用至其子元件。 另請參閱 [MSM最佳作法](/help/sites-administering/msm-best-practices.md#components-and-container-synchronization) 以取得其他資訊。

>[!NOTE]
>
>当您重新启用继承时，组件不会自动与源同步。如果需要，您可以手动请求同步。

取消继承可更改组件内容或删除组件：

1. 单击或点按要为其取消继承的组件。

   ![chlimage_1-230](assets/chlimage_1-230.png)

1. 在组件工具栏上，单击或点按&#x200B;**取消继承**&#x200B;图标。

   ![图像](do-not-localize/chlimage_1-8.png)

1. 在“取消继承”对话框中，单击&#x200B;**是**&#x200B;确认操作。

   这将更新组件工具栏以包含所有（适当的）编辑命令。

### 重新啟用元件的繼承 {#re-enabling-inheritance-for-a-component}

要启用组件的继承，请单击或点按组件工具栏上的&#x200B;**重新启用继承**&#x200B;图标。

![图像](do-not-localize/chlimage_1-9.png)

### 更改 Live Copy 页面上的组件顺序 {#changing-the-order-of-components-on-a-live-copy-page}

如果即時副本包含屬於段落系統一部分的元件，則該段落系統的繼承會遵循以下規則：

* 即使建立了继承，也可修改继承的段落系统中的组件顺序。
* 在推出时，将从 Blueprint 中恢复组件顺序。如果在轉出前已將新元件新增到live copy，則這些新元件將會與其上方新增的元件一起重新排序。
* 如果取消段落系統的繼承，轉出時元件的順序將不會恢復，並將保持與即時副本中的相同。

>[!NOTE]
>
>在段落系统上恢复取消的继承时，组件的顺序&#x200B;**将不会自动从 Blueprint 恢复**。如果需要，您可以手动请求同步。

使用以下过程可取消段落系统的继承。

1. 開啟即時副本頁面。
1. 将现有组件拖动到页面上的新位置。
1. 在&#x200B;**取消继承**&#x200B;对话框中，单击&#x200B;**是**&#x200B;确认操作。

### 覆盖 Live Copy 页面的属性 {#overriding-properties-of-a-live-copy-page}

依預設，即時副本頁面的頁面屬性是從來源頁面繼承（且不可編輯）。

當您需要變更即時副本的屬性值時，可以取消屬性的繼承。 链接图标表示为属性启用继承。

![chlimage_1-231](assets/chlimage_1-231.png)

在取消继承时，可以更改属性值。断开链接图标表示取消继承。

![chlimage_1-232](assets/chlimage_1-232.png)

如果需要，您可以稍后重新启用属性的继承。

>[!NOTE]
>
>當您重新啟用繼承時，即時副本頁面屬性不會自動與來源屬性同步。 如果需要，您可以手动请求同步。

1. 使用下列任一項來開啟即時副本頁面的屬性： **檢視屬性** 的選項 **網站** 主控台或 **頁面資訊** 圖示加以檢視。
1. 要取消属性的继承，请单击或点按属性右侧显示的链接图标。

   ![图像](do-not-localize/chlimage_1-10.png)

1. 在&#x200B;**取消继承**&#x200B;确认对话框中，单击或点按&#x200B;**是**。

### 还原 Live Copy 页面的属性 {#revert-properties-of-a-live-copy-page}

要为属性启用继承，请单击或点按属性旁边显示的&#x200B;**还原继承**&#x200B;图标。

![图像](do-not-localize/chlimage_1-11.png)

### 重置 Live Copy 页面 {#resetting-a-live-copy-page}

將即時副本頁面重設為：

* 删除所有继承取消并
* 将页面返回到与源页面相同的状态。

重設會影響您對頁面屬性、段落系統和元件所做的變更。

#### 从页面属性重置 Live Copy 页面 {#reset-a-live-copy-page-from-the-page-properties}

1. 在 **網站** 主控台，選取即時副本頁面並選取 **檢視屬性**.
1. 打开 **Live Copy** 选项卡。
1. 从工具栏中选择&#x200B;**重置**。

   ![chlimage_1-233](assets/chlimage_1-233.png)

1. 在&#x200B;**重置 Live Copy** 对话框中，单击&#x200B;**重置**&#x200B;进行确认。

#### 从 Live Copy 概述重置 Live Copy 页面 {#reset-a-live-copy-page-from-the-live-copy-overview}

在选择 Live Copy 页面时，[也可以从 Live Copy 概述执行重置操作](/help/sites-administering/msm-livecopy-overview.md#using-the-live-copy-overview)。

1. 打开 [Live Copy 概述](/help/sites-administering/msm-livecopy-overview.md#using-the-live-copy-overview)并选择 Live Copy 页面。
1. 从工具栏中选择&#x200B;**重置**。
1. 在&#x200B;**重置 Live Copy** 对话框中确认&#x200B;**重置**&#x200B;操作。

   ![chlimage_1-234](assets/chlimage_1-234.png)

## 比较 Live Copy 页面与 Blueprint 页面 {#comparing-a-live-copy-page-with-a-blueprint-page}

若要追蹤您所做的變更，您可以在中檢視Blueprint頁面 **引用** 並與其即時副本頁面比較：

1. 在 **網站** 主控台， [導覽至Blueprint或即時副本頁面並加以選取](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources).
1. 開啟 **[引用](/help/sites-authoring/basic-handling.md#references)** 面板並選取：

   * **Blueprint** （當選取即時副本頁面時）
   * **即時副本** （選取Blueprint頁面時）

1. 選取您特定的即時副本，然後：

   * **與Blueprint比較** （當選取即時副本頁面時）
   * **與即時副本比較** （選取Blueprint頁面時）

   例如：

   ![chlimage_1-235](assets/chlimage_1-235.png)

1. 兩個頁面（即時副本和Blueprint）將並排開啟。

   如需關於使用此功能的完整資訊，請參閱 [頁面差異](/help/sites-authoring/page-diff.md).

## 分离 Live Copy {#detaching-a-live-copy}

分離會永久移除即時副本與其來源/Blueprint頁面之間的即時關係。 所有MSM相關屬性都會從即時副本中移除，且即時副本頁面會成為獨立副本。

>[!CAUTION]
>
>分離即時副本後，您無法恢復即時關係。
>
>若要移除即時關係並選擇稍後恢復它，您可以 [取消即時副本繼承](#suspending-inheritance-for-a-page) 用於頁面。

这会对树中使用&#x200B;**分离**&#x200B;的位置产生影响：

* **在即時副本的根頁面上分離**

   在即時副本的根頁面上執行此操作時，它會移除Blueprint的所有頁面與其LiveCopy之間的即時關係。

   Blueprint中頁面的進一步變更（依原樣） **不會** 會影響livecopy （原樣）。

* **在即時副本的子頁面上分離**

   在即時副本的子頁面（或分支）上執行此操作時：

   * 隨即會移除該子頁面（或分支）的即時關係
   * 而即時副本分支中的（子）頁面會被視為已手動建立。

   *但是*，子頁面仍受父分支的即時關係約束，因此藍圖頁面的進一步轉出將：

   1. 重命名分离的页面：

      * 這是因為MSM將它們視為手動建立的頁面，這些頁面因與其嘗試建立的LiveCopy頁面具有相同名稱而造成衝突。
   1. 以原始名稱建立新（即時副本）頁面，其中包含轉出的變更。

   >[!NOTE]
   >
   >有关此类情况的详细信息，请参阅 [MSM 转出冲突](/help/sites-administering/msm-rollout-conflicts.md)。

### 从页面属性分离 Live Copy 页面 {#detach-a-live-copy-page-from-the-page-properties}

若要分離即時副本：

1. 在 **網站** 主控台，選取即時副本頁面，然後按一下或點選 **檢視屬性**.
1. 打开 **Live Copy** 选项卡。
1. 在工具栏上，选择&#x200B;**分离**。

   ![chlimage_1-236](assets/chlimage_1-236.png)

1. 这将显示一个确认对话框，请选择&#x200B;**分离**&#x200B;以完成此操作。

### 从 Live Copy 概述分离 Live Copy 页面 {#detach-a-live-copy-page-from-the-live-copy-overview}

在选择 Live Copy 页面时，[也可以从 Live Copy 概述执行分离操作](/help/sites-administering/msm-livecopy-overview.md#using-the-live-copy-overview)。

1. 打开 [Live Copy 概述](/help/sites-administering/msm-livecopy-overview.md#using-the-live-copy-overview)并选择 Live Copy 页面。
1. 从工具栏中选择&#x200B;**分离**。
1. 在&#x200B;**分离 Live Copy** 对话框中确认&#x200B;**分离**&#x200B;操作：

   ![chlimage_1-237](assets/chlimage_1-237.png)
