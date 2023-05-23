---
title: 編輯內容頁面屬性
description: 为页面定义所需的属性.
uuid: d3a2183b-8082-4cfc-aeed-26facbf3f3e6
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 1e9dd0d7-209a-4989-b66b-bca0d04b437a
docset: aem65
exl-id: 3cd9374f-6f16-40fb-97cf-5f9a750b8dd2
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '1885'
ht-degree: 61%

---

# 编辑页面属性{#editing-page-properties}

您可以为页面定义所需的属性。这些属性会因页面性质而异。例如，某些页面可能会连接到 Live Copy，而其他页面则可能不会，Live Copy 信息将在适当情况下才可用。

## 页面属性 {#page-properties}

属性分布于多个选项卡中。

### 基本 {#basic}

* **标题**

   頁面的標題會顯示在各種位置。 例如， **網站** 索引標籤清單和 **網站** 卡片/清單檢視。

   这是必填字段。

* **标记**

   您可以在此處更新選取方塊中的清單，從頁面新增或移除標籤：

   * 选择标记后，它会列在选择框下。您可以使用“x”从此列表中移除标记。
   * 可通过在空白选择框中键入名称输入全新标记。

      * 按 Enter 将创建新标记。
      * 随后将会显示新标记，其右侧带有一个小星星，表示该标记为新标记。
   * 使用下拉列表功能，可从现有标记中进行选择。
   * 当您将鼠标悬停在选择框中的标记条目上时，会显示 x，用于为此页面删除该标记。

   有关标记的更多信息，请访问[使用标记](/help/sites-authoring/tags.md)。

* **隐藏导航**

   指示在生成的站点的页面导航中是显示还是隐藏页面。

* **品牌化**

   通过将品牌概要附加到每个页面标题，跨页面应用一致的品牌识别。此功能需要使用 2.14.0 版或更高版本的[核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hans)中的页面组件。

   * **覆盖** – 选中可在此页面上定义品牌概要。
      * 该值将由任何子页面继承，除非它们也设置了&#x200B;**覆盖**&#x200B;值。
   * **覆盖值** – 要附加到页面标题的品牌概要的文本。
      * 该值附加到页面标题后的竖线字符后，例如“骑行 Tuscany | 始终准备好使用 WKND”
* **页面标题**

   頁面上使用的標題。 通常由标题组件使用。如果留空，则将使用&#x200B;**标题**。

* **导航标题**

   您可以指定個別標題以在導覽中使用（例如，如果您想要更簡潔的內容）。 如果為空， **標題** 將會使用。

* **子标题**

   頁面上使用的副標題。

* **描述**

   頁面的說明、用途或您要新增的任何其他詳細資訊。

* **开始时间**

   啟動已發佈頁面的日期和時間。 發佈後，此頁面將保持休眠狀態，直到指定的時間。

   對於您要立即發佈的頁面（一般情境），請將這些欄位留空。

* **结束时间**

   已發佈頁面將停用的時間。

   同樣地，請將這些欄位留空以便立即採取行動。

* **虚 URL**

   允许您输入此页面的虚 URL，以便使用更短并且/或者含意更清楚的 URL。

   例如，如果虛名URL設為 `welcome`至路徑所識別的頁面 `/v1.0/startpage`適用於網站 `http://example.com,` 則 `http://example.com/welcome`會是虛名URL `http://example.com/content/v1.0/startpage`

   >[!CAUTION]
   >
   >虚 URL：
   >
   >* 必须是唯一的，因此您应该确保该值没有被其他页面使用。
   >* 不支持正则表达式模式。
   >* 不应设置为现有页面。


   您也需要設定Dispatcher以啟用對虛名URL的存取權。 另請參閱 [啟用對虛名URL的存取權](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#enabling-access-to-vanity-urls-vanity-urls) 以取得更多詳細資料。

* **重定向虚 URL**

   指示您是否希望页面使用虚 URL。

### 高级 {#advanced}

* **语言**

   頁面語言。

* **语言根目录**

   如果頁面是語言副本的根目錄，則必須核取。

* **重定向**

   指出此頁面應該自動重新導向的頁面。

* **Design**

   指出 [設計](/help/sites-developing/designer.md) 用於此頁面。

* **别名**

   指定要用於此頁面的別名。

   * 例如，如果您为页面 `/content/wknd/us/en/magazine/members-only` 定义别名 `private`，则也可以通过 `/content/wknd/us/en/magazine/private` 访问此页面
   * 创建别名将设置页面节点上的 `sling:alias` 属性，这只会影响资源，而不会影响存储库路径。
   * 无法发布编辑器中按别名处理的页面。编辑器中的[发布选项](/help/sites-authoring/publishing-pages.md)仅适用于通过其实际路径访问的页面。
   * 有关详细信息，请参阅[“SEO 和 URL 管理最佳实践”下的“本地化的页面名称”](/help/managing/seo-and-url-management.md#localized-page-names)。

* **繼承自&lt;*路徑*>**

   指示頁面是否繼承。 以及從何處取得。

* **云配置**

   設定的路徑。

* **允许的模板**

   [定義可用的範本清單](/help/sites-authoring/templates.md#allowingatemplate) 在此支行內。

* **啟用** （驗證需求）

   啟用（或停用）使用驗證來存取頁面。

   >[!NOTE]
   >
   >已关闭的用户组在&#x200B;**[权限](/help/sites-authoring/editing-page-properties.md#permissions)**&#x200B;选项卡上定义。

   >[!CAUTION]
   >
   >此 **[許可權](/help/sites-authoring/editing-page-properties.md#main-pars-procedure-949394300)** 索引標籤可讓您根據以下專案是否存在，編輯CUG設定： `granite:AuthenticationRequired` mixin. 如果頁面許可權是透過已棄用的CUG設定進行設定，需依據是否存在 `cq:cugEnabled` 屬性，底下將顯示警告訊息 **驗證需求** 且選項將不可編輯，也不會編輯 [許可權](/help/sites-authoring/editing-page-properties.md#permissions) 可編輯。
   >
   >
   >在這種情況下，必須在以下位置編輯CUG許可權： [傳統UI](/help/sites-classic-ui-authoring/classic-page-author-edit-page-properties.md).

* **登录页面**

   用於登入的頁面。

* **导出配置**

   指定匯出設定。

### 缩略图 {#thumbnail}

顯示頁面縮圖影像。 您可以：

* **生成预览**

   產生頁面預覽，以做為縮圖使用。

* **上传图像**

   上傳要當作縮圖的影像。

* **选择图像**

   選取現有資產以用作縮圖。

* **还原**

   在您變更縮圖後，此選項就會變為可用。 如果不想保留您的更改，可以在保存前还原更改。

### 社交媒体 {#social-media}

* **社交媒体共享**

   定義頁面上可用的共用選項。 顯示以下專案可用的選項： [共用核心元件](https://helpx.adobe.com/experience-manager/core-components/using/sharing.html).

   * **啟用Facebook的使用者共用**
   * **啟用Pinterest的使用者共用**
   * **首选体验片段变体**
定义用于为页面生成元数据的体验片段变体

### Cloud Service {#cloud-services}

* **Cloud Service**

   定義屬性 [雲端服務](/help/sites-developing/extending-cloud-config.md).

### 个性化 {#personalization}

* **ContextHub 配置**

   選取 [ContextHub設定](/help/sites-developing/ch-configuring.md) 和 [區段路徑](/help/sites-administering/segmentation.md).

* **定位配置**

   选择一个[品牌以指定定位的范围](/help/sites-authoring/target-adobe-campaign.md)。

   >[!NOTE]
   >此选项要求用户帐户属于 `Target Adminstrators` 组。

### 权限 {#permissions}

* **权限**

   在此索引標籤中，您可以：

   * [添加权限](/help/sites-administering/user-group-ac-admin.md)
   * [编辑已关闭的用户组](/help/sites-administering/cug.md#applying-your-closed-user-group-to-content-pages)

   * 查看[有效权限](/help/sites-administering/user-group-ac-admin.md)
   >[!CAUTION]
   >
   >此 **許可權** 索引標籤可讓您根據以下專案是否存在，編輯CUG設定： `granite:AuthenticationRequired` mixin. 如果頁面許可權是透過已棄用的CUG設定進行設定，需依據是否存在 `cq:cugEnabled` 屬性，則會顯示警告訊息，且CUG許可權將不可編輯，驗證需求也不會顯示於 [進階](/help/sites-authoring/editing-page-properties.md#advanced) 標籤可編輯。
   >
   >
   >在這種情況下，必須在以下位置編輯CUG許可權： [傳統UI](/help/sites-classic-ui-authoring/classic-page-author-edit-page-properties.md).

   >[!NOTE]
   >
   >「許可權」索引標籤不允許建立空的CUG群組，這是拒絕存取每個使用者的簡單方式，會很實用。 若要這麼做，必須使用CRX Explorer。 檢視檔案 [使用者、群組和存取許可權管理](/help/sites-administering/user-group-ac-admin.md) 以取得詳細資訊。

### Blueprint {#blueprint}

* **Blueprint**

   在中定義Blueprint頁面的屬性 [多網站管理](/help/sites-administering/msm.md). 控制將修改傳播至即時副本的情況。

### Live Copy {#live-copy}

* **Live Copy**

   在中定義即時副本頁面的屬性 [多網站管理](/help/sites-administering/msm.md). 控制從Blueprint傳播修改的情況。

### 站点结构 {#site-structure}

* 提供具有全站点功能的页面的链接，例如&#x200B;**注册页面**、**脱机页面**&#x200B;以及其他。

## 编辑页面属性 {#editing-page-properties-1}

您可以定義頁面屬性：

* 从&#x200B;**站点**&#x200B;控制台中：

   * [创建一个新页面](/help/sites-authoring/managing-pages.md#creating-a-new-page)（一部分属性）

   * 单击或点按&#x200B;**属性**

      * 单页面
      * 多个页面（只有一部分属性可用于整体编辑）

* 从页面编辑器中：

   * 使用&#x200B;**页面信息**（然后&#x200B;**打开属性**）

### 从“站点”控制台中 – 单个页面 {#from-the-sites-console-single-page}

单击或点按&#x200B;**属性**&#x200B;以定义页面属性：

1. 使用&#x200B;**站点**&#x200B;控制台，导航到要查看和编辑属性的页面位置。

1. 使用以下任一方式为所需的页面选择&#x200B;**属性**&#x200B;选项：

   * [快速操作](/help/sites-authoring/basic-handling.md#quick-actions)
   * [选择模式](/help/sites-authoring/basic-handling.md#selectionmode)

   此时将使用相应的选项卡显示页面属性。

1. 查看或编辑所需的属性。

1. 然后，使用&#x200B;**保存**&#x200B;来保存您的更新，接着使用&#x200B;**关闭**&#x200B;返回到控制台。

### 编辑页面时 {#when-editing-a-page}

在编辑页面时，您可以使用&#x200B;**页面信息**&#x200B;来定义页面属性：

1. 打开要编辑属性的页面。

1. 选择&#x200B;**页面信息**&#x200B;图标以打开选择菜单：

   ![screen_shot_2018-03-22at095740](assets/screen_shot_2018-03-22at095740.png)

1. 選取 **開啟屬性** 而且會開啟對話方塊，讓您編輯屬性（依適當的索引標籤排序）。 工具栏右侧还提供以下按钮：

   * **取消**
   * **保存并关闭**

1. 使用&#x200B;**保存并关闭**&#x200B;按钮以保存更改。

### 从“站点”控制台中 – 多个页面 {#from-the-sites-console-multiple-pages}

从&#x200B;**“站点”**&#x200B;控制台中，您可以选择多个页面，然后使用&#x200B;**查看属性**，查看和／或编辑页面属性。 这称为批量编辑页面属性。

>[!NOTE]
>
>也可以对资产使用批量编辑属性功能。其操作大体相同，只有少数几点差别。另請參閱 [編輯多個資產的屬性](/help/assets/metadata.md) 以取得詳細資訊。
>
>此外， [大量編輯器](/help/sites-administering/bulk-editor.md)，可讓您使用GQL (Google查詢語言)從多個頁面搜尋內容，然後直接在大量編輯器中編輯內容，再將變更儲存至原始頁面。

可以通过多种方法选择要批量编辑的多个页面，这些方法包括：

* 在浏览 **Sites** 控制台时
* 在使用&#x200B;**搜索**&#x200B;找到一组页面后

![epp-01](assets/epp-01.png)

选择页面后，单击或点按&#x200B;**属性选项**，此时将会显示批量属性：

![epp-02](assets/epp-02.png)

只有符合以下条件的页面才能进行批量编辑：

* 属于同一资源类型
* 不是 Live Copy 的一部分

   * 如果有任何页面在 Live Copy 中，将会在属性打开时显示一条消息。

进入“批量编辑”后，您可以：

* **查看**

   檢視多個頁面的頁面屬性時，您可以看到：

   * 受影响的页面列表

      * 您可以根据需要进行选择/取消选择
   * 选项卡

      * 与查看单页面的属性时一样，这些属性按选项卡进行排序。
   * 一部分属性

      * 将显示所有选定页面的可用属性，这些属性已明确定义为可批量编辑。
      * 如果将选择的页面减少到一页，则会显示所有属性。
   * 具有相同值的通用属性

      * 在“查看”模式中，只显示具有相同值的属性。
      * 当字段有多个值时（例如“标记”），只有在&#x200B;*所有值*&#x200B;均相同的情况下，才会显示这些值。如果只有部分值相同，则仅在编辑时才显示它们。

   如果不存在具有相同值的属性，则会显示一条消息。

* **编辑**

   編輯多個頁面的頁面屬性時：

   * 您可以更新可用字段中的值。

      * 当您选择&#x200B;**完成**&#x200B;时，新值将会应用于所有选定页面。
      * 当字段有多个值时（例如“标记”），您可以附加一个新值，也可以删除相同的值。
   * 如果不同页面具有相同的字段，但这些字段的值不同，则会用一个特殊的值表示它们，例如，文本 `<Mixed Entries>`。


>[!NOTE]
>
>可以对页面组件进行配置，以指定可批量编辑的字段。另請參閱 [設定頁面以大量編輯頁面屬性](/help/sites-developing/bulk-editing.md).
