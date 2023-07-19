---
title: 在中搜索数字资源和图像 [!DNL Adobe Experience Manager]
description: 了解如何在中查找所需的资产 [!DNL Adobe Experience Manager] 使用“筛选器”面板，以及如何使用搜索中显示的资源。
contentOwner: AG
mini-toc-levels: 1
feature: Search, Metadata
role: User
exl-id: 588433b2-564a-430f-9d04-480465ece2ad
hide: true
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '5739'
ht-degree: 5%

---

# 搜索中的数字资产 [!DNL Adobe Experience Manager] {#search-assets-in-aem}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/search-assets.html?lang=en) |
| AEM 6.5 | 本文 |

[!DNL Adobe Experience Manager Assets] 提供强大的资源发现方法，帮助您实现更高的内容速度。 您的团队可以使用开箱即用的功能和自定义方法，通过无缝、智能的搜索体验缩短上市时间。 搜索资产对于数字资产管理系统的使用至关重要，无论它是供创意人员进一步使用、供业务用户和营销人员稳健管理资产，还是DAM管理员进行管理。 您可以通过执行的简单、高级和自定义搜索 [!DNL Assets] 用户界面或其他应用程序和表面有助于完成这些用例。

[!DNL Experience Manager Assets] 支持以下用例，本文介绍这些用例的使用、概念、配置、限制和疑难解答。

| 搜索资源 | 配置和管理搜索功能 | 使用搜索结果 |
|---|---|---|
| [基本搜索](#searchbasics) | [搜索索引](#searchindex) | [排序结果](#sort) |
| [了解搜索用户界面](#searchui) | [视觉或相似性搜索](#configvisualsearch) | [检查资源的属性和元数据](#checkinfo) |
| [搜索建议](#searchsuggestions) | [必需元数据](#mandatorymetadata) | [下载](#download) |
| [了解搜索结果和行为](#searchbehavior) | [修改搜索彩块化](#searchfacets) | [批量元数据更新](#metadataupdates) |
| [搜索排名和提升](#searchrank) | [文本提取](#extracttextupload) | [智能收藏集](#collections) |
| [高级搜索：筛选条件和搜索范围](#scope) | [自定义谓词](#custompredicates) | [了解意外结果并排除其故障](#unexpected-results) |
| [从其他解决方案和应用程序进行搜索](#search-assets-other-surfaces)：<ul><li>[Adobe Asset Link](#aal)</li><li>[Brand Portal](#brand-portal)</li><li>[Experience Manager桌面应用程序](#desktop-app)</li><li>[Adobe Stock图像](#adobe-stock)</li><li>[Dynamic Media资源](#dynamic-media)</li></ul> | | |
| [资源选择器](#asset-picker) | | |
| [限制](#limitations) 和 [提示](#tips) | | |
| [说明示例](#samples) | | |

使用顶部的Omnisearch字段搜索数字资产 [!DNL Experience Manager] Web界面。 转到 **[!UICONTROL 资产]** > **[!UICONTROL 文件]** 在 [!DNL Experience Manager]，单击 ![search_icon](assets/do-not-localize/search_icon.png) 在顶部栏中，输入搜索关键字，然后选择 `Return`. 或者，使用关键字快捷键 `/` （正斜杠）以打开Omnisearch字段。 `Location:Assets` 已预选中，以将搜索限制在DAM资产。 [!DNL Experience Manager] 在开始键入搜索关键词时提供建议。

使用 **[!UICONTROL 筛选器]** 用于搜索资源、文件夹、标记和元数据的面板。 您可以根据各种选项（谓词）筛选搜索结果，例如文件类型、文件大小、上次修改日期、资源状态、分析数据和Adobe Stock许可。 您可以自定义“筛选器”面板，并使用添加或删除搜索谓词 [搜索Facet](/help/assets/search-facets.md). 此 [!UICONTROL 文件类型] 在中筛选 [!UICONTROL 筛选器] 面板具有混合状态复选框。 因此，除非选择所有嵌套的谓词（或格式），否则将部分选中第一级复选框。

[!DNL Experience Manager] 搜索功能支持搜索收藏集和搜索收藏集中的资产。 参见 [搜索收藏集](/help/assets/manage-collections.md).

## 了解搜索界面 {#searchui}

熟悉搜索界面和可用的操作。

![了解Experience Manager Assets搜索结果界面](assets/aem_search_results.png)

*图：了解 [!DNL Experience Manager Assets] 搜索结果界面。*

**答：** 将搜索另存为智能收藏集。 **B.** 用于缩小搜索结果的过滤器或谓词。 **C.** 显示文件、文件夹或两者。 **D.** 单击“过滤器”以打开或关闭左边栏。**E.** 搜索位置为 DAM。**F.** 具有用户提供的搜索关键字的Omnisearch字段。 **G.** 选择加载的搜索结果。 **H.** 在搜索结果总数中显示的搜索结果数。 **我。** 关闭搜索。 **J.** 在卡片视图和列表视图之间切换。

### 动态搜索Facet {#dynamicfacets}

您可以使用搜索Facet中动态更新的预期搜索结果数，更快地从搜索结果页面发现所需的资产。 即使在应用搜索过滤器之前，也会更新预期的资源数。 查看筛选器的预期计数可帮助您快速高效地浏览搜索结果。

![查看搜索Facet中不筛选搜索结果的大致资源数。](assets/asset_search_results_in_facets_filters.png)

*图：在搜索Facet中查看未筛选搜索结果的大致资源数。*

## 了解搜索结果和行为 {#searchbehavior}

### 基本搜索词和结果 {#searchbasics}

您可以从OmniSearch字段运行关键字搜索。 关键词搜索不区分大小写，是一种全文搜索（跨常用元数据字段）。 如果使用多个关键字， `AND` 是关键字之间的默认运算符。

结果按相关性排序，从最接近的匹配项开始。 对于多个关键词，更相关的结果是在其元数据中包含这两个术语的资源。 在元数据中，显示为智能标记的关键字的排名高于显示在其他元数据字段中的关键字。 [!DNL Experience Manager] 允许为特定搜索词赋予更高的权重。 此外，还可以 [提升排名](#searchrank) 特定搜索词的几个目标资产中。

为了快速找到相关资产，丰富的界面提供了筛选、排序和选择机制。 您可以根据多个条件筛选结果，并查看各种筛选条件的搜索资源数。 或者，您可以通过更改Omnisearch字段中的查询来重新运行搜索。 当您更改搜索词或筛选器时，其他筛选器仍将应用，以保留您的搜索上下文。

当结果中有许多资产时， [!DNL Experience Manager] 在卡片视图中显示前100个，在列表视图中显示前200个。 用户滚动时，会加载更多资源。 这是为了改进性能。 观看视频演示 [显示的资源数](https://www.youtube.com/watch?v=LcrGPDLDf4o).

有时，您可能会在搜索结果中看到一些意外的资产。 有关更多信息，请参阅 [意外结果](#unexpected-results).

[!DNL Experience Manager] 可以搜索多种文件格式，并且可以自定义搜索过滤器以满足您的业务要求。 请联系您的管理员，了解您的DAM存储库有哪些搜索选项可用，以及您的帐户有哪些限制。

### 使用和不使用增强型智能标记的结果 {#withsmarttags}

默认情况下， [!DNL Experience Manager] 搜索将搜索词与AND子句组合在一起。 例如，考虑搜索关键词woman running。 默认情况下，只有元数据中同时包含女性和运行关键字的资源才会显示在搜索结果中。 当关键字中使用特殊字符（句点、下划线或破折号）时，将保留相同的行为。 以下搜索查询返回相同的结果：

* `woman running`
* `woman.running`
* `woman-running`

但是，查询 `woman -running` 返回不包含 `running` 在其元数据中。
使用智能标记会额外添加 `OR` 子句查找任何搜索词作为应用的智能标记。 使用任一标记进行标记的资产 `woman` 或 `running` 使用智能标记也会出现在此类搜索查询中。 所以搜索结果是，

* 具有的资产 `woman` 和 `running` 元数据中的关键字（默认行为）。

* 使用任一关键字进行智能标记的资产（智能标记行为）。

### 键入内容时搜索建议 {#searchsuggestions}

当您开始键入关键字时， [!DNL Experience Manager] 建议可能的搜索关键字或短语。 这些建议基于现有资源的元数据。 [!DNL Experience Manager] 对所有元数据字段编制索引以帮助搜索。 为了提供搜索建议，系统使用以下几个元数据字段的值。 要提供搜索建议，请考虑使用相应的关键字填充以下字段：

* 资产标记。 (映射到 `jcr:content/metadata/cq:tags`)
* 资源标题。 (映射到 `jcr:content/metadata/dc:title`)
* 资源描述。 (映射到 `jcr:content/metadata/dc:description`)
* JCR存储库中的标题。 该值可能会映射到资源标题。 (映射到 `jcr:content/jcr:title`)
* JCR存储库中的描述。 该值可能会映射到资源描述。 (映射到 `jcr:content/jcr:description`)

要接收多个搜索关键字的建议，请继续键入所有关键字，而不为单个关键字选择任何建议。

![键入多个关键字以查看适合所有关键字的建议](assets/search_suggestionsmanykeywords.gif)

*图：键入多个关键字以查看适合所有关键字的建议。*

### 搜索排名和提升 {#searchrank}

首先显示与元数据字段中的所有搜索词匹配的搜索结果，随后显示与智能标记中的任何搜索词匹配的搜索结果。 在上例中，搜索结果的大致显示顺序为：

1. 匹配项 `woman running` 在各个元数据字段中。
1. 匹配项 `woman running` 在智能标记中。
1. 匹配项 `woman` 或 `running` 在智能标记中。

您可以提高特定资产的关键字相关性，以帮助基于关键词提升搜索量。 换言之，当您基于这些关键词进行搜索时，促销特定关键词的图像会显示在搜索结果的顶部。

1. 从 [!DNL Assets] 用户界面中，打开资产的属性页面。 单击 **[!UICONTROL 高级]** 并单击 **[!UICONTROL 添加]** 下 **[!UICONTROL 提升搜索关键词]**.
1. 在 **[!UICONTROL 搜索提升]** 框中，指定要增加图像搜索的关键字，然后单击 **[!UICONTROL 添加]**. 您可以按相同方式指定多个关键字。
1. 单击“**[!UICONTROL 保存并关闭]**”。您针对此关键字提升的资产会出现在排名最前的搜索结果中。

您可以使用它来提升目标关键词搜索结果中某些资产的排名，这对您有利。 请观看下面的示例视频。 有关详细信息，请参阅 [搜索范围 [!DNL Experience Manager]](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/search-and-discovery/search-boost.html).

>[!VIDEO](https://video.tv.adobe.com/v/16766/?quality=6)

*视频：了解搜索结果的排名方式以及排名会受到何种影响。*

## 高级搜索 {#scope}

[!DNL Experience Manager] 提供了多种方法（如适用于搜索到的资产的过滤器），以帮助您更快地找到所需的资产。 下面介绍了一些常用方法。 部分 [说明示例](#samples) 将在下面共享。

**搜索文件或文件夹**：在搜索结果中，查看文件和/或文件夹。 起始日期 **[!UICONTROL 筛选器]** 面板中，您可以选择相应的选项。 参见 [搜索界面](#searchui).

**在文件夹中搜索资源**：您可以将搜索限制在特定文件夹中。 在 **[!UICONTROL 筛选器]** 面板，添加文件夹的路径。 一次只能选择一个文件夹。

![通过在“筛选器”面板中添加文件夹路径，将搜索结果限制为文件夹](assets/search_folder_select.gif)

*图：通过在“筛选器”面板中添加文件夹路径，将搜索结果限制为文件夹。*

### 查找类似图像 {#visualsearch}

要查找与用户选择的图像视觉上相似的图像，请从图像的卡片视图或工具栏中单击&#x200B;**[!UICONTROL 查找类似]**&#x200B;选项。[!DNL Experience Manager] 显示 DAM 存储库中与用户所选图像相似的智能标记图像。请参阅[如何配置相似性搜索](#configvisualsearch)。

![使用卡片视图中的选项查找类似图像](assets/search_find_similar.png)

*图：使用卡片视图中的选项查找类似图像。*

### Adobe Stock图像 {#adobe-stock}

从 [!DNL Experience Manager] 用户界面，用户可以进行搜索 [Adobe Stock资源](/help/assets/aem-assets-adobe-stock.md) 并许可所需的资产。 添加 `Location: Adobe Stock` 在Omnisearch酒吧。 您还可以使用“筛选器”面板查找所有许可或未许可的资源，或使用Adobe Stock文件号搜索特定资源。

### Dynamic Media资源 {#dmassets}

您可以通过选择&#x200B;**[!UICONTROL 过滤器]**&#x200B;面板中的 **[!UICONTROL Dynamic Media]** > **[!UICONTROL 集]**&#x200B;来过滤 Dynamic Media 图像。该操作可过滤并显示图像集、轮播集、混合媒体集和旋转集等资产。

### 使用元数据字段中的特定值的GQL搜索 {#gql-search}

您可以根据元数据字段（如标题、描述和创建者）的精确值搜索数字资源。 GQL全文搜索功能仅会提取其元数据值与搜索查询完全匹配的资源。 属性的名称（创建者、标题等）和值区分大小写。

| 元数据字段 | Facet值和用法 |
|---|---|
| 标题 | title：John |
| 创建者 | 创建者：John |
| 位置 | location：NA |
| 描述 | description：&quot;示例图像&quot; |
| 创建者工具 | creatortool：&quot;Adobe Photoshop&quot; |
| 版权所有者 | 版权所有：“Adobe Systems” |
| 参与者 | 投稿人：John |
| 使用条款 | 使用条款：“保留复制权利” |
| 创建时间 | created：YYYY-MM-DDTHH |
| 过期日期 | expires：YYYY-MM-DDTHH |
| 准时 | ontime：YYYY-MM-DDTHH |
| 关闭时间 | offtime：YYYY-MM-DDTHH |
| 时间范围(expires dateontime，offtime) | Facet字段：下限……上界 |
| 路径 | /content/dam/&lt;folder name=&quot;&quot;> |
| PDF 标题 | pdftitle：&quot;Adobe文档&quot; |
| 主题 | 主题：“培训” |
| 标记 | 标记：“位置和旅行” |
| 类型 | 类型：&quot;image\png&quot; |
| 图像宽度 | width：lowerbound..上界 |
| 图像高度 | 高度：下限……上界 |
| 人员 | 人员：John |

属性 `path`， `limit`， `size`、和 `orderby` 不能使用以下方式组合 `OR` 运算符和任何其他属性。

<!-- TBD: Where are the limit, size, orderby properties defined?
-->

用户生成的属性的关键字是属性编辑器中的字段标签（小写），其中删除了空格。

以下是复杂查询的搜索格式的一些示例：

* 要显示具有多个Facet字段的所有资源(例如：title=John Doe和创建者工具= Adobe Photoshop)，请执行以下操作： `title:"John Doe" creatortool:Adobe*`
* 当Facet值不是单个单词而是句子时（例如：title=Scott Reynolds）显示所有资产： `title:"Scott Reynolds"`
* 要显示具有单个属性的多个值的资产（例如：title=Scott Reynolds或John Doe），请执行以下操作： `title:"Scott Reynolds" OR "John Doe"`
* 要显示其属性值以特定字符串开头的资产（例如：title是Scott Reynolds），请执行以下操作： `title:Scott*`
* 要显示其属性值以特定字符串结尾的资产（例如：title是Scott Reynolds），请执行以下操作： `title:*Reynolds`
* 要显示其属性值包含特定字符串的资产（例如：title = Basel Meeting Room），请执行以下操作： `title:*Meeting*`
* 要显示包含特定字符串并具有特定属性值的资源(例如：在title=John Doe的资源中搜索字符串Adobe)，请执行以下操作： `*Adobe* title:"John Doe"`

## 从其他搜索数字资产 [!DNL Experience Manager] 产品或界面 {#search-assets-other-surfaces}

[!DNL Adobe Experience Manager] 将DAM存储库连接到其他各种存储库 [!DNL Experience Manager] 提供对数字资产的更快速访问并简化创意工作流的解决方案。 任何资源发现都从浏览或搜索开始。 在各种表面和解决方案中，搜索行为基本上保持不变。 有些搜索方法会随着目标受众、用例和用户界面在中的不同而有所变化。 [!DNL Experience Manager] 解决方案。 通过下面的链接，为各个解决方案记录了具体方法。 本文记录了一些普遍适用的提示和行为。

### 从Adobe资源链接面板搜索数字资源 {#aal}

通过使用AdobeAsset Link，创意专业人士现在可以访问中存储的内容 [!DNL Experience Manager Assets]，无需离开支持的Adobe Creative Cloud应用程序。 创意人员可以使用 [!DNL Adobe Creative Cloud] 应用程序： [!DNL Adobe Photoshop]， [!DNL Adobe Illustrator]、和 [!DNL Adobe InDesign]. Asset Link还允许用户搜索视觉上类似的结果。 可视化搜索显示结果由Adobe Sensei的机器学习算法提供支持，并帮助用户查找在美学上相似的图像。 参见 [搜索和浏览资源](https://helpx.adobe.com/cn/enterprise/using/manage-assets-using-adobe-asset-link.html#UseAdobeAssetLink) 使用AdobeAsset Link。

### 搜索中的数字资产 [!DNL Experience Manager] 桌面应用程序 {#desktop-app}

创意专业人士使用桌面应用程序来 [!DNL Experience Manager Assets] 可轻松搜索并在其本地桌面(Win或Mac)上使用。 创意人员可以轻松地在Mac Finder或Windows资源管理器中显示所需的资源（在桌面应用程序中打开，并在本地更改） — 更改将保存回 [!DNL Experience Manager] 在存储库中创建一个新版本。 该应用程序支持使用一个或多个关键字进行基本搜索， `*` 和 `?` 通配符，和 `AND` 运算符。 参见 [浏览、搜索和预览资源](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#browse-search-preview-assets) 在桌面应用程序中。

### 搜索中的数字资产 [!DNL Brand Portal] {#brand-portal}

业务线用户和营销人员使用Brand Portal与其扩展的内部团队、合作伙伴和经销商高效地安全地共享获得批准的数字资产。 参见 [在Brand Portal上搜索资源](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/search-capabilities/brand-portal-searching.html).

### 搜索 [!DNL Adobe Stock] 图像 {#adobe-stock1}

从 [!DNL Experience Manager] 界面，用户可以搜索Adobe Stock资源并许可所需的资源。 添加 `Location: Adobe Stock` 在Omnisearch字段中。 您还可以使用 **[!UICONTROL 筛选器]** 面板以查找所有许可或未许可的资源，或使用Adobe Stock文件号搜索特定资源。 参见 [管理 [!DNL Adobe Stock] 中的图像 [!DNL Experience Manager]](/help/assets/aem-assets-adobe-stock.md#usemanage).

### 搜索 [!DNL Dynamic Media] 资产 {#dynamic-media}

您可以通过选择&#x200B;**[!UICONTROL 过滤器]**&#x200B;面板中的 **[!UICONTROL Dynamic Media]** > **[!UICONTROL 集]**&#x200B;来过滤 Dynamic Media 图像。该操作可过滤并显示图像集、轮播集、混合媒体集和旋转集等资产。在创作网页时，作者可以在内容查找器中搜索集。弹出菜单中提供集的过滤器。

### 创作网页时在Content Finder中搜索数字资产 {#content-finder}

作者可以使用内容查找器在DAM存储库中搜索相关资产，并在他们创建的网页中使用资产。 作者还可以使用“连接的资产”功能搜索远程可用的资产 [!DNL Experience Manager] 部署。 然后，作者可以在本地的网页中使用这些资源 [!DNL Experience Manager] 部署。 参见 [使用远程资产](/help/assets/use-assets-across-connected-assets-instances.md#use-remote-assets).

### 搜索收藏集 {#collections}

[!DNL Experience Manager] 搜索功能支持搜索收藏集和搜索收藏集中的资产。 参见 [搜索收藏集](/help/assets/manage-collections.md).

## 资源选择器 {#asset-picker}

>[!NOTE]
>
>已调用资源选择器 [资产选取器](https://helpx.adobe.com/experience-manager/6-2/assets/using/asset-picker.html) 在早期版本中 [!DNL Adobe Experience Manager].

资源选择器允许您以特殊方式搜索、筛选和浏览DAM资源。 资源选择器位于 `https://[aem_server]:[port]/aem/assetpicker.html`. 您可以使用资源选择器获取所选资源的元数据。 您可以使用支持的请求参数启动它，例如资源类型（图像、视频、文本）和选择模式（单选或多选）。 这些参数为特定搜索实例设置资源选择器的上下文，并在整个选择过程中保持不变。

资源选择器使用HTML5 `Window.postMessage` 消息以将所选资产的数据发送给收件人。 它仅在浏览模式下工作，并且仅适用于Omnisearch结果页面。

在URL中传递以下请求参数，以在特定上下文中启动资产选择器：

| 名称 | 值 | 示例 | 用途 |
|---|---|---|---|
| 资源后缀(B) | 文件夹路径作为URL中的资源后缀： [https://localhost:4502/aem/assetpicker.html/&lt;folder_path>](https://localhost:4502/aem/assetpicker.html) | 在选中特定文件夹（例如文件夹）的情况下启动资产选择器 `/content/dam/we-retail/en/activities` 选中，则URL应采用以下格式： `https://localhost:4502/aem/assetpicker.html/content/dam/we-retail/en/activities?assettype=images` | 如果在启动资产选择器时要求选择特定文件夹，请将其作为资源后缀传递。 |
| `mode` | 单个，多个 | <ul><li>`https://localhost:4502/aem/assetpicker.html?mode=single`</li><li>`https://localhost:4502/aem/assetpicker.html?mode=multiple`</li></ul> | 在多个模式下，您可以使用资源选择器同时选择多个资源。 |
| `dialog` | true， false | [https://localhost:4502/aem/assetpicker.html?dialog=true](https://localhost:4502/aem/assetpicker.html?dialog=true) | 使用这些参数以Granite对话框形式打开资产选择器。 仅当通过Granite路径字段启动资产选择器，并将其配置为pickerSrc URL时，此选项才适用。 |
| `root` | &lt;folder_path> | `https://localhost:4502/aem/assetpicker.html?assettype=images&root=/content/dam/we-retail/en/activities` | 使用此选项可指定资源选择器的根文件夹。 在这种情况下，资产选择器允许您仅选择根文件夹下的子资产（直接/间接）。 |
| `viewmode` | 搜索 | | 要在搜索模式下启动资产选择器，请执行以下操作 `assettype` 和 `mimetype` 参数。 |
| `assettype` | 图像、文档、多媒体、存档。 | <ul><li>`https://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=images`</li><li> `https://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=documents` </li><li> `https://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=multimedia` </li><li> `https://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=archives` </li></ul> | 使用选项可根据提供的值筛选资源类型。 |
| `mimetype` | MIME类型(`/jcr:content/metadata/dc:format`)（也支持通配符）。 | <ul><li>`https://localhost:4502/aem/assetpicker.html?mimetype=image/png`</li><li>`https://localhost:4502/aem/assetpicker.html?mimetype=*png`</li><li>`https://localhost:4502/aem/assetpicker.html?mimetype=*presentation`</li><li>`https://localhost:4502/aem/assetpicker.html?mimetype=*presentation&mimetype=*png`</li></ul> | 使用它根据MIME类型筛选资源。 |

要访问资源选择器界面，请转到 `https://[aem_server]:[port]/aem/assetpicker`. 导航到所需的文件夹，然后选择一个或多个资源。 或者，从Omnisearch框中搜索所需的资源，根据需要应用过滤器，然后选择该资源。

![在资源选择器中浏览并选择资源](assets/assetpicker.png)

*图：浏览并选择资源选择器中的资源。*

## 限制 {#limitations}

中的搜索功能 [!DNL Experience Manager Assets] 具有以下限制：

* 请勿在搜索查询中输入前导空格，否则搜索不起作用。
* [!DNL Experience Manager] 从搜索结果中选择资产的属性，然后取消搜索后，可以继续显示搜索词。 <!-- (CQ-4273540) -->
* 搜索文件夹或文件和文件夹时，搜索结果无法按任何参数排序。
* 如果您选择 `Return` 不输入Omnisearch栏， [!DNL Experience Manager] 仅返回文件列表，而不返回文件夹列表。 如果您在不使用关键字的情况下专门搜索文件夹， [!DNL Experience Manager] 未返回任何结果。
* 您可以对文件夹执行全文搜索。 指定要使搜索起作用的搜索词。

可视搜索或相似性搜索具有以下限制：

* 可视搜索最适合大型存储库。 虽然没有获得良好结果所需的最小图像数量，但少数图像的匹配质量不如大型存储库中的匹配质量。
* 不能更改模型或训练 [!DNL Experience Manager] 以查找相似图像。 例如，在少数资产中添加或删除智能标记不会更改模型。 资产确实会从视觉上相似的搜索结果中排除。

在以下场景中，搜索功能可能存在性能限制：

* 与列表视图相比，卡片视图的加载时间更短，可显示搜索结果。

## 搜索提示 {#tips}

* 在监控资产的审核状态时，使用相应的选项查找已批准的资产或待批准的资产。
* 使用见解谓词，根据从各种创意应用程序获得的使用情况统计数据，搜索支持的资产。 使用情况数据按使用情况得分、展示次数、点击次数和媒体渠道进行分组，资产在这些渠道中显示类别。
* 使用 **[!UICONTROL 全选]** 复选框，以选择搜索到的资源。 [!DNL Experience Manager] 最初在卡片视图中显示100个资源，在列表视图中显示200个资源。 滚动搜索结果时将加载更多资源。 您可以选择比加载的资源更多的资源。 选定资源的计数显示在搜索结果页面的右上角。 您可以对选择进行操作，例如，下载选定的资源、批量更新选定资源的元数据属性或将选定的资源添加到收藏集。 当选择的资源多于显示的资源时，会对所有选定的资源应用操作，或者会显示一个对话框，显示应用操作的资源数量。 要将操作应用于未加载的资源，请确保已显式选择所有资源。
* 要搜索不包含必需元数据的资源，请参阅 [必需元数据](#mandatorymetadata).
* 搜索使用所有元数据字段。 一般搜索（例如搜索12）通常会返回许多结果。 为了获得更好的结果，请使用双引号（而非单引号）或确保数字与不带特殊字符(例如 `shoe12`)。
* 全文搜索支持运算符，例如 `-` 和 `^`. 要将这些字母搜索为字符串文字，请用双引号将搜索表达式括起来。 例如，使用 `"Notebook - Beauty"` 而不是 `Notebook - Beauty`.
* 如果搜索结果太多，请限制 [搜索范围](#scope) 零入所需的资产。 当您了解如何更好地查找所需资源（例如，特定文件类型、特定位置、特定元数据等）时，此工具将发挥最佳作用。

* **标记**：标记可帮助您对可以更高效地浏览和搜索的资源进行分类。 标记有助于将适当的分类传播给其他用户和工作流程。[!DNL Experience Manager] 提供了一些方法，可使用Adobe Sensei的人工智能服务自动标记资产，从而更好地通过使用和培训来标记资产。 搜索资产时，如果您的帐户中启用了智能标记，则会将智能标记考虑在内。 它与内置搜索功能配合使用。 参见 [搜索行为](#searchbehavior). 要优化搜索结果的显示顺序，您可以 [提升搜索排名](#searchrank) 少数精选资源的。

* **索引**：搜索结果中仅返回索引元数据和资源。 为了获得更好的覆盖率和性能，请确保正确编制索引并遵循最佳实践。 参见 [索引](#searchindex).

* 要从搜索结果中排除特定资源，请使用 `excludedPath` 属性。

## 一些说明搜索的示例 {#samples}

在关键词前后使用双引号可查找包含精确短语的资源，其顺序与用户指定的完全一致。

![带引号和不带引号的搜索行为](assets/search_with_quotes.gif)

*图：带引号和不带引号的搜索行为。*

**使用星号通配符搜索**：要扩大搜索范围，请在搜索词前后使用星号以匹配任意数量的字符。 例如，搜索没有星号的运行时，不会返回包含该词的任何变体的资产（包括在元数据中）。 星号可替代任意数量的字符。 例如，

* `run` 返回带有exactly run关键字的资产
* `run*` 通过以下方式返回资产 `running`， `run`， `runaway`，等等。
* `*run` 通过以下方式返回资产 `outrun`， `rerun`，等等。
* `*run*` 返回所有可能的组合。

![使用示例说明星号通配符在资产搜索中的用法](assets/search_with_asterisk_run.gif)

*图：通过一个示例说明星号通配符在Asset搜索中的用法。*

**使用问号通配符搜索**：要扩大搜索范围，请使用一个或多个“？” 个字符，以匹配确切的字符数。 例如，在下图中，

* `run???` 查询不匹配任何资源。

* `run????` 查询与单词匹配 `running` 后面有四个字符 `run`.

* `??run` 查询与单词匹配 `rerun` 之前包含两个字符 `run`.

![使用示例说明问号通配符在资产搜索中的用法](assets/search_with_questionmark_run.gif)

*图：使用示例说明在Asset搜索中使用问号通配符的情况。*

**排除关键字**：使用短划线搜索不包含关键字的资源。 例如， `running -shoe` 查询返回包含的资源 `running`，但不匹配 `shoe`. 同样， `camp -night` 查询返回包含的资源 `camp` 但不是 `night`. 查询 `camp-night` 返回同时包含两者的资产 `camp` 和 `night`.

![使用短划线搜索不包含排除关键字的资产](assets/search_dash_exclude_keyword.gif)

*图：使用短划线搜索不包含排除关键字的资产。*

## 与搜索功能相关的配置和管理任务 {#configadmin}

### 搜索索引配置 {#searchindex}

资产发现依赖于DAM内容（包括元数据）的索引。 更快、更准确的资产发现依赖于优化的索引和适当的配置。 参见 [搜索索引](/help/assets/performance-tuning-guidelines.md#search-indexes)， [oak查询和索引](/help/sites-deploying/queries-and-indexing.md)、和 [最佳实践](/help/sites-deploying/best-practices-for-queries-and-indexing.md).

要从搜索结果中排除特定资源，请使用 `excludedPath` 属性。

### 视觉或相似性搜索 {#configvisualsearch}

可视化搜索使用智能标记。 配置智能标记功能后，请按照以下步骤操作。

1. In [!DNL Experience Manager] CRXDE，输入 `/oak:index/lucene` 节点，添加以下属性和值并保存更改。

   * `costPerEntry` 类型的属性 `Double` 具有值 `10`.
   * `costPerExecution` 类型的属性 `Double` 具有值 `2`.
   * `refresh` 类型的属性 `Boolean` 具有值 `true`.

   此配置允许从相应的索引进行搜索。

1. 要创建Lucene索引，请在CRXDE中的 `/oak:index/damAssetLucene/indexRules/dam:Asset/properties`，创建名为的节点 `imageFeatures` 类型 `nt-unstructured`. In `imageFeatures` 节点，

   * 添加 `name` 类型的属性 `String` 具有值 `jcr:content/metadata/imageFeatures/haystack0`.
   * 添加 `nodeScopeIndex` 类型的属性 `Boolean` 其值为 `true`.
   * 添加 `propertyIndex` 类型的属性 `Boolean` 其值为 `true`.
   * 添加 `useInSimilarity` 类型的属性 `Boolean` 具有值 `true`.

   保存更改。

1. 访问 `/oak:index/damAssetLucene/indexRules/dam:Asset/properties/predictedTags` 并添加 `similarityTags` 类型的属性 `Boolean` 其值为 `true`.
1. 将智能标记应用于中的资产 [!DNL Experience Manager] 存储库。 参见 [如何配置智能标记](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/configuring/tagging.html#configuring).
1. 在CRXDE中，在 `/oak-index/damAssetLucene` 节点，设置 `reindex` 属性至 `true`. 保存更改。
1. （可选）如果已自定义搜索表单，请复制 `/libs/settings/dam/search/facets/assets/jcr%3Acontent/items/similaritysearch` 节点至 `/conf/global/settings/dam/search/facets/assets/jcr:content/items`. 保存更改。

有关相关信息，请参阅 [了解Experience Manager中的智能标记](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/metadata/image-smart-tags.html) 和 [如何管理智能标记](/help/assets/enhanced-smart-tags.md).

>[!CAUTION]
>
>如果Lucene索引完成于 [!DNL Adobe Experience Manager]，则基于智能标记的搜索无法按预期工作。

### 必需元数据 {#mandatorymetadata}

业务用户、管理员或DAM库管理员可以将某些元数据定义为必需元数据，这是业务流程工作所必需的元数据。 由于各种原因，某些资产可能缺少此元数据，例如旧版资产或批量迁移的资产。 系统会根据索引的元数据属性检测和报告元数据缺失或无效的资源。 要对其进行配置，请参阅 [必需元数据](/help/assets/metadata-schemas.md#define-mandatory-metadata).

### 修改搜索彩块化 {#searchfacets}

为了提高发现速度， [!DNL Experience Manager Assets] 提供搜索Facet，您可以使用它筛选搜索结果。 默认情况下，“筛选器”面板包含几个标准方面。 管理员可以自定义“筛选器”面板，以使用内置谓词修改默认Facet。 [!DNL Experience Manager] 提供了一个良好的内置谓词集合和一个用于自定义Facet的编辑器。 参见 [搜索Facet](/help/assets/search-facets.md).

### 上传资产时提取文本 {#extracttextupload}

您可以配置 [!DNL Experience Manager] 用于在用户上传资源(如PSD或PDF文件)时从资源中提取文本。 [!DNL Experience Manager] 为提取的文本编制索引，并帮助用户根据提取的文本搜索这些资源。 参见 [上传资产](/help/assets/manage-assets.md#uploading-assets).

如果文本提取对于您的部署来说过于耗费资源，请考虑以下事项 [禁用文本提取](https://helpx.adobe.com/experience-manager/kb/Disable-binary-text-extraction-to-optimize-Lucene-indexing-AEM.html).

### 用于筛选搜索结果的自定义谓词 {#custompredicates}

谓词用于创建Facet。 管理员可以使用预配置的谓词自定义“筛选器”面板中的搜索彩块化。 可以使用叠加自定义这些谓词。 参见 [创建自定义谓词](/help/assets/searchx.md).

您可以根据以下一个或多个属性搜索数字资产。 默认情况下，适用于其中一些属性的过滤器可用，可以自定义创建一些其他过滤器以应用于其他属性。

| 搜索字段 | 搜索属性值 |
|-----------------|----------------------------------------------------------------------------------------------------------------------------------------|
| MIME 类型 | 图像、文档、多媒体、存档或其他。 |
| 上次修改时间 | 小时、日、周、月或年。 |
| 文件大小 | 小、中、大。 |
| 发布状态 | 已发布或已取消发布。 |
| 批准状态 | 已批准或已拒绝。 |
| 方向 | “水平”、“垂直”或“方形”。 |
| 样式 | 彩色或黑白。 |
| 视屏高度 | 指定为最小值和最大值。 值仅存储在视频演绎版的元数据中。 |
| 视频宽度 | 指定为最小值和最大值。 值仅存储在视频演绎版的元数据中。 |
| 视频格式 | DVI、Flash、MPEG4、MPEG、OGG Theora、QuickTime、Windows Media。 值存储在源视频的元数据和任何演绎版中。 |
| 视频编解码 | x264。 值仅存储在视频演绎版的元数据中。 |
| 视频比特率 | 指定为最小值和最大值。 值仅存储在视频演绎版的元数据中。 |
| 音频编解码器 | Libvorbis、Lame MP3、AAC编码。 值仅存储在视频演绎版的元数据中。 |
| 音频比特率 | 指定为最小值和最大值。 值仅存储在视频演绎版的元数据中。 |

## 使用资源搜索结果 {#aftersearch}

您可以使用搜索到的资源执行以下操作 [!DNL Experience Manager]：

* 查看元数据属性和其他信息。
* 下载一个或多个资源。
* 使用桌面操作在桌面应用程序中打开这些资产。
* 创建智能收藏集。
* 创建一个版本
* 启动工作流
* 关联或取消关联资产
* 使用执行搜索后自动显示的过滤器面板应用过滤器以缩小搜索结果范围。

### 对搜索结果排序 {#sort}

对搜索结果排序，以更快地发现所需的资源。 您只能在列表视图中排序搜索结果，并且仅在您选择时 **[[!UICONTROL 文件]](#searchui)** 从 **[!UICONTROL 筛选器]** 面板。 [!DNL Assets] 使用服务器端排序快速对文件夹或搜索查询结果中的所有资产（无论数量多少）进行排序。 与客户端排序相比，服务器端排序提供更快、更准确的结果。

在列表视图中，您可以对搜索结果进行排序，就像对任何文件夹中的资源进行排序一样。 排序仅对以下列起作用 — 名称、标题、状态、Dimension、大小、评级、使用情况、（日期）创建、（日期）修改、（日期）发布、工作流和签出。

有关排序功能的限制，请参阅 [限制](#limitations).

### 检查资源的详细信息 {#checkinfo}

您可以从搜索结果页面中检查搜索到的资源的详细信息。

要查看某个资源的所有元数据，请选择该资源并单击 **[!UICONTROL 属性]** 工具栏中。

要检查对资产或资产版本历史记录的注释，请单击资产以打开大型预览。 打开左边栏中的时间轴，然后选择“ **[!UICONTROL 注释]** ”或“ **[!UICONTROL 版本]**”。 您还可以按时间顺序对时间轴活动（如注释或版本）进行排序。

![对搜索资产的时间轴条目排序](assets/sort_timeline_search_results.gif)

*图：对搜索资产的时间轴条目进行排序。*

### 下载搜索到的资源 {#download}

您可以下载搜索到的资源及其演绎版，就像从文件夹下载常规资源一样。 从搜索结果中选择一个或多个资源并单击 **[!UICONTROL 下载]** 工具栏中。

### 批量更新元数据属性 {#metadataupdates}

可以对多个资源的常用元数据字段进行批量更新。 从搜索结果中，选择一个或多个资源。 单击 **[!UICONTROL 属性]** 并根据需要更新元数据。 单击 **[!UICONTROL 保存并关闭]** 完成时。 更新字段中先前存在的元数据将被覆盖。

对于在单个文件夹或收藏集中可用的资产，更易于执行以下操作 [批量更新元数据](/help/assets/metadata.md) 而不使用搜索功能。 对于跨文件夹可用的资源或符合通用标准的资源，通过搜索批量更新元数据会更快一些。

### 智能收藏集 {#smart-collections}

收藏集是一组经过排序的资产，可以包含来自不同位置的资产，因为收藏集仅包含对这些资产的引用。 收藏集属于以下两种类型：

* 资产、文件夹和其他收藏集的静态引用列表。
* 根据搜索条件填充收藏集中资产的动态列表（智能收藏集）。

您可以根据搜索条件创建智能收藏集。从&#x200B;**[!UICONTROL 过滤器]**&#x200B;面板中，选择&#x200B;**[!UICONTROL 文件]**，然后单击&#x200B;**[!UICONTROL 保存智能收藏集]**。请参阅[管理收藏集](/help/assets/manage-collections.md)。

### 创建一个版本 {#create-version}

为搜索结果中显示的资源创建版本。 选择资源并单击 **[!UICONTROL 创建]** > **[!UICONTROL 版本]**. 添加可选标签或注释，然后单击 **[!UICONTROL 创建]**. 您还可以选择多个资源并同时为其创建版本。

### 创建工作流 {#create-workflow}

与创建版本功能类似，您还可以为搜索结果中显示的资产创建工作流。 选择资源并单击 **[!UICONTROL 创建]** > **[!UICONTROL 工作流]**. 选择工作流模型，指定工作流的标题，然后单击 **[!UICONTROL 开始]**.

### 关联和取消关联资产 {#relate-unrelate-assets}

关联和取消关联搜索结果中显示的资源。 选择资源并单击 **[!UICONTROL 相关]** 或 **[!UICONTROL 取消关联]**.

## 意外的搜索结果和问题 {#unexpected-results}

| 错误、问题、症状 | 可能的原因 | 对问题的可能修复或了解 |
|---|---|---|
| 搜索缺少元数据的资源时结果不正确。 | 搜索缺少必需元数据的资源时， [!DNL Experience Manager] 可能会显示一些具有有效元数据的资源。 结果基于索引的元数据属性。 | 元数据更新后，需要重新索引以反映资源元数据的正确状态。 参见 [必需元数据](metadata-schemas.md#define-mandatory-metadata). |
| 搜索结果太多。 | 广泛搜索参数。 | 考虑限制 [搜索范围](#scope). 使用智能标记可能会为您提供比预期更多的搜索结果。 参见 [使用智能标记搜索行为](#withsmarttags). |
| 不相关或部分相关的搜索结果。 | 使用智能标记可更改搜索行为。 | 了解 [智能标记后搜索如何更改](#withsmarttags). |
| 没有针对资产的自动完成建议。 | 新上传的资产尚未编入索引。 当您开始在Omnisearch栏中输入搜索关键字时，元数据无法立即作为建议使用。 | [!DNL Experience Manager] 会等待一个超时时间到期（默认为一小时）后才运行后台作业，以便为所有新上传或更新后的资源索引元数据，然后将元数据添加到建议列表中。 |
| 无搜索结果. | <ul><li>不存在与查询匹配的资源。 </li><li> 在搜索查询之前添加了空格。 </li><li> 不支持的元数据字段包含您搜索的关键字。</li><li> 在资源空闲时间进行的搜索。 </li></ul> | <ul><li>使用其他关键词进行搜索。 或者，使用智能标记或相似性搜索来改进搜索结果。 </li><li>[已知限制](#limitations).</li><li>搜索时不考虑所有元数据字段。 参见 [范围](#scope).</li><li>稍后搜索或修改所需资产的开启时间和关闭时间。</li></ul> |
| 搜索过滤器或谓词不可用。 | <ul><li>未配置搜索筛选器。</li><li>它不可用于您的登录。</li><li>（不太可能）未在您使用的部署中自定义搜索选项。</li></ul> | <ul><li>联系管理员以检查搜索自定义项是否可用。</li><li>联系管理员以检查您的帐户是否具有使用自定义设置的权限。</li><li>联系管理员并查看可用的自定义项 [!DNL Assets] 您正在使用的部署。</li></ul> |
| 搜索视觉上相似的图片时，缺少预期的图片。 | <ul><li>图像在中不可用 [!DNL Experience Manager].</li><li>图像未编入索引。 通常是在最近上传时。</li><li>图像未智能标记。</li></ul> | <ul><li>将图像添加到 [!DNL Assets].</li><li>请与管理员联系以重新索引存储库。 此外，请确保您使用的是适当的索引。</li><li>请联系您的管理员以智能标记相关资产。</li></ul> |
| 在搜索视觉上相似的图像时，显示不相关的图像。 | 视觉搜索行为。 | [!DNL Experience Manager] 尽可能多地显示潜在相关的资产。 不太相关的图像（如果有）会添加到结果中，但搜索排名较低。 向下滚动搜索结果时，搜索资产的匹配质量和相关性会降低。 |
| 选择并操作搜索结果时，不会操作所有搜索到的资产。 | 此 [!UICONTROL 全选] 选项仅选择卡片视图中的前100个搜索结果和列表视图中的前200个搜索结果。 | |

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 搜索实施指南](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/developing/search-tutorial-develop.html)
>* [用于提升搜索结果的高级配置](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/search-and-discovery/search-boost.html)
>* [配置智能翻译搜索](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/translation/smart-translation-search-technical-video-setup.html)
