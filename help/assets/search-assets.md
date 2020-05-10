---
title: 在中搜索数字资产和图像 [!DNL Adobe Experience Manager]。
description: 了解如何使用“过滤器”面 [!DNL Adobe Experience Manager] 板查找所需的资产，以及如何使用显示在搜索中的资产。
contentOwner: AG
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 5f3af7041029a1b4dd1cbb4c65bd488b62c7e10c
workflow-type: tm+mt
source-wordcount: '5872'
ht-degree: 7%

---


# 在 [!DNL Adobe Experience Manager] {#search-assets-in-aem}

[!DNL Adobe Experience Manager Assets] 提供强大的资产发现方法，帮助您实现更高的内容速度。 您的团队使用开箱即用的功能和自定义方法，通过无缝、智能的搜索体验缩短上市时间。 搜索资产对于数字资产管理系统的使用至关重要——无论是供创意人员进一步使用、供业务用户和营销人员对资产进行可靠管理，还是供DAM管理员管理。 简单、高级和自定义搜索，您可以通过用户界面或其 [!DNL Assets] 他应用程序和界面执行这些搜索，这些搜索有助于完成这些用例。

[!DNL Experience Manager Assets] 支持以下用例，本文介绍这些用例的用法、概念、配置、限制和疑难解答。

| 搜索资产 | 配置和管理 | 处理搜索结果 |
|---|---|---|
| [基本搜索](#searchbasics) | [搜索索引](#searchindex) | [对结果排序](#sort) |
| [了解搜索UI](#searchui) | [视觉或相似性搜索](#configvisualsearch) | [检查资产的属性和元数据](#checkinfo) |
| [搜索建议](#searchsuggestions) | [强制元数据](#mandatorymetadata) | [下载](#download) |
| [了解搜索结果和行为](#searchbehavior) | [修改搜索彩块化](#searchfacets) | [批量元数据更新](#metadataupdates) |
| [搜索排名和提升](#searchrank) | [文本提取](#extracttextupload) | [智能收藏集](#collections) |
| [高级搜索： 筛选和搜索范围](#scope) | [自定义谓词](#custompredicates) | [了解意外结果和疑难解答](#troubleshoot-unexpected-search-results-and-issues) |
| [从其他解决方案和应用程序中搜索](#beyondomnisearch):<ul><li>[Adobe Asset Link](#aal)</li><li>[Brand Portal](#brandportal)</li><li>[Experience Manager桌面应用程序](#desktopapp)</li><li>[Adobe Stock图像](#adobestock)</li><li>[Dynamic Media资产](#dynamicmedia)</li></ul> |  |  |
| [资产选取器](#assetselector) |  |  |
| [限制](#limitations) 和提 [示](#tips) |  |  |
| [示例](#samples) |  |  |

使用Web界面顶部的“全名搜索”字段搜索 [!DNL Experience Manager] 资产。 转到 **[!UICONTROL 资产]** >文 **[!UICONTROL 件]** , [!DNL Experience Manager]单击顶栏中的搜索图标，输入搜索关键字，然后按回车键。 或者，使用关键字快捷键/（正斜杠）打开Omnisearch字段。 `Location:Assets` 已预先选择，以将搜索限制为DAM资产。 [!DNL Experience Manager] 在开始键入搜索关键字时提供建议。

使用 **[!UICONTROL 过滤器]** 面板，根据各种选项（谓词）筛选搜索结果，从而缩小搜索范围。这些选项（谓词）包括文件类型、文件大小、上次修改日期、资产状态、洞察数据和Adobe Stock许可。 您的管理员可以自定义“过滤器”面板，并使用搜索彩块化添加或删除搜索谓词。 “ [!UICONTROL 过滤器] ”面板中的“文 [!UICONTROL 件类] 型”筛选器包含混合状态复选框。 因此，除非您选择所有嵌套的谓词（或格式），否则将部分选中第一级复选框。

[!DNL Experience Manager] 搜索功能支持搜索收藏集和搜索收藏集中的资产。 请参阅 [搜索集合](/help/assets/managing-collections-touch-ui.md)。

## 了解搜索界面 {#searchui}

熟悉搜索界面和可用的操作。

![了解Experience Manager资产的搜索结果界面](assets/aem_search_results.png)

*图： 了解[!DNL Experience Manager Assets]搜索结果界面。*

**答：将搜索** 另存为智能收藏集。 **B.过滤器** 或谓词，以缩小搜索结果。 **C.显示文件** 、文件夹，或同时显示这两个文件。 **D.** 单击“过滤器”以打开或关闭左边栏。**E.** 搜索位置为 DAM。**F. Omnisearch** 字段，其中包含用户提供的搜索关键字。 **G.选择** 加载的搜索结果。 **H.** 在总搜索结果中显示的搜索结果数。 **I.关闭** 搜索 **J.在卡视图** 和列表视图之间切换。

### 动态搜索彩块化 {#dynamicfacets}

您可以使用动态更新的搜索彩块化中预期搜索结果数量，更快地从搜索结果页面发现所需的资产。 预期的资产数量会在应用搜索筛选器之前进行更新。 查看筛选器的预期计数有助于您快速、高效地浏览搜索结果。 有关详细信息，请参 [阅在Experience Manager中搜索资产](search-assets.md)。

![在搜索彩块化中查看资产的大致数量，无需筛选搜索结果。](assets/asset_search_results_in_facets_filters.png)

*图： 在搜索彩块化中查看资产的大致数量，无需筛选搜索结果。*

## 了解搜索结果和行为 {#searchbehavior}

### 基本搜索词和结果 {#searchbasics}

您可以从OmniSearch字段运行关键字搜索。 关键字搜索不区分大小写，并且是全文搜索（跨常用元数据字段）。 如果搜索了多个关键字，则关键字之间的默认运算符是默 `AND` 认搜索，而是在资 `OR` 产被智能标记时。

结果按相关性排序，以最接近的匹配项开始。 对于多个关键字，更具相关性的结果是包含这两个术语的资产在其元数据中。 在元数据中，显示为智能标记的关键字的排名高于其他元数据字段中显示的关键字。 [!DNL Experience Manager] 允许赋予特定搜索词更高的权重。 此外，还可以提升 [特定搜索词的](#searchrank) 少数目标资产的排名。

为了快速找到相关资产，富界面提供了筛选、排序和选择机制。 您可以根据多个条件筛选结果，并查看搜索到的各种过滤器的资产数。 或者，也可以通过在“全搜索”字段中更改查询来重新运行搜索。 当您更改搜索词或过滤器时，其他过滤器仍然被应用以保留搜索的上下文。

当结果为多个资产时， [!DNL Experience Manager] 在卡视图中显示前100个，在列表视图中显示200个。 用户滚动时，会加载更多资产。 这是为了提高性能。

>[!VIDEO](https://www.youtube.com/watch?v=LcrGPDLDf4o)

有时，您可能会在搜索结果中看到一些意外的资产。 有关详细信息，请参 [阅意外结果](#troubleshoot-unexpected-search-results-and-issues)。

[!DNL Experience Manager] 可以搜索多种文件格式，并可以自定义搜索过滤器符以满足您的业务需求。 请与管理员联系，了解为您的DAM存储库提供了哪些搜索选项以及您的帐户有哪些限制。

### 包含和不包含增强的智能标签的结果 {#withsmarttags}

默认情况下， [!DNL Experience Manager] 搜索将搜索词与AND子句组合在一起。 例如，考虑搜索正在运行的关键字妇女。 默认情况下，搜索结果中只显示元数据中同时包含女性和正在运行关键字的资产。 在将特殊字符（句点、下划线或虚线）与关键字一起使用时，会保留相同的行为。 以下搜索查询返回相同的结果：

* `woman running`
* `woman.running`
* `woman-running`

但是，查询会返 `woman -running` 回元数据中没 `running` 有的资产。
使用智能标记可添加 `OR` 额外的子句，以查找任何作为已应用智能标记的搜索词。 标记有或使用智 `woman` 能标 `running` 记的资产也会出现在此类搜索查询中。 搜索结果是，

* 元数据 `woman` 中包含 `running` 和关键字的资产（默认行为）。

* 使用任一关键字标记的资产（智能标记行为）。

### Search suggestions as you type {#searchsuggestions}

在开始键入关键字时， [!DNL Experience Manager] 建议可能的搜索关键字或短语。 建议基于现有资产的元数据。 [!DNL Experience Manager] 索引所有元数据字段以帮助搜索。 为了提供搜索建议，系统使用以下几个元数据字段的值。 要提供搜索建议，请考虑使用适当的关键字填充以下字段：

* 资产标记。 (映射到 `jcr:content/metadata/cq:tags`)
* 资产标题。 (映射到 `jcr:content/metadata/dc:title`)
* 资产描述。 (映射到 `jcr:content/metadata/dc:description`)
* JCR存储库中的标题。 该值可能会映射到资产标题。 (映射到 `jcr:content/jcr:title`)
* JCR存储库中的说明。 该值可能会映射到资产描述。 (映射到 `jcr:content/jcr:description`)

要接收多个搜索关键字的建议，请继续键入所有关键字，而不为单个关键字选择任何建议。

![键入多个关键字以视图建议，使其全部适合](assets/search_suggestionsmanykeywords.gif)

*图： 键入多个关键字以视图建议，使其全部适合。*

### 搜索排名和提升 {#searchrank}

首先显示与元数据字段中所有搜索词匹配的搜索结果，然后显示与智能标记中任何搜索词匹配的搜索结果。 在上例中，搜索结果的近似显示顺序为：

1. 各个元 `woman running` 数据字段中的匹配项。
1. 智能标 `woman running` 签中的匹配项。
1. 智能标 `woman` 记的匹 `running` 配项或匹配项。

您可以提高特定资产的关键字相关性，从而帮助根据关键字提高搜索速度。 换言之，当您根据这些关键字进行搜索时，提升特定关键字的图像将显示在搜索结果顶部。

1. From the [!DNL Assets] user interface, open the properties page for the asset. 单击&#x200B;**[!UICONTROL 高级]**，然后单击/点按&#x200B;**[!UICONTROL 提升搜索关键词**[!UICONTROL &#x200B;下的&#x200B;]**添加]**。
1. 在“搜 **[!UICONTROL 索提升]** ”框中，指定要提升其图像搜索的关键字，然后单击／点按 **[!UICONTROL 添加]**。 可以以相同方式指定多个关键字。
1. 单击／点按保 **[!UICONTROL 存并关闭]**。 您为此关键字提升的资产会显示在顶级搜索结果中。

您可以通过提升目标关键字的搜索结果中某些资产的排名来利用此功能。 请观看下面的示例视频。 有关详细信息，请参 [阅在Experience Manager中搜索](https://helpx.adobe.com/experience-manager/kt/assets/using/search-feature-video-use.html)。

>[!VIDEO](https://video.tv.adobe.com/v/16766/?quality=6)

*了解搜索结果的排名方式以及排名如何受影响。*

## Advanced search {#scope}

[!DNL Experience Manager] 提供了各种方法(如应用于搜索的资产的过滤器)，以帮助您更快地找到所需的资产。 下面介绍了一些常用的方法。 下面 [分享了一些](#samples) 带插图的示例。

**搜索文件或文件夹**: 在搜索结果中，可查看文件、文件夹或两者。 从“ **[!UICONTROL 过滤器]** ”面板中，可以选择相应的选项。 请参阅 [搜索界面](#searchui)。

**在文件夹内搜索资产**: 您可以将搜索限制为特定文件夹。 在“ **[!UICONTROL 过滤器]** ”面板中，添加文件夹的路径。 一次只能选择一个文件夹。

![通过在“过滤器”面板中添加文件夹路径，将搜索结果限制为文件夹](assets/search_folder_select.gif)

*图： 通过在“过滤器”面板中添加文件夹路径，将搜索结果限制为文件夹。*

### 查找类似图像 {#visualsearch}

要查找与用户选择的图像视觉上相似的图像，请从图像的卡片视图或工具栏中单击&#x200B;**[!UICONTROL 查找类似]**&#x200B;选项。[!DNL Experience Manager] 显示 DAM 存储库中与用户所选图像相似的智能标记图像。请参阅[如何配置相似性搜索](#configvisualsearch)。

![使用卡视图中的选项查找类似图像](assets/search_find_similar.png)

*图： 使用卡视图中的选项查找类似图像。*

### Adobe Stock图像 {#adobestock}

在用户界 [!DNL Experience Manager] 面中，用户可以搜 [索Adobe Stock资源](/help/assets/aem-assets-adobe-stock.md) ，并许可所需的资源。 添加 `Location: Adobe Stock` 到Omnisearch栏中。 您还可以使用“过滤器”面板查找所有授权或未授权的资源，或使用Adobe Stock文件号搜索特定资源。

### Dynamic Media资产 {#dmassets}

您可以通过选择&#x200B;**[!UICONTROL 过滤器]**&#x200B;面板中的 **[!UICONTROL Dynamic Media]** > **[!UICONTROL 集]**&#x200B;来过滤 Dynamic Media 图像。该操作可过滤并显示图像集、轮播集、混合媒体集和旋转集等资产。

### 在元数据字段中使用特定值进行搜索 {#gqlsearch}

您可以根据特定元数据字段的确切值（如标题、描述和作者）搜索资产。 GQL全文搜索功能只获取元数据值与搜索查询完全匹配的资产。 属性的名称（例如作者、标题等）和值区分大小写。

| 元数据字段 | Facet值和用法 |
| ----------------------------------------- | ------------------------------------- |
| 标题 | title:John |
| 创建者 | creator:John |
| 位置 | 位置：NA |
| 描述 | description:&quot;Sample Image&quot; |
| 创建程序工具 | creatortool:&quot;Adobe Photoshop CC 2015&quot; |
| 版权所有者 | copyrightowner:&quot;Adobe Systems&quot; |
| 参与者 | contributor:John |
| 使用条款 | usageterms:&quot;CopyRights Reserved&quot; |
| 创建时间 | created:YYYY-MM-DDTHH |
| 过期日期 | expires:YYYY-MM-DDTHH |
| 开始时间 | ontime:YYYY-MM-DDTHH |
| 结束时间 | offtime:YYYY-MM-DDTHH |
| 时间范围（过期日期、开始时间、结束时间） | facet字段： lowerbound...上界 |
| 路径 | /content/dam/&lt;folder name> |
| PDF 标题 | pdftitle:&quot;Adobe Document&quot; |
| 主题 | subject:&quot;Training&quot; |
| 标记 | tags:&quot;Location And Travel&quot; |
| 类型 | type:&quot;image\png&quot; |
| 图像宽度 | width:lowerbound..上界 |
| 图像高度 | height:lowerbound...上界 |
| 人员 | person:John |

属性路径、限制、大小和排序依据不能与任何其他属性一起使用。

用户生成的属性的关键字是属性编辑器中的字段标签，以小写形式显示，删除了空格。

以下是复杂查询的一些搜索格式示例：

* To display all assets with multiple facets fields (for example: title=John Doe and creator tool = Adobe Photoshop): `tiltle:"John Doe" creatortool : Adobe*`
* To display all assets when the facets value is not a single word but a sentence (for example: title=Scott Reynolds): `title:"Scott Reynolds"`
* To display assets with multiple values of a single property (for example: title=Scott Reynolds or John Doe): `title:"Scott Reynolds" OR "John Doe"`
* To display assets with property values starting with a specific string (for example: title is Scott Reynolds): `title:Scott*`
* To display assets with property values ending with a specific string (for example: title is Scott Reynolds): `title:*Reynolds`
* To display assets with a property value that contains a specific string (for example: title = Basel Meeting Room): `title:*Meeting*`
* To display assets that contain a particular string and have a specific property value (for example: search for string Adobe in assets having title=John Doe): `*Adobe* title:"John Doe"`

## 从其他产品或界面 [!DNL Experience Manager] 搜索资产 {#beyondomnisearch}

[!DNL Adobe Experience Manager] 将DAM存储库连接到各种其 [!DNL Experience Manager] 他解决方案，以便更快地访问数字资产并简化创意工作流。 具有浏览或搜索的任何资产发现开始。 搜索行为在不同的表面和解决方案上基本保持不变。 某些搜索方法会随着目标受众、用例和用户界面的不同而发生变化，而且这些解决方案会有所 [!DNL Experience Manager] 不同。 下面的链接介绍了针对各个解决方案的具体方法。 本文描述了普遍适用的提示和行为。

### 从Adobe Asset Link面板搜索资产 {#aal}

创意专业人士现在可以使用Adobe Asset Link访问存储在中的内容， [!DNL Experience Manager Assets]而无需离开受支持的Adobe Creative Cloud应用程序。 创意人员可以使用Creative Cloud应用程序中的应用程序内面板无缝地浏览、搜索、注销和登记资产： Photoshop、Illustrator和InDesign。 资产链接还允许用户搜索视觉效果相似的结果。 可视搜索显示结果由Adobe Sensei的机器学习算法提供支持，并帮助用户找到美学上相似的图像。 请参 [阅使用Adobe资产链接](https://helpx.adobe.com/cn/enterprise/using/manage-assets-using-adobe-asset-link.html#UseAdobeAssetLink) 搜索和浏览资产。

### 在桌面应用程序 [!DNL Experience Manager] 中搜索资产 {#desktopapp}

创意专业人士使用桌面应用程 [!DNL Experience Manager Assets] 序使本地桌面（Win或Mac）可轻松搜索和使用。 Creatives可以轻松地在Mac Finder或Windows资源管理器中显示所需的资产，在桌面应用程序中打开并在本地进行更改——这些更改将通过在存储库中创建 [!DNL Experience Manager] 的新版本保存回来。 应用程序支持使用一个或多个关键字、通配符 `*` 和运 `?` 算符进行基本 `AND` 搜索。 请参 [阅浏览、搜索和预览桌面应用程](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html#browse-search-preview-assets) 序中的资产。

### 在 [!DNL Brand Portal] {#brandportal}

业务线用户和营销人员使用Brand Portal与其扩展的内部团队、合作伙伴和经销商高效安全地共享获准的数字资产。 See [search assets on Brand Portal](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/search-capabilities/brand-portal-searching.html).

### 搜索图 [!DNL Adobe Stock] 像 {#adobestock-1}

在用户界 [!DNL Experience Manager] 面中，用户可以搜索Adobe Stock资源并许可所需的资源。 添加 `Location: Adobe Stock` 到Omnisearch字段。 您还可以使用 **[!UICONTROL 过滤器]** 面板查找所有授权或未授权的资源，或使用Adobe Stock文件号搜索特定资源。 请参 [阅在Experience Manager中管理Adobe Stock图像](/help/assets/aem-assets-adobe-stock.md#usemanage)。

### 搜索Dynamic Media资产 {#dynamicmedia}

您可以通过选择&#x200B;**[!UICONTROL 过滤器]**&#x200B;面板中的 **[!UICONTROL Dynamic Media]** > **[!UICONTROL 集]**&#x200B;来过滤 Dynamic Media 图像。该操作可过滤并显示图像集、轮播集、混合媒体集和旋转集等资产。在创作网页时，作者可以在内容查找器中搜索集。弹出菜单中提供集的过滤器。

### 创作网页时在内容查找器中搜索资产 {#contentfinder}

作者可以使用内容查找器搜索DAM存储库中的相关资产，并在他们创建的网页中使用资产。 作者还可以使用连接的资产功能搜索远程部署中可用的 [!DNL Experience Manager] 资产。 然后，作者可以在本地部署的网页中使用这些 [!DNL Experience Manager] 资源。 See [use remote assets](/help/assets/use-assets-across-connected-assets-instances.md#use-remote-assets).

### 搜索集合 {#collections}

[!DNL Experience Manager] 搜索功能支持搜索收藏集和搜索收藏集中的资产。 请参阅 [搜索集合](/help/assets/managing-collections-touch-ui.md)。

## 资产选取器 {#assetselector}

通过资产选取器，您可以以特殊方式搜索、筛选和浏览DAM资产。 资产选取器在上可 `https://[aem-server]:[port]/aem/assetpicker.html`用。 您可以使用此功能提取您选择的资产的元数据。 您可以使用支持的请求参数启动它，如资产类型（图像、视频、文本）和选择模式（单个或多个选择）。 这些参数为特定搜索实例设置资产选取器的上下文，并在整个选择过程中保持不变。

资产选取器使用HTML5 `Window.postMessage` 消息将选定资产的数据发送到收件人。 资产选取器仅在浏览模式下工作，并且仅在全搜索结果页面中工作。

您可以在URL中传递以下请求参数，以在特定上下文中启动资产选取器：

| 名称 | 值 | 示例 | 用途 |
|---|---|---|---|
| 资源后缀(B) | 作为URL中资源后缀的文件夹路[径：https://localhost:4502/aem/assetpicker.html/&lt;folder_path>](https://localhost:4502/aem/assetpicker.html) | 要在选定特定文件夹的情况下启动资产选取器(例如，在选 `/content/dam/we-retail/en/activities` 定文件夹时),URL应采用以下格式： [https://localhost:4502/aem/assetpicker.html/content/dam/we-retail/en/activities?assettype=images](https://localhost:4502/aem/assetpicker.html/content/dam/we-retail/en/activities?assettype=images) | 如果在启动资产选择器时需要选择特定文件夹，请将其作为资源后缀进行传递。 |
| 模式 | 单个，多个 | <ul><li>[https://localhost:4502/aem/assetpicker.html?mode=single](https://localhost:4502/aem/assetpicker.html?mode=single)</li><li>[https://localhost:4502/aem/assetpicker.html?mode=multiple](https://localhost:4502/aem/assetpicker.html?mode=multiple)</li></ul> | 在多个模式下，您可以使用资产选择器同时选择多个资产。 |
| mimetype | 资产的mimetype(`/jcr:content/metadata/dc:format`s)()(还支持通配符 | <ul><li>[https://localhost:4502/aem/assetpicker.html?mimetype=image/png](https://localhost:4502/aem/assetpicker.html?mimetype=image/png)</li><li>[https://localhost:4502/aem/assetpicker.html?mimetype=*png](https://localhost:4502/aem/assetpicker.html?mimetype=*png)</li><li>[https://localhost:4502/aem/assetpicker.html?mimetype=*presentation](https://localhost:4502/aem/assetpicker.html?mimetype=*presentation)</li><li>[https://localhost:4502/aem/assetpicker.html?mimetype=*presentation&amp;mimetype=*png](https://localhost:4502/aem/assetpicker.html?mimetype=*presentation&amp;mimetype=*png)</li></ul> | 使用它根据MIME类型筛选资产 |
| 对话框 | true、false | [https://localhost:4502/aem/assetpicker.html?dialog=true](https://localhost:4502/aem/assetpicker.html?dialog=true) | 使用这些参数以Granite对话框的形式打开资产选择器。 仅当您通过Granite路径字段启动资产选择器并将其配置为pickerSrc URL时，此选项才适用。 |
| 资源类型(S) | 图像，文档，多媒体，存档 | <ul><li>[https://localhost:4502/aem/assetpicker.html?assettype=images](https://localhost:4502/aem/assetpicker.html?assettype=images)</li><li>[https://localhost:4502/aem/assetpicker.html?assettype=documents](https://localhost:4502/aem/assetpicker.html?assettype=documents)</li><li>[https://localhost:4502/aem/assetpicker.html?assettype=multimedia](https://localhost:4502/aem/assetpicker.html?assettype=multimedia)</li><li>[https://localhost:4502/aem/assetpicker.html?assettype=archives](https://localhost:4502/aem/assetpicker.html?assettype=archives)</li></ul> | 使用此选项可根据传递的值筛选资产类型。 |
| 根 | &lt;folder_path> | [https://localhost:4502/aem/assetpicker.html?assettype=images&amp;root=/content/dam/we-retail/en/activities](https://localhost:4502/aem/assetpicker.html?assettype=images&amp;root=/content/dam/we-retail/en/activities) | 使用此选项可指定资产选择器的根文件夹。 在这种情况下，资产选择器允许您仅选择根文件夹下的子资产（直接／间接）。 |

To access the asset Picker interface, go to `https://[aem_server]:[port]/aem/assetpicker`. 导航到所需的文件夹，然后选择一个或多个资产。 或者，从搜索框中搜索所需的资产，根据需要应用筛选器，然后选择它。

![在资产选取器中浏览并选择资产](assets/assetpicker.png)

*图： 在资产选取器中浏览并选择资产。*

## 限制 {#limitations}

中的搜索功 [!DNL Experience Manager Assets] 能有以下限制：

* 请勿在搜索查询中输入前导空格，否则搜索无效。
* [!DNL Experience Manager] 在您从搜索结果中选择资产的属性，然后取消搜索后，可能会继续显示搜索词。 <!-- (CQ-4273540) -->
* 在搜索文件夹或文件和文件夹时，无法按任何参数对搜索结果进行排序。
* 如果按回车键时未在Omnisearch栏中键入任何内容， [!DNL Experience Manager] 则返回仅包含文件的列表，而不包含文件夹。 如果您在不使用关键字的情况下专门搜索文 [!DNL Experience Manager] 件夹，则不返回任何结果。
* 使用 **[!UICONTROL 搜索页]** 面右上角的“全选”选项选择搜索的资产。 [!DNL Experience Manager] 最初以卡视图显示100个资产，以列表视图显示200个资产。 滚动搜索结果时会加载更多资产。 您可以选择比加载的资产更多的资产。 选定资产的计数会显示在搜索结果页面的右上角。 您可以对所选内容进行操作，例如，下载选定的资产、批量更新选定资产的元数据属性，或将选定的资产添加到收藏集。 当选择的资产多于显示的资产数时，将对所有选定的资产应用一个操作，或者出现一个对话框，显示所应用的资产数。 要对未加载的资产应用操作，请确保已明确选择所有资产。

视觉搜索或相似性搜索具有以下限制：

* 视觉搜索最适合于较大的存储库。 尽管没有获得最佳结果所需的最少图像数，但与几个图像匹配的质量可能不如来自大型存储库的匹配质量好。
* 不能更改模型或训练以 [!DNL Experience Manager] 查找类似图像。 例如，向少数资产添加或删除智能标记不会更改模型。 资产会从视觉上相似的搜索结果中排除。

在以下情况下，搜索功能可能存在性能限制：

* 与显示搜索结果的视图视图相比，卡列表的加载时间更短。

## 搜索提示 {#tips}

* 在监视资产的审核状态时，请使用适当的选项来查找已批准的资产或待批准的资产。
* 使用“分析”谓词，根据从各种Creative应用程序获取的资产使用情况统计信息搜索受支持的资产。 使用情况渠道按使用情况得分、展示次数、点击次数和显示资产的媒体类别进行分组。
* 使用全 **[!UICONTROL 选复选框]** ，选择已搜索的资产。 [!DNL Experience Manager] 最初以卡视图显示100个资产，以列表视图显示200个资产。 滚动搜索结果时会加载更多资产。 您可以选择比加载的资产更多的资产。 选定资产的计数会显示在搜索结果页面的右上角。 您可以对所选内容进行操作，例如，下载选定的资产、批量更新选定资产的元数据属性，或将选定的资产添加到收藏集。 当选择的资产多于显示的资产数时，将对所有选定的资产应用一个操作，或者出现一个对话框，显示所应用的资产数。 要对未加载的资产应用操作，请确保已明确选择所有资产。
* 要搜索不包含强制元数据的资产，请参阅强制 [元数据](#mandatorymetadata)。
* 搜索使用所有元数据字段。 通常，搜索12等通用搜索会返回许多结果。 为获得更好的效果，请使用多次（非单引号），或确保数字与没有特殊字符的单词相邻(例如 *shoe12*)。
* 全文搜索支持-、^等运算符。 要将这些字母作为字符串文本搜索，请将搜索表达式括在多次引号中。 例如，使用“笔记本——美容”而不是“笔记本——美容”。
* 如果搜索结果太多，请将所 [需资产的搜](#scope) 索范围限制为零。 当您了解如何更好地查找所需的资产（例如特定文件类型、特定位置、特定元数据等）时，它会发挥最佳作用。

* **标记**: 标记可帮助您更高效地对可以浏览和搜索的资产进行分类。 标记有助于将相应的分类传播到其他用户和工作流。 [!DNL Experience Manager] 优惠使用Adobe Sensei的人为智能服务自动标记资产的方法，这些服务通过使用和培训不断改进资产标记功能。 在搜索资产时，如果您的帐户启用了智能标记，则智能标记会被纳入其中。 它与内置的搜索功能配合使用。 查看 [搜索行为](#searchbehavior)。 要优化搜索结果的显示顺序，您可以提 [升几个选定资产](#searchrank) 的搜索排名。

* **索引**: 搜索结果中只返回已索引的元数据和资产。 为获得更好的覆盖和性能，请确保正确的索引并遵循最佳做法。 请参阅 [索引](#searchindex)。

## 一些说明搜索的示例 {#samples}

使用关键字周围的多次语录可以按用户指定的确切顺序查找包含确切短语的资产。

![带引号和不带引号的搜索行为](assets/search_with_quotes.gif)

*图： 带引号和不带引号的搜索行为。*

**使用星号通配符搜索**: 要扩大搜索范围，请在搜索单词之前或之后使用星号来匹配任意数量的字符。 例如，搜索不带星号的运行不会返回包含该单词任何变体（包括在元数据中）的资产。 星号可替换任意数量的字符。 例如，

* `run` 返回具有完全运行关键字的资产
* `run*` 返回资产，包括流动、流动、失控等。
* `*run` 返回结束、重新运行等。
* `*run*` 返回所有可能的组合。

![通过示例说明在资产搜索中使用星号通配符](assets/search_with_asterisk_run.gif)

*图： 通过示例说明在资产搜索中使用星号通配符。*

**使用问号通配符搜索**: 要扩展搜索范围，请使用一个或多个“?” 字符与字符数完全匹配。 例如，在下图中，

* `run???` 查询与任何资产不匹配。

* `run????` 查询将单词 `running` 与四个字符匹配 `run`。

* `??run` 查询将单词 `rerun` 与前两个字符 `run`匹配。

![通过示例说明在资产搜索中使用问号通配符](assets/search_with_questionmark_run.gif)

*图： 通过示例说明在资产搜索中使用问号通配符。*

**排除关键字**: 使用短划线搜索不包含关键字的资产。 例如， `running -shoe` 查询返回包含但 `running`不包含的资 `shoe`产。 同样， `camp -night` 查询会返回包含但 `camp` 不包含的 `night`资产。 请注意， `camp-night` 查询会返回同时包含和的 `camp` 资产 `night`。

![使用短划线搜索不包含被排除关键字的资产](assets/search_dash_exclude_keyword.gif)

*图： 使用短划线搜索不包含被排除关键字的资产。*

## 与搜索功能相关的配置和管理任务 {#configadmin}

### 搜索索引配置 {#searchindex}

资产发现依赖于DAM内容（包括元数据）的索引。 更快、更准确的资源发现依赖于优化的索引和适当的配置。 请参 [阅搜索索引](/help/assets/performance-tuning-guidelines.md#search-indexes)、 [Oak查询和索引](/help/sites-deploying/queries-and-indexing.md)，以及 [最佳实践](/help/sites-deploying/best-practices-for-queries-and-indexing.md)。

### 视觉或相似性搜索 {#configvisualsearch}

视觉搜索使用智能标记， [!DNL Experience Manager] 并且需要6.5.2.0或更高版本。 配置智能标记功能后，请按照以下步骤操作。

1. 在 [!DNL Experience Manager] CRXDE的节点 `/oak:index/lucene` 中，添加以下属性和值并保存更改。

   * `costPerEntry` 类型的 `Double` 属性和值 `10`。

   * `costPerExecution` 类型的 `Double` 属性和值 `2`。

   * `refresh` 类型的 `Boolean` 属性和值 `true`。
   此配置允许从相应的索引中进行搜索。

1. 要创建Lucene索引，请在CRXDE中， `/oak:index/damAssetLucene/indexRules/dam:Asset/properties`创建名为类型 `imageFeatures` 的节点 `nt-unstructured`。 在节 `imageFeatures` 点中，

   * 添加 `name` 具有该值 `String` 的类型的属性 `jcr:content/metadata/imageFeatures/haystack0`。

   * 添加 `nodeScopeIndex` 值为 `Boolean` 的类型属性 `true`。

   * 添加 `propertyIndex` 值为 `Boolean` 的类型属性 `true`。

   * 添加 `useInSimilarity` 具有该值 `Boolean` 的类型的属性 `true`。
   保存更改。

1. 访 `/oak:index/damAssetLucene/indexRules/dam:Asset/properties/predictedTags` 问并添 `similarityTags` 加值为 `Boolean` 的类型属性 `true`。
1. 将智能标记应用于存储库中的 [!DNL Experience Manager] 资产。 了解 [如何配置智能标记](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/metadata/smart-tags-technical-video-setup.html)。
1. 在CRXDE的节点 `/oak-index/damAssetLucene` 中，将属性 `reindex` 设置为 `true`。 保存更改。
1. （可选）如果您具有自定义的搜索表单，则将节 `/libs/settings/dam/search/facets/assets/jcr%3Acontent/items/similaritysearch` 点复制到 `/conf/global/settings/dam/search/facets/assets/jcr:content/items`。 保存所有更改。

有关信息，请参 [阅了解Experience Manager中的智能标记](https://helpx.adobe.com/experience-manager/kt/assets/using/smart-tags-feature-video-understand.html)[以及如何管理智能标记](/help/assets/managing-smart-tags.md)。

### 强制元数据 {#mandatorymetadata}

商业用户、管理员或DAM图书管理员可以将某些元数据定义为必须的元数据，这是业务流程工作所必需的。 由于各种原因，某些资产可能缺少此元数据，如批量迁移的旧资产或资产。 会根据索引元数据属性检测和报告元数据缺失或无效的资产。 要进行配置，请参阅必 [需的元数据](/help/assets/metadata-schemas.md#define-mandatory-metadata)。

### 修改搜索彩块化 {#searchfacets}

为了提高搜索速度，请 [!DNL Experience Manager Assets] 优惠搜索彩块化，您可以使用它筛选搜索结果。 默认情况下，“过滤器”面板包含一些标准彩块化。 管理员可以自定义过滤器面板，以使用内置谓词修改默认彩块化。 [!DNL Experience Manager] 提供了一个用于自定义facet的内置谓词和编辑器的良好集合。 请参阅 [搜索彩块化](/help/assets/search-facets.md)。

### 上传资产时提取文本 {#extracttextupload}

您可以配 [!DNL Experience Manager] 置为在用户上传资产（如PSD或PDF文件）时从资产中提取文本。 [!DNL Experience Manager] 索引提取的文本，并帮助用户根据提取的文本搜索这些资产。 请参阅 [上传资产](/help/assets/managing-assets-touch-ui.md#uploading-assets)。

### 用于筛选搜索结果的自定义谓词 {#custompredicates}

谓词用于创建彩块化。 管理员可以使用预配置的谓词在“过滤器”面板中自定义搜索彩块化。 这些谓词可以使用叠加进行自定义。 请参阅 [创建自定义谓词](/help/assets/searchx.md)。

您可以根据以下一个或多个属性搜索数字资产。 默认情况下，应用于这些属性中的某些过滤器可用，并且可以自定义创建某些其他过滤器以应用于其他属性。

| 搜索字段 | 搜索属性值 |
|---|---|
| MIME类型 | 图像、文档、多媒体、存档或其他。 |
| 上次修改时间 | “小时”、“天”、“周”、“月”或“年”。 |
| 文件大小 | “小”、“中”或“大”。 |
| 发布状态 | “已发布”或“已取消发布”。 |
| 批准状态 | “已批准”或“已拒绝”。 |
| 方向 | “水平”、“垂直”或“正方形”。 |
| 样式 | “彩色”或“黑白”。 |
| 视屏高度 | 指定为最小值和最大值。 值仅存储在视频演绎版的元数据中。 |
| 视频宽度 | 指定为最小值和最大值。 值仅存储在视频演绎版的元数据中。 |
| 视频格式 | DVI、Flash、MPEG4、MPEG、OGG Theora、QuickTime、Windows Media。 值存储在源视频和任何演绎版的元数据中。 |
| 视频编解码器 | x264。 值仅存储在视频演绎版的元数据中。 |
| 视频比特率 | 指定为最小值和最大值。 值仅存储在视频演绎版的元数据中。 |
| 音频编解码器 | Libvorbis、Lame MP3、AAC编码。 值仅存储在视频演绎版的元数据中。 |
| 音频比特率 | 指定为最小值和最大值。 值仅存储在视频演绎版的元数据中。 |

## 使用资产搜索结果 {#aftersearch}

当您看到一些搜索的资产与您的条件匹配后，您可以对这些搜索结果执行以下典型任务或执行以下操作：

* 视图元数据属性和其他信息。
* 下载一个或多个资源。
* 使用桌面操作在桌面应用程序中打开这些资产。
* 创建智能收藏集。

### 对搜索结果进行排序 {#sort}

对搜索结果排序可帮助您更快地发现所需的资产。 对搜索结果排序仅在列表视图中有效，并且仅在您从“筛选器 **[!UICONTROL [”面板](#searchui)]**中选择“**[!UICONTROL &#x200B;文件&#x200B;]**”时有效。[!DNL Experience Manager Assets]使用服务器端排序功能快速对某个文件夹或搜索查询的结果中的所有资产（无论数量多少）进行排序。 与客户端排序相比，服务器端排序提供更快、更准确的结果。

在列表视图中，您可以像对任意文件夹中的资产进行排序一样对搜索结果进行排序。 排序功能适用于这些列——名称、标题、状态、维度、大小、评级、使用情况、创建日期、修改日期、发布日期、工作流和检出。

有关排序功能的限制，请参 [阅限制](#limitations)。

### 检查资产的详细信息 {#checkinfo}

您可以从搜索结果页面检查已搜索资产的详细信息。

要查看资产的所有元数据，请选择资产，然后单 **[!UICONTROL 击工]** 具栏中的属性。

要检查对资产或资产版本历史记录的注释，请单击资产以打开大型预览。 打开左边栏中的时间轴，然后选择“ **[!UICONTROL 注释]** ”或“ **[!UICONTROL 版本]**”。 您还可以按时间顺序对时间轴活动（如注释或版本）进行排序。

![对搜索资产的时间轴条目进行排序](assets/sort_timeline_search_results.gif)

*图： 对搜索资产的时间轴条目进行排序。*

### 下载搜索的资源 {#download}

您可以像从文件夹下载常规资产一样下载搜索的资产及其演绎版。 从搜索结果中选择一个或多个资产，然后单 **[!UICONTROL 击工]** 具栏中的下载。

### 批量更新元数据属性 {#metadataupdates}

可以批量更新多个资产的公用元数据字段。 从搜索结果中，选择一个或多个资产。 单击 **[!UICONTROL 工具栏]** 中的属性，然后根据需要更新元数据。 完成 **[!UICONTROL 后，单击]** “保存并关闭”。 更新字段中以前存在的元数据将被覆盖。

对于单个文件夹或集合中的可用资产，无需使用搜索功 [能即可批量更新元](/help/assets/managing-multiple-assets.md) 数据。 对于跨文件夹可用或符合通用标准的资产，通过搜索批量更新元数据会更快。

### 智能收藏集 {#collections-1}

收藏集是一组有序的资产，可以包含来自不同位置的资产，因为收藏集只包含对这些资产的引用。 集合有以下两种类型：

* 资产、文件夹和其他收藏集的静态引用列表。
* 动态列表（智能收藏集），它根据搜索条件填充收藏集中的资产。

您可以根据搜索条件创建智能收藏集。从&#x200B;**[!UICONTROL 过滤器]**&#x200B;面板中，选择&#x200B;**[!UICONTROL 文件]**，然后单击&#x200B;**[!UICONTROL 保存智能收藏集]**。请参阅[管理收藏集](/help/assets/managing-collections-touch-ui.md)。

## 对意外搜索结果和问题进行疑难解答 {#troubleshoot-unexpected-search-results-and-issues}

| 错误、问题、症状 | 可能的原因 | 可能的问题修复或理解 |
|---|---|---|
| 搜索缺少元数据的资产时结果不正确 | 在搜索缺少必需元数据的资产时，可 [!DNL Experience Manager] 能会显示一些具有有效元数据的资产。 结果基于索引元数据属性。 | 更新元数据后，需要重新编制索引以反映资产元数据的正确状态。 请参阅 [必填元数据](metadata-schemas.md#define-mandatory-metadata)。 |
| 搜索结果过多 | 广泛的搜索参数。 | 请考虑限 [制搜索范围](#scope)。 使用智能标记可能会为您带来超出预期的搜索结果。 查看 [带有智能标记的搜索行为](#withsmarttags)。 |
| 不相关或部分相关的搜索结果 | 搜索行为会随智能标记而改变。 | 了解 [搜索在智能标记后的变化](#withsmarttags)。 |
| 没有资产自动完成建议 | 尚未对新上传的资产建立索引。 当您在Omnisearch栏中开始键入搜索关键字时，元数据不会立即作为建议可用。 | [!DNL Assets] 等到超时期（默认为一小时）到期后，运行后台作业为所有新上传或更新的资产索引元数据，然后将元数据添加到建议列表。 |
| 无搜索结果 | <ul><li>不存在与您的查询匹配的资产。</li><li>您在搜索查询前添加了空白。</li><li>不支持的元数据字段包含您搜索的关键字。</li><li>为资产配置了开始时间和结束时间，搜索是在资产结束时间进行的。</li></ul> | <ul><li>使用其他关键字进行搜索。 或者，使用（智能）标记来改进搜索结果。</li><li>这是已知 [的限制](#limitations)。</li><li>并非所有元数据字段都会被考虑用于搜索。 请参 [阅范围](#scope)。</li><li>稍后搜索或修改所需资产的开启和结束时间。</li></ul> |
| 搜索筛选器／谓词不可用 | <ul><li>未配置搜索筛选器。</li><li>登录时不提供此选项。</li><li>（不太可能）搜索选项未在您所使用的部署上进行自定义。</li></ul> | <ul><li>联系管理员以检查搜索自定义是否可用。</li><li>联系管理员以检查您的帐户是否具有使用自定义项的权限／权限。</li><li>联系管理员并检查您所使用的部 [!DNL Assets] 署的可用自定义项。</li></ul> |
| 在搜索视觉上相似的图像时，缺少期望的图像 | <ul><li>图像在中不可用 [!DNL Experience Manager]。</li><li>图像未编制索引。 通常，在最近上传时。</li><li>图像未标记为智能图像。</li></ul> | <ul><li>将图像添加到 [!DNL Assets]。</li><li>请与管理员联系以重新为存储库编制索引。 另外，请确保您使用的是适当的索引。</li><li>与管理员联系以智能标记相关资产。</li></ul> |
| 搜索视觉上相似的图像时，将显示不相关的图像 | 视觉搜索行为。 | [!DNL Experience Manager] 显示尽可能多的潜在相关资产。 相关度较低的图像（如果有）会添加到结果中，但搜索级别较低。 当您向下滚动搜索结果时，匹配项的质量和搜索资产的相关性会降低。 |
| 在选择并操作搜索结果时，所有搜索的资产都不会运行在 | “全 [!UICONTROL 选] ”选项仅选择卡视图中的前100个搜索结果和列表视图中的前200个搜索结果。 |  |

>[!MORELIKETHIS]
>
>* [Experience Manager搜索实施指南](https://docs.adobe.com/content/help/en/experience-manager-learn/sites/developing/search-tutorial-develop.html)
>* [多值和标记搜索谓词的高级配置](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/metadata/search-feature-video-use.html)
>* [配置智能翻译搜索](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/translation/smart-translation-search-technical-video-setup.html)

