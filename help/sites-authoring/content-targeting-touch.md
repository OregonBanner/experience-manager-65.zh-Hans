---
title: 使用定位模式创作目标内容
seo-title: Authoring Targeted Content Using Targeting Mode
description: 目標定位模式和Target元件提供建立體驗內容的工具
seo-description: Targeting mode and the Target component provide tools for creating content for experiences
uuid: cea85c1b-1bc3-4498-9eaa-4ad10dc58ea4
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
discoiquuid: 9d940744-3b00-4721-829a-96d17bb738e8
docset: aem65
exl-id: edde225d-0be7-4306-8dda-d18d46fae977
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '5349'
ht-degree: 33%

---

# 使用定位模式创作目标内容{#authoring-targeted-content-using-targeting-mode}

可使用 AEM 的定位模式创作目标内容。目標定位模式和Target元件提供建立體驗內容的工具：

* 輕鬆辨識頁面上的目標內容。 虛線會形成所有目標內容周圍的邊框。
* 選取品牌和活動以檢視體驗。
* 新增體驗至活動或移除體驗。
* 執行A/B測試並轉換獲勝者(僅限Adobe Target)。
* 透過建立優惠方案或使用資料庫中的優惠方案，將優惠方案新增至體驗。
* 設定目標並監控效能。
* 模擬使用者體驗。
* 如需更多自訂內容，請設定Target元件。

您可以使用AEM或Adobe Target作為目標定位引擎(您必須具備有效的Adobe Target帳戶才能使用Adobe Target)。 如果您使用Adobe Target，必須先設定整合。 另請參閱 [與Adobe Target整合的說明](/help/sites-administering/target.md).

![chlimage_1-8](assets/chlimage_1-8.png)

您在Target模式中看到的活動和體驗會反映 [活動主控台](/help/sites-authoring/activitylib.md)：

* 您使用定位模式對活動和體驗所做的變更，會反映在活動主控台中。
* 在「活動」主控台中所做的變更會反映在「鎖定目標」模式中。

>[!NOTE]
>
>在 Adobe Target 中创建营销活动时，会为每个营销活动分配名为 `thirdPartyId` 的属性。在 Adobe Target 中删除营销活动时，不会删除 thirdPartyId。您不能为不同类型（AB、XT）的营销活动重复使用 `thirdPartyId`，也不能手动删除此属性。为避免出现此问题，请为每个营销活动指定唯一的名称；这样，营销活动名称便无法在不同的营销活动类型中重复使用。
>
>如果在同一种营销活动类型中使用相同的名称，则会覆盖现有的营销活动。
>
>如果在同步时遇到错误“请求失败。`thirdPartyId` 已存在”，请更改营销活动的名称，然后重新进行同步。

>[!NOTE]
>
>鎖定目標時，品牌和活動組合會保留在使用者層級，而不是頻道層級。

## 切換至目標定位模式 {#switching-to-targeting-mode}

切換至Target模式以存取用於編寫目標內容的工具。

若要切換至目標模式：

1. 開啟您要為其創作目標內容的頁面。
1. 在页面顶部的工具栏中，单击或点按模式下拉菜单，以显示可用的模式类型。

   ![chlimage_1-9](assets/chlimage_1-9.png)

1. 单击或点按&#x200B;**定位**。定位选项随即会显示在页面顶部。

   ![chlimage_1-10](assets/chlimage_1-10.png)

## 使用定位模式新增活動 {#adding-an-activity-using-targeting-mode}

使用目標定位模式將活動新增至品牌。 新增活動時，活動會包含預設體驗。 新增活動後，您就會開始活動的內容鎖定目標程式。

您也可以選擇目標引擎(AEM或Adobe Target)並選取活動型別（體驗鎖定目標或A/B測試），從AEM建立和管理Adobe Target活動。

此外，您可以管理所有Adobe Target活動的目標與量度，並管理Adobe Target對象。 Adobe Target活動報告也包括在內，包括轉換A/B測試的獲勝者。

新增活動時，它也會出現在 [活動主控台](/help/sites-authoring/activitylib.md).

若要新增活動：

1. 使用 **品牌** 下拉式功能表以選取您要建立活動的品牌。

   >[!NOTE]
   >
   >建議用於 [透過「活動」主控台建立品牌](/help/sites-authoring/activitylib.md#creating-a-brand-using-the-activities-console).
   >
   >
   >如果您以任何其他方式创建品牌，请确保存在节点 `/campaigns/<brand>/master`，否则在您尝试创建活动时将产生错误。

1. 按一下或點選「+」旁的 **活動** 下拉式功能表。
1. 輸入活動的名稱。

   >[!NOTE]
   >
   >在创建新活动时，如果已将 Adobe Target 云配置附加到页面或其某个父页面，则 AEM 会自动将 Adobe Target 视为定位引擎。

1. 在&#x200B;**定位**&#x200B;引擎下拉菜单中，选择您的定位引擎。

   * 如果您选择 **ContextHub AEM**，则其余字段会变暗且不再可用。单击或点按&#x200B;**创建**。

   * 如果您選取 **Adobe Target**，您可以選取設定(根據預設，此設定是您在 [已設定帳戶](/help/sites-administering/opt-in.md))和活動型別。

   * 如果您使用AEM/Adobe Campaign整合併傳送目標內容（電子報），請選取 **Adobe Campaign**. 另請參閱 [與Adobe Campaign整合](/help/sites-administering/campaign.md) 以取得詳細資訊。

1. 在「活動」功能表中，選取 **體驗鎖定** 或 **A/B測試**.

   * 體驗鎖定目標 — 從AEM管理Adobe Target活動。
   * A/B測試 — 從AEM在Adobe Target中建立/管理A/B測試活動。

## 目標定位程式：建立、目標定位以及目標與設定 {#the-targeting-process-create-target-and-goals-settings}

目標定位模式可讓您設定活動的幾個方面。 使用下列三個步驟的流程來建立品牌活動的目標內容：

1. [建立](#create-authoring-the-experiences)：新增或移除體驗，並為每個體驗新增選件。
1. [Target](#diagramtargetconfiguringtheaudiences)：指定每個體驗鎖定的對象。 您可以鎖定特定對象，以及如果使用A/B測試來決定流向哪個體驗的流量百分比。
1. [目標與設定](#settingsgoalssettingsconfiguringtheactivityandsettinggoals)：排程活動並設定優先順序。 您也可以設定成功量度目標。

使用以下程式，開始活動的內容鎖定目標程式。

>[!NOTE]
>
>要使用该定位流程，您必须是“Target 活动作者”用户组的成员。

若要新增活動：

1. 在 **品牌** 下拉式功能表，選取包含您正在處理之活動的品牌。
1. 在 **活動** 下拉式功能表，選取您要為其編寫目標內容的活動。
1. 若要顯示引導您完成目標定位程式的控制項，請按一下或點選 **開始定位**.

   ![chlimage_1-11](assets/chlimage_1-11.png)

   >[!NOTE]
   >
   >若要變更您正在使用的活動，請按一下或點選 **返回**.

## 建立：編寫體驗 {#create-authoring-the-experiences}

內容目標定位的「建立」步驟涉及建立體驗。 在此步驟中，您可以建立或刪除活動的體驗，並向每個體驗新增選件。

### 在目標定位模式中檢視體驗選件 {#seeing-experience-offers-in-targeting-mode}

在您之後 [開始目標定位程式](/help/sites-authoring/content-targeting-touch.md#the-targeting-process-create-target-and-goals-settings)，選取體驗以檢視為該體驗提供的選件。 當您選取體驗時，頁面上的目標元件會變更，顯示該體驗的選件。

>[!CAUTION]
>
>當您停用編寫執行個體中已鎖定的元件的鎖定目標時，請務必小心。 相应的活动也将自动从发布实例中删除。

>[!NOTE]
>
>選件是目標元件的內容。

体验显示在“受众”窗格中。 在以下示例中，体验包 **括Default**、 **Female**、Female 30 **岁以上的体验和****** Female 30以下的体验。 此示例显示了目标图像组件的默认 **选件** 。

![chlimage_1-12](assets/chlimage_1-12.png)

选择其他体验后，图像组件会显示该所选体验的选件。

![chlimage_1-13](assets/chlimage_1-13.png)

选择某个体验且目标组件不包含该体验的选件时，该组件会在半透明的默认选件上叠加显示 **添加选件** 。 尚未为体验创建选件时，系统会为映射 **到该体验的区段显示** “默认选件”。

![chlimage_1-14](assets/chlimage_1-14.png)

如果访客属性与映射到体验的任何区段都不匹配，则也会显示默认体验。请参阅[使用定位模式添加体验](#adding-and-removing-experiences-using-targeting-mode)。

### 自訂選件和資料庫選件 {#custom-offers-and-library-offers}

符合以下條件的優惠方案 [在頁面上撰寫](/help/sites-authoring/content-targeting-touch.md#adding-a-custom-offer) 用於單一體驗的，稱為自訂選件。 下列影像重疊在自訂選件的內容上：

![chlimage_1-15](assets/chlimage_1-15.png)

以下图像将叠加显示在[从选件库添加](/help/sites-authoring/content-targeting-touch.md#adding-an-offer-from-an-offer-library)的选件上：

![chlimage_1-16](assets/chlimage_1-16.png)

如果您決定要重複使用自訂優惠方案，可以將自訂優惠方案儲存至優惠方案程式庫。 如果您想要修改體驗的內容，也可以將資料庫選件轉換為自訂選件。 編輯後，您可以再次將選件儲存回程式庫。

### 使用定位模式新增和移除體驗 {#adding-and-removing-experiences-using-targeting-mode}

使用的建立步驟 [目標定位程式](/help/sites-authoring/content-targeting-touch.md#the-targeting-process-create-target-and-goals-settings)，您可以新增和移除體驗。 此外，您也可以複製體驗並重新命名。

#### 使用定位模式新增體驗 {#adding-experiences-using-targeting-mode}

若要新增體驗：

1. 要添加体验，请单击或点按&#x200B;**受众**&#x200B;窗格中现有体验下方显示的 **+** **添加体验定位**。
1. 選取和對象。 依預設，該名稱是體驗的名稱。 您可以視需要輸入其他名稱。 按一下或點選 **確定**.

#### 使用定位模式移除體驗 {#removing-experiences-using-targeting-mode}

若要刪除體驗：

1. 单击或点按体验名称旁边的箭头。

   ![chlimage_1-17](assets/chlimage_1-17.png)

1. 单击&#x200B;**删除**。

#### 使用定位模式重新命名體驗 {#renaming-experiences-using-targeting-mode}

若要使用定位模式重新命名體驗：

1. 单击或点按体验名称旁边的箭头。
1. 单击&#x200B;**重命名体验**，然后键入新名称。
1. 单击或点按屏幕上的其他位置以保存更改。

#### 使用定位模式編輯對象 {#editing-audiences-using-targeting-mode}

若要使用鎖定目標模式編輯對象：

1. 单击或点按体验名称旁边的箭头。
1. 单击&#x200B;**编辑受众**，然后选择新受众。
1. 单击&#x200B;**确定**。

#### 使用定位模式複製體驗 {#duplicating-experiences-using-targeting-mode}

若要使用定位模式複製體驗：

1. 单击或点按体验名称旁边的箭头。
1. 单击&#x200B;**复制**，然后选择受众。
1. 視需要重新命名體驗，然後按一下 **確定**.

### 使用定位模式建立優惠方案 {#creating-offers-using-targeting-mode}

將元件設為目標，以建立體驗的選件。 目標元件會提供作為體驗選件的內容。

* [鎖定現有元件](/help/sites-authoring/content-targeting-touch.md#creating-a-default-offer-by-targeting-an-existing-component). 內容會變成預設體驗的選件。
* [添加 Target 组件](/help/sites-authoring/content-targeting-touch.md#creating-an-offer-by-adding-a-target-component)，然后向该组件中添加内容。

鎖定元件後，您可以為每個體驗新增選件：

* [新增自訂優惠方案](/help/sites-authoring/content-targeting-touch.md#adding-a-custom-offer).
* [從程式庫新增選件](/help/sites-authoring/content-targeting-touch.md#adding-an-offer-from-an-offer-library).

可使用下列工具來處理選件：

* [新增自訂優惠方案至優惠方案庫](/help/sites-authoring/content-targeting-touch.md#adding-a-custom-offer-to-a-library).
* [將資料庫選件轉換為自訂選件](/help/sites-authoring/content-targeting-touch.md#converting-a-library-offer-to-a-custom-library).
* [開啟程式庫選件並編輯內容](/help/sites-authoring/content-targeting-touch.md#editing-a-library-offer).

#### 透過定位現有元件來建立預設選件 {#creating-a-default-offer-by-targeting-an-existing-component}

在頁面上定位元件，以將其用作活動的預設體驗的選件。 當您鎖定元件為目標時，它會封裝在Target元件中，且其內容會成為預設體驗的選件。

當您鎖定元件為目標時，選件中只能使用該元件。 您無法從選件中移除元件，也無法新增其他元件至選件。

在下列步驟之後 [開始目標定位程式](/help/sites-authoring/content-targeting-touch.md#the-targeting-process-create-target-and-goals-settings).

1. 按一下或點選要定位的元件。 元件工具列隨即出現，類似於以下範例。

   ![chlimage_1-18](assets/chlimage_1-18.png)

1. 单击或点按“定位”图标。

   ![](do-not-localize/chlimage_1.png)

   该组件内容随即会成为默认体验的选件。定位某个组件后，其默认节点会被复制到每个体验中。在进行特定于体验的创作时，需要具有此默认节点，才能编辑正确的内容节点。对于默认体验之外的其他体验，可[添加自定义选件](/help/sites-authoring/content-targeting-touch.md#adding-a-custom-offer)或[添加库选件](/help/sites-authoring/content-targeting-touch.md#adding-an-offer-from-an-offer-library)。

#### 通过添加 Target 组件创建选件 {#creating-an-offer-by-adding-a-target-component}

可添加 Target 组件，以创建默认体验的选件。Target 组件是用于存放其他组件的容器，放置在其中的组件会成为目标组件。使用 Target 组件时，可以在其中添加多个组件以创建选件。此外，您还可以在每个体验中使用不同的组件，以创建不同的选件。

有关自定义 Target 组件的信息，请参阅[配置 Target 组件选项](/help/sites-authoring/content-targeting-touch.md#configuring-target-component-options)。

>[!NOTE]
>
>使用[“选件”控制台](/help/sites-authoring/offerlib.md)创建的选件也可以包含多个组件。這些選件屬於一個選件資料庫，且可用於多個體驗。

由於Target元件是容器，因此會顯示為其他元件的放置區域。

在Target模式中，Target元件具有藍色邊框，而下拉目標訊息會指出鎖定目標的性質。

![chlimage_1-19](assets/chlimage_1-19.png)

在编辑模式下，Target 组件具有一个靶心图标。

![](do-not-localize/chlimage_1-1.png)

将组件拖放到 Target 组件后，它们即成为目标组件。

![chlimage_1-20](assets/chlimage_1-20.png)

將元件新增至Target元件時，它會提供特定體驗的內容。 若要指定體驗，請在新增元件之前選取體驗。

您可以在「編輯」模式或「目標」模式中將Target元件新增至頁面。 您只能在Target模式中新增元件至Target元件。 Target元件屬於Personalization元件群組。

如果要编辑目标内容，您必须单击或点按&#x200B;**开始定位**，然后才能进行编辑。

1. 將Target元件拖曳至您要顯示選件的頁面。
1. 依預設，未設定位置ID。 按一下或點選「設定齒輪」以設定位置。

   >[!NOTE]
   >
   >如果管理员进行了相应设置，您可能需要明确设置此位置。
   >
   >
   >管理员可以决定是否需要在以下位置设置此配置：**https://&lt;host>：&lt;port>/system/console/configMgr/com.day.cq.personalization.impl.servlets.TargetingConfigurationServlet**
   若要要求使用者輸入位置，請選取**強制位置**核取方塊。

1. 選取您要建立選件的體驗。
1. 建立選件：

   * 对于默认体验，请将组件拖动到目标拖放区域，然后按常规方式编辑组件属性以创建选件内容。
   * 對於非預設體驗，可以 [新增自訂優惠方案](#adding-a-custom-offer) 或 [新增資料庫選件](/help/sites-authoring/content-targeting-touch.md#adding-an-offer-from-an-offer-library).

#### 新增自訂優惠方案 {#adding-a-custom-offer}

在「鎖定目標」模式中製作目標元件的內容，以建立選件。 當您建立自訂選件時，會將其用作單一體驗的選件。

如果您决定要将选件用于其他体验，则可以先创建自定义选件，然后再[将其添加到库](/help/sites-authoring/content-targeting-touch.md#adding-a-custom-offer-to-a-library)。有关如何使用“选件”控制台创建可重复使用的选件的信息，请参阅[将选件添加到选件库](/help/sites-authoring/offerlib.md#add-an-offer-to-an-offer-library)。

1. 選取您要新增選件的體驗。
1. 若要顯示元件功能表，請按一下或點選要新增選件的目標元件。

   ![chlimage_1-21](assets/chlimage_1-21.png)

1. 按一下或點選+圖示。

   預設選件的內容會作為目前體驗的選件。

1. 按一下或點選選選件以顯示選件功能表，然後按一下或點選編輯圖示。

   ![](do-not-localize/chlimage_1-2.png)

1. 編輯元件的內容。

#### 從選件資料庫新增選件 {#adding-an-offer-from-an-offer-library}

可将[选件库](/help/sites-authoring/offerlib.md)中的选件添加到体验。您可以添加当前定位的品牌的库中包含的任何选件。

您無法將資料庫選件新增至預設體驗。

1. 選取您要新增選件的體驗。
1. 若要顯示元件功能表，請按一下或點選要新增選件的目標元件。

   ![chlimage_1-22](assets/chlimage_1-22.png)

1. 单击或点按文件夹图标。

   ![](do-not-localize/chlimage_1-3.png)

1. 从库中选择选件，然后单击或点按复选标记图标。

   ![chlimage_1-23](assets/chlimage_1-23.png)

   選件選擇器可讓您瀏覽或篩選選件。 瀏覽或篩選時，您可能也想要排序選件並變更其檢視方式。 右上方的數字表示目前資料庫中有多少選件可供使用。

   * 单击或点按&#x200B;**浏览**&#x200B;可导航到其他文件夹。导航窗格随即会打开，单击箭头可向下浏览文件夹。再次单击或点按&#x200B;**浏览**&#x200B;可关闭导航窗格。

   ![chlimage_1-24](assets/chlimage_1-24.png)

   * 单击或点按&#x200B;**过滤器**&#x200B;可按关键字或标记筛选选件。您可以輸入關鍵字，並從下拉式選單中選取標籤。 再次单击或点按&#x200B;**过滤器**&#x200B;可关闭筛选窗格。

   ![chlimage_1-25](assets/chlimage_1-25.png)

   * 单击或点按&#x200B;**最新到最旧**&#x200B;旁边的箭头可更改选件排序方式。可以按“最新到最旧”或“最旧到最新”方式对选件进行排序。

   ![chlimage_1-26](assets/chlimage_1-26.png)

   单击或点按&#x200B;**查看方式**&#x200B;旁边的图标可采用拼贴或列表方式查看选件。

   ![chlimage_1-27](assets/chlimage_1-27.png)

#### 新增自訂選件至程式庫 {#adding-a-custom-offer-to-a-library}

將自訂優惠方案新增至 [優惠資料庫](/help/sites-authoring/offerlib.md) ，可作為多個體驗的選件。 您可以將選件新增至您鎖定目標的目前品牌資料庫。

有关如何使用“选件”控制台创建可重复使用的选件的信息，请参阅[将选件添加到选件库](/help/sites-authoring/offerlib.md#add-an-offer-to-an-offer-library)。

1. 選取體驗以顯示自訂選件。
1. 按一下或點選自訂選件以顯示選件功能表，然後按一下或點選 **將選件儲存至選件資料庫** 圖示。

   ![](do-not-localize/chlimage_1-4.png)

1. 輸入選件的名稱，並選取您要新增選件的資料庫，然後按一下或點選核取標籤圖示。

#### 將資料庫選件轉換為自訂資料庫 {#converting-a-library-offer-to-a-custom-library}

將資料庫選件轉換為自訂選件，以變更目前體驗的選件，而不變更其他體驗中的選件。

1. 選取要顯示資料庫選件的體驗。
1. 按一下或點選資料庫選件以顯示選件功能表，然後按一下或點選「轉換為內嵌選件」圖示。

   ![](do-not-localize/chlimage_1-5.png)

#### 編輯程式庫選件 {#editing-a-library-offer}

在「鎖定目標」模式中，從體驗開啟資料庫選件，以編輯選件。 您所做的變更會顯示在使用該選件的所有體驗中。

1. 選取要顯示資料庫選件的體驗。
1. 將資料庫選件轉換為本機/自訂選件。 请参阅[将库选件转换为自定义选件](#converting-a-library-offer-to-a-custom-library)。
1. 编辑选件的内容。

1. 将选件重新保存到库。请参阅[将自定义选件添加到库](#adding-a-custom-offer-to-a-library)。

## Target：設定對象 {#target-configuring-the-audiences}

的目標步驟： [目標定位程式](/help/sites-authoring/content-targeting-touch.md#the-targeting-process-create-target-and-goals-settings) 包括將對象與您在「建立」步驟中使用的體驗對應。 Target頁面會顯示每個體驗所定位的對象。 您可以指定或變更每個體驗的對象。 如果您使用Adobe Target，也可以建立A/B測試，讓您為特定體驗鎖定對象流量的百分比。

### 如果您使用的是 AEM 定位或 Adobe Target（体验定位） ... {#if-you-are-using-aem-targeting-or-adobe-target-experience-targeting}

受众会显示在映射图左侧，而体验则会显示在右侧。

![chlimage_1-28](assets/chlimage_1-28.png)

可使用区段定义受众。頁面的雲端設定會決定您可以使用的區段。 當頁面未與Adobe Target雲端設定關聯時，AEM區段可用於定義對象。 當頁面與Adobe Target雲端設定相關聯時，您會使用Target區段。

如需鎖定目標引擎的詳細資訊，請參閱 [目標定位引擎](/help/sites-authoring/personalization.md#targeting-engine).

對象不可由多個體驗使用。 當體驗對應至對象且對象已對應至其他體驗時，警告符號會出現在體驗旁邊。

![](do-not-localize/chlimage_1-6.png)

### 將體驗與受眾建立關聯(AEM或Adobe Target) {#associating-experiences-with-audiences-aem-or-adobe-target}

使用AEM鎖定目標(或Adobe Target體驗鎖定目標)時，請依照下列程式將體驗與對象建立關聯：

1. 按一下或點選對象方塊中，對應至體驗的下一個下拉式箭頭。
1. （可选）单击或点按&#x200B;**编辑**，然后键入关键字搜索所需区段。
1. 在受众列表中，选择受众，然后单击或点按&#x200B;**确定**。

### 如果您使用的是 A/B 测试 (Adobe Target) ... {#if-you-are-using-a-b-testing-adobe-target}

如果您有A/B測試活動，對象位於左側，每個體驗的檢視百分比位於中間，而體驗位於右側。

只要百分比加總為100%，您就可以變更百分比。 一個對象可供A/B測試中的多個體驗使用。

![chlimage_1-29](assets/chlimage_1-29.png)

### 將對象和流量百分比與A/B測試建立關聯 {#associating-audiences-and-traffic-percentages-with-a-b-testing}

1. 按一下或點選已對應至體驗之對象旁的下拉式方塊。
1. （可選）按一下 **編輯**，然後輸入關鍵字以搜尋所需的區段。
1. 单击或点按&#x200B;**确定**。
1. 輸入百分比，以設定將受眾流量路由至每個體驗的方式。 總數必須等於100。
1. （可選）按一下體驗名稱旁邊的下拉式功能表，以編輯體驗名稱。

## 目標與設定：設定活動與設定目標 {#goals-settings-configuring-the-activity-and-setting-goals}

[定位流程](/help/sites-authoring/content-targeting-touch.md#the-targeting-process-create-target-and-goals-settings)的“目标和设置”步骤涉及配置品牌活动的行为。指定活動開始和結束的時間，以及活動優先順序。 此外，您也可以追蹤目標。 具體來說，您可以決定要在活動中測量哪些專案。

目標量度僅在您使用Adobe Target作為定位引擎時才能使用。 您必須至少定義一個目標量度。 如果您已設定Adobe Analytics且已設定A4T Analytics雲端設定，則可以選取您要讓報表來源為Adobe Target還是Adobe Analytics。

系統只會針對已發佈的行銷活動測量目標量度。

如果使用AEM作為定位引擎：

![chlimage_1-30](assets/chlimage_1-30.png)

如果使用 Adobe Target 作为定位引擎：

![chlimage_1-31](assets/chlimage_1-31.png)

如果使用 Adobe Target 作为定位引擎，并且您为帐户配置了 A4T 分析，则您还有一个额外的&#x200B;**报告源**&#x200B;下拉菜单：

![chlimage_1-32](assets/chlimage_1-32.png)

可以使用以下成功量度（仅用于发布）：

<table>
 <tbody>
  <tr>
   <td><strong>转化</strong></td>
   <td><p>已单击正在测试的体验的任何部分的访客的百分比。转化可以按每个访客计数一次，也可以在每次访客完成转化时计数一次。转化量度设置为以下项之一: </p>
    <ul>
     <li><strong>已檢視頁面</strong>  — 您可以透過選取以下任一專案來定義對象檢視的頁面 <strong>URL是</strong> 然後定義URL或多個URL，或透過選取 <strong>URL包含</strong> 然後新增路徑或關鍵字。</li>
     <li><strong>已檢視mbox</strong>  — 您可以透過輸入mbox的名稱來定義對象檢視的mbox。 您可以按一下「 」，輸入多個mbox <strong>新增Mbox</strong>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>收入</strong></td>
   <td><p>访问产生的收入。您可以從下列收入量度中選擇：</p>
    <ul>
     <li>每位訪客帶來的收入(RPV)</li>
     <li>平均订单值 (AOV)</li>
     <li>销售总额 </li>
     <li>订单</li>
    </ul> <p>对于这些选项中的任一选项，是否已查看 mbox 指示是否已达到目标。您可以定义一个或多个 mbox。</p> </td>
  </tr>
  <tr>
   <td><strong>参与</strong></td>
   <td><p>您可以衡量三种类型的参与: </p>
    <ul>
     <li>页面视图</li>
     <li>自定义得分</li>
     <li>网站停留时间</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

此外，進階設定可讓您決定如何計算成功量度。 選項包括計算每次曝光或每位訪客一次的量度，並選擇讓使用者留在活動中或將其移除。

使用進階設定來判斷情形 **晚於** 使用者遇到目標量度。 下表顯示可用的選項。

<table>
 <tbody>
  <tr>
   <td><strong>在用户遇到此目标量度后...</strong></td>
   <td><strong>您选择以下操作...</strong></td>
  </tr>
  <tr>
   <td><strong>增量计数并保持用户处于活动状态</strong></td>
   <td>指定計數的遞增方式：
    <ul>
     <li>每個加入者一次</li>
     <li>每次曝光時，排除頁面重新整理</li>
     <li>每次曝光時</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>增量计数、释放用户并允许再次进入</strong></td>
   <td>選取訪客重新進入活動時看到的體驗：
    <ul>
     <li>相同體驗</li>
     <li>隨機體驗</li>
     <li>未見的體驗</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>增加計數、釋出使用者並禁止重新進入</strong></td>
   <td>決定使用者會看到什麼而非活動內容：
    <ul>
     <li>相同的體驗，無追蹤</li>
     <li>預設內容或其他活動內容</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

另請參閱 [Adobe Target檔案](https://experienceleague.adobe.com/docs/target/using/activities/success-metrics/success-metrics.html) 以取得成功量度的詳細資訊。

### 設定設定(AEM鎖定目標) {#configuring-settings-aem-targeting}

若要在使用AEM定位時進行設定：

1. 若要指定活動開始的時間，請使用 **開始** 下拉式功能表以選取下列其中一個值：

   * **啟用時**：活動從包含目標內容的頁面啟動時開始。
   * **指定的日期和時間**：特定時間。 选择此选项时，单击或点按日历图标，选择日期，然后指定活动开始的时间。

1. 若要指定活動結束的時間，請使用 **結束** 下拉式功能表以選取下列其中一個值：

   * **停用時**：活動會在包含目標內容的頁面停用時結束。
   * **指定的日期和時間**：特定時間。 選取此選項時，按一下或點選日曆圖示，選取日期，並指定活動結束時間。

1. 若要指定活動的優先順序，請使用滑桿來選取 **低**， **一般**，或 **高**.

### 設定目標與設定(Adobe Target) {#configuring-goals-settings-adobe-target}

若要在使用Adobe Target時設定目標與設定：

1. 若要指定活動開始的時間，請使用 **開始** 下拉式功能表以選取下列其中一個值：

   * **啟用時**：活動從包含目標內容的頁面啟動時開始。
   * **指定的日期和時間**：特定時間。 选择此选项时，单击或点按日历图标，选择日期，然后指定活动开始的时间。

1. 若要指定活動結束的時間，請使用 **結束** 下拉式功能表以選取下列其中一個值：

   * **停用時**：活動會在包含目標內容的頁面停用時結束。
   * **指定的日期和時間**：特定時間。 選取此選項時，按一下或點選日曆圖示，選取日期，並指定活動結束時間。

1. 若要指定活動的優先順序，請使用滑桿來選取 **低**， **一般**，或 **高**.
1. 如果您已使用Adobe Target帳戶設定Adobe Analytics，則會看到 **報表來源** 下拉式功能表。 选 **择Adobe Target****或Adobe Analytics** 作为源。

   如果您選取 **Adobe Analytics**，選取公司和報表套裝。 如果您選取 **Adobe Target**，無需採取任何動作。

   ![chlimage_1-33](assets/chlimage_1-33.png)

1. 在“目 **标量度** ”区域的“我的主要目标 **** ”下，选择要跟踪的成功量度——转化率、收入、参与度——并输入度量的度量方式（或受众采取什么操作指示已达到目标）。 请参阅上表中目标量度的定义，并参阅 [Adobe Target成功量度相关文档](https://experienceleague.adobe.com/docs/target/using/activities/success-metrics/success-metrics.html) 。

   您可以通过单击右上角的三个圆点，然后选择&#x200B;**重命名**&#x200B;来重命名目标。

   如果需要清除所有字段，请单击右上角的三个圆点，然后选择&#x200B;**清除所有字段**。

   所有量度都有您可以定義的進階設定。 選取 **進階設定** 以存取這些。 请参阅上一个表中的成功量度计数方式的定义以及 [Adobe Target 文档](https://experienceleague.adobe.com/docs/target/using/activities/success-metrics/success-metrics.html)。

   >[!NOTE]
   您必须至少定义一个目标。

   ![chlimage_1-34](assets/chlimage_1-34.png)

   >[!NOTE]
   如果您的量度中遺漏資訊，會在量度周圍加上紅線。

1. 按一下 **新增量度** 以設定其他成功量度。

   ![chlimage_1-35](assets/chlimage_1-35.png)

   >[!NOTE]
   您可以按一下或點選三個點，然後按一下或點選，以移除其他目標 **刪除**. AEM要求您至少定義一個目標。

1. 如果您想要更好地控制成功量度的计数方式，请单击或点按&#x200B;**高级设置**&#x200B;以访问相应的设置。
1. 单击&#x200B;**保存**。

設定後，您可以 [檢視活動績效](/help/sites-authoring/activitylib.md#viewing-performance-and-converting-winning-experiences-a-b-test) 使用Adobe Target （體驗或A/B測試鎖定目標）的客戶。 此外，透過A/B測試鎖定目標，您可以 [轉換獲勝者。](/help/sites-authoring/activitylib.md#viewing-performance-and-converting-winning-experiences-a-b-test)

## 模擬體驗 {#simulating-an-experience}

模擬訪客的體驗，以確認頁面內容會根據目標內容的設計如預期般顯示。 模擬時，載入不同的使用者設定檔，然後檢視該使用者的目標內容。

下列條件決定模擬訪客體驗時顯示的內容：

* 使用者工作階段存放區中的資料（透過Context Hub）。
* 此 [活動位於](/help/sites-authoring/activitylib.md).
* 此 [定義區段的規則](/help/sites-administering/campaign-segmentation.md).
* Target元件中的體驗內容。
* 此 [目標定位引擎的設定](/help/sites-authoring/activitylib.md).

如果您在載入設定檔時頁面上出現非預期的內容，請檢查此清單中每個專案的設定。

>[!NOTE]
如果您使用A/B測試，模擬體驗時將會根據流量百分比顯示。 這項操作由Adobe Target控制，可能會對作者造成非預期的結果。 (作者活動會與特定設定同步，以便在模擬期間重新評估(_A)。) 作者可能需要重新整理，才能根據其流量設定檢視其他體驗。

若要模擬訪客的體驗，請使用下列工具：

* 鎖定目標模式下的模擬活動：頁面會顯示目前在Context Hub中選取之使用者的選件。 您可以編輯以使用者為目標的選件。
* 預覽模式：使用Context Hub選取符合您的體驗所根據之區段條件的使用者和位置。 當您的Context Hub選擇變更時，目標內容會相應變更。

1. 要切换到预览模式，请在工具栏中单击或点按&#x200B;**预览**。
1. 在工具栏上，单击或点按 Context Hub 图标。

   ![](do-not-localize/chlimage_1-7.png)

1. 使用Context Hub變更內容屬性。 例如，按一下或點選Persona屬性以選取其他使用者。

   ![chlimage_1-36](assets/chlimage_1-36.png)

   頁面會變更，顯示目前內容的目標內容。

1. 若要變更顯示的選件，請切換至鎖定目標模式。 選取模擬活動後，編輯您在「預覽」模式中設定的內容選件。

## 設定Target元件選項 {#configuring-target-component-options}

您可以透過下列兩種方式之一存取元件的選項來自訂Target元件：

1. 將元件設為目標後，在Target元件中，按一下或點選元件，然後按一下設定圖示(cog)。

   ![](do-not-localize/chlimage_1-8.png)

   AEM 随即会显示 Target 组件选项窗口。

   ![chlimage_1-37](assets/chlimage_1-37.png)

1. 或者，要在全屏模式下访问这些设置，请在 Target 组件选项窗口中，单击或点按全屏图标。

   ![](do-not-localize/chlimage_1-9.png)

   AEM 随即会显示 Target 组件选项全屏窗口。

   ![chlimage_1-38](assets/chlimage_1-38.png)

1. 请按下表中所述配置 Target 组件设置。

<table>
 <tbody>
  <tr>
   <td><strong>选项</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td><strong>位置</strong></td>
   <td><p>位置是一个字符串，它为目标内容位置提供一个名称，并将选件与其在页面上的放置位置（或组件）连接起来。</p> <p>此字段是一个通用值。</p> <p>如果您将选件放置在某个组件中，则选件会记住位置 ID。執行頁面時，引擎會評估使用者的區段，並據此解析應顯示的作用中行銷活動的體驗。 然後，它會檢查頁面上的位置ID，並嘗試將選件與對應的位置ID進行比對。</p> </td>
  </tr>
  <tr>
   <td><strong>引擎</strong></td>
   <td>選擇範圍 <strong>使用者端規則（不追蹤）、Adobe Target、ContextHub、 </strong>和<strong> Adobe Campaign </strong>視您要使用的引擎而定。</td>
  </tr>
 </tbody>
</table>

如果选择 Adobe Target 作为引擎：

![chlimage_1-39](assets/chlimage_1-39.png)

<table>
 <tbody>
  <tr>
   <td><strong>选项</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td><strong>准确定位</strong></td>
   <td><p>启用“准确定位”可告知组件等到客户端上下文或上下文中心数据可用之后，再将请求发送到 Adobe Target。这可能会增加加载时间。在创作时，“准确定位”始终处于启用状态。</p> <p>如果您選取 <strong>準確定位</strong> 核取方塊，mbox會執行 <code>mboxDefine</code> 第一個和 <code>mboxUpdate</code> 之後，會在資料可供使用時產生Ajax請求。</p> <p>如果您未選取 <strong>準確定位</strong> 核取方塊，mbox會執行 <code>mboxCreate</code> 立即產生同步請求（在此情況下，可能尚未提供所有內容資料）。</p> <p><strong>注意：</strong> 啟用或停用特定元件的準確定位不會影響您全域設定的設定。 您始终可以通过在组件中选择“准确定位”来覆盖全局设置。</p> </td>
  </tr>
  <tr>
   <td><strong>包含已解析的区段</strong></td>
   <td><p>选中此复选框可包括 mbox 调用中的所有已解析的区段以及页面和框架中配置的任何参数。</p> <p>这仅适用于通过 XML API 同步 AEM 区段的情况。如果您的 AEM 中存在不由 Adobe Target 处理的区段（如脚本区段），则此选项允许您在 AEM 中解析这些区段，并发送信息告知 Adobe Target 这些区段处于活动状态。</p> </td>
  </tr>
  <tr>
   <td><strong>继承的上下文参数</strong></td>
   <td>列出从 Adobe Target 框架继承的与所选页面关联的上下文参数（如果有）。</td>
  </tr>
  <tr>
   <td><strong>上下文参数</strong></td>
   <td>按一下或點選 <strong>新增欄位</strong> 以設定其他內容引數（與Target架構中可用的引數相同）。 已新增到元件的內容引數適用 <i>僅限</i> 至元件，而不是至其他元件，如果您直接將內容引數新增至框架，就會發生這種情況。</td>
  </tr>
  <tr>
   <td><strong>静态参数</strong></td>
   <td>按一下或點選 <strong>新增欄位</strong> 以設定其他靜態引數（與Target架構中可用的引數相同）。 套用新增至元件的靜態引數 <i>僅限</i> 至元件，而非至其他元件，如果您直接將靜態引數新增至架構，就會發生這種情況。 静态参数不是来自于上下文（内容中心的客户端上下文）。</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
當您選取元件並使其可鎖定目標時，AEM也會取代該元件並插入Adobe Target元件。 (Adobe Target元件不僅會在您手動新增至頁面時使用，也會在鎖定現有元件為目標時使用。)

如果您選取Client Context (client side)作為引擎：

![chlimage_1-40](assets/chlimage_1-40.png)

<table>
 <tbody>
  <tr>
   <td><strong>选项</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td><strong>使用者端的選項 — 策略</strong></td>
   <td><p>從下列任一項中選取：</p>
    <ul>
     <li><strong>第一個</strong>：清單中最上層的體驗，如行銷活動中所排序。</li>
     <li><strong>Random</strong>：使用任何體驗。</li>
     <li><strong>點按資料流分數</strong>：使用在使用者端內容中追蹤的標籤和相關標籤點選。 系統會比較Teaser頁面上定義之標籤的點選率。</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

如果要将 AEM 与 Adobe Campaign 集成，请选择 **Adobe Campaign** 作为引擎。另請參閱 [將AEM與Adobe Campaign整合](/help/sites-administering/campaign.md) 以取得詳細資訊。

如果要使用 ContextHub 进行定位，请选择 **ContextHub** 作为引擎。另請參閱 [正在設定ContextHub。](/help/sites-developing/ch-configuring.md)
