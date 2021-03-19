---
title: 在 [!DNL Adobe Experience Manager]中搜索数字资产和图像
description: 了解如何使用“过滤器”面板在 [!DNL Adobe Experience Manager] 中查找所需的资源，以及如何使用在搜索中显示的资源。
contentOwner: AG
mini-toc-levels: 1
feature: 搜索、元数据
role: 业务从业者
translation-type: tm+mt
source-git-commit: 2e734041bdad7332c35ab41215069ee696f786f4
workflow-type: tm+mt
source-wordcount: '5720'
ht-degree: 6%

---


# 在[!DNL Adobe Experience Manager] {#search-assets-in-aem}中搜索资产

[!DNL Adobe Experience Manager Assets] 提供强大的资产发现方法，帮助您提高内容速度。您的团队可以使用开箱即用的功能和自定义方法，通过无缝、智能的搜索体验缩短上市时间。 搜索资产对于数字资产管理系统的使用至关重要 — 无论是供创意人员进一步使用、供业务用户和营销人员对资产进行可靠管理，还是供DAM管理员管理。 可通过[!DNL Assets]用户界面或其他应用程序和界面执行的简单、高级和自定义搜索有助于满足这些用例。

[!DNL Experience Manager Assets] 支持以下用例，本文介绍这些用例的用法、概念、配置、限制和疑难解答。

| 搜索资产 | 配置和管理 | 处理搜索结果 |
|---|---|---|
| [基本搜索](#searchbasics) | [搜索索引](#searchindex) | [对结果排序](#sort) |
| [了解搜索UI](#searchui) | [视觉或相似性搜索](#configvisualsearch) | [检查资产的属性和元数据](#checkinfo) |
| [搜索建议](#searchsuggestions) | [强制元数据](#mandatorymetadata) | [下载](#download) |
| [了解搜索结果和行为](#searchbehavior) | [修改搜索彩块化](#searchfacets) | [批量元数据更新](#metadataupdates) |
| [搜索排名和提升](#searchrank) | [文本提取](#extracttextupload) | [智能收藏集](#collections) |
| [高级搜索：筛选和搜索范围](#scope) | [自定义谓词](#custompredicates) | [了解意外结果并排除其他故障](#unexpectedresults) |
| [从其他解决方案和应用程序中搜索](#beyondomnisearch):<ul><li>[Adobe Asset Link](#aal)</li><li>[Brand Portal](#brandportal)</li><li>[Experience Manager桌面应用程序](#desktopapp)</li><li>[Adobe Stock图像](#adobestock)</li><li>[Dynamic Media assets](#dynamicmedia)</li></ul> |  |  |
| [资产选择器](#assetpicker) |  |  |
| [限](#limitations) 制和提 [示](#tips) |  |  |
| [插图示例](#samples) |  |  |

使用[!DNL Experience Manager] Web界面顶部的Omnisearch字段搜索资产。 转至[!DNL Experience Manager]中的&#x200B;**[!UICONTROL 资产]** > **[!UICONTROL 文件]**，单击顶栏中的![search_icon](assets/do-not-localize/search_icon.png)，输入搜索关键字，然后选择`Return`。 或者，使用关键字快捷键`/`（正斜杠）打开Omnisearch字段。 `Location:Assets` 已预选，以将搜索限制为DAM资产。[!DNL Experience Manager] 在开始键入搜索关键字时提供建议。

使用&#x200B;**[!UICONTROL 过滤器]**&#x200B;面板可搜索资产、文件夹、标记和元数据。 您可以根据各种选项（谓词）(如文件类型、文件大小、上次修改日期、资产状态、分析数据和Adobe Stock许可)筛选搜索结果。 您可以自定义“过滤器”面板，并使用[search facets](/help/assets/search-facets.md)添加或删除搜索谓词。 [!UICONTROL 过滤器]面板中的[!UICONTROL 文件类型]筛选器具有混合状态复选框。 因此，除非您选择所有嵌套的谓词（或格式），否则将部分选中第一级复选框。

[!DNL Experience Manager] 搜索功能支持搜索收藏集和搜索收藏集中的资产。请参阅[搜索集合](/help/assets/manage-collections.md)。

## 了解搜索接口{#searchui}

熟悉搜索界面和可用的操作。

![了解Experience Manager Assets搜索结果界面](assets/aem_search_results.png)

*图：了解 [!DNL Experience Manager Assets] 搜索结果界面。*

**答：将** 搜索另存为智能收藏集。**B.** 过滤器或谓词以缩小搜索结果。**C.显** 示文件、文件夹或两者。**D.** 单击“过滤器”以打开或关闭左边栏。**E.** 搜索位置为 DAM。**包含用** 户提供的搜索关键字的F.Omnisearch字段。**G.选** 择加载的搜索结果。**H.显** 示的搜索结果总数中显示的搜索结果数。**闭** 门搜索。**J.在** 卡视图和列表视图之间切换。

### 动态搜索彩块化{#dynamicfacets}

您可以使用搜索彩块化中动态更新的预期搜索结果数量，从搜索结果页面更快地发现所需的资产。 预期的资产数量会在应用搜索筛选器之前进行更新。 查看过滤器的预期计数可帮助您快速、高效地浏览搜索结果。

![在搜索彩块化中查看资产的大致数量，而无需筛选搜索结果。](assets/asset_search_results_in_facets_filters.png)

*图：在搜索彩块化中查看资产的大致数量，而无需筛选搜索结果。*

## 了解搜索结果和行为{#searchbehavior}

### 基本搜索词和结果{#searchbasics}

您可以从OmniSearch字段运行关键字搜索。 关键字搜索不区分大小写，并且是全文搜索（跨常用元数据字段）。 如果使用了多个关键字，则`AND`是关键字之间的默认运算符。

结果按相关性排序，从最接近的匹配开始。 对于多个关键字，更具相关性的结果是资产的元数据中包含这两个术语。 在元数据中，显示为智能标记的关键字比其他元数据字段中显示的关键字排名更高。 [!DNL Experience Manager] 允许赋予特定搜索词更高的权重。此外，还可以[提升特定搜索词的少数目标资产的排名](#searchrank)。

为了快速找到相关资源，富界面提供了筛选、排序和选择机制。 您可以根据多个条件筛选结果，并查看针对各种过滤器搜索的资产数。 或者，也可以通过更改“全搜索”字段中的查询重新运行搜索。 当您更改搜索词或过滤器时，其他过滤器仍会被应用以保留搜索的上下文。

当结果为多个资产时，[!DNL Experience Manager]在卡视图中显示前100个，在列表视图中显示200个。 用户滚动时，会加载更多资源。 这是为了提高性能。 观看显示的[资产数量](https://www.youtube.com/watch?v=LcrGPDLDf4o)的视频演示。

有时，您可能会在搜索结果中看到一些意外的资产。 有关详细信息，请参阅[意外结果](#troubleshoot-unexpected-search-results-and-issues)。

[!DNL Experience Manager] 可以搜索多种文件格式，并且可以自定义搜索过滤器以满足您的业务需求。请与管理员联系，了解为您的DAM存储库提供了哪些搜索选项以及您的帐户具有哪些限制。

### 包含和不包含增强的智能标签{#withsmarttags}

默认情况下，[!DNL Experience Manager]搜索将搜索词与AND子句组合。 例如，请考虑搜索关键词“women running”。 默认情况下，搜索结果中只显示元数据中同时包含女性和正在运行关键字的资产。 当将特殊字符（句点、下划线或破折号）与关键字一起使用时，将保留相同的行为。 以下搜索查询返回相同的结果：

* `woman running`
* `woman.running`
* `woman-running`

但是，查询`woman -running`返回元数据中没有`running`的资产。
使用智能标记可添加额外的`OR`子句，以查找任何作为所应用智能标记的搜索词。 在此类搜索查询中，也会显示使用智能标签标记为`woman`或`running`的资产。 搜索结果是，

* 元数据中具有`woman`和`running`关键字的资产（默认行为）。

* 使用任一关键字标记的资产（智能标记行为）。

### 在键入{#searchsuggestions}时搜索建议

当您开始键入关键字时，[!DNL Experience Manager]建议可能的搜索关键字或短语。 建议基于现有资产的元数据。 [!DNL Experience Manager] 索引所有元数据字段以帮助搜索。为了提供搜索建议，系统使用以下几个元数据字段的值。 要提供搜索建议，请考虑使用适当的关键字填充以下字段：

* 资产标记。 （映射到`jcr:content/metadata/cq:tags`）
* 资产标题。 （映射到`jcr:content/metadata/dc:title`）
* 资产描述。 （映射到`jcr:content/metadata/dc:description`）
* JCR存储库中的标题。 该值可能会被映射到资产标题。 （映射到`jcr:content/jcr:title`）
* JCR存储库中的说明。 该值可能会被映射到资产描述。 （映射到`jcr:content/jcr:description`）

要接收多个搜索关键字的建议，请继续键入所有关键字，而不为单个关键字选择任何建议。

![键入多个关键字以视图建议，使其全部适合](assets/search_suggestionsmanykeywords.gif)

*图：键入多个关键字以视图建议，使其全部适合。*

### 搜索排名和提升{#searchrank}

首先显示与元数据字段中所有搜索词匹配的搜索结果，然后显示与智能标记中任何搜索词匹配的搜索结果。 在上例中，搜索结果的大致显示顺序为：

1. `woman running`在各种元数据字段中的匹配项。
1. 智能标记中`woman running`的匹配项。
1. 智能标记中`woman`或`running`的匹配项。

您可以提高特定资产的关键字相关性，以帮助根据关键字提升搜索。 换句话说，当您基于这些关键字进行搜索时，您提升其特定关键字的图像会显示在搜索结果的顶部。

1. 从[!DNL Assets]用户界面中，打开资产的属性页。 单击&#x200B;**[!UICONTROL 高级]**，然后单击&#x200B;**[!UICONTROL 提升搜索关键字]**&#x200B;下的&#x200B;**[!UICONTROL 添加]**。
1. 在&#x200B;**[!UICONTROL 搜索提升]**&#x200B;框中，指定要提升图像搜索的关键字，然后单击&#x200B;**[!UICONTROL 添加]**。 可以以相同方式指定多个关键字。
1. 单击&#x200B;**[!UICONTROL 保存并关闭]**。您为此关键字提升的资产会显示在顶级搜索结果中。

您可以通过提升目标关键字的搜索结果中某些资产的排名来利用此功能。 请参阅下面的示例视频。 有关详细信息，请参阅[在 [!DNL Experience Manager]](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/search-and-discovery/search-boost.html)中搜索。

>[!VIDEO](https://video.tv.adobe.com/v/16766/?quality=6)

*视频：了解搜索结果的排名方式以及排名的影响。*

## 高级搜索{#scope}

[!DNL Experience Manager] 提供了各种方法(如应用于搜索的资源的过滤器)，以帮助您更快地查找所需的资源。下面介绍了一些常用的方法。 下面共享了一些[说明示例](#samples)。

**搜索文件或文件夹**:在搜索结果中，可查看文件、文件夹或两者。从&#x200B;**[!UICONTROL 过滤器]**&#x200B;面板中，可以选择相应的选项。 请参阅[搜索接口](#searchui)。

**在文件夹内搜索资产**:您可以将搜索限制为特定文件夹。在&#x200B;**[!UICONTROL 过滤器]**&#x200B;面板中，添加文件夹的路径。 一次只能选择一个文件夹。

![通过在“过滤器”面板中添加文件夹路径，将搜索结果限制为文件夹](assets/search_folder_select.gif)

*图：通过在“过滤器”面板中添加文件夹路径，将搜索结果限制为文件夹。*

### 查找类似图像{#visualsearch}

要查找与用户选择的图像视觉上相似的图像，请从图像的卡片视图或工具栏中单击&#x200B;**[!UICONTROL 查找类似]**&#x200B;选项。[!DNL Experience Manager] 显示 DAM 存储库中与用户所选图像相似的智能标记图像。请参阅[如何配置相似性搜索](#configvisualsearch)。

![使用卡视图中的选项查找类似图像](assets/search_find_similar.png)

*图：使用卡视图中的选项查找类似图像。*

### Adobe Stock图像{#adobestock}

在[!DNL Experience Manager]用户界面中，用户可以搜索[Adobe Stock资产](/help/assets/aem-assets-adobe-stock.md)并许可所需的资产。 在搜索栏中添加`Location: Adobe Stock`。 您还可以使用“过滤器”面板查找所有授权或未授权的资源，或使用Adobe Stock文件号搜索特定资源。

### Dynamic Media assets {#dmassets}

您可以通过选择&#x200B;**[!UICONTROL 过滤器]**&#x200B;面板中的 **[!UICONTROL Dynamic Media]** > **[!UICONTROL 集]**&#x200B;来过滤 Dynamic Media 图像。该操作可过滤并显示图像集、轮播集、混合媒体集和旋转集等资产。

### 使用元数据字段{#gqlsearch}中的特定值进行搜索

您可以根据特定元数据字段（如标题、描述和作者）的准确值搜索资产。 GQL全文搜索功能仅获取其元数据值与您的搜索查询完全匹配的资产。 属性的名称（例如作者、标题等）和值区分大小写。

| 元数据字段 | Facet值和用法 |
| ----------------------------------------- | --------------------------------------- |
| 标题 | `title:John` |
| 创建者 | `creator:John` |
| 位置 | `location:NA` |
| 描述 | `description:"Sample Image"` |
| 创建者工具 | `creatortool:"Adobe Photoshop CC 2020"` |
| 版权所有者 | `copyrightowner:"Adobe Systems"` |
| 参与者 | `contributor:John` |
| 使用条款 | `usageterms:"CopyRights Reserved"` |
| 创建时间 | `created`:YYYY-MM-DDTHH |
| 过期日期 | `expires`:YYYY-MM-DDTHH |
| 开始时间 | `ontime`:YYYY-MM-DDTHH |
| 结束时间 | `offtime`:YYYY-MM-DDTHH |
| 时间范围（过期日期、开始时间、结束时间） | `facet field`:lowerbound...上 |
| 路径 | /content/dam/&lt;folder name> |
| PDF 标题 | `pdftitle`:&quot;Adobe文档&quot; |
| 主题 | `subject:"Training"` |
| 标记 | `tags:"Location And Travel"` |
| 类型 | `type:"image\png"` |
| 图像宽度 | `width`:lowerbound...上 |
| 图像高度 | `height`:lowerbound...上 |
| 人员 | `person:John` |

不能将属性`OR`、`limit`、`size`和`orderby`与任何其他属性一起使用。`path`

用户生成的属性的关键字是属性编辑器中的字段标签（以小写形式），删除了空格。

以下是复杂查询的一些搜索格式示例：

* 要显示包含多个facet字段的所有资产，请执行以下操作：title=John Doe and creator tool = Adobe Photoshop):`title:"John Doe" creatortool:Adobe*`
* 要在facet值不是单个词而是句子时显示所有资产(例如：title=Scott Reynolds):`title:"Scott Reynolds"`
* 要显示具有单个属性的多个值的资产，请执行以下操作：title=Scott Reynolds或John Doe):`title:"Scott Reynolds" OR "John Doe"`
* 要显示包含以特定字符串开头的属性值的资产(例如：标题是Scott Reynolds):`title:Scott*`
* 要显示具有以特定字符串结尾的属性值的资产(例如：标题是Scott Reynolds):`title:*Reynolds`
* 要显示包含包含特定字符串的属性值的资产，请执行以下操作：title =巴塞尔会议室):`title:*Meeting*`
* 要显示包含特定字符串并具有特定属性值的资产(例如：在标题为John Doe的资产中搜索字符串Adobe):`*Adobe* title:"John Doe"`

## 从其他[!DNL Experience Manager]产品或接口{#beyondomnisearch}搜索资产

[!DNL Adobe Experience Manager] 将DAM存储库连接到各种其他解 [!DNL Experience Manager] 决方案，以便更快地访问数字资产并简化创意工作流。具有浏览或搜索的任何资源发现开始。 搜索行为在不同的界面和解决方案中基本保持不变。 某些搜索方法会随着目标受众、用例和用户界面的不同而改变，而这些方法会随着[!DNL Experience Manager]解决方案的不同而改变。 以下链接介绍了针对各个解决方案的具体方法。 本文描述了普遍适用的技巧和行为。

### 从“Adobe资源链接”面板{#aal}搜索资源

使用Adobe Asset Link，创意专业人士现在可以访问存储在[!DNL Experience Manager Assets]中的内容，而无需离开受支持的Adobe Creative Cloud应用程序。 Creatives可以使用[!DNL Adobe Creative Cloud apps]中的应用程序内面板无缝地浏览、搜索、注销和登录资产：[!DNL Adobe Photoshop]、[!DNL Adobe Illustrator]和[!DNL Adobe InDesign]。 资产链接还允许用户搜索视觉上相似的结果。 可视搜索显示结果由Adobe Sensei的机器学习算法提供支持，并帮助用户查找美学上相似的图像。 请参阅使用Adobe资产链接搜索和浏览资产](https://helpx.adobe.com/cn/enterprise/using/manage-assets-using-adobe-asset-link.html#UseAdobeAssetLink)。[

### 在[!DNL Experience Manager]桌面应用程序{#desktopapp}中搜索资产

创意专业人士使用桌面应用程序使[!DNL Experience Manager Assets]易于搜索并可在其本地桌面（Win或Mac）上使用。 Creatives可以轻松地在Mac Finder或Windows资源管理器中显示所需的资产，在桌面应用程序中打开，并在本地进行更改 — 这些更改将通过在存储库中创建的新版本保存回[!DNL Experience Manager]。 应用程序支持使用一个或多个关键字、`*`和`?`通配符以及`AND`运算符进行基本搜索。 请参阅[在桌面应用程序中浏览、搜索和预览资产](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#browse-search-preview-assets)。

### 在[!DNL Brand Portal] {#brandportal}中搜索资产

业务线用户和营销人员使用Brand Portal与其扩展的内部团队、合作伙伴和经销商高效、安全地共享获准的数字资产。 请参阅[在Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/search-capabilities/brand-portal-searching.html)上搜索资产。

### 搜索[!DNL Adobe Stock]图像{#adobestock-1}

在[!DNL Experience Manager]用户界面中，用户可以搜索Adobe Stock资产并许可所需的资产。 在Omnisearch字段中添加`Location: Adobe Stock`。 您还可以使用&#x200B;**[!UICONTROL 过滤器]**&#x200B;面板查找所有授权或未授权的资源，或使用Adobe Stock文件号搜索特定资源。 请参阅[在Experience Manager](/help/assets/aem-assets-adobe-stock.md#usemanage)中管理Adobe Stock映像。

### 搜索Dynamic Media资产{#dynamicmedia}

您可以通过选择&#x200B;**[!UICONTROL 过滤器]**&#x200B;面板中的 **[!UICONTROL Dynamic Media]** > **[!UICONTROL 集]**&#x200B;来过滤 Dynamic Media 图像。该操作可过滤并显示图像集、轮播集、混合媒体集和旋转集等资产。在创作网页时，作者可以在内容查找器中搜索集。弹出菜单中提供集的过滤器。

### 创作网页时在内容查找器中搜索资产{#contentfinder}

作者可以使用内容查找器在DAM存储库中搜索相关资产，并使用他们创建的网页中的资产。 作者还可以使用“已连接资产”功能搜索远程[!DNL Experience Manager]部署中可用的资产。 然后，作者可以在本地[!DNL Experience Manager]部署的网页中使用这些资源。 请参阅[使用远程资源](/help/assets/use-assets-across-connected-assets-instances.md#use-remote-assets)。

### 搜索集合{#collections}

[!DNL Experience Manager] 搜索功能支持搜索收藏集和搜索收藏集中的资产。请参阅[搜索集合](/help/assets/manage-collections.md)。

## 资产选择器{#assetpicker}

>[!NOTE]
>
>资产选择器在[!DNL Adobe Experience Manager]的先前版本中称为[资产选取器](https://helpx.adobe.com/experience-manager/6-2/assets/using/asset-picker.html)。

通过资产选择器，您可以以一种特殊的方式浏览、搜索和筛选DAM资产。 您可以使用`https://[aem-server]:[port]/aem/assetpicker.html`在[!DNL Experience Manager]实例中启动资产选择器。 此URL将在浏览模式下打开资产选择器。 使用支持的请求参数作为后缀，如`mode`（单选或多选）或`viewmode`（图像、视频、文本）和`mimetype`。 `assettype`这些参数为特定搜索实例设置资产选择器的上下文，并在整个选择过程中保持不变。 您还可以使用此功能获取您选择的资产的元数据。

资产选择器使用HTML5 `Window.postMessage`消息将选定资产的数据发送到收件人。 它仅在浏览模式下工作，并且仅在Omnisearch结果页面中工作。

在URL中传递以下请求参数，以在特定上下文中启动资产选择器：

| 名称 | 值 | 示例 | 用途 |
|---|---|---|---|
| 资源后缀(B) | 作为URL中资源后缀的文件夹路径：[https://localhost:4502/aem/assetpicker.html/&lt;folder_path>](https://localhost:4502/aem/assetpicker.html) | 要启动资产选择器并选择特定的文件夹（例如，选择了文件夹`/content/dam/we-retail/en/activities`），URL应采用以下格式：[https://localhost:4502/aem/assetpicker.html/content/dam/we-retail/en/activities?assettype=images](https://localhost:4502/aem/assetpicker.html/content/dam/we-retail/en/activities?assettype=images) | 如果在启动资产选择器时需要选择特定文件夹，请将其作为资源后缀进行传递。 |
| `mode` | 单个，多个 | <ul><li>[https://localhost:4502/aem/assetpicker.html?mode=single](https://localhost:4502/aem/assetpicker.html?mode=single)</li><li>[https://localhost:4502/aem/assetpicker.html?mode=multiple](https://localhost:4502/aem/assetpicker.html?mode=multiple)</li></ul> | 在多个模式中，您可以使用资产选择器同时选择多个资产。 |
| `dialog` | true、false | [https://localhost:4502/aem/assetpicker.html?dialog=true](https://localhost:4502/aem/assetpicker.html?dialog=true) | 使用这些参数以Granite对话框的形式打开资产选择器。 此选项仅在您通过Granite路径字段启动资产选择器并将其配置为pickerSrc URL时适用。 |
| `root` | &lt;folder_path> | [https://localhost:4502/aem/assetpicker.html?assettype=images&amp;root=/content/dam/we-retail/en/activities](https://localhost:4502/aem/assetpicker.html?assettype=images&amp;root=/content/dam/we-retail/en/activities) | 使用此选项可指定资产选择器的根文件夹。 在这种情况下，资产选择器允许您仅选择根文件夹下的子资产（直接/间接）。 |
| `viewmode` | 搜索 |  | 要在搜索模式下启动资产选择器，请使用资产类型和mimetype参数。 |
| `assettype` | 图像、文档、多媒体、存档。 | <ul><li>[https://localhost:4502/aem/assetpicker.html?viewmode=search&amp;assettype=images](https://localhost:4502/aem/assetpicker.html?viewmode=search&amp;assettype=images)</li><li>[https://localhost:4502/aem/assetpicker.html?viewmode=search&amp;assettype=documents](https://localhost:4502/aem/assetpicker.html?assettype=documents)</li><li>[https://localhost:4502/aem/assetpicker.html?viewmode=search&amp;assettype=multimedia](https://localhost:4502/aem/assetpicker.html?viewmode=search&amp;assettype=multimedia)</li><li>[https://localhost:4502/aem/assetpicker.html?viewmode=search&amp;assettype=archives](https://localhost:4502/aem/assetpicker.html?viewmode=search&amp;assettype=archives)</li></ul> | 使用此选项可根据提供的值筛选资产类型。 |
| `mimetype` | 资产的MIME类型(`/jcr:content/metadata/dc:format`)（也支持通配符）。 | <ul><li>[https://localhost:4502/aem/assetpicker.html?viewmode=search&amp;mimetype=image/png](https://localhost:4502/aem/assetpicker.html?viewmode=search&amp;mimetype=image/png)</li><li>[https://localhost:4502/aem/assetpicker.html?viewmode=search&amp;mimetype=*png](https://localhost:4502/aem/assetpicker.html?viewmode=search&amp;mimetype=*png)</li><li>[https://localhost:4502/aem/assetpicker.html?viewmode=search&amp;mimetype=*presentation](https://localhost:4502/aem/assetpicker.html?viewmode=search&amp;mimetype=*presentation)</li><li>[https://localhost:4502/aem/assetpicker.html?viewmode=search&amp;mimetype=*presentation&amp;mimetype=*png](https://localhost:4502/aem/assetpicker.html?viewmode=search&amp;mimetype=*presentation&amp;mimetype=*png)</li></ul> | 使用它可以根据MIME类型筛选资产。 |

要访问资产选择器接口，请转至`https://[aem_server]:[port]/aem/assetpicker`。 导航到所需的文件夹，然后选择一个或多个资产。 或者，从搜索框中搜索所需的资产，根据需要应用筛选器，然后选择它。

![在资产选择器中浏览并选择资产](assets/assetpicker.png)

*图：在资产选择器中浏览并选择资产。*

## 限制 {#limitations}

[!DNL Experience Manager Assets]中的搜索功能具有以下限制：

* 请勿在搜索查询中输入行距，否则搜索无效。
* [!DNL Experience Manager] 在您从搜索结果中选择资产的属性，然后取消搜索后，可能会继续显示搜索词。  <!-- (CQ-4273540) -->
* 在搜索文件夹或文件和文件夹时，无法按任何参数对搜索结果排序。
* 如果您选择`Return`而未在Omnisearch栏中键入内容，[!DNL Experience Manager]将返回仅包含文件而非文件夹的列表。 如果您专门搜索文件夹而不使用关键字，[!DNL Experience Manager]不会返回任何结果。

视觉搜索或相似性搜索具有以下限制：

* 视觉搜索在大型存储库中效果最佳。 虽然没有获得最佳效果所需的最少图像数，但与几个图像的匹配质量不如来自大型存储库的匹配质量好。
* 不能更改模型或训练[!DNL Experience Manager]以查找类似图像。 例如，向一些资产添加或删除智能标记不会更改模型。 资产会从视觉上相似的搜索结果中排除。

在以下情况下，搜索功能可能存在性能限制：

* 与显示搜索结果的列表视图相比，卡视图的加载时间更短。

## 搜索提示{#tips}

* 在监视资产的审核状态时，请使用相应的选项来查找已批准的资产或正在等待批准的资产。
* 使用“分析”谓词，根据从各种Creative应用程序获取的资产使用情况统计信息搜索受支持的资产。 使用情况渠道按使用情况得分、展示次数、点击次数和资产显示类别的媒体数据分组。
* 使用&#x200B;**[!UICONTROL 全选]**&#x200B;复选框选择已搜索的资产。 [!DNL Experience Manager] 最初在卡视图中显示100个资产，在列表视图中显示200个资产。滚动搜索结果时会加载更多资产。 您可以选择比加载的资产更多的资产。 选定资产的计数会显示在搜索结果页面的右上角。 您可以对所选内容进行操作，例如，下载选定的资产、批量更新选定资产的元数据属性或将选定的资产添加到收藏集。 当选择的资产多于显示的资产时，会对所有选定的资产应用一个操作，或者出现一个对话框，显示所应用的资产数。 要对未加载的资产应用操作，请确保已明确选择所有资产。
* 要搜索不包含强制元数据的资产，请参阅[强制元数据](#mandatorymetadata)。
* 搜索使用所有元数据字段。 通常，搜索12等通用搜索会返回许多结果。 为获得更好的效果，请使用多次（非单引号），或确保数字与没有特殊字符的单词相邻（例如`shoe12`）。
* 全文搜索支持`-`和`^`等运算符。 要将这些字母作为字符串文本搜索，请将搜索表达式括在多次引号中。 例如，使用`"Notebook - Beauty"`代替`Notebook - Beauty`。
* 如果搜索结果太多，请将所需资产的搜索范围[限制为零。 ](#scope)如果您对如何更好地查找所需的资源（例如特定文件类型、特定位置、特定元数据等）有所了解，它最适合您。

* **标记**:标记可帮助您对可以更高效地浏览和搜索的资产进行分类。Tagging有助于将适当的分类传播到其他用户和工作流。 [!DNL Experience Manager] 优惠使用Adobe Sensei的人为智能服务自动标记资源的方法，这些服务通过使用和培训不断改进资产标记功能。在您搜索资产时，如果您的帐户中启用了该功能，则智能标记也会纳入其中。 它与内置的搜索功能配合使用。 请参阅[搜索行为](#searchbehavior)。 要优化搜索结果的显示顺序，您可以[提升少数选定资产的搜索排名](#searchrank)。

* **索引**:搜索结果中只返回已索引的元数据和资产。为获得更好的覆盖和性能，请确保正确编制索引并遵循最佳做法。 请参阅[索引](#searchindex)。

* 要从搜索结果中排除特定资产，请使用Lucene索引中的`excludedPath`属性。

## 说明搜索{#samples}的一些示例

使用关键字周围的多次语录，查找按用户指定的准确顺序包含相应短语的资产。

![带引号和不带引号的搜索行为](assets/search_with_quotes.gif)

*图：带引号和不带引号的搜索行为。*

**使用星号通配符搜索**:要扩大搜索范围，请在搜索词之前或之后使用星号来匹配任意数量的字符。例如，搜索运行时不带星号不会返回包含该单词任何变体（包括在元数据中）的资产。 星号替代任意数字。 例如，

* `run` 返回具有准确运行关键字的资产
* `run*` 返回 `running`包含 `run`、 `runaway`等的资产。
* `*run` 返回 `outrun`资产 `rerun`等。
* `*run*` 返回所有可能的组合。

![通过示例说明在资产搜索中使用星号通配符](assets/search_with_asterisk_run.gif)

*图：通过示例说明在资产搜索中使用星号通配符。*

**使用问号通配符搜索**:要扩大搜索范围，请使用一个或多个“？”字符数与字符数完全匹配。 例如，在下图中，

* `run???` 查询与任何资产均不匹配。

* `run????` 查询匹配后 `running` 面带四个字符的 `run`单词。

* `??run` 查询与前面带 `rerun` 有两个字符的单词 `run`匹配。

![通过示例说明在资产搜索中使用问号通配符](assets/search_with_questionmark_run.gif)

*图：通过示例说明在资产搜索中使用问号通配符。*

**排除关键字**:使用短划线搜索不包含关键字的资产。例如，`running -shoe` 查询返回包含`running`但不包含`shoe`的资产。 同样，`camp -night` 查询返回包含`camp`但不包含`night`的资产。 查询`camp-night`返回同时包含`camp`和`night`的资产。

![使用虚线搜索不包含排除关键字的资产](assets/search_dash_exclude_keyword.gif)

*图：使用短划线搜索不包含排除的关键字的资产。*

## 与搜索功能{#configadmin}相关的配置和管理任务

### 搜索索引配置{#searchindex}

资产发现依赖于DAM内容（包括元数据）的索引。 更快、更准确的资产发现依赖于优化的索引和适当的配置。 请参阅[搜索索引](/help/assets/performance-tuning-guidelines.md#search-indexes)、[oak查询和索引](/help/sites-deploying/queries-and-indexing.md)和[最佳做法](/help/sites-deploying/best-practices-for-queries-and-indexing.md)。

要从搜索结果中排除特定资产，请使用Lucene索引中的`excludedPath`属性。

### 视觉或相似性搜索{#configvisualsearch}

视觉搜索使用智能标记，并需要[!DNL Experience Manager] 6.5.2.0或更高版本。 配置智能标记功能后，请执行以下步骤：

1. 在[!DNL Experience Manager] CRXDE的`/oak:index/lucene`节点中，添加以下属性和值并保存更改。

   * `costPerEntry` 值类型 `Double` 的属性 `10`
   * `costPerExecution` 值类型 `Double` 的属性 `2`
   * `refresh` 值类型 `Boolean` 的属性 `true`

   此配置允许从相应的索引中进行搜索。

1. 要创建Lucene索引，请在CRXDE的`/oak:index/damAssetLucene/indexRules/dam:Asset/properties`处创建名为`imageFeatures`的`nt-unstructured`类型的节点。 在`imageFeatures`节点中，

   * 添加`name`属性，类型为`String`，值为`jcr:content/metadata/imageFeatures/haystack0`。
   * 添加`Boolean`类型的`nodeScopeIndex`属性，其值为`true`。
   * 添加`Boolean`类型的`propertyIndex`属性，其值为`true`。
   * 添加`useInSimilarity`属性，类型为`Boolean`，值为`true`。

   保存更改。

1. 访问`/oak:index/damAssetLucene/indexRules/dam:Asset/properties/predictedTags`并添加`Boolean`类型的`similarityTags`属性，其值为`true`。
1. 将智能标记应用于[!DNL Experience Manager]存储库中的资产。
1. 在CRXDE的`/oak-index/damAssetLucene`节点中，将`reindex`属性设置为`true`。 保存更改。
1. （可选）如果您已自定义搜索表单，则将`/libs/settings/dam/search/facets/assets/jcr%3Acontent/items/similaritysearch`节点复制到`/conf/global/settings/dam/search/facets/assets/jcr:content/items`。 保存更改。

有关信息，请参阅[了解Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/metadata/image-smart-tags.html)中的智能标签和[如何管理智能标签](/help/assets/enhanced-smart-tags.md)。

>[!CAUTION]
>
>如果在[!DNL Adobe Experience Manager]之外完成了Lucene索引，则基于智能标签的搜索不会按预期工作。

### 必需元数据{#mandatorymetadata}

业务用户、管理员或DAM管理员可以将某些元数据定义为必须的元数据，这是业务流程正常工作所必须的。 由于各种原因，某些资产可能缺少此元数据，例如批量迁移的旧资产或资产。 系统会根据索引元数据属性检测并报告元数据缺失或无效的资产。 要进行配置，请参阅[必备元数据](/help/assets/metadata-schemas.md#define-mandatory-metadata)。

### 修改搜索彩块化{#searchfacets}

为了提高搜索速度，[!DNL Experience Manager Assets]会优惠搜索彩块化，您可以使用这些彩块来筛选搜索结果。 默认情况下，“过滤器”面板包含一些标准彩块化。 管理员可以自定义“过滤器”面板，以使用内置谓词修改默认彩块化。 [!DNL Experience Manager] 提供了一系列内置谓词和用于自定义facet的编辑器。请参阅[搜索彩块化](/help/assets/search-facets.md)。

### 上传资产{#extracttextupload}时提取文本

您可以配置[!DNL Experience Manager]以在用户上传资产（如PSD或PDF文件）时从资产中提取文本。 [!DNL Experience Manager] 对提取的文本进行索引，并帮助用户根据提取的文本搜索这些资产。请参阅[上传资产](/help/assets/manage-assets.md#uploading-assets)。

如果文本提取对您的部署而言资源占用过多，请考虑[禁用文本提取](https://helpx.adobe.com/experience-manager/kb/Disable-binary-text-extraction-to-optimize-Lucene-indexing-AEM.html)。

### 用于筛选搜索结果{#custompredicates}的自定义谓词

谓词用于创建彩块化。 管理员可以使用预配置的谓词自定义“过滤器”面板中的搜索彩块化。 可以使用叠加自定义这些谓词。 请参阅[创建自定义谓词](/help/assets/searchx.md)。

您可以根据以下一个或多个属性搜索数字资产。 默认情况下，应用于这些属性中某些属性的过滤器可用，而某些其他过滤器可以自定义创建以应用于其他属性。

| 搜索字段 | 搜索属性值 |
|-----------------|----------------------------------------------------------------------------------------------------------------------------------------|
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
| 音频编解码器 | Libvorbis、Lame MP3、AAC Encoding。 值仅存储在视频演绎版的元数据中。 |
| 音频比特率 | 指定为最小值和最大值。 值仅存储在视频演绎版的元数据中。 |

## 使用资产搜索结果{#aftersearch}

您可以对已在[!DNL Experience Manager]中搜索的资产执行以下操作：

* 视图元数据属性和其他信息。
* 下载一个或多个资源。
* 使用桌面操作在桌面应用程序中打开这些资产。
* 创建智能收藏集。

### 对搜索结果{#sort}排序

对搜索结果排序，以更快地发现所需的资源。 只有在从&#x200B;**[!UICONTROL 过滤器]**&#x200B;面板中选择&#x200B;**[[!UICONTROL 文件]](#searchui)**&#x200B;时，才能对搜索结果排序。 [!DNL Assets] 使用服务器端排序功能快速对文件夹或搜索查询结果中的所有资源（无论多少）进行排序。与客户端排序相比，服务器端排序提供更快、更准确的结果。

您可以对搜索结果进行排序，就像对任意文件夹中的资源排序一样。 排序功能适用于这些列 — 名称、标题、状态、Dimension、大小、评级、使用情况（创建日期）、修改日期（日期）、发布日期、工作流和签出。

有关排序功能的限制，请参阅[限制](#limitations)。

### 检查资产{#checkinfo}的详细信息

您可以从搜索结果页面中查看搜索资产的详细信息。

要查看资产的所有元数据，请选择资产，然后单击工具栏中的&#x200B;**[!UICONTROL 属性]**。

要检查对资产或资产版本历史记录的注释，请单击资产以打开大型预览。 打开左边栏中的时间轴，然后选择“ **[!UICONTROL 注释]** ”或“ **[!UICONTROL 版本]**”。 您还可以按时间顺序对时间轴活动（如注释或版本）进行排序。

![对搜索资产的时间轴条目排序](assets/sort_timeline_search_results.gif)

*图：对搜索资产的时间轴条目进行排序。*

### 下载搜索的资源{#download}

您可以像从文件夹下载常规资产一样下载搜索的资产及其演绎版。 从搜索结果中选择一个或多个资产，然后单击工具栏中的&#x200B;**[!UICONTROL 下载]**。

### 批量更新元数据属性{#metadataupdates}

可以批量更新多个资产的常见元数据字段。 从搜索结果中，选择一个或多个资产。 单击工具栏中的&#x200B;**[!UICONTROL 属性]**，然后根据需要更新元数据。 完成后，单击&#x200B;**[!UICONTROL 保存并关闭]**。 更新字段中以前存在的元数据将被覆盖。

对于单个文件夹或集合中可用的资产，您可以更轻松地[批量](/help/assets/metadata.md)更新元数据，而无需使用搜索功能。 对于跨文件夹可用或符合通用标准的资产，通过搜索批量更新元数据速度更快。

### 智能收藏集{#smart-collections}

收藏集是一组有序的资产，可以包含来自不同位置的资产，因为收藏集仅包含对这些资产的引用。 集合有以下两种类型：

* 资产、文件夹和其他收藏集的静态引用列表。
* 一种动态列表（智能收藏集），用于根据搜索条件填充收藏集中的资产。

您可以根据搜索条件创建智能收藏集。从&#x200B;**[!UICONTROL 过滤器]**&#x200B;面板中，选择&#x200B;**[!UICONTROL 文件]**，然后单击&#x200B;**[!UICONTROL 保存智能收藏集]**。请参阅[管理收藏集](/help/assets/manage-collections.md)。

## 意外的搜索结果和问题{#unexpectedresults}

| 错误、问题、症状 | 可能的原因 | 可能修复或了解问题 |
|---|---|---|
| 搜索缺少元数据的资产时结果不正确。 | 搜索缺少必需元数据的资产时，[!DNL Experience Manager]可能会显示一些具有有效元数据的资产。 结果基于索引元数据属性。 | 更新元数据后，需要重新编制索引以反映资产元数据的正确状态。 请参阅[必需元数据](metadata-schemas.md#define-mandatory-metadata)。 |
| 搜索结果过多。 | 广泛的搜索参数。 | 请考虑限制搜索范围[](#scope)。 使用智能标记可能为您带来比预期更多的搜索结果。 请参阅[使用智能标签](#withsmarttags)搜索行为。 |
| 无关或部分相关的搜索结果。 | 搜索行为会随智能标记而改变。 | 了解[搜索在智能标记](#withsmarttags)后如何更改。 |
| 没有自动完成资产的建议。 | 尚未对新上传的资产编制索引。 当您在搜索栏中键入搜索关键字时，元数据不会立即作为建议可用。 | [!DNL Experience Manager] 等到超时期（默认为一小时）到期，然后运行后台作业为所有新上传或更新的资产的元数据编制索引，然后将元数据添加到建议列表。 |
| 无搜索结果. | <ul><li>与您的查询匹配的资产不存在。 </li><li> 在搜索查询之前添加了空格。 </li><li> 不支持的元数据字段包含您搜索的关键字。</li><li> 在资产的离职时间进行搜索。 </li></ul> | <ul><li>使用其他关键字进行搜索。 或者，使用智能标记或相似性搜索来改进搜索结果。 </li><li>[已知限制](#limitations)。</li><li>搜索时不会考虑所有元数据字段。 请参见[范围](#scope)。</li><li>稍后搜索或修改所需资产的准时和非准时。</li></ul> |
| 搜索筛选器或谓词不可用。 | <ul><li>未配置搜索筛选器。</li><li>它不适用于您的登录。</li><li>（不太可能）未在您使用的部署上自定义搜索选项。</li></ul> | <ul><li>联系管理员以检查搜索自定义是否可用。</li><li>请与管理员联系以检查您的帐户是否具有使用自定义项的权限/权限。</li><li>联系管理员并检查您所使用的[!DNL Assets]部署的可用自定义项。</li></ul> |
| 在搜索视觉上相似的图像时，缺少期望的图像。 | <ul><li>图像在[!DNL Experience Manager]中不可用。</li><li>未对图像编制索引。 通常，在最近上传时。</li><li>图像未加智能标签。</li></ul> | <ul><li>将图像添加到[!DNL Assets]。</li><li>请联系您的管理员以重新为存储库编制索引。 另外，请确保您使用了相应的索引。</li><li>请联系您的管理员以智能标记相关资产。</li></ul> |
| 在搜索视觉上相似的图像时，将显示不相关的图像。 | 可视搜索行为。 | [!DNL Experience Manager] 显示尽可能多的潜在相关资产。相关度较低的图像（如果有）会添加到结果中，但搜索排名较低。 当您向下滚动搜索结果时，搜索资产的匹配质量和相关性会降低。 |
| 在选择和操作搜索结果时，不会对所有搜索的资产进行操作。 | [!UICONTROL 选择全部]选项仅选择卡视图中的前100个搜索结果和列表视图中的前200个搜索结果。 |  |

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 搜索实施指南](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/developing/search-tutorial-develop.html)
>* [用于提升搜索结果的高级配置](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/search-and-discovery/search-boost.html)
>* [配置智能翻译搜索](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/translation/smart-translation-search-technical-video-setup.html)

