---
title: 管理活动
seo-title: Managing Activities
description: 「活動」主控台可讓您建立、組織和管理品牌的行銷活動
seo-description: The Activities console enables you to create, organize, and manage the marketing activities of your brands
uuid: 0aebf88e-f298-410a-8c82-4076b671624f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
discoiquuid: ef2321a3-cd51-4298-8782-e1a2ca721868
docset: aem65
exl-id: f510ca08-977d-45d5-86af-c4b7634b01ba
source-git-commit: 084e5d561e25dcbaee4489b65f423fc9166832be
workflow-type: tm+mt
source-wordcount: '2000'
ht-degree: 36%

---

# 管理活动{#managing-activities}

「活動」主控台可讓您建立、組織和管理行銷 [活動](/help/sites-authoring/personalization.md#activities) 您的品牌：

* 添加品牌.
* 为每个品牌添加并配置活动.
* 管理活动.

>[!NOTE]
>
>如果您使用Adobe Target作為目標定位引擎，您也可以 [檢視活動的效能資料](#viewing-performance-and-converting-winning-experiences-a-b-test). 如果您使用A/B測試，您可以 [轉換獲勝者](#viewing-performance-and-converting-winning-experiences-a-b-test).

在「活動」主控台上，活動會依品牌組織。 您可以使用品牌和資料夾來建構活動的組織。 您可以點選/按一下，導覽至「活動」主控台 **個人化** 和點選/按一下 **活動**.

在“定位”模式下，可以使用活动来[创作目标内容](/help/sites-authoring/content-targeting-touch.md)，您也可以在该模式下创建活动。您在「鎖定目標」模式中建立的活動會顯示在「活動」主控台中。

活動會以描述所定義活動型別的標籤顯示：

* XT - Adobe Target體驗鎖定目標
* A/B - Adobe Target A/B測試
* AEM - Adobe Experience Manager目標定位（contexthub或clientcontext導向）

![chlimage_1-114](assets/chlimage_1-114.png)

>[!NOTE]
>
>可用的活动类型由以下因素决定：
>
>* 如果 **xt_only** 在AEM端使用的Adobe Target租使用者(clientcode)上啟用選項以連線至Adobe Target，然後您可以建立 **僅限** AEM中的XT活動。
>
>* 如果 **xt_only** 選項為 **not** 已在Adobe Target租使用者(clientcode)上啟用，然後您可以建立 **兩者** AEM中的XT和A/B活動
>
>**其他附註：** **xt_only** options是套用至特定Target租使用者(clientcode)的設定，只能在Adobe Target中直接修改。 您无法在 AEM 中启用或禁用此选项。

>[!CAUTION]
>
>您必须确保发布实例中的活动设置节点 **cq:ActivitySettings** 安全，以使其不可由普通用户访问。该活动设置节点应当只能由负责将活动同步到 Adobe Target 的服务访问。
>
>请参阅[与 Adobe Target 集成的先决条件](/help/sites-administering/target-requirements.md#securingtheactivitysettings)，以了解详细信息。

## 使用「活動」控制檯建立品牌 {#creating-a-brand-using-the-activities-console}

建立您要管理行銷活動的品牌。

使用“活动”控制台创建品牌后，[“选件”控制台](/help/sites-authoring/offerlib.md)（可在此处创建活动体验的选件）中也会出现该品牌。

1. 在“导航”控制台中，单击或点按&#x200B;**个性化**。按一下或點選 **活動**.

   ![screen_shot_2018-03-21at151821](assets/screen_shot_2018-03-21at151821.png)

1. 在「活動」主控台中，按一下或點選 **建立**&#x200B;則&#x200B;**建立品牌**.
1. 選取品牌範本，然後按一下或點選 **下一個**.
1. 輸入您希望品牌在「活動」和「選件」主控台中顯示的標題。 或者，輸入或選取一或多個要與品牌關聯的標籤。
1. 单击或点按&#x200B;**创建**。您的品牌會出現在「活動」主控台中。

## 使用「活動主控台」新增/編輯活動 {#adding-editing-an-activity-using-the-activities-console}

新增活動或編輯現有活動，以將您的行銷工作聚焦於特定對象。 建立/編輯活動時，需指定下列資訊：

* **名称：**&#x200B;活动的名称。
* **定位引擎：**&#x200B;将 [AEM](/help/sites-authoring/personalization.md#aem) 或 [Adobe Target](/help/sites-authoring/personalization.md#adobe-target) 作为目标内容的引擎。

* **选择 Target 配置：**（仅限 Adobe Target）此活动连接到 Adobe Target 的云配置。只有为定位引擎选择了 Adobe Target 时，才会显示此选项。
* **活動型別： **活動型別 — A/B測試或體驗鎖定目標
* **目标：**（可选）活动描述。
* **体验：**&#x200B;受众名称和您定位的营销区段之间的映射。
* **流量百分比：**&#x200B;如果选择 A/B 测试，则可以更改每个体验的流量（百分比）。
* **持续时间：**&#x200B;应用活动的时间段。
* **优先级：**&#x200B;活动的相对优先级。当活动为相同的用户区段提供内容时，具有较高优先级的活动优先。
* **目标量度：**&#x200B;如果选择 Adobe Target 作为定位引擎，则可向活动添加成功量度。需要一个成功量度。

>[!NOTE]
>
>新的 Adobe Target 活动需要在目标内容编辑器中（而不是在&#x200B;**活动**&#x200B;控制台中）***创建***，因为与 Adobe Target 的同步将失败。
>
>不過，您可以在主控台中編輯現有的Adobe Target活動。

若要新增活動：

1. 按一下或點選您要建立活動的品牌、按一下或點選 **建立** 然後 **建立活動**. 如果您要編輯，請選取活動，然後按一下或點選 **編輯**.
1. 提供下列資訊，然後按一下或點選 **下一個**：

   * 活動的名稱。
   * 要使用的目標定位引擎。 預設會選取ContextHub (AEM)。 如果您需要使用Adobe Target，請在目標內容編輯器中建立活動。
   * 如果您已選取Adobe Target作為定位引擎，請選取/編輯用來連線至Adobe Target的雲端設定。 （請注意，您不會選取為雲端設定建立的架構。）
   * （選用）活動的目標或說明。
   * 選取「活動型別」。

1. 向活动添加一个或多个体验。 单击或点按 **添加体验**。
1. 如果您正在使用AEM鎖定目標或Adobe Target體驗鎖定目標：

   1. 按一下或點選**選取對象**，然後選取您的體驗鎖定目標的區段。
   1. 单击或点按&#x200B;**添加体验**，键入名称，然后单击或点按&#x200B;**确定**。

   1. 单击或点按&#x200B;**下一步**。


   如果您使用Adobe Target A/B測試：

   1. 按一下或點選「對象」方塊中的鉛筆，以選取對象。
   1. 单击或点按&#x200B;**添加体验**，键入名称，然后单击或点按&#x200B;**确定**。

   1. 輸入顯示每個體驗的流量百分比。
   1. 单击或点按&#x200B;**下一步**。



1. 若要指定活動開始的時間，請使用 **開始** 下拉式功能表以選取下列其中一個值：

   * **啟用時：** 活動從包含目標內容的頁面啟動時開始。
   * **指定的日期和時間：** 特定時間。 选择此选项时，单击或点按日历图标，选择日期，然后指定活动开始的时间。

1. 若要指定活動結束的時間，請使用「結束」下拉式選單來選取下列其中一個值：

   * **停用時**：活動會在包含目標內容的頁面停用時結束。
   * **指定的日期和時間**：特定時間。 選取此選項時，按一下或點選日曆圖示，選取日期，並指定活動結束時間。

1. 若要指定活動的優先順序，請使用滑桿來選取 **低**， **一般**，或 **高**.
1. 如果您使用Adobe Target作為目標定位引擎，請選取您要透過此活動測量的內容。 请参阅[配置活动和设置目标](/help/sites-authoring/content-targeting-touch.md)，以了解有关可用成功量度的更多信息。您必須至少選取一個目標。
1. 按一下或點選 **儲存**.

   >[!NOTE]
   >
   >建立活動後，您需要發佈活動才能使用。

## 發佈和取消發佈活動 {#publishing-and-unpublishing-activities}

您需要發佈活動才能使其可用。 相反地，您可能想要透過取消發佈來讓活動無法使用。

>[!NOTE]
>
>取消发布活动时，除非您刷新页面，否则活动的状态不会改变。

若要發佈或取消發佈活動：

1. 按一下或點選品牌，然後按一下包含您要發佈或取消發佈之活動的區域。
1. 點選或按一下您要發佈或取消發佈的一或多個活動旁的圖示。

   ![screen-shot_2019-03-05at123846](assets/screen-shot_2019-03-05at123846.png)

1. 若要發佈，請點選或按一下 **發佈**. 若要取消發佈，請點選或按一下 **取消發佈**. 您的活動已發佈或已取消發佈，且狀態在「活動」主控台中變更（可能需要重新整理）。

## 製作和發佈例項上的活動 {#activities-on-author-and-publish-instances}

當使用Adobe Target目標定位引擎的活動啟動時，會在發佈執行個體上建立第二個活動：

* 製作執行個體上的活動會追蹤製作執行個體上的活動，且對於模擬訪客體驗相當實用。 為此活動記錄的分析僅反映作者執行個體上發生的情況。
* 發佈執行個體上的活動會反映和回應發佈伺服器上的活動。 這是在公用網站上執行的活動。 只有發佈活動與追蹤和分析實際公共網站的使用情況相關。

## 檢視效能和轉換成功體驗（A/B測試） {#viewing-performance-and-converting-winning-experiences-a-b-test}

您可以檢視任何Adobe Target活動（XT或A/B）的效能。 如果您使用A/B測試，也可以轉換成功體驗，這會成為預設體驗。

要查看活动业绩并转换入选体验，请执行以下操作：

1. 在&#x200B;**个性化**&#x200B;中，单击或点按&#x200B;**活动**，以导航到&#x200B;**活动**&#x200B;控制台。
1. 单击或点按要查看其活动的品牌。
1. ********&#x200B;显示性能数据。

   ![chlimage_1-115](assets/chlimage_1-115.png)

1. 单击或点按&#x200B;**推送入选方**&#x200B;链接，以将入选体验推送为默认体验。

   如果转换入选方，则会：

   * 禁用当前活动
   * 修改所有页面，并将目标内容替换为入选体验的实际内容。入选体验的内容&#x200B;**无需**&#x200B;定位即可成为常规页面的一部分。

   ![chlimage_1-116](assets/chlimage_1-116.png)

   成功體驗是指根據轉換率，在報表中產生更多提升度的體驗。

1. 按一下或點選 **是** 若要確認您要轉換獲勝者，請停用目前的體驗，並將其取代為獲勝者體驗的內容。

## 使用Adobe Target同步活動 {#synchronizing-activities-with-adobe-target}

使用Adobe Target目標定位引擎的活動會與Adobe Target行銷活動同步。 當符合下列條件時，活動會自動同步至Adobe Target：

* 活動至少包含一個體驗。
* 至少一個體驗包含對應的區段和一個選件。
* 活動中的每個體驗都必須有相同數量的選件。

這些條件適用於作者和發佈執行個體上的活動。

同步活動時，會在Adobe Target中建立對應的行銷活動：

* 發佈執行個體上的活動與對應的Adobe Target行銷活動具有相同名稱。
* 创作实例中的活动与具有相同名称但带有 `_author` 后缀的 Target 营销活动相对应。

![chlimage_1-117](assets/chlimage_1-117.png)

修改活動時，會立即同步_author活動。 即時同步可讓您使用Client Context或ContextHub來模擬活動。

當活動發佈至AEM發佈執行個體時，會同步發佈活動。

## 疑難排解活動同步 {#troubleshooting-activity-synchronization}

与 Adobe Target 同步活动时，AEM 中包含一个名为 `thirdPartyId` 的活动属性。此属性的值基于活动在 AEM 存储库中的路径。Adobe Target 中的任意两个营销活动不能具有相同的 `thirdPartyId` 属性值。因此，如果 Adobe Target 中的某个现有营销活动（具有不同的类型：AB、XT）使用的 `thirdPartyId` 值与某个活动相同，则该活动的同步操作会失败。

此情況可能發生在以下情況下：

1. 活動會建立並與Adobe Target同步。
1. 在其他AEM執行個體上，活動會以相同品牌並使用相同名稱建立。 嘗試同步此活動時失敗。

此情況也可能發生在下列情況下：

1. 活動會建立並與Adobe Target同步。 然後，活動就會在AEM上刪除。
1. 活動會在相同品牌下建立，並使用與已刪除活動相同的名稱。 嘗試同步此活動時失敗。

若要避免同步化問題，請一律對活動使用唯一名稱。 如果活动同步失败，您可以删除 Adobe Target 中具有相同名称的营销活动，但前提是该营销活动未在使用中。

>[!NOTE]
>
>在Adobe Target中建立行銷活動時，會指派名為的屬性 `thirdPartyId t`每個行銷活動的。 在 Adobe Target 中删除营销活动时，不会删除 `thirdPartyId`。您不能为不同类型（AB、XT）的营销活动重复使用 `thirdPartyId`，也不能手动删除此属性。为避免出现此问题，请为每个营销活动指定唯一的名称；这样，营销活动名称便无法在不同的营销活动类型中重复使用。
>
>如果在同一种营销活动类型中使用相同的名称，则会覆盖现有的营销活动。
>
>如果在同步时遇到错误“请求失败。`thirdPartyId` 已存在”，请更改营销活动的名称，然后重新进行同步。
