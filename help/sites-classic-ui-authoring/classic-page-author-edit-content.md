---
title: 編輯頁面內容
description: 使用可拖曳至頁面上的元件來新增內容。 然后，可以就地编辑、移动或删除这些内容。
uuid: e7b65ceb-263c-46f2-91e3-11dec3a016fa
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: de321869-ebf9-41a1-8203-e12bdb088678
docset: aem65
exl-id: e1b5aea0-983c-4e7b-9d35-d7beeee45dc7
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '1755'
ht-degree: 13%

---

# 编辑页面内容{#editing-page-content}

创建页面（新页面或者作为启动项或 Live Copy 的一部分）后，您可以编辑内容，以进行所需的更新。

內容新增方式： [元件](/help/sites-classic-ui-authoring/classic-page-author-default-components.md) （適用於內容型別）可供拖曳至頁面上。 然后，可以就地编辑、移动或删除这些内容。

>[!NOTE]
>
>您的帳戶需要 [適當的存取許可權](/help/sites-administering/security.md) 和 [許可權](/help/sites-administering/security.md#permissions) 編輯頁面；例如，新增、編輯或刪除元件、註釋、解除鎖定。
>
>如果您遇到任何问题，我们建议您与系统管理员联系。

## Sidekick {#sidekick}

sidekick是編寫頁面時的關鍵工具。 它會在編寫頁面時浮動，所以一律可見。

有數個標籤和圖示可供使用，包括：

* 组件
* 页面
* 信息
* 版本控制
* 工作流
* 模式
* 基架
* ClientContext
* 网站

![chlimage_1-71](assets/chlimage_1-71.png)

這些可讓您存取廣泛的功能選擇；包括：

* [選取元件](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#sidekick)
* [顯示引用](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#showing-references)
* [存取稽核記錄](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#audit-log)
* [切換模式](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#page-modes)
* [建立](/help/sites-classic-ui-authoring/classic-page-author-work-with-versions.md#creating-a-new-version)， [還原](/help/sites-classic-ui-authoring/classic-page-author-work-with-versions.md#restoring-a-page-version-from-sidekick) 和 [比較](/help/sites-classic-ui-authoring/classic-page-author-work-with-versions.md#comparing-with-a-previous-version) 版本

* [發佈](/help/sites-classic-ui-authoring/classic-page-author-publish-pages.md#publishing-a-page)， [取消發佈](/help/sites-classic-ui-authoring/classic-page-author-publish-pages.md#unpublishing-a-page) 頁面

* [編輯頁面屬性](/help/sites-classic-ui-authoring/classic-page-author-edit-page-properties.md)

* [支架](/help/sites-authoring/scaffolding.md)

* [使用者端內容](/help/sites-administering/client-context.md)

## 插入组件 {#inserting-a-component}

### 插入组件 {#inserting-a-component-1}

開啟頁面後，您可以開始新增內容。 若要這麼做，請新增元件（也稱為段落）。

若要插入新元件：

1. 選取要插入的段落型別的方法有幾種：

   * 連按兩下標示為的區域 **將元件或資產拖曳到這裡……** - **插入新元件** 工具列開啟。 選取元件並按一下 **確定**.

   * 從浮動工具列拖曳元件（稱為sidekick）以插入新段落。
   * 在現有段落上按一下滑鼠右鍵，然後選取 **新增……**  — 插入新元件工具列開啟。 選取元件並按一下 **確定**.

   ![screen_shot_2012-02-15at115605am](assets/screen_shot_2012-02-15at115605am.png)

1. 在sidekick和 **插入新元件** 工具列會顯示可用元件的清單（段落型別）。 這些區段可以分割成不同的區段（例如，「一般」、「欄」等），可視需要展開。

   視您的生產環境而定，這些選項可能有所不同。 如需有關元件的完整詳細資訊，請參閱 [預設元件](/help/sites-classic-ui-authoring/classic-page-author-default-components.md).

1. 在頁面上插入您想要的元件。 然後按兩下該段落，即會開啟一個視窗，讓您設定段落並新增內容。

### 使用內容尋找器插入元件 {#inserting-a-component-using-the-content-finder}

您也可以從以下位置拖曳資產，將新元件新增至頁面： [內容尋找器](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#the-content-finder). 這會自動建立包含資產的適當型別的新元件。

這適用於下列資產型別（部分將取決於頁面/段落系統）：

| 资产类型 | 結果元件型別 |
|---|---|
| 图像 | 图像 |
| 文档 | 下载 |
| 产品 | 产品 |
| 视频 | 闪光灯 |

>[!NOTE]
>
>可针对您的安装配置此行为。另請參閱 [設定段落系統以便拖曳資產建立元件例項](/help/sites-developing/developing-components.md#configuring-a-paragraph-system-so-that-dragging-an-asset-creates-a-component-instance) 以取得更多詳細資料。

要通过拖动以上某一资产类型创建组件，请执行以下操作：

1. 确保页面处于&#x200B;[**编辑**&#x200B;模式](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#page-modes)。
1. 開啟 [內容尋找器](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#the-content-finder).
1. 將所需資產拖曳至所需位置。 此 [元件預留位置](#componentplaceholder) 顯示元件將放置的位置。

   將在所需位置建立適合資產型別的元件 — 它將包含所選資產。

1. [編輯](#editmovecopypastedelete) 元件（若有需要）。

## 編輯元件（內容和屬性） {#editing-a-component-content-and-properties}

若要編輯現有段落，請執行下列任一項動作：

* **按兩下** 段落以開啟它。 您會看到與使用現有內容建立段落時相同的視窗。 進行變更並按一下 **確定**.

* **按一下右鍵** 段落並按一下 **編輯**.

* **按一下** 在段落上按兩下（緩慢連按兩下）以進入就地編輯模式。 您將能夠直接編輯頁面上的文字，而不是在對話方塊視窗內。 在此模式中，頁面頂端會提供工具列。 只需進行變更，系統就會自動儲存變更。

## 移动组件 {#moving-a-component}

若要移動段落，請執行下列動作：

>[!NOTE]
>
>您也可以使用[剪切并粘贴](#cut-copy-paste-a-component)来移动组件。

1. 選取要移動的段落：

   ![screen_shot_2012-02-15at115855am](assets/screen_shot_2012-02-15at115855am.png)

1. 將段落拖曳至新位置 — AEM會以綠色核取記號指出可將段落移動至何處。 將其拖曳至所需位置。
1. 您的段落已移動：

   ![screen_shot_2012-02-15at120030pm](assets/screen_shot_2012-02-15at120030pm.png)

## 刪除元件 {#deleting-a-component}

若要刪除段落，請執行下列動作：

1. 選取段落並 **按一下右鍵**：

   ![screen_shot_2012-02-15at120220pm](assets/screen_shot_2012-02-15at120220pm.png)

1. 選取 **刪除** 功能表中的。 AEM WCM會要求確認您要刪除段落，因為此動作無法復原。
1. 单击&#x200B;**确定**。

>[!NOTE]
>
>如果您已設定 [顯示全域編輯工具列的使用者屬性](/help/sites-classic-ui-authoring/author-env-user-props.md) 您也可以對段落執行某些動作，方法是使用 **複製**， **剪下**， **貼上**， **刪除** 按鈕可用。
>
>各種 [鍵盤快速鍵](/help/sites-classic-ui-authoring/classic-page-author-keyboard-shortcuts.md) 也可供使用。

## 剪下/複製/貼上元件 {#cut-copy-paste-a-component}

當 [刪除元件](#deleting-a-component) 您可以使用快顯選單來複製、剪下和/或貼上元件

>[!NOTE]
>
>如果您已設定 [顯示全域編輯工具列的使用者屬性](/help/sites-classic-ui-authoring/author-env-user-props.md) 您也可以對段落執行某些動作，方法是使用 **複製**， **剪下**， **貼上**， **刪除** 按鈕可用。
>
>各種 [鍵盤快速鍵](/help/sites-classic-ui-authoring/classic-page-author-keyboard-shortcuts.md) 也可供使用。

>[!NOTE]
>
>僅支援在相同頁面中剪下、複製和貼上內容。

## 继承组件 {#inherited-components}

继承组件可能是多种情况的产物，包括：

* [多網站管理](/help/sites-administering/msm.md)；也與 [支架](/help/sites-classic-ui-authoring/classic-feature-scaffolding.md#scaffolding-with-msm-inheritance).

* [啟動](/help/sites-classic-ui-authoring/classic-launches.md) （當以livecopy為基準時）。
* 特定元件；例如Geometrixx內的繼承段落系統。

您可以取消（随后也可以重新启用）继承。根據元件，這可從以下位置取得：

1. **Live Copy**

   如果元件是LiveCopy或Launch的一部分，則會以掛鎖圖示表示。 您可以按一下掛鎖來取消繼承。

   * 選取元件時會顯示掛鎖圖示；例如：

   ![chlimage_1-72](assets/chlimage_1-72.png)

   * 掛鎖也會顯示在元件的對話方塊中；例如：

   ![chlimage_1-73](assets/chlimage_1-73.png)

1. **繼承的段落系統**

   設定對話方塊。 例如，與Geometrixx中的繼承段落系統一樣：

   ![chlimage_1-74](assets/chlimage_1-74.png)

## 添加注释 {#adding-annotations}

[註解](/help/sites-classic-ui-authoring/classic-page-author-annotations.md) 允許其他作者對您的內容提供意見回饋。 這通常用於審查和驗證目的。

## 預覽頁面 {#previewing-pages}

Sidekick的底部邊框中有兩個圖示對預覽頁面很重要：

![](do-not-localize/chlimage_1-5.png)

* 鉛筆圖示會顯示您目前處於編輯模式，您可以在此新增、修改、移動或刪除內容。

   ![](do-not-localize/chlimage_1-6.png)

* 放大鏡圖示可讓您選取預覽模式，其中頁面會顯示在發佈環境中（有時也需要重新整理頁面）：

   ![](do-not-localize/chlimage_1-7.png)

   在預覽模式中sidekick將會減少，按一下向下箭頭圖示以返回編輯模式：

   ![](do-not-localize/chlimage_1-8.png)

## 查找并替换 {#find-replace}

若要對相同片語進行更大規模的編輯，請 **[尋找和取代](/help/sites-classic-ui-authoring/author-env-search.md#find-and-replace)** 功能表選項可讓您在網站的某個區段中搜尋和取代字串的多個執行個體。

## 锁定页面 {#locking-a-page}

AEM可讓您鎖定頁面，讓其他人無法修改內容。 當您對某個特定頁面進行大量編輯，或需要凍結頁面一段時間時，此功能會很有用。

>[!CAUTION]
>
>鎖定頁面時應謹慎使用，因為唯一可以解鎖頁面的人是鎖定頁面的人（或具有管理員許可權的帳戶）。

若要鎖定頁面：

1. 在 **網站** 索引標籤中，選取您要鎖定的頁面。
1. 連按兩下頁面以開啟頁面進行編輯。
1. 在 **頁面** sidekick索引標籤，選擇 **鎖定頁面**：

   ![screen_shot_2012-02-08at15750pm](assets/screen_shot_2012-02-08at15750pm.png)

   訊息會顯示您的頁面已鎖定給其他使用者。 此外，在 **網站** 主控台、AEM WCM會將頁面顯示為已鎖定，並指出已鎖定頁面的使用者。

   ![screen_shot_2012-02-08at20657pm](assets/screen_shot_2012-02-08at20657pm.png)

## 解锁页面 {#unlocking-a-page}

若要解除鎖定頁面：

1. 在 **網站** 索引標籤中，選取您要解除鎖定的頁面。
1. 連按兩下頁面以開啟。
1. 在 **頁面** sidekick索引標籤，選擇 **解鎖頁面**.

## 撤消和重做页面编辑 {#undoing-and-redoing-page-edits}

當頁面的內容框架具有焦點時，請使用下列鍵盤快速鍵：

* 還原：Ctrl+Z (Windows)或Cmd+Z (Mac)
* 重做：Ctrl+Y (Windows)或Cmd+Y (Mac)

當您復原或重做一個或多個段落的移除、新增或重新定位時，閃爍（預設行為）的醒目提示會指出受影響的段落。

>[!NOTE]
>
>有关撤消和重做页面编辑时可执行操作的完整详细信息，请参阅[撤消和重做页面编辑 - 理论](#undoing-and-redoing-page-edits-the-theory)。

## 撤消和重做页面编辑 – 理论 {#undoing-and-redoing-page-edits-the-theory}

>[!NOTE]
>
>您的系統管理員可以 [設定「復原/重做」功能的各個層面](/help/sites-administering/config-undo.md) 根據您執行個體的需求。

AEM會儲存您執行動作的歷史記錄，以及執行動作的順序。 因此，您可以依照執行動作的順序復原數個動作。 然後，您可以使用重做來重新套用一或多個動作。

如果選取了內容頁面上的元素，則復原和重做命令會套用至選取的專案，例如文字元件。

復原和重做命令的行為與其他軟體程式中的類似。 當您決定內容時，請使用命令來還原網頁的最近狀態。 例如，如果您将文本段落移至页面上的其他位置，可以使用撤消命令移回该段落。如果您隨後再次決定移動段落，請使用重做命令。

>[!NOTE]
>
>您可以：
>
>* 只要您使用復原後尚未進行頁面編輯，就可以重做動作。
>* 最多可復原20個編輯動作（預設設定）。
>* 也使用 [鍵盤快速鍵](/help/sites-classic-ui-authoring/classic-page-author-keyboard-shortcuts.md) 「復原」和「重做」。
>


您可以對下列型別的頁面變更使用還原和重做：

* 新增、編輯、移除和移動段落
* 就地編輯段落內容
* 在頁面中複製、剪下和貼上專案
* 跨頁面複製、剪下和貼上專案
* 新增、移除和變更檔案和影像
* 新增、移除和變更註釋和草圖
* 支架的變更
* 新增和移除參照
* 變更元件對話方塊中的屬性值。

表單元件轉譯的表單欄位不應在編寫頁面時指定值。 因此，「還原」和「重做」指令不會影響您對這些元件型別值所做的變更。 例如，您無法還原在下拉式清單中選取值的作業。

>[!NOTE]
>
>对文件和图像的更改执行撤消和重做操作需要特殊的权限。此外，復原檔案和影像變更的歷史記錄至少會持續數小時。 然而，在這段時間之後，無法保證會復原變更。 您的管理員可以提供許可權並變更十小時的預設時間。
