---
title: 使用应用程序控制台创建和编辑应用程序
seo-title: 使用应用程序控制台创建和编辑应用程序
description: 请阅读本页，了解有关使用应用程序控制台创建和编辑应用程序的信息。
seo-description: 请阅读本页，了解有关使用应用程序控制台创建和编辑应用程序的信息。
uuid: 4f7db978-ae2b-4ca6-89f1-26e091d9140a
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: 9890d045-cead-4d70-b797-95319284e0d8
exl-id: 49e0b3f6-7ac7-4417-9c31-cc3d3c2305f3
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2638'
ht-degree: 0%

---

# 使用应用程序控制台创建和编辑应用程序{#creating-and-editing-apps-using-the-apps-console}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md)。

AEM移动应用程序开发过程认识到拥有不同专业知识的用户对移动应用程序的开发做出了贡献。 以下流程图说明了内容作者和应用程序开发人员执行任务的一般顺序。

![chlimage_1-10](assets/chlimage_1-10.gif)

有关如何执行营销人员任务的信息，请参阅此页面。 有关开发人员任务的信息，请参阅构建PhoneGap应用程序。

## 移动应用程序的结构{#the-structure-of-mobile-applications}

AEM Mobile提供了用于创建移动应用程序的Phonegap应用程序蓝图。 Blueprint定义您创建的应用程序的结构。 应用程序包括以下项目：

* 根页面。
* 应用程序的语言变体。
* 语言变体的主页。

### Phonegap应用程序的根{#the-root-of-a-phonegap-app}

您在AEM中创建的移动设备应用程序的根页面将显示在“应用程序”控制台中。

根页面存储在创建应用程序时指定的应用程序的Destination Path属性下方（默认路径为/content/phonegap/apps）。 页面名称是应用程序的Name属性。 例如，名为`myphonegapapp`的站点根页面的默认URL为`http://localhost:4502/content/phonegap/apps/myphonegapapp.html`。

![chlimage_1-146](assets/chlimage_1-146.png)

### PhoneGap应用程序{#the-language-variation-of-a-phonegap-app}的语言变体

根页面的第一个子页面是应用程序的语言变体。 每个页面的名称是为其创建应用程序的语言。 例如，“英语”是应用程序的英文变体的名称。

**注意：** 默认的PhoneGap Blueprint仅创建英语应用程序。您的开发人员可以修改Blueprint，以便创建更多语言变体。

![chlimage_1-147](assets/chlimage_1-147.png)

语言页面有两个用途：

* 页面内容是应用程序语言变体的快速页面。
* 页面属性可控制应用程序的多个设计方面，例如用于请求内容更新的URL，以及有关连接到云内部版本和Adobe Analytics服务集成的信息。

![chlimage_1-148](assets/chlimage_1-148.png)

### 主页{#the-home-page}

在打开应用程序时，将显示应用程序语言变体的主页或index.html页。主页为用户提供一个指向应用程序中各个页面的链接菜单。 段落系统允许您向页面添加组件以创建内容。

## 创建移动应用程序{#creating-a-mobile-application}

移动设备应用程序基于定义页面结构和属性的蓝图。 您可以配置以下应用程序属性：

* **标题：** 应用程序标题。
* **目标路径：** 存储应用程序的存储库中的位置。将保留默认设置，以便根据应用程序名称创建路径。

* **名称：** 默认值是删除空格字符的Title属性值。该名称在CQ中用于引用应用程序，例如，用于表示该应用程序的存储库节点。
* **描述：** 应用程序的描述。
* **服务器URL:** 为应用程序提供无线(OTA)内容更新的URL。默认值是用于创建应用程序（从外部器服务获取）的实例的发布服务器URL。 请注意，这必须是发布服务器实例，而不是需要身份验证的作者。

您还可以提供要用作应用程序缩略图的图像文件，选择要使用的PhoneGap Build配置，然后选择要使用的移动设备应用程序分析配置。 此图像仅用作缩略图，用于在Experience Manager的移动设备应用程序控制台中表示您的移动设备应用程序。

内部版本云服务以及将AdobeMobile Services SDK插件集成到您的应用程序中，还存在其他（可选）选项卡。

* 内部版本：单击此处管理配置并设置build.phonegap.com构建服务。 然后，从下拉列表中，您将能够选择新创建的PhoneGap内部版本云服务。
* Analytics:单击管理配置并设置[AdobeMobile Services SDK](https://docs.adobe.com/content/help/en/mobile-services/using/home.html)云服务。 然后，您将能够从下拉菜单中选择新创建的Mobile Service，以将其集成到您的移动设备应用程序中。

>[!NOTE]
>
>开发人员可以使用AEM PhoneGap Starter Kit创建应用程序并将其添加到控制台。

以下过程使用触屏UI创建移动应用程序。

1. 在边栏中，单击应用程序。
1. 单击或点按创建图标。

   ![](do-not-localize/chlimage_1-7.png)

1. （可选）在高级选项卡上，提供应用程序的说明，并根据需要更改服务器URL。
1. （可选）如果您使用PhoneGap Build编译应用程序，请在“生成”选项卡上，选择要使用的配置。

   要创建PhoneGap内部版本配置，请单击管理配置。

1. （可选）如果您使用SiteCatalyst跟踪应用程序活动，请在Analytics选项卡中，选择要使用的配置。

   要创建移动设备应用程序配置，请单击管理配置。

1. （可选）要提供应用程序图标，请单击“浏览”按钮，从文件系统中选择图像文件，然后单击“打开”。
1. 单击创建。

### 更改移动应用程序的属性{#changing-the-properties-of-a-mobile-application}

在创建移动应用程序后，您可以更改属性。

#### 更改标题、描述和图标{#change-the-title-description-and-icon}

1. 在边栏中，单击或点按应用程序。
1. 选择要配置的应用程序，然后单击查看页面属性图标。

   ![](do-not-localize/chlimage_1-8.png)

1. 要更改属性值，请单击或点按编辑图标。

   ![](do-not-localize/chlimage_1-9.png)

1. 配置基本和高级属性，然后单击或点按完成图标。

   ![](do-not-localize/chlimage_1-10.png)

#### 配置应用程序的语言变体{#configure-a-language-variation-of-the-application}

1. 在边栏中，单击或点按应用程序。
1. 单击可深入查看您希望在应用程序管理控制台中编辑的移动应用程序。 选择要配置的应用程序的语言版本，然后单击查看应用程序属性图标。

   ![](do-not-localize/chlimage_1-11.png)

1. 要更改属性值，请单击或点按编辑图标。

   ![](do-not-localize/chlimage_1-12.png)

1. 在“基本”、“高级”、“生成”和“Analytics”选项卡上配置属性，然后单击或点按完成图标。

   ![](do-not-localize/chlimage_1-13.png)

### 创作移动应用程序的内容{#authoring-the-content-of-a-mobile-application}

在创建移动应用程序后，添加用作应用程序UI的内容。

1. 在边栏中，单击或点按应用程序。
1. 单击或点按应用程序，然后单击或点按英语。
1. 编辑主页，或根据需要添加子页面。

### 将内容移到移动设备应用程序{#moving-content-to-mobile-applications}

AEM发布实例上的内容同步缓存可用作移动设备应用程序的内容存储库：

* 开发人员编译应用程序时，内容同步缓存中的内容会包含在应用程序中。
* 缓存中的内容可用于已安装的移动应用程序，以更新应用程序内容。

移动设备应用程序包括“更新”命令，用于下载和安装更新的应用程序内容。 当应用程序实例发送更新请求时，内容同步会确定自上次更新或安装应用程序以来哪些内容发生了更改，并提供新内容。

![chlimage_1-149](assets/chlimage_1-149.png)

要使更新的内容可供应用程序使用，请更新内容同步缓存。 首次更新缓存时，会添加所有已发布的内容。 后续更新仅会添加自上次更新以来发生更改的已发布内容。

内容同步还会跟踪何时进行更新。 根据此信息，内容同步可以确定要发送到移动应用程序的缓存更新。

对要更新缓存的实例执行以下过程。 例如，如果应用程序从发布实例请求更新，则对发布实例执行该过程。

1. 在边栏中，单击或点按应用程序，然后单击或点按您的应用程序。
1. 选择启动页面，然后单击或点按更新缓存图标。

   ![](do-not-localize/chlimage_1-14.png)

### 使用应用程序模板{#using-app-templates}

这是应用程序6.1功能包2中提供的一项功能，为在AEM中创建新应用程序提供了一种利用现有应用程序模板的简单方法。

什么是应用程序模板？ 可将其视为页面模板和组件的集合，这些模板和组件代表应用程序的基线或基础。
根据其他应用程序的模板创建新应用程序时，您将获得一个具有起点代表的应用程序，该应用程序是从中创建该应用程序的。

您必须拥有现有的移动设备应用程序模板（或安装了应用程序模板的应用程序）才能使用此功能。

最新的AEM Apps 6.1示例包中包含带有应用程序模板的Geometrixx应用程序更新版本。 或者，您也可以安装StarterKit，该StarterKit还提供模板。

基于应用程序模板创建新应用程序的步骤：

1. 确保您已安装最新的AEM Apps 6.1功能包和参考示例包
1. 单击左边栏中的“应用程序”。

![chlimage_1-1](assets/chlimage_1-1.jpeg)

1. 单击顶部的+创建按钮，然后选择创建应用程序。
1. 显示应用程序模板列表后，请选择一个：

![chlimage_1-2](assets/chlimage_1-2.jpeg)

1. 单击下一步。
1. 提供应用程序ID和标题，但您可能还希望包含名称和描述。

   1. 此外，您还可以通过浏览AEM资产，将PNG（支持的PhoneGap图标格式）作为图标。
   1. 请记住，在“管理应用程序”拼贴中创建应用程序后，您可以编辑所有这些字段。 除应用程序ID之外，在设置应用程序ID后，您将无法更改它。

![chlimage_1-150](assets/chlimage_1-150.png)

1. 单击创建按钮，您将看到2个选项，即完成（返回到应用程序目录视图）或管理应用程序（打开应用程序功能板）。
1. 创建后，您应会看到应用程序目录中列出了新应用程序：

![chlimage_1-3](assets/chlimage_1-3.jpeg)

1. 单击该应用程序以将其打开，则表示您已根据现有应用程序的模板成功创建了新应用程序。

>[!NOTE]
>
>如果您从AEM中卸载Geometrixx Outdoors引用应用程序包，并根据其模板创建了应用程序，则该应用程序将无法再正常运行。 可以删除Geometrixx Outdoors应用程序，但是，如果其他移动设备应用程序使用应用程序模板，则必须保留该应用程序模板。

## 浏览示例Geometrixx Outdoors应用程序{#exploring-the-sample-geometrixx-outdoors-app}

Geometrixx Outdoors应用程序是一个示例PhoneGap应用程序，用于演示默认PhoneGap应用程序Blueprint和示例移动组件的功能。

要打开应用程序，请在边栏中单击移动设备应用程序，然后选择Geometrixx Outdoors应用程序。

### 常见页面功能 — Geometrixx移动应用程序{#common-page-features-geometrixx-mobile-app}

移动设备应用程序的每个页面都包含以下功能：

* 返回到父页面的返回按钮。 请注意，“返回”按钮不显示在主页上。
* 可扩展的边栏，提供命令和链接菜单：

   * 打开位置页面。
   * 打开购物车。
   * 登录。
   * 更新应用程序。

* 段落系统，用于添加组件和创建内容。

### 主页 — Geometrixx移动应用程序{#the-home-page-geometrixx-mobile-app}

主页的内容由以下导航工具组成：

* 菜单列表组件，提供指向“齿轮”、“评论”、“新闻”和“关于美国”子页面的链接。
* 轻扫轮播组件，显示子页面。

### 齿轮页面 — Geometrixx移动应用程序{#the-gear-page-geometrixx-mobile-app}

“齿轮”页面为用户提供了产品页面的访问权限。 通过菜单列表组件，可以访问“齿轮”页面的子页面。 子页面是网站功能的产品类别。

* 季
* 服装
* 性别
* 活动

每个类别页面使用与“齿轮”页面相同的内容结构。 轮播可提供对子页面（产品的子类别）的访问。 子类别页面包含提供产品页面链接的产品列表。

### 产品页面 — Geometrixx移动设备应用程序{#the-products-page-geometrixx-mobile-app}

“产品”页面及其子页面的层级为产品页面实施分类系统。 层级的每个分支中最低的页面是包含ng产品组件的产品页面。

应用程序用户无法使用“产品”页面。 齿轮页面提供对每个产品页面的访问权限。

### “审阅”页面 — Geometrixx移动应用程序{#the-reviews-page-geometrixx-mobile-app}

包含返回按钮。 段落系统允许您添加组件。

使用应用程序时，“审阅”页面可从“英文”页面的轮播中找到。

### 新闻页面 — Geometrixx移动应用程序{#the-news-page-geometrixx-mobile-app}

包含返回按钮。 段落系统允许您添加组件。

使用应用程序时，可从英文页面的轮播中获取“新闻”页面。

### 关于美国页面 — Geometrixx移动设备应用程序{#the-about-us-page-geometrixx-mobile-app}

关于us页面包含若干两列行组件。 每列都包含图像组件或文本组件。 组件是可编辑的，段落系统允许您添加组件。

使用应用程序时，可以从英文页面的轮播中找到“关于美国”页面。

### 位置页面 — Geometrixx移动设备应用程序{#the-locations-page-geometrixx-mobile-app}

位置页面包含位置组件。

使用应用程序时，“位置”(Locations)页面可从“英文”(English)页面的菜单列表中找到。

## 移动设备组件示例{#sample-mobile-components}

创作移动应用程序的页面时，Sidekick中会立即提供一些组件。 这些组件属于PhoneGap组件组。

### 轻扫传送 {#swipe-carousel}

轻扫轮播组件是用于展示和导航网站页面的工具。 该组件包含一个轮播，该轮播在页面链接列表上方的页面中对图像进行循环。 编辑组件以指定要显示的页面以及轮播的行为。

请注意，对于以特定方式与图像关联的页面，图像会显示在轮播中。 当页面与图像不关联时，只会显示链接列表。

![chlimage_1-151](assets/chlimage_1-151.png)

**轮播属性选项卡**

配置轮播的行为：

* 播放速度：显示下一幅图像之前，每幅图像显示的时间（以毫秒为单位）。
* 过渡时间：图像过渡动画的持续时间（以毫秒为单位）。
* 控件样式：为在图像之间移动而提供的控件类型。

**列表属性选项卡**

指定页面列表的生成方式：

* 生成列表：用于指定要包含在轮播中的页面的方法。 请参阅生成页面列表。
* 订购方式：选择要用于对页面列表进行排序的页面属性。 例如，选择jcr:title可按标题的字母顺序对页面进行排序。
* 限制：要包含的最大页面数。 此属性适用于基于搜索的页面列表生成方法。

#### 生成页面列表{#building-the-page-list}

轻扫轮播组件为“使用生成列表”属性提供了以下值。 编辑对话框会根据您选择的值发生更改：

**子页面**

组件列出了特定页面的所有子页面。 选择此值后，在“子页面”选项卡上选择该页面，或者指定不列出当前页面的子页面的值。

**固定列表**

指定包含的页面列表。 选择此值后，在选择固定列表时显示的“固定列表”选项卡上配置列表：

* 要添加页面，请单击“添加项目”，然后浏览页面。
* 使用向上和向下箭头图标在列表中移动页面。
* 单击删除按钮可从列表中删除页面。

顺序依据属性不影响固定列表的顺序。

**搜索**

使用关键词搜索结果填充列表。 搜索在您指定页面的子页面中执行：

1. 要指定搜索的根页面，请使用开始位置属性选择页面路径。 指定当前页面下方的搜索路径。
1. 在搜索查询属性中，输入搜索关键词。

**高级搜索**

使用[Querybuilder](/help/sites-developing/querybuilder-api.md)查询填充列表。

### 图像 {#image}

向应用程序内容中添加图像。

### 文本 {#text}

向应用程序内容添加富文本。

### 存储位置 {#store-locations}

“商店位置”组件为用户提供了查找营业网点的工具：

* 搜索
* 接近或远离设备GPS坐标的位置列表。

组件要求存储库包含每个存储的位置信息。 示例位置安装在/etc/commerce/locations/adobe节点。 ![chlimage_1-152](assets/chlimage_1-152.png)

### 两列行{#two-column-row}

允许您向页面中添加并排组件。

![chlimage_1-153](assets/chlimage_1-153.png)
