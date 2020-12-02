---
title: 使用“应用程序”控制台创建和编辑应用程序
seo-title: 使用“应用程序”控制台创建和编辑应用程序
description: 可查看本页以了解有关使用应用程序控制台创建和编辑应用程序的信息。
seo-description: 可查看本页以了解有关使用应用程序控制台创建和编辑应用程序的信息。
uuid: 4f7db978-ae2b-4ca6-89f1-26e091d9140a
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: 9890d045-cead-4d70-b797-95319284e0d8
translation-type: tm+mt
source-git-commit: 70b18dbe351901abb333d491dd06a6c1c1c569d6
workflow-type: tm+mt
source-wordcount: '2638'
ht-degree: 0%

---


# 使用应用程序控制台创建和编辑应用程序{#creating-and-editing-apps-using-the-apps-console}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如，React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md).

AEM移动应用程序开发流程认识到拥有不同专业知识的用户对移动应用程序开发的贡献。 以下流程图说明了内容作者和应用程序开发人员执行任务的一般顺序。

![chlimage_1-10](assets/chlimage_1-10.gif)

有关如何执行营销人员任务的信息将显示在此页面上。 有关开发人员任务的信息，请参阅构建PhoneGap应用程序。

## 移动应用程序的结构{#the-structure-of-mobile-applications}

AEM Mobile提供了用于创建移动应用程序的Phonegap应用程序蓝图。 蓝图定义了您创建的应用程序的结构。 应用程序包括以下项目：

* 根页面。
* 应用程序的语言变体。
* 语言变体的主页。

### Phonegap应用程序的根{#the-root-of-a-phonegap-app}

您在AEM中创建的移动应用程序的根页面将显示在应用程序控制台中。

根页面存储在创建应用程序时指定的应用程序的“目标路径”属性下（默认路径为/content/phonegap/apps）。 页面名称是应用程序的“名称”属性。 例如，名为`myphonegapapp`的站点的根页面的默认URL为`http://localhost:4502/content/phonegap/apps/myphonegapapp.html`。

![chlimage_1-146](assets/chlimage_1-146.png)

### PhoneGap应用程序{#the-language-variation-of-a-phonegap-app}的语言变体

根页面的第一个子页面是应用程序的语言变体。 每页的名称是创建应用程序的语言。 例如，“英语”是应用程序的“英语”变体的名称。

**注意：默** 认的PhoneGap蓝图仅创建英文应用程序。您的开发人员可以修改蓝图，以创建更多语言版本。

![chlimage_1-147](assets/chlimage_1-147.png)

语言页面有两个用途：

* 页面内容是应用程序的语言变体的弹出页面。
* 页面属性控制应用程序的多个设计方面，如用于请求内容更新的URL，以及有关连接到云构建和Adobe Analytics服务集成的信息。

![chlimage_1-148](assets/chlimage_1-148.png)

### 主页{#the-home-page}

当应用程序打开时，将显示应用程序的语言变体的主页或index.html页。主页为用户提供一个指向应用程序中不同页面的链接菜单。 段落系统允许您向页面添加组件以创建内容。

## 创建移动应用程序{#creating-a-mobile-application}

移动应用程序基于定义页面结构和属性的蓝图。 您可以配置以下应用程序属性：

* **标题：** 应用程序标题。
* **目标路径：** 存储应用程序的存储库中的位置。保留默认值，以根据应用程序名称创建路径。

* **名称：** 默认值是删除空格字符的标题属性的值。该名称在CQ中用于引用应用程序，例如，用于表示应用程序的存储库节点。
* **说明：** 应用程序的说明。
* **服务器** URL：为应用程序提供无线(OTA)内容更新的URL。默认值是用于创建应用程序（从externalizer服务获取）的实例的发布服务器URL。 注意，这必须是发布服务器实例，而不是需要身份验证的作者。

您还可以提供一个图像文件，用作应用程序缩略图，选择要使用的PhoneGap Build配置，然后选择要使用的移动应用程序分析配置。 此图像仅用作缩略图，以在Experience Manager的移动应用程序控制台中代表您的移动应用程序。

还存在其他（和可选）选项卡，用于构建云服务并将AdobeMobile Services SDK插件集成到您的应用程序中。

* 构建：单击“管理配置”并在此处设置build.phonegap.com构建服务。 然后，您将能够从下拉菜单中选择新创建的PhoneGap构建云服务。
* 分析：单击“管理配置”并设置[AdobeMobile Services SDK](https://docs.adobe.com/content/help/en/mobile-services/using/home.html)云服务。 然后，您将能够从下拉列表中选择新创建的Mobile Service以集成到您的移动应用程序中。

>[!NOTE]
>
>开发人员可以使用AEM PhoneGap Starter Kit创建应用程序并将其添加到控制台。

以下过程使用触屏UI创建移动应用程序。

1. 在边栏上，单击“应用程序”。
1. 单击或点按创建图标。

   ![](do-not-localize/chlimage_1-7.png)

1. （可选）在“高级”选项卡上，提供应用程序的说明，并根据需要更改服务器URL。
1. （可选）如果您使用PhoneGap Build编译应用程序，请在“构建”选项卡上，选择要使用的配置。

   要创建PhoneGap构建配置，请单击“管理配置”。

1. （可选）如果您使用SiteCatalyst跟踪应用程序活动，请在“分析”选项卡上，选择要使用的配置。

   要创建移动应用程序配置，请单击“管理配置”。

1. （可选）要提供应用程序图标，请单击“浏览”按钮，从文件系统中选择图像文件，然后单击“打开”。
1. 单击创建。

### 更改移动应用程序{#changing-the-properties-of-a-mobile-application}的属性

创建手机应用程序后，可以更改属性。

#### 更改标题、说明和图标{#change-the-title-description-and-icon}

1. 在边栏上，单击或点按应用程序。
1. 选择要配置的应用程序，然后单击视图页属性图标。

   ![](do-not-localize/chlimage_1-8.png)

1. 要更改属性值，请单击或点按编辑图标。

   ![](do-not-localize/chlimage_1-9.png)

1. 配置基本和高级属性，然后单击或点按完成图标。

   ![](do-not-localize/chlimage_1-10.png)

#### 配置应用程序{#configure-a-language-variation-of-the-application}的语言变体

1. 在边栏上，单击或点按应用程序。
1. 单击可进入您希望在应用程序管理控制台中编辑的移动应用程序。 选择要配置的应用程序的语言版本，然后单击“视图应用程序属性”图标。

   ![](do-not-localize/chlimage_1-11.png)

1. 要更改属性值，请单击或点按编辑图标。

   ![](do-not-localize/chlimage_1-12.png)

1. 在“基本”、“高级”、“构建”和“分析”选项卡上配置属性，然后单击或点按完成图标。

   ![](do-not-localize/chlimage_1-13.png)

### 创作移动应用程序的内容{#authoring-the-content-of-a-mobile-application}

创建手机应用程序后，添加用作应用程序UI的内容。

1. 在边栏上，单击或点按应用程序。
1. 单击或点按应用程序，然后单击或点按英语。
1. 编辑主页，或根据需要添加子页面。

### 将内容移到移动应用程序{#moving-content-to-mobile-applications}

AEM发布实例上的内容同步缓存用作移动应用程序的内容存储库：

* 当开发人员编译应用程序时，内容同步缓存中的内容将包含在应用程序中。
* 缓存中的内容可用于已安装的移动应用程序更新应用程序内容。

移动应用程序包含“更新”命令，用于下载和安装更新的应用程序内容。 当应用程序实例发送更新请求时，内容同步会确定自上次更新或安装应用程序以来哪些内容已发生更改，并提供新内容。

![chlimage_1-149](assets/chlimage_1-149.png)

要使更新的内容对应用程序可用，请更新内容同步缓存。 首次更新缓存时，将添加所有已发布的内容。 后续更新仅添加自上次更新以来已更改的已发布内容。

内容同步还会跟踪更新发生的时间。 利用此信息，内容同步可确定要发送到移动应用程序的缓存更新。

对要更新缓存的实例执行以下过程。 例如，如果应用程序从发布实例请求更新，请对发布实例执行该过程。

1. 在边栏上，单击或点按应用程序，然后单击或点按您的应用程序。
1. 选择初始页面，然后单击或点按更新缓存图标。

   ![](do-not-localize/chlimage_1-14.png)

### 使用应用程序模板{#using-app-templates}

这是Apps 6.1 Feature Pack 2提供的功能，它提供了一种轻松的方式，利用现有的应用程序模板在AEM内创建新的应用程序。

什么是应用程序模板？ 将它视为表示应用程序基线或基础的页面模板和组件的集合。
根据其他应用程序的模板创建新应用程序时，您将获得一个应用程序，其起点代表从中创建该应用程序的应用程序。

您必须拥有现有的移动应用程序模板（或安装有应用程序模板的应用程序）才能利用此功能。

最新的AEM Apps 6.1范例包包含具有应用程序模板的Geometrixx应用程序的更新版本。 或者，您也可以安装StarterKit，它也提供一个模板。

根据应用程序模板创建新应用程序的步骤：

1. 确保您安装了最新的AEM Apps 6.1功能包和参考示例包
1. 单击左边栏中的“应用程序”。

![chlimage_1-1](assets/chlimage_1-1.jpeg)

1. 单击顶部的+创建按钮，然后选择创建应用程序。
1. 显示应用程序模板的列表后，请选择一个：

![chlimage_1-2](assets/chlimage_1-2.jpeg)

1. 单击下一步。
1. 提供应用程序ID和标题，但您可能还希望包括名称和说明。

   1. 此外，您还可以通过浏览AEM资产将PNG（支持的PhoneGap图标格式）作为图标提供。
   1. 请记住，在“管理应用程序”拼贴中创建应用程序后，您可以编辑所有这些字段。 除App Id外，一旦设置了App Id，您便无法更改它。

![chlimage_1-150](assets/chlimage_1-150.png)

1. 单击创建按钮，您将看到2个选项，即完成(返回至应用程序目录视图)或管理应用程序(打开应用程序仪表板)。
1. 创建后，您应会看到新应用程序列在应用程序目录中：

![chlimage_1-3](assets/chlimage_1-3.jpeg)

1. 单击该应用程序以将其打开，您已基于现有应用程序的模板成功创建了新应用程序。

>[!NOTE]
>
>如果您从AEM卸载Geometrixx Outdoors引用应用程序包，并基于其模板创建了应用程序，则该应用程序将不再正常工作。 Geometrixx Outdoors应用程序可以删除，但是，如果其他移动应用程序使用该应用程序，则该应用程序模板必须保留。

## 浏览示例Geometrixx Outdoors应用程序{#exploring-the-sample-geometrixx-outdoors-app}

Geometrixx Outdoors应用程序是一个示例PhoneGap应用程序，它演示了默认PhoneGap应用程序蓝图和示例移动组件的功能。

要打开应用程序，请在边栏中单击“移动应用程序”，然后选择“Geometrixx Outdoors应用程序”。

### 常见页面功能-Geometrixx移动应用程序{#common-page-features-geometrixx-mobile-app}

移动应用程序的每个页面都包含以下功能：

* 返回父页面的返回按钮。 请注意，返回按钮不显示在主页上。
* 优惠命令和链接菜单的可扩展边栏：

   * 打开位置页面。
   * 打开购物车。
   * 登录。
   * 更新应用程序。

* 段落系统，用于添加组件和创建内容。

### 主页-Geometrixx移动应用程序{#the-home-page-geometrixx-mobile-app}

主页的内容由以下导航工具组成：

* 一个菜单列表组件，它提供指向“齿轮”、“评论”、“新闻”和“关于我们”子页面的链接。
* 一个轻扫传送组件，它显示子页面。

### 齿轮页-Geometrixx移动应用程序{#the-gear-page-geometrixx-mobile-app}

齿轮页面为用户提供对产品页面的访问权。 菜单列表组件提供对齿轮页子页面的访问。 子页面是网站提供的一类别产品。

* 季节
* 服装
* 性别
* 活动

每个类别页面使用与“齿轮”页面相同的内容结构。 轮盘提供对子页面的访问，子页面是产品的子类别。 子类别页面包含提供产品页面链接的产品列表。

### 产品页-Geometrixx移动应用程序{#the-products-page-geometrixx-mobile-app}

“产品”页面及其子页面层次结构为产品页面实施了分类系统。 层次结构的每个分支中的最低页面是包含ng产品组件的产品页面。

“产品”页面对应用程序用户不可用。 齿轮页面提供对每个产品页面的访问。

### 评论页-Geometrixx移动应用程序{#the-reviews-page-geometrixx-mobile-app}

包含返回按钮。 段落系统允许您添加组件。

使用应用程序时，“审阅”页面可从“英语”页面的轮盘中访问。

### 新闻页-Geometrixx移动应用程序{#the-news-page-geometrixx-mobile-app}

包含返回按钮。 段落系统允许您添加组件。

使用应用程序时，“News”（新闻）页面可从“English”（英语）页面的轮盘中访问。

### “关于美国”页-Geometrixx移动应用程序{#the-about-us-page-geometrixx-mobile-app}

“关于我们”页包含多个两列行组件。 每列都包含图像或文本组件。 组件是可编辑的，段落系统允许您添加组件。

使用应用程序时，“关于我们”页面可从“英语”页面的轮盘中访问。

### 位置页-Geometrixx移动应用程序{#the-locations-page-geometrixx-mobile-app}

位置页面包含位置组件。

使用应用程序时，可从“英语”页面的菜单列表中找到“位置”页。

## 移动组件示例{#sample-mobile-components}

创作移动应用程序的页面时，Sidekick中会立即提供多个组件。 这些组件属于PhoneGap组件组。

### 轻扫传送 {#swipe-carousel}

轻扫传送组件是用于展示和导航站点页面的工具。 该组件包含一个轮盘，它循环浏览页面链接列表上方的页面的图像。 编辑组件以指定要显示的页面以及传送的行为。

请注意，与图像关联的页面的图像以特定方式显示在传送中。 当页面与图像不关联时，仅显示链接列表。

![chlimage_1-151](assets/chlimage_1-151.png)

**传送属性选项卡**

配置传送的行为：

* 播放速度：显示下一个图像之前显示每个图像的时间（以毫秒为单位）。
* 过渡时间：图像过渡动画的持续时间（以毫秒为单位）。
* 控件样式：提供用于在图像之间移动的控件的类型。

**列表属性选项卡**

指定页面列表的生成方式：

* 构建列表使用：用于指定要包含在传送中的页面的方法。 请参阅构建页面列表。
* 订购依据：选择用于对页面列表排序的页面属性。 例如，选择jcr:title可按标题的字母顺序对页面排序。
* 限制：要包括的最大页数。 此属性适用于基于搜索的页面列表构建方法。

#### 构建页面列表{#building-the-page-list}

轻扫传送组件为“构建列表使用”属性提供以下值。 编辑对话框会根据您选择的值而更改：

**子页面**

该组件列表特定页面的所有子页面。 选择此值后，在“子页面”选项卡上选择该页面，或指定任何值以列表当前页面的子页面。

**固定列表**

指定包含页面的列表。 选择此值后，在选择“固定列表”时显示的“固定列表”选项卡上配置列表:

* 要添加页面，请单击“添加项目”，然后浏览页面。
* 使用向上和向下箭头图标在列表中移动页面。
* 单击“删除”按钮，从列表中删除页面。

“排序依据”属性不影响固定列表的顺序。

**搜索**

使用关键字搜索的结果填充列表。 搜索是在指定页面的子页面中执行的：

1. 要指定搜索的根页面，请使用“开始位置”属性选择页面路径。 指定当前页面下方的搜索路径。
1. 在搜索查询属性中，输入搜索关键字。

**高级搜索**

使用[Querybuilder](/help/sites-developing/querybuilder-api.md)列表填充查询。

### 图像 {#image}

向应用程序内容中添加图像。

### 文本 {#text}

向应用程序内容添加富文本。

### 存储位置 {#store-locations}

商店位置组件为用户提供了查找商业网点的工具：

* 搜索
* 列表接近或远离设备GPS坐标的位置。

组件要求存储库包含每个存储的位置信息。 示例位置安装在/etc/commerce/locations/adobe节点。 ![chlimage_1-152](assets/chlimage_1-152.png)

### 两列行{#two-column-row}

允许您向页面添加并排组件。

![chlimage_1-153](assets/chlimage_1-153.png)
