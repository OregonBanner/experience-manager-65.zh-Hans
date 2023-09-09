---
title: 使用应用程序控制台创建和编辑应用程序
description: 按照此页面了解如何使用Apps Console创建和编辑应用程序。
uuid: 4f7db978-ae2b-4ca6-89f1-26e091d9140a
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: 9890d045-cead-4d70-b797-95319284e0d8
exl-id: 49e0b3f6-7ac7-4417-9c31-cc3d3c2305f3
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '2692'
ht-degree: 0%

---

# 使用应用程序控制台创建和编辑应用程序{#creating-and-editing-apps-using-the-apps-console}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如React）的项目使用SPA编辑器。 [了解详情](/help/sites-developing/spa-overview.md)。

AEM移动应用程序开发过程认识到，拥有不同专业知识的用户对移动应用程序的开发有贡献。 以下流程图说明了内容作者和应用程序开发人员执行任务的一般顺序。

![chlimage_1-10](assets/chlimage_1-10.gif)

有关如何执行营销人员任务的信息将显示在此页面上。 有关开发人员任务的信息，请参阅构建PhoneGap应用程序。

## 移动应用程序的结构 {#the-structure-of-mobile-applications}

AEM Mobile提供了用于创建移动应用程序的Phonegap应用程序Blueprint。 Blueprint定义您创建的应用程序的结构。 应用程序包括以下项目：

* 根页面。
* 应用程序的语言变体。
* 语言变体的主页。

### Phonegap应用程序的根目录 {#the-root-of-a-phonegap-app}

您在AEM中创建的移动设备应用程序的根页面将显示在“应用程序”控制台中。

根页面存储在创建应用程序时指定的应用程序的“目标路径”属性下（默认路径为/content/phonegap/apps）。 页面名称是应用程序的Name属性。 例如，站点的根页面的默认URL名为 `myphonegapapp` 是 `http://localhost:4502/content/phonegap/apps/myphonegapapp.html`.

![chlimage_1-146](assets/chlimage_1-146.png)

### PhoneGap应用程序的语言变量 {#the-language-variation-of-a-phonegap-app}

根页面的第一个子页面是应用程序的语言变体。 每个页面的名称是为其创建应用程序的语言。 例如， English是应用程序的英文变体的名称。

**注意：** 默认的PhoneGap Blueprint仅创建英语应用程序。 您的开发人员可以修改Blueprint，以便创建更多语言变量。

![chlimage_1-147](assets/chlimage_1-147.png)

语言页面有两个用途：

* 页面内容是应用程序语言变体的垃圾页面。
* 页面属性控制应用程序的多个设计方面，例如用于请求内容更新的URL，以及有关连接到Cloud Build和Adobe Analytics服务集成的信息。

![chlimage_1-148](assets/chlimage_1-148.png)

### 主页 {#the-home-page}

打开应用程序时，将显示应用程序语言变体的Home页或index.html页。 主页为用户提供了一个菜单，其中包含指向应用程序中各个页面的链接。 段落系统允许您向页面添加组件以创建内容。

## 创建移动应用程序 {#creating-a-mobile-application}

移动设备应用程序基于定义页面结构和属性的Blueprint。 您可以配置以下应用程序属性：

* **标题：** 应用程序标题。
* **目标路径：** 存储库中存储应用程序的位置。 保留默认值以根据应用程序名称创建路径。

* **名称：** 默认值为删除了空格字符的Title属性的值。 该名称在CQ中用于引用应用程序，例如表示应用程序的存储库节点。
* **描述：** 应用程序的描述。
* **服务器URL：** 为应用程序提供Over-the-Air (OTA)内容更新的URL。 默认值为用于创建应用程序的实例的发布服务器URL（获取自外部化器服务）。 注意，这必须是发布服务器实例，而不是作者，后者需要身份验证。

您还可以提供要用作应用程序缩略图的图像文件，选择要使用的PhoneGap Build配置，然后选择要使用的移动设备应用程序分析配置。 此图像仅用作缩略图，以在Experience Manager的移动应用程序控制台中表示您的移动应用程序。

存在用于构建Cloud Service以及将AdobeMobile Services SDK插件集成到应用程序中的其他（和可选）选项卡。

* 构建：单击管理配置并在此处设置您的build.phonegap.com构建服务。 然后，您可以从下拉菜单中选择新创建的PhoneGap Build云服务。
* Analytics：单击管理配置并设置您的 [AdobeMobile Services SDK](https://experienceleague.adobe.com/docs/mobile-services/using/home.html) 云服务。 然后，您可以从下拉菜单中选择新创建的移动服务，以将其集成到移动应用程序中。

>[!NOTE]
>
>开发人员可以使用AEM PhoneGap Starter Kit创建应用程序并将它们添加到控制台。

以下过程使用触屏UI创建移动应用程序。

1. 在边栏上，单击应用程序。
1. 单击创建图标。

   ![正方形内由加号表示的“创建”图标。](do-not-localize/chlimage_1-7.png)

1. （可选）在高级选项卡上，提供应用程序的说明，并根据需要更改服务器URL。
1. （可选）如果要使用PhoneGap Build编译应用程序，请在“生成”选项卡上选择要使用的配置。

   要创建PhoneGap Build配置，请单击管理配置。

1. （可选）如果您使用SiteCatalyst来跟踪应用程序活动，请在Analytics选项卡上，选择要使用的配置。

   要创建移动设备应用程序配置，请单击管理配置。

1. （可选）要提供应用程序图标，请单击“浏览”按钮，从文件系统中选择图像文件，然后单击“打开”。
1. 单击创建。

### 更改移动应用程序的属性 {#changing-the-properties-of-a-mobile-application}

创建移动应用程序后，可以更改属性。

#### 更改标题、描述和图标 {#change-the-title-description-and-icon}

1. 在边栏上，单击或点按应用程序。
1. 选择要配置的应用程序，然后单击查看页面属性图标。

   ![圆圈中的字母I表示的“查看页面属性”图标。](do-not-localize/chlimage_1-8.png)

1. 要更改属性值，请单击或点按编辑图标。

   ![铅笔指示的“编辑”图标。](do-not-localize/chlimage_1-9.png)

1. 配置基本和高级属性，然后单击或点按完成图标。

   ![由复选标记符号指示的“完成”图标。](do-not-localize/chlimage_1-10.png)

#### 配置应用程序的语言变体 {#configure-a-language-variation-of-the-application}

1. 在边栏上，单击应用程序。
1. 单击以深入查看要在应用程序Admin Console中编辑的移动应用程序。 选择要配置的应用程序的语言版本，然后单击查看应用程序属性图标。

   ![圆圈内的字母I表示的View Application Properties图标。](do-not-localize/chlimage_1-11.png)

1. 要更改属性值，请单击或点按编辑图标。

   ![铅笔指示的“编辑”图标。](do-not-localize/chlimage_1-12.png)

1. 在“基本”、“高级”、“生成”和“Analytics”选项卡上配置属性，然后单击或点按完成图标。

   ![由复选标记符号指示的“完成”图标。](do-not-localize/chlimage_1-13.png)

### 创作移动应用程序的内容 {#authoring-the-content-of-a-mobile-application}

创建移动设备应用程序后，添加用作应用程序UI的内容。

1. 在边栏上，单击或点按应用程序。
1. 单击或点按应用程序，然后单击或点按英语。
1. 编辑主页，或根据需要添加子页面。

### 将内容移动到移动应用程序 {#moving-content-to-mobile-applications}

AEM发布实例上的内容同步缓存用作移动设备应用程序的内容存储库：

* 当开发人员编译应用程序时，应用程序中将包含内容同步缓存中的内容。
* 缓存中的内容可供已安装的移动应用程序用于更新应用程序内容。

移动应用程序包括一个“更新”命令，用于下载和安装更新的应用程序内容。 当应用程序实例发送更新请求时，内容同步会确定自上次更新或安装应用程序以来更改了哪些内容，并提供新内容。

![chlimage_1-149](assets/chlimage_1-149.png)

要使更新的内容对应用程序可用，需要更新内容同步缓存。 第一次更新缓存时，将添加所有已发布的内容。 后续更新仅添加自上次更新以来发生更改的已发布内容。

内容同步还会在发生更新时进行跟踪。 利用这些信息，内容同步可以确定要发送到移动应用程序的缓存更新。

在要更新缓存的实例上执行以下过程。 例如，如果您的应用程序请求从发布实例进行更新，请在发布实例上执行该过程。

1. 在边栏上，单击或点按应用程序，然后单击或点按您的应用程序。
1. 选择启动页面，然后单击或点按更新缓存图标。

   ![“更新缓存”图标由带有循环符号的条状边栏表示。](do-not-localize/chlimage_1-14.png)

### 使用应用程序模板 {#using-app-templates}

这是Apps 6.1 Feature Pack 2中提供的功能，它提供了一种利用现有应用程序模板在AEM中创建新应用程序的简单方法。

什么是应用程序模板？ 可将其视为一组页面模板和组件，它们代表应用程序的基线或基础。
在基于其他应用程序的模板创建新应用程序时，您将获得一个应用程序，该应用程序的起点代表创建该应用程序的应用程序。

您必须拥有现有的移动设备应用程序模板（或安装的应用程序具有应用程序模板），才能使用此功能。

最新的AEM Apps 6.1示例包中包含带有应用程序模板的Geometrixx应用程序的更新版本。 或者，您可以安装同时提供模板的StarterKit。

基于应用程序模板创建新应用程序的步骤：

1. 确保您已安装最新的AEM Apps 6.1功能包和参考示例包
1. 单击左边栏中的应用程序。

![chlimage_1-1](assets/chlimage_1-1.jpeg)

1. 单击顶部的+创建按钮，然后选择创建应用程序。
1. 向您显示应用程序模板列表后，请选择一个模板：

![chlimage_1-2](assets/chlimage_1-2.jpeg)

1. 单击“下一个”。
1. 提供应用程序ID和标题，但您可能还希望包含名称和描述。

   1. 此外，您还可以通过浏览AEM Assets提供PNG（支持的PhoneGap图标格式）作为图标。
   1. 请记住，在管理应用程序图块中创建应用程序后，您可以编辑所有这些字段。 应用程序ID除外，设置应用程序ID后，您将无法对其进行更改。

![chlimage_1-150](assets/chlimage_1-150.png)

1. 单击“创建”按钮，系统将显示两个选项，即“完成”（返回到“应用程序”目录视图）或“管理应用程序”（打开应用程序功能板）。
1. 创建应用程序后，您应该会在应用程序目录中看到新应用程序列出：

![chlimage_1-3](assets/chlimage_1-3.jpeg)

1. 单击应用程序以将其打开，表示您已根据现有应用程序的模板成功创建了新应用程序。

>[!NOTE]
>
>如果您从AEM中卸载Geometrixx Outdoors引用应用程序包，并根据其模板创建了应用程序，则该应用程序将无法再正常使用。 可以删除Geometrixx Outdoors应用程序，但是，如果其他移动设备应用程序正在使用该模板，则必须保留该应用程序模板。

## 浏览示例Geometrixx Outdoors应用程序 {#exploring-the-sample-geometrixx-outdoors-app}

Geometrixx Outdoors应用程序是一个示例PhoneGap应用程序，用于演示默认PhoneGap应用程序Blueprint和示例移动组件的功能。

要打开应用程序，请在边栏中单击移动设备应用程序，然后选择Geometrixx Outdoors应用程序。

### 常见页面功能 — Geometrixx移动应用程序 {#common-page-features-geometrixx-mobile-app}

移动设备应用程序的每个页面都包含以下功能：

* 用于返回到父页面的返回按钮。 请注意，“Home（主页）”页面上不显示“Back（后退）”按钮。
* 提供命令和链接菜单的可消耗边栏：

   * 打开“位置”页面。
   * 打开购物车。
   * 登录。
   * 更新应用程序。

* 段落系统，用于添加组件和创建内容。

### 主页 — Geometrixx移动设备应用程序 {#the-home-page-geometrixx-mobile-app}

主页的内容由以下导航工具组成：

* 菜单列表组件，提供指向“齿轮”、“审核”、“新闻”和“关于我们”子页面的链接。
* 可显示子页面的轻扫轮盘组件。

### 齿轮页面 — Geometrixx移动应用程序 {#the-gear-page-geometrixx-mobile-app}

通过“齿轮”页面，用户可以访问产品页面。 通过菜单列表组件可访问“齿轮”页面的子页面。 子页面是网站所具有的产品类别。

* 季
* 服装
* 性别
* 活动

每个类别页面使用与“齿轮”页面相同的内容结构。 通过轮播，可访问作为产品子类别的子页面。 子类别页面包含产品列表，提供指向产品页面的链接。

### “产品”页面 — Geometrixx移动设备应用程序 {#the-products-page-geometrixx-mobile-app}

产品页面及其子页面的层次结构实施产品页面的分类系统。 层次结构的每个分支中的最低页面是包含ng Product组件的产品页面。

应用程序用户无法使用“产品”页面。 通过“齿轮”页面可访问每个产品页面。

### “审核”页面 — Geometrixx移动应用程序 {#the-reviews-page-geometrixx-mobile-app}

包含返回按钮。 段落系统允许您添加组件。

使用应用程序时，可通过英语页面上的轮播访问“审阅”页面。

### 新闻页面 — Geometrixx移动应用程序 {#the-news-page-geometrixx-mobile-app}

包含返回按钮。 段落系统允许您添加组件。

使用应用程序时，可通过英语页面上的轮播访问新闻页面。

### “关于我们”页面 — Geometrixx移动应用程序 {#the-about-us-page-geometrixx-mobile-app}

“关于我们”页包含两个列行组件。 每列都包含图像或文本组件。 组件是可编辑的，可通过段落系统添加组件。

使用应用程序时，可通过英语页面上的轮盘访问“关于我们”页面。

### “位置”页面 — Geometrixx移动设备应用程序 {#the-locations-page-geometrixx-mobile-app}

“位置”页包含位置组件。

使用应用程序时，“位置”页面可从英文页面上的菜单列表中找到。

## 示例移动组件 {#sample-mobile-components}

创作移动应用程序的页面时，Sidekick中会立即提供几个组件。 这些组件属于PhoneGap组件组。

### 轻扫传送 {#swipe-carousel}

轻扫轮盘组件是一个用于展示和导航站点页面的工具。 该组件包括一个轮盘，该轮盘在页面链接列表上方的页面上循环浏览图像。 编辑组件以指定要公开的页面和轮播的行为。

请注意，对于以特定方式与图像关联的页面，图像会显示在轮播中。 当页面不与图像关联时，只显示链接列表。

![chlimage_1-151](assets/chlimage_1-151.png)

**“轮播属性”选项卡**

配置轮播的行为：

* 播放速度：显示下一张图像之前每个图像显示的时间（以毫秒为单位）。
* 过渡时间：图像过渡的动画持续时间（以毫秒为单位）。
* 控件样式：为在图像之间移动而提供的控件的类型。

**列表属性选项卡**

指定生成页面列表的方式：

* 生成列表使用：用于指定要包含在轮播中的页面的方法。 请参阅生成页面列表。
* 排序依据：选择用于排序页面列表的页面属性。 例如，选择jcr：title可按标题的字母顺序对页面进行排序。
* 限制：包含的最大页数。 此属性适用于构建页面列表的基于搜索的方法。

#### 构建页面列表 {#building-the-page-list}

轻扫轮播组件为Build List Using属性提供了以下值。 编辑对话框会根据您选择的值而发生更改：

**子页面**

该组件列出了特定页面的所有子页面。 选择此值后，请在“子页面”选项卡中选择该页面，或者不指定任何值以列出当前页面的子页面。

**固定列表**

指定包含页面的列表。 选择此值后，配置选择固定列表时显示的固定列表选项卡上的列表：

* 要添加页面，请单击“添加项目”，然后浏览该页面。
* 使用向上和向下箭头图标在列表中移动页面。
* 单击删除按钮可从列表中删除页面。

Order By属性不会影响固定列表的顺序。

**搜索**

使用关键词搜索结果填充列表。 在您指定的页面的子页面中执行搜索：

1. 要指定搜索的根页面，请使用“起始位置”属性选择页面路径。 指定当前页面下没有要搜索的路径。
1. 在“搜索查询”属性中，输入搜索关键字。

**高级搜索**

使用填充列表 [Querybuilder](/help/sites-developing/querybuilder-api.md) 查询。

### 图像 {#image}

向应用程序内容添加图像。

### 文本 {#text}

向应用程序内容添加富文本。

### 商店位置 {#store-locations}

商店位置组件为用户提供了用于查找业务网点的工具：

* 搜索
* 与设备的GPS坐标接近或远离的位置列表。

组件要求存储库包含每个存储的位置信息。 示例位置安装在/etc/commerce/locations/adobe节点上。 ![chlimage_1-152](assets/chlimage_1-152.png)

### 两列行 {#two-column-row}

使您能够将并排组件添加到页面中。

![chlimage_1-153](assets/chlimage_1-153.png)
