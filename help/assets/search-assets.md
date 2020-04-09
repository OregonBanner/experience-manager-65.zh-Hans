---
title: 在AEM中搜索数字资产和图像
description: 了解如何使用过滤器面板在AEM中查找所需的资产，以及如何使用在搜索中显示的资产。
contentOwner: AG
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 25acffc6a0101be4ea6811b92c40bc76f554f5f0

---


# 在AEM中搜索资产 {#search-assets-in-aem}

Adobe Experience Manager(AEM)资产提供了强大的资产发现方法，可帮助您提高内容速度。 您的团队使用开箱即用的功能和自定义方法，通过无缝、智能的搜索体验缩短上市时间。 搜索资产是数字资产管理系统使用的核心——无论是供创意人员进一步使用、供商业用户和营销人员对资产进行可靠管理还是供DAM管理员管理。 您可以通过AEM资产用户界面或其他应用程序和界面执行的简单、高级和自定义搜索功能有助于完成这些使用案例。

AEM支持以下用例，本文介绍了这些用例的用法、概念、配置、限制和疑难解答。

| 搜索资产 | 配置和管理 | 处理搜索结果 |
|---|---|---|
| [基本搜索](#searchbasics) | [搜索索引](#searchindex) | [排序结果](#sort) |
| [了解搜索UI](#searchui) | [视觉或相似性搜索](#configvisualsearch) | [检查资产的属性和元数据](#checkinfo) |
| [搜索建议](#searchsuggestions) | [强制元数据](#mandatorymetadata) | [下载](#download) |
| [了解搜索结果和行为](#searchbehavior) | [修改搜索彩块化](#searchfacets) | [批量元数据更新](#metadataupdates) |
| [搜索排名和提升](#searchrank) | [文本提取](#extracttextupload) | [智能收藏集](#collections) |
| [高级搜索：筛选和搜索范围](#scope) | [自定义谓词](#custompredicates) | [了解意外结果和疑难解答](#troubleshoot-unexpected-search-results-and-issues) |
| [从其他解决方案和应用程序中搜索](#beyondomnisearch):<ul><li>[Adobe Asset Link](#aal)</li><li>[Brand Portal](#brandportal)</li><li>[AEM 桌面应用程序](#desktopapp)</li><li>[Adobe Stock图像](#adobestock)</li><li>[Dynamic Media资产](#dynamicmedia)</li></ul> |  |  |
| [资产选取器](#assetselector) |  |  |
| [限制](#limitations) 和提 [示](#tips) |  |  |
| [插图示例](#samples) |  |  |

使用AEM Web界面顶部的Omnisearch字段搜索资产。 转到 **[!UICONTROL AEM中的“资]** 产 **** ” > “文件”，单击顶栏中的搜索图标，输入搜索关键字，然后按回车键。 或者，使用关键字快捷键/（正斜杠）打开Omnisearch字段。 位置：资产已预先选中，可将搜索限制为DAM资产。 AEM在您的开始键入搜索关键字时提供建议。

使用 **[!UICONTROL 过滤器]** 面板，根据各种选项（谓词）筛选搜索结果以缩小搜索范围，这些选项（谓词）包括文件类型、文件大小、上次修改日期、资产状态、洞察数据和Adobe Stock许可。 您的管理员可以自定义过滤器面板并使用搜索彩块化添加或删除搜索谓词。 “ [!UICONTROL 过滤器] ”面板中的“文件类 [!UICONTROL 型”] (File Type)筛选器包含混合状态复选框。 因此，除非您选择所有嵌套的谓词（或格式），否则将部分选中第一级复选框。

AEM搜索功能支持搜索集合和搜索集合中的资产。 请参阅 [搜索集合](/help/assets/managing-collections-touch-ui.md)。

## 了解搜索界面 {#searchui}

熟悉搜索界面和可用的操作。

![了解资产搜索结果界面的各个部分](assets/aem_search_results.png)

*图：了解资产搜索结果界面的各个部分*

**A.** 将搜索另存为智能收藏集。**B.** 过滤（谓词）以缩小搜索结果。**C.** 在搜索结果中显示文件和/或文件夹。**D.** 单击“过滤器”以打开或关闭左边栏。**E.** 搜索位置为 DAM。**F.** 包含用户提供的搜索关键字的Omnisearch字段。 **G.** 选中此复选框可选择所有搜索结果。 **H.** 显示的搜索结果数（从总搜索结果中）。 **I.** 关闭搜索 **J。** 在卡视图和列表视图之间切换。

### 动态搜索彩块化 {#dynamicfacets}

您可以使用搜索彩块化中动态更新的预期搜索结果数量，从搜索结果页面更快地发现所需的资产。 预期的资产数量会在应用搜索筛选器之前进行更新。 查看筛选器的预期计数可帮助您快速、高效地浏览搜索结果。 有关详细信息，请参 [阅在AEM中搜索资产](search-assets.md)。

![无需筛选搜索彩块化中的搜索结果，即可查看资产的大致数量。](assets/asset_search_results_in_facets_filters.png)

*图：在搜索彩块化中查看资产的大致数量，无需筛选搜索结果*

## 了解搜索结果和行为 {#searchbehavior}

### 基本搜索词和结果 {#searchbasics}

您可以从OmniSearch字段运行关键字搜索。 关键字搜索不区分大小写，并且是全文搜索（跨常用元数据字段）。 如果搜索了多个关键字，则关键字之间的默认运算符是默认搜 `AND` 索，而是在资产被智能标记 `OR` 时进行的搜索。

结果按相关性排序，以最接近的匹配项开始。 对于多个关键字，更具相关性的结果是在元数据中包含这两个术语的资产。 在元数据中，显示为智能标记的关键字的排名高于其他元数据字段中显示的关键字。 AEM允许为特定搜索词赋予更高的权重。 此外，还可以提高 [特定搜索词的](#searchrank) 少数目标资产的排名。

为了快速找到相关资产，富界面提供了筛选、排序和选择机制。 您可以根据多个条件筛选结果，并查看针对各种过滤器搜索的资产数量。 或者，也可以通过在“Omnisearch”（全球搜索）字段中更改查询重新运行搜索。 当您更改搜索词或过滤器时，其他过滤器将保留搜索的上下文。

当结果为多个资产时，AEM会在卡视图中显示前100个，在列表视图中显示200个。 用户滚动时，会加载更多资产。 这是为了提高性能。

>[!VIDEO](https://www.youtube.com/watch?v=LcrGPDLDf4o)

有时，您可能会在搜索结果中看到一些意外的资产。 有关详细信息，请参阅 [意外的结果](#troubleshoot-unexpected-search-results-and-issues)。

AEM可以搜索多种文件格式，并且可以自定义搜索过滤器以满足您的业务需求。 请联系您的管理员以了解为您的DAM存储库提供了哪些搜索选项以及您的帐户有哪些限制。

### 包含和不包含增强的智能标记的结果 {#withsmarttags}

默认情况下，AEM搜索将搜索词与AND子句组合在一起。 例如，请考虑搜索正在运行的关键字妇女。 默认情况下，搜索结果中只显示元数据中同时包含女性和正在运行关键字的资产。 当将特殊字符（句点、下划线或虚线）与关键字一起使用时，将保留相同的行为。 以下搜索查询返回相同的结果：

* `woman running`
* `woman.running`
* `woman-running`

但是，该查询会 `woman -running` 返回元数据中 `running` 没有的资产。
使用智能标记可添加一 `OR` 个额外的子句，以查找任何作为所应用智能标记的搜索词。 此类搜索查询中也 `woman` 会显 `running` 示使用或使用智能标记标记的资产。 搜索结果是，

* 元数据中 `woman` 包含 `running` 关键字和关键字的资产（默认行为）。

* 使用任一关键字标记的资产（智能标记行为）。

### Search suggestions as you type {#searchsuggestions}

当您开始键入关键字时，AEM会建议可能的搜索关键字或短语。 建议基于现有资产的元数据。 AEM为所有元数据字段编制索引以帮助搜索。 为了提供搜索建议，系统使用以下几个元数据字段的值。 要提供搜索建议，请考虑使用适当的关键字填充以下字段：

* 资产标记。 (映射到 `jcr:content/metadata/cq:tags`)
* 资产标题。 (映射到 `jcr:content/metadata/dc:title`)
* 资产描述。 (映射到 `jcr:content/metadata/dc:description`)
* JCR存储库中的标题。 该值可能会映射到资产标题。 (映射到 `jcr:content/jcr:title`)
* JCR存储库中的说明。 该值可能会映射到资产描述。 (映射到 `jcr:content/jcr:description`)

要接收多个搜索关键字的建议，请继续键入所有关键字，而不为单个关键字选择任何建议。

![键入多个关键字以视图符合其全部要求的建议](assets/search_suggestionsmanykeywords.gif)

*图：键入多个关键字以视图符合其全部要求的建议*

### 搜索排名和提升 {#searchrank}

首先显示与元数据字段中的所有搜索词匹配的搜索结果，然后显示与智能标记中的任意搜索词匹配的搜索结果。 在上例中，搜索结果的显示大致顺序为：

1. 各个元 `woman running` 数据字段中的匹配项。
1. 智能标 `woman running` 记中的匹配项。
1. 智能标 `woman` 记的匹 `running` 配项或匹配项。

您可以提高特定资产的关键字的相关性，以帮助根据关键字提升搜索。 换句话说，当您基于这些关键字进行搜索时，您为其提升特定关键字的图像将显示在搜索结果顶部。

1. 从 Assets 用户界面中，打开资产的属性页面。单击&#x200B;**[!UICONTROL 高级]**，然后单击/点按&#x200B;**[!UICONTROL 提升搜索关键词**[!UICONTROL &#x200B;下的&#x200B;]**添加]**。
1. 在“搜 **[!UICONTROL 索提升]** ”框中，指定要提升图像搜索的关键字，然后单击／点按添 **[!UICONTROL 加]**。 可以以相同的方式指定多个关键字。
1. 单击／点按保 **[!UICONTROL 存并关闭]**。 您为此关键字提升的资产会显示在顶级搜索结果中。

您可以通过提升目标关键字的搜索结果中某些资产的排名来利用此功能。 请观看以下视频示例。 有关详细信息，请参 [阅在AEM中搜索](https://helpx.adobe.com/experience-manager/kt/assets/using/search-feature-video-use.html)。

>[!VIDEO](https://video.tv.adobe.com/v/16766/?quality=6)

*了解搜索结果的排名方式以及排名如何受到影响。*

## Advanced search {#scope}

AEM提供了各种方法(如适用于搜索的资产的过滤器)，以帮助您更快地找到所需的资产。 下面介绍了一些常用的方法。 下面 [分享了一些图示](#samples) 。

**搜索文件或文件夹**:在搜索结果中，可查看文件、文件夹或两者。 从 **[!UICONTROL 过滤器]** 面板中，可以选择相应的选项。 请参阅 [搜索界面](#searchui)。

**在文件夹内搜索资产**:您可以将搜索限制为特定文件夹。 在过滤器 **[!UICONTROL 面板中]** ，添加文件夹的路径。 一次只能选择一个文件夹。

![通过在“过滤器”面板中添加文件夹路径，将搜索结果限制在文件夹中](assets/search_folder_select.gif)

*图：通过在“过滤器”面板中添加文件夹路径，将搜索结果限制在文件夹中*

### 查找类似图像 {#visualsearch}

要查找与用户选择的图像视觉上相似的图像，请从图像的卡片视图或工具栏中单击&#x200B;**[!UICONTROL 查找类似]**&#x200B;选项。AEM 显示 DAM 存储库中与用户所选图像相似的智能标记图像。请参阅[如何配置相似性搜索](#configvisualsearch)。

![使用卡视图中的选项查找类似图像](assets/search_find_similar.png)

*图：使用卡视图中的选项查找类似图像*

### Adobe Stock图像 {#adobestock}

在AEM用户界面中，用户可以搜索 [Adobe Stock资产](/help/assets/aem-assets-adobe-stock.md) ，并许可所需的资产。 添加 `Location: Adobe Stock` 到Omnisearch栏中。 您还可以使用过滤器面板查找所有授权或未授权的资源，或使用Adobe Stock文件号搜索特定资源。

### Dynamic Media资产 {#dmassets}

您可以通过选择&#x200B;**[!UICONTROL 过滤器]**&#x200B;面板中的 **[!UICONTROL Dynamic Media > 集]**&#x200B;来过滤 Dynamic Media 图像。该操作可过滤并显示图像集、轮播集、混合媒体集和旋转集等资产。

### 使用元数据字段中的特定值进行搜索 {#gqlsearch}

您可以根据特定元数据字段（如标题、说明和作者）的确切值搜索资产。 GQL全文搜索功能只获取其元数据值与您的搜索查询完全匹配的资产。 属性的名称（例如，作者、标题等）和值区分大小写。

| 元数据字段 | Facet值和用法 |
|---|---|
| 标题 | title:John |
| 创建者 | creator:John |
| 位置 | 位置：NA |
| 描述 | description:&quot;Sample Image&quot; |
| 创建程序工具 | creatortool:“Adobe Photoshop CC 2015” |
| 版权所有者 | copyrightowner:&quot;Adobe Systems&quot; |
| 参与者 | contributor:John |
| 使用条款 | usageterms:&quot;CopyRights Reserved&quot; |
| 创建时间 | created:YYYY-MM-DDTHH |
| 过期日期 | expires:YYYY-MM-DDTHH |
| 开始时间 | ontime:YYYY-MM-DDTHH |
| 结束时间 | offtime:YYYY-MM-DDTHH |
| 时间范围（过期日期、开始时间、结束时间） | facet字段：下界……上界 |
| 路径 | /content/dam/&lt;folder name> |
| PDF 标题 | pdftitle:&quot;Adobe Document&quot; |
| 主题 | subject:&quot;Training&quot; |
| 标记 | tags:&quot;Location And Travel&quot; |
| 类型 | type:&quot;image\png&quot; |
| 图像宽度 | width:lowerbound..上界 |
| 图像高度 | height:lowerbound..上界 |
| 人员 | person:John |

属性路径、限制、大小和排序依据不能与任何其他属性一起使用。

用户生成的属性的关键字是属性编辑器中的字段标签（以小写形式），并删除了空格。

以下是复杂查询的一些搜索格式示例：

* To display all assets with multiple facets fields (for example: title=John Doe and creator tool = Adobe Photoshop): `tiltle:"John Doe" creatortool : Adobe*`
* To display all assets when the facets value is not a single word but a sentence (for example: title=Scott Reynolds): `title:"Scott Reynolds"`
* To display assets with multiple values of a single property (for example: title=Scott Reynolds or John Doe): `title:"Scott Reynolds" OR "John Doe"`
* To display assets with property values starting with a specific string (for example: title is Scott Reynolds): `title:Scott*`
* To display assets with property values ending with a specific string (for example: title is Scott Reynolds): `title:*Reynolds`
* To display assets with a property value that contains a specific string (for example: title = Basel Meeting Room): `title:*Meeting*`
* To display assets that contain a particular string and have a specific property value (for example: search for string Adobe in assets having title=John Doe): `*Adobe* title:"John Doe"`

## 从其他AEM产品或界面搜索资产 {#beyondomnisearch}

Adobe Experience Manager(AEM)将DAM存储库连接到各种其他AEM解决方案，以便更快地访问数字资产并简化创作工作流。 任何具有浏览或搜索功能的资产发现开始。 搜索行为在不同的表面和解决方案上基本保持不变。 某些搜索方法会随着目标受众、用例和用户界面的不同而改变，这些搜索方法会因AEM解决方案而异。 下面的链接介绍了各个解决方案的具体方法。 本文介绍了普遍适用的提示和行为。

### 从Adobe Asset Link面板搜索资产 {#aal}

使用Adobe Asset Link，创意专业人士现在可以访问存储在AEM资产中的内容，而无需离开受支持的Adobe Creative Cloud应用程序。 创意人员可以使用Creative Cloud应用程序中的应用程序内面板无缝地浏览、搜索、注销和登记资产：Photoshop、Illustrator和InDesign。 资产链接还允许用户搜索视觉效果相似的结果。 视觉搜索显示结果由Adobe Sensei的机器学习算法提供支持，并帮助用户查找美学上相似的图像。 请参 [阅使用Adobe资产链接搜索](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html#UseAdobeAssetLink) 和浏览资产。

### 在AEM桌面应用程序中搜索资产 {#desktopapp}

创意专业人士使用桌面应用程序使AEM资产可轻松搜索并在其本地桌面（Win或Mac）上可用。 创意人员可以在Mac Finder或Windows资源管理器中轻松显示所需的资产，在桌面应用程序中打开并在本地更改——这些更改将保存回AEM并在存储库中创建了新版本。 应用程序支持使用一个或多个关键字*和？进行基本搜索 通配符和AND运算符。 请参 [阅在桌面应用程序中浏览、搜索和预览](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html#browse-search-preview-assets) 资源。

### Search assets in Brand Portal {#brandportal}

业务线用户和营销人员使用Brand Portal与其扩展的内部团队、合作伙伴和经销商高效、安全地共享获准的数字资产。 See [search assets on Brand Portal](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/search-capabilities/brand-portal-searching.html).

### 搜索Adobe Stock图像 {#adobestock-1}

从AEM用户界面中，用户可以搜索Adobe Stock资产并许可所需的资产。 添加 `Location: Adobe Stock` 到Omnisearch字段。 您还可以使用 **[!UICONTROL 过滤器面板]** ，查找所有授权或未授权的资源，或使用Adobe Stock文件号搜索特定资源。 请参 [阅在AEM中管理Adobe Stock图像](/help/assets/aem-assets-adobe-stock.md#usemanage)。

### 搜索Dynamic Media资产 {#dynamicmedia}

您可以通过选择&#x200B;**[!UICONTROL 过滤器]**&#x200B;面板中的 **[!UICONTROL Dynamic Media]** > **[!UICONTROL 集]**&#x200B;来过滤 Dynamic Media 图像。该操作可过滤并显示图像集、轮播集、混合媒体集和旋转集等资产。在创作网页时，作者可以在内容查找器中搜索集。弹出菜单中提供集的过滤器。

### 在创作网页时在内容查找器中搜索资产 {#contentfinder}

作者可以使用内容查找器在DAM存储库中搜索相关资产，并在他们创建的网页中使用资产。 作者还可以使用“已连接的资产”功能搜索远程AEM部署中可用的资产。 然后，作者可以在本地AEM部署的网页中使用这些资产。 See [use remote assets](/help/assets/use-assets-across-connected-assets-instances.md#use-remote-assets).

### 搜索集合 {#collections}

AEM搜索功能支持搜索集合和搜索集合中的资产。 请参阅 [搜索集合](/help/assets/managing-collections-touch-ui.md)。

## 资产选取器 {#assetselector}

通过资产选取器，您可以以特殊方式搜索、筛选和浏览DAM资产。 资产选取器在上可用 `https://[aem-server]:[port]/aem/assetpicker.html`。 您可以使用此功能提取您选择的资产的元数据。 您可以使用支持的请求参数启动它，例如资产类型（图像、视频、文本）和选择模式（单选或多选）。 这些参数为特定搜索实例设置资产选取器的上下文，并在整个选择过程中保持不变。

资产选取器使用HTML5消 `Window.postMessage` 息将选定资产的数据发送到收件人。 资产选取器仅在浏览模式下工作，并且仅适用于Omnisearch结果页面。

您可以在URL中传递以下请求参数，以在特定上下文中启动资产选取器：

| 名称 | 值 | 示例 | 用途 |
|---|---|---|---|
| 资源后缀(B) | 作为URL中资源后缀的文件夹路径：[https://localhost:4502/aem/assetpicker.html/&lt;folder_path>](https://localhost:4502/aem/assetpicker.html) | 要启动资产选取器并选择特定文件夹(例如，在选定文件夹 `/content/dam/we-retail/en/activities` 的情况下),URL应采用以下形式： [https://localhost:4502/aem/assetpicker.html/content/dam/we-retail/en/activities?assettype=images](https://localhost:4502/aem/assetpicker.html/content/dam/we-retail/en/activities?assettype=images) | 如果在启动资产选择器时需要选择某个特定文件夹，请将其作为资源后缀进行传递。 |
| 模式 | 单个，多个 | <ul><li>[https://localhost:4502/aem/assetpicker.html?mode=single](https://localhost:4502/aem/assetpicker.html?mode=single)</li><li>[https://localhost:4502/aem/assetpicker.html?mode=multiple](https://localhost:4502/aem/assetpicker.html?mode=multiple)</li></ul> | 在多个模式中，您可以使用资产选择器同时选择多个资产。 |
| mimetype | 资产的mimetype(s)(`/jcr:content/metadata/dc:format`)（也支持通配符） | <ul><li>[https://localhost:4502/aem/assetpicker.html?mimetype=image/png](https://localhost:4502/aem/assetpicker.html?mimetype=image/png)</li><li>[https://localhost:4502/aem/assetpicker.html?mimetype=*png](https://localhost:4502/aem/assetpicker.html?mimetype=*png)</li><li>[https://localhost:4502/aem/assetpicker.html?mimetype=*presentation](https://localhost:4502/aem/assetpicker.html?mimetype=*presentation)</li><li>[https://localhost:4502/aem/assetpicker.html?mimetype=*presentation&amp;mimetype=*png](https://localhost:4502/aem/assetpicker.html?mimetype=*presentation&amp;mimetype=*png)</li></ul> | 使用它根据MIME类型筛选资产 |
| 对话框 | true,false | [https://localhost:4502/aem/assetpicker.html?dialog=true](https://localhost:4502/aem/assetpicker.html?dialog=true) | 使用这些参数以Granite对话框的形式打开资产选择器。 仅当您通过Granite路径字段启动资产选择器并将其配置为pickerSrc URL时，此选项才适用。 |
| assettype(S) | 图像，文档，多媒体，存档 | <ul><li>[https://localhost:4502/aem/assetpicker.html?assettype=images](https://localhost:4502/aem/assetpicker.html?assettype=images)</li><li>[https://localhost:4502/aem/assetpicker.html?assettype=documents](https://localhost:4502/aem/assetpicker.html?assettype=documents)</li><li>[https://localhost:4502/aem/assetpicker.html?assettype=multimedia](https://localhost:4502/aem/assetpicker.html?assettype=multimedia)</li><li>[https://localhost:4502/aem/assetpicker.html?assettype=archives](https://localhost:4502/aem/assetpicker.html?assettype=archives)</li></ul> | 使用此选项可根据传递的值筛选资产类型。 |
| 根 | &lt;folder_path> | [https://localhost:4502/aem/assetpicker.html?assettype=images&amp;root=/content/dam/we-retail/en/activities](https://localhost:4502/aem/assetpicker.html?assettype=images&amp;root=/content/dam/we-retail/en/activities) | 使用此选项可指定资产选择器的根文件夹。 在这种情况下，资产选择器允许您仅选择根文件夹下的子资产（直接／间接）。 |

To access the asset Picker interface, go to `https://[aem_server]:[port]/aem/assetpicker`. 导航到所需的文件夹，然后选择一个或多个资产。 或者，从Omnisearch框中搜索所需的资产，根据需要应用筛选器，然后选择它。

![在资产选取器中浏览并选择资产](assets/assetpicker.png)

*图：在资产选取器中浏览并选择资产*

## 限制 {#limitations}

AEM资产中的搜索功能有以下限制：

* 请勿在搜索查询中输入前导空间，否则搜索无效。
* 在您从搜索的结果中选择资产的属性，然后取消搜索后，AEM可能会继续显示搜索词。 <!-- (CQ-4273540) -->
* 搜索文件夹或文件和文件夹时，无法对任何参数对搜索结果进行排序。
* 如果按回车键时未在Omnisearch栏中键入任何内容，AEM将返回仅包含文件（而非文件夹）的列表。 如果您在不使用关键字的情况下专门搜索文件夹，则AEM不会返回任何结果。
* 使用“全 [!UICONTROL 选] ”复选框，您只能选择卡视图中搜索的前100个资产和列表视图中搜索的前200个资产。 如果您在用户界面中滚动并加载更多资产，则可以使用全选选项选 [!UICONTROL 择更多] 。

视觉搜索或相似性搜索具有以下限制：

* 视觉搜索最适合于较大的存储库。 虽然没有达到最佳效果所需的最少图像数，但与一些图像匹配的质量可能不如来自大型存储库的匹配质量好。
* 您无法更改模型或培训AEM以查找类似图像。 例如，向一些资产添加或删除智能标记不会更改模型。 资产确实会从视觉上相似的搜索结果中排除。

在以下情况下，搜索功能可能会有性能限制：

* 与显示搜索结果的视图视图相比，卡列表具有更快的加载时间。

## 搜索提示 {#tips}

* 在监视资产的审核状态时，请使用相应的选项来查找已批准的资产或待批准的资产。
* 使用“分析”谓词，根据从各种Creative应用程序获取的资产使用情况统计信息搜索受支持的资产。 使用情况数据按使用情况得分、印象、点击量和显示资产的媒体渠道进行分组。
* 使用全 **[!UICONTROL 选复选框]** ，选择已搜索的资产。 它选择卡视图中的前100个资源和列表视图中的前200个资源。 您可以对所选内容进行操作，例如，下载选定的资产、批量更新选定资产的元数据属性或将选定的资产添加到收藏集。
* 要搜索不包含强制元数据的资产，请参阅强制 [元数据](#mandatorymetadata)。
* 搜索使用所有元数据字段。 通常，搜索12等通用搜索会返回许多结果。 为获得更好的效果，请使用多次（非单引号），或确保数字与没有特殊字符的单词相邻(例如 *shoe12*)。
* 全文搜索支持-、^等运算符。 要将这些字母作为字符串文本搜索，请将搜索表达式括在多次引号中。 例如，使用“Notebook - Beauty”（笔记本——美容）而不是“Notebook - Beauty”（笔记本——美容）。
* 如果搜索结果过多，请将所 [需资产的搜索范围](#scope) 限制为零。 当您了解如何更好地查找所需的资产（例如，特定文件类型、特定位置、特定元数据等）时，它最适合使用。

* **标记**:标记可帮助您对可以更高效地浏览和搜索的资产进行分类。 标记有助于将相应的分类传播到其他用户和工作流。 AEM优惠了使用Adobe Sensei的人工智能服务自动标记资产的方法，这些服务通过使用和培训不断改进为资产标记的功能。 在搜索资产时，如果帐户中启用了该功能，则智能标记会被纳入其中。 它与AEM的内置搜索功能一起使用。 请参阅 [搜索行为](#searchbehavior)。 要优化搜索结果的显示顺序，您可以提 [升几个选定资产的](#searchrank) 搜索排名。

* **索引**:搜索结果中只返回已索引的元数据和资产。 为获得更好的覆盖面和性能，请确保正确的索引并遵循最佳做法。 请参阅 [索引](#searchindex)。

## 说明搜索的一些示例 {#samples}

使用关键字周围的多次语言可以查找包含用户指定的精确顺序的确切短语的资产。

![带引号和不带引号的搜索行为](assets/search_with_quotes.gif)

*图：带引号和不带引号的搜索行为*

**使用星号通配符搜索**:要扩大搜索范围，请在搜索单词前后使用星号来匹配任意数量的字符。 例如，搜索不带星号的运行不会返回包含该单词任何变体（包括在元数据中）的资产。 星号可替代任意数量的字符。 例如，

* `run` 返回具有精确运行关键字的资产
* `run*` 返回资产，包括运行、运行、失控等。
* `*run` 返回结束、重新运行等。
* `*run*` 返回所有可能的组合。

![使用示例说明在资产搜索中使用星号通配符](assets/search_with_asterisk_run.gif)

*图：使用示例说明在资产搜索中使用星号通配符*

**使用问号通配符搜索**:要扩大搜索范围，请使用一个或多个“?” 字符以匹配字符数。 例如，在下图中，

* `run???` 查询与任何资产均不匹配。

* `run????` 查询将单词与 `running` 后面四个字符匹配 `run`。

* `??run` 查询匹配前面带 `rerun` 有两个字符的单词 `run`。

![通过示例说明在资产搜索中使用问号通配符的方法](assets/search_with_questionmark_run.gif)

*图：通过示例说明在资产搜索中使用问号通配符的方法*

**排除关键字**:使用虚线搜索不包含关键字的资产。 例如， `running -shoe` 查询会返回包含但 `running`不包含的资产 `shoe`。 同样， `camp -night` 查询会返回包含但不 `camp` 包含的资 `night`产。 请注意， `camp-night` 查询会返回同时包含和的 `camp` 资产 `night`。

![使用虚线搜索不包含被排除关键字的资产](assets/search_dash_exclude_keyword.gif)

*图：使用虚线搜索不包含被排除关键字的资产*

## 与搜索功能相关的配置和管理任务 {#configadmin}

### 搜索索引配置 {#searchindex}

资产发现依赖于DAM内容（包括元数据）的索引。 更快、更准确的资源发现依赖于优化的索引和适当的配置。 请参 [阅搜索索引](/help/assets/performance-tuning-guidelines.md#search-indexes)、Oak [查询和索引](/help/sites-deploying/queries-and-indexing.md)，以及 [最佳实践](/help/sites-deploying/best-practices-for-queries-and-indexing.md)。

### 视觉或相似性搜索 {#configvisualsearch}

视觉搜索使用智能标记，并且需要AEM 6.5.2.0或更高版本。 配置智能标记功能后，请按照以下步骤操作。

1. 在AEM CRXDE的节点中， `/oak:index/lucene` 添加以下属性和值并保存更改。

   * `costPerEntry` 类型的属 `Double` 性和值 `10`。

   * `costPerExecution` 类型的属 `Double` 性和值 `2`。

   * `refresh` 类型的属 `Boolean` 性和值 `true`。
   此配置允许从相应的索引中进行搜索。

1. 要创建Lucene索引，请在CRXDE中， `/oak:index/damAssetLucene/indexRules/dam:Asset/properties`创建名为类型 `imageFeatures` 的节点 `nt-unstructured`。 在节 `imageFeatures` 点中，

   * 添 `name` 加具有值 `String` 的类型属性 `jcr:content/metadata/imageFeatures/haystack0`。

   * 添 `nodeScopeIndex` 加值为 `Boolean` 的类型属性 `true`。

   * 添 `propertyIndex` 加值为 `Boolean` 的类型属性 `true`。

   * 添 `useInSimilarity` 加具有值 `Boolean` 的类型属性 `true`。
   保存更改。

1. 访 `/oak:index/damAssetLucene/indexRules/dam:Asset/properties/predictedTags` 问并添 `similarityTags` 加值为 `Boolean` 的类型属性 `true`。
1. 将智能标记应用于AEM存储库中的资产。 了解 [如何配置智能标记](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/metadata/smart-tags-technical-video-setup.html)。
1. 在CRXDE中，在节 `/oak-index/damAssetLucene` 点中，将属性设 `reindex` 置为 `true`。 保存更改。
1. （可选）如果您已自定义搜索表单，则将节 `/libs/settings/dam/search/facets/assets/jcr%3Acontent/items/similaritysearch` 点复制到 `/conf/global/settings/dam/search/facets/assets/jcr:content/items`。 保存所有更改。

有关相关信息，请参 [阅了解AEM中的智能标记](https://helpx.adobe.com/experience-manager/kt/assets/using/smart-tags-feature-video-understand.html) ，以 [及如何管理智能标记](/help/assets/managing-smart-tags.md)。

### 强制元数据 {#mandatorymetadata}

商业用户、管理员或DAM管理员可以将某些元数据定义为必须的元数据，这是业务流程工作所必需的。 由于各种原因，某些资产可能缺少此元数据，如批量迁移的旧版资产或资产。 会根据索引元数据属性检测和报告元数据缺失或无效的资产。 要进行配置，请参阅必 [需的元数据](/help/assets/metadata-schemas.md#define-mandatory-metadata)。

### 修改搜索彩块化 {#searchfacets}

为提高搜索速度，AEM资产会优惠搜索彩块化，您可以使用它筛选搜索结果。 默认情况下，过滤器面板包含一些标准彩块化。 管理员可以自定义过滤器面板，以使用内置谓词修改默认彩块化。 AEM提供了一组不错的内置谓词，以及一个用于自定义彩块化的编辑器。 请参阅 [搜索彩块化](/help/assets/search-facets.md)。

### 上传资产时提取文本 {#extracttextupload}

您可以配置AEM以在用户上传资产（如PSD或PDF文件）时从资产中提取文本。 AEM为提取的文本编制索引，并帮助用户根据提取的文本搜索这些资产。 请参阅 [上传资产](/help/assets/managing-assets-touch-ui.md#uploading-assets)。

### 用于筛选搜索结果的自定义谓词 {#custompredicates}

谓词用于创建彩块化。 管理员可以使用预配置的谓词在“过滤器”面板中自定义搜索彩块化。 这些谓词可以使用叠加进行自定义。 请参阅 [创建自定义谓词](/help/assets/searchx.md)。

您可以根据以下一个或多个属性搜索数字资产。 默认情况下，对这些属性中的某些属性应用的过滤器可用，并且可以自定义创建某些其他过滤器以应用于其他属性。

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
| 视频格式 | DVI、Flash、MPEG4、MPEG、OGG Theora、QuickTime、Windows Media。 值存储在源视频和任何再现的元数据中。 |
| 视频编解码器 | x264。 值仅存储在视频演绎版的元数据中。 |
| 视频比特率 | 指定为最小值和最大值。 值仅存储在视频演绎版的元数据中。 |
| 音频编解码器 | Libvorbis、Lame MP3、AAC编码。 值仅存储在视频演绎版的元数据中。 |
| 音频比特率 | 指定为最小值和最大值。 值仅存储在视频演绎版的元数据中。 |

## 使用资产搜索结果 {#aftersearch}

当您看到一些已搜索的资产符合您的条件后，您可以对这些搜索结果执行以下典型任务或执行以下操作：

* 视图元数据属性和其他信息。
* 下载一个或多个资源。
* 使用“桌面操作”在桌面应用程序中打开这些资产。
* 创建智能收藏集。

### 对搜索结果进行排序 {#sort}

对搜索结果排序可帮助您更快地发现所需的资产。 对搜索结果排序仅在列表视图中有效，并且仅在您从“筛选器 **[!UICONTROL [”面板](#searchui)]**中选择“**[!UICONTROL &#x200B;文件&#x200B;]**”时有效。 AEM资产使用服务器端排序来快速对某个文件夹或搜索查询结果中的所有资产（无论数量多少）进行排序。 与客户端排序相比，服务器端排序提供更快、更准确的结果。

在列表视图中，您可以像对任意文件夹中的资产进行排序一样对搜索结果进行排序。 排序适用于这些列——名称、标题、状态、维度、大小、评级、使用情况、（创建日期）、修改日期、（日期）发布、工作流和签出。

有关排序功能的限制，请参 [阅限制](#limitations)。

### 检查资产的详细信息 {#checkinfo}

您可以从搜索结果页面检查已搜索资产的详细信息。

要查看资产的所有元数据，请选择资产，然后单击工 **[!UICONTROL 具栏中]** 的属性。

要检查对资产或资产版本历史记录的注释，请单击资产以打开大型预览。 打开左边栏中的时间轴，然后选择“ **[!UICONTROL 注释]** ”或“ **[!UICONTROL 版本]**”。 您还可以按时间顺序对时间轴活动（如注释或版本）进行排序。

![对搜索资产的时间轴条目进行排序](assets/sort_timeline_search_results.gif)

*图：对搜索资产的时间轴条目进行排序*

### 下载搜索的资源 {#download}

您可以像从文件夹下载常规资产一样下载搜索的资产及其演绎版。 从搜索结果中选择一个或多个资产，然后单击工 **[!UICONTROL 具栏中]** 的下载。

### 批量更新元数据属性 {#metadataupdates}

可以批量更新多个资产的公用元数据字段。 从搜索结果中，选择一个或多个资产。 单击 **[!UICONTROL 工具栏中]** “属性”，然后根据需要更新元数据。 完成 **[!UICONTROL 后，单击“保存并关闭]** ”。 更新的字段中以前存在的元数据将被覆盖。

对于单个文件夹或集合中可用的资产，无需使用搜索功能即可 [更轻松地批量更新元数](/help/assets/managing-multiple-assets.md) 据。 对于跨文件夹可用或符合通用标准的资产，通过搜索批量更新元数据会更快。

### 智能收藏集 {#collections-1}

收藏集是一组有序的资产，可以包含来自不同位置的资产，因为收藏集只包含对这些资产的引用。 集合有以下两种类型：

* 资产、文件夹和其他集合的静态引用列表。
* 动态列表（智能收藏集），它根据搜索条件填充收藏集中的资产。

您可以根据搜索条件创建智能收藏集。从&#x200B;**[!UICONTROL 过滤器]**&#x200B;面板中，选择&#x200B;**[!UICONTROL 文件]**，然后单击&#x200B;**[!UICONTROL 保存智能收藏集]**。请参阅[管理收藏集](/help/assets/managing-collections-touch-ui.md)。

## 对意外搜索结果和问题进行疑难解答 {#troubleshoot-unexpected-search-results-and-issues}

| 错误、问题、症状 | 可能的原因 | 可能的问题修复或理解 |
|---|---|---|
| 搜索缺少元数据的资产时结果不正确 | 在搜索缺少必需元数据的资产时，AEM可能会显示一些具有有效元数据的资产。 结果基于索引元数据属性。 | 更新元数据后，需要重新构建索引以反映资产元数据的正确状态。 请参阅 [必填元数据](metadata-schemas.md#define-mandatory-metadata)。 |
| 搜索结果过多 | 广泛的搜索参数。 | 考虑限制 [搜索范围](#scope)。 使用智能标记可能会为您提供比预期更多的搜索结果。 查看 [带有智能标记的搜索行为](#withsmarttags)。 |
| 不相关或部分相关的搜索结果 | 搜索行为会随智能标记而改变。 | 了解 [搜索在智能标记后的变化情况](#withsmarttags)。 |
| 没有资产的自动完成建议 | 尚未对新上传的资产编制索引。 在Omnisearch栏中开始键入搜索关键字时，元数据不会立即作为建议可用。 | AEM资产会等到超时期（默认为一小时）到期，然后运行后台作业为所有新上传或更新的资产的元数据编制索引，然后将元数据添加到建议列表。 |
| 无搜索结果 | <ul><li>不存在与您的查询匹配的资产。</li><li>您在搜索查询前添加了空白。</li><li>不支持的元数据字段包含您搜索的关键字。</li><li>为资产配置了开始时间和结束时间，搜索是在资产的结束时间进行的。</li></ul> | <ul><li>使用其他关键字进行搜索。 或者，使用（智能）标记来改进搜索结果。</li><li>这是已知 [的限制](#limitations)。</li><li>并非所有元数据字段都会用于搜索。 请参阅 [范围](#scope)。</li><li>稍后搜索或修改所需资产的开启和关闭时间。</li></ul> |
| 搜索筛选器／谓词不可用 | <ul><li>未配置搜索筛选器。</li><li>登录名中不提供此选项。</li><li>（不太可能）搜索选项未在您使用的部署中自定义。</li></ul> | <ul><li>联系管理员以检查搜索自定义是否可用。</li><li>联系管理员以检查您的帐户是否具有使用自定义的权限。</li><li>联系管理员并检查您所使用的AEM资产部署的可用自定义设置。</li></ul> |
| 在搜索视觉上相似的图像时，缺少期望的图像 | <ul><li>图像在AEM中不可用。</li><li>未索引图像。 通常，在最近上传时。</li><li>图像未标记为智能。</li></ul> | <ul><li>将图像添加到AEM资产。</li><li>请与管理员联系以重新为存储库编制索引。 另外，请确保您使用的是相应的索引。</li><li>请联系您的管理员以智能标记相关资产。</li></ul> |
| 搜索视觉上相似的图像时，将显示不相关的图像 | 视觉搜索行为。 | AEM会显示尽可能多的潜在相关资产。 相关性较差的图像（如果有）会添加到结果中，但搜索级别较低。 当您向下滚动搜索结果时，搜索资产的匹配质量和相关性会降低。 |
| 在选择并操作搜索结果时，所有搜索的资产都不会在 | “全 [!UICONTROL 选] ”选项仅选择卡视图中的前100个搜索结果和列表视图中的前200个搜索结果。 |  |

>[!MORELIKETHIS]
>
>* [AEM搜索实施指南](https://docs.adobe.com/content/help/en/experience-manager-learn/sites/developing/search-tutorial-develop.html)
>* [多值和标记搜索谓词的高级配置](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/metadata/search-feature-video-use.html)
>* [配置智能翻译搜索](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/translation/smart-translation-search-technical-video-setup.html)

