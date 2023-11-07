---
title: ClientContext
description: 了解如何使用Client Context查看有关Adobe Experience Manager中当前页面和访客的信息。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
docset: aem65
exl-id: 69c66c82-fbd6-406e-aefd-b85480a62109
source-git-commit: fc2f26a69c208947c14e8c6036825bb217901481
workflow-type: tm+mt
source-wordcount: '1978'
ht-degree: 0%

---


# ClientContext{#client-context}

>[!NOTE]
>
>ContextHub已取代客户端上下文。 有关更多详细信息，请参阅相关的 [配置](/help/sites-developing/ch-configuring.md) 和 [开发人员](/help/sites-developing/contexthub.md) 文档。

Client Context是一种机制，可为您提供有关当前页面和访客的特定信息。 可使用以下方式打开它 **Ctrl-Alt-c** (windows)或 **control-option-c** (Mac)：

![“客户端上下文”窗口的示例](assets/clientcontext_alisonparker.png)

在发布和创作环境中，它会显示有关以下项的信息：

* 访客；根据您的实例，将请求或派生某些信息。
* 页面标记以及当前访客访问这些标记的次数（当您将鼠标移动到特定标记上时显示） 。
* 页面信息。
* 有关技术环境的信息；如IP地址、浏览器和屏幕分辨率。
* 当前已解析的任何区段。

这些图标（仅在创作环境中可用）允许您配置客户端上下文的详细信息：

![“客户端上下文”窗口的“编辑”、“加载”和“重置”图标](do-not-localize/clientcontext_icons.png)

* **编辑**
此时将打开一个新页面，让您可以 [编辑、添加或删除配置文件属性](#editingprofiledetails).

* **加载**
您可以 [从配置文件列表中进行选择并加载配置文件](#loading-a-new-user-profile) 你想测试。

* **重置**
您可以 [重置配置文件](#resetting-the-profile-to-the-current-user) 到当前用户的密码。

## 可用的客户端上下文组件 {#available-client-context-components}

Client Context可以显示以下属性([根据使用编辑选择的内容](#adding-a-property-component))：

**网上冲浪者信息** 显示以下客户端信息：

* 该 **IP地址**
* **关键字** 用于搜索引擎反向链接
* 该 **浏览器** 正在使用
* 该 **操作系统** （操作系统）正在使用
* 屏幕 **resolution**
* 该 **鼠标X** position
* 该 **鼠标Y** position

**活动流** 这提供了有关用户在各种平台上的社交活动的信息；例如，AEM论坛、博客、评级等。

**营销活动** 允许作者模拟营销活动的特定体验。 此组件将覆盖正常的营销活动分辨率和体验选择，以便启用各种置换的测试。

营销活动解析通常基于营销活动的优先级属性。 体验通常基于分段进行选择。

**购物车** 显示购物车信息，包括产品条目（标题、数量、价格格式等）、已解决的促销活动（标题、消息等）和优惠券（代码、描述等）。

购物车会话存储还可以使用ClientContextCartServlet将已解决的促销更改通知（基于分段更改）到服务器。

**通用存储** 是显示存储内容的通用组件。 它是常规存储属性组件的较低版本。

必须使用JS渲染器配置通用存储，该渲染器将以自定义方式显示数据。

**常规存储属性** 是显示存储内容的通用组件。 它是通用存储组件的较高级版本。

通用存储属性组件包括一个默认呈现器，该呈现器列出了配置的属性（以及缩略图）。

**地理位置** 显示客户端的纬度和经度。 它使用HTML5地理位置API在浏览器中查询当前位置。 这会导致向访客显示弹出窗口，浏览器会询问访客是否同意共享其位置。

在Context Cloud中显示时，该组件使用Google API将地图显示为缩略图。 组件受Google API的约束 [使用限制](https://developers.google.com/maps/documentation/staticmaps/intro#Limits).

>[!NOTE]
>
>在AEM 6.1中，地理位置存储不再提供反向地理编码功能。 因此，地理位置存储不再检索有关当前位置的详细信息，如城市名称或国家/地区代码。 使用此存储数据的区段将无法正常运行。 地理位置存储仅包含位置的纬度和经度。

**JSONP存储** 显示与您的安装相关的内容的组件。

JSONP标准是JSON的补充，允许规避相同源策略（使得Web应用程序无法与位于其他域上的服务器通信）。 它包含在函数调用中封装JSON对象，以便能够将其加载为 `<script>` 来自其他域（这是允许对同一源策略执行的例外）。

JSONP存储与任何其他存储一样，但它可以加载来自其他域的信息，而无需在当前域上为该信息设置代理。 请参阅中的示例。 [通过JSONP在客户端上下文中存储数据](/help/sites-administering/client-context.md#storing-data-in-client-context-via-jsonp).

>[!NOTE]
>
>JSONP存储不缓存Cookie中的信息，而是在每次加载页面时检索该数据。

**配置文件数据** 显示用户配置文件中收集的信息。 例如，性别、年龄、电子邮件地址等。

**已解析的段** 显示当前解析的区段（通常取决于客户端上下文中显示的其他信息）。 这在配置营销活动时很有用。

例如，鼠标当前位于窗口的左手部分还是右手部分。 此区段主要用于测试，因为可以立即看到更改。

**社交图** 显示用户的好友和关注者的社交图。

>[!NOTE]
>
>目前这是一个演示功能，它依赖于演示用户的配置文件节点上预配置的数据集。 例如，请参阅:
>
>`/home/users/geometrixx/aparker@geometrixx.info/profile` => friends资产

**标记云** 显示在当前页面上设置的标记以及浏览网站时收集的标记。 将鼠标悬停在标签上会显示当前用户访问包含该特定标签的页面的次数。

>[!NOTE]
>
在DAM资产上设置的标记（显示在访问的页面中）不会被计数。

**Technographics商店** 此组件取决于您的安装。

**ViewedProducts** 跟踪购物者已查看的产品。 可查询最近查看过的产品或购物车中尚不存在的最近查看过的产品。

此会话存储没有默认的客户端上下文组件。

有关其他信息，请参阅 [客户端上下文详细信息](/help/sites-developing/client-context.md).

>[!NOTE]
>
页面数据不再作为默认组件存在于客户端上下文中。 如果需要，您可以通过编辑客户端上下文并添加 **常规存储属性** 组件，然后配置此项以定义 **存储** 作为 `pagedata`.

## 更改客户端上下文配置文件 {#changing-the-client-context-profile}

Client Context允许您以交互方式更改详细信息：

* 通过更改在Client Context中使用的配置文件，您可以看到各个用户将在当前页面上看到的不同体验。
* 除了更改用户配置文件外，您还可以更改某些配置文件详细信息，以查看页面体验在各种条件下的差异。

### 加载新的用户配置文件 {#loading-a-new-user-profile}

您可以通过以下任一方式更改配置文件：

* [使用加载图标](#loading-a-new-visitor-profile-with-the-load-profile-icon)
* [使用选择滑块](#loadinganewvisitorprofilewiththeselectionslider)

完成后，您可以 [重置配置文件](#resetting-the-profile-to-the-current-user).

#### 使用加载配置文件图标加载新访客配置文件 {#loading-a-new-visitor-profile-with-the-load-profile-icon}

1. 单击Load Profile图标：

   ![Client Context的“加载配置文件”图标](do-not-localize/clientcontext_loadprofile.png)

1. 这将打开对话框，您可以在此处选择要加载的配置文件：

   ![配置文件加载器对话框，其中显示了用于选择配置文件的下拉列表](assets/clientcontext_profileloader.png)

1. 单击 **确定** 以加载。

#### 使用选择滑块加载新的用户配置文件 {#loading-a-new-user-profile-with-the-selection-slider}

您还可以使用选择滑块选择配置文件：

1. 双击表示当前用户的图标。 选择器将打开，使用箭头导航并查看可用的配置文件：

   ![用户选择器](assets/clientcontext_profileselector.png)

1. 单击要加载的配置文件。 加载详细信息后，单击选择器外部以关闭。

#### 将配置文件重置为当前用户 {#resetting-the-profile-to-the-current-user}

1. 使用重置图标将Client Context中的配置文件返回到当前用户的配置文件：

   ![重置图标](do-not-localize/clientcontext_resetprofile.png)

### 更改浏览器平台 {#changing-the-browser-platform}

1. 双击表示浏览器平台的图标。 选择器将打开，使用箭头导航并查看可用的平台/浏览器：

   ![浏览器平台选择器](assets/clientcontext_browserplatform.png)

1. 单击要加载的平台浏览器。 加载详细信息后，单击选择器外部以关闭。

### 更改地理位置 {#changing-the-geolocation}

1. 双击地理位置图标。 展开的地图将打开，您可以在此处将标记拖动到新位置：

   ![地理位置详细信息](assets/clientcontext_geomocationrelocate.png)

1. 在地图外部单击以关闭。

### 更改标记选择 {#changing-the-tag-selection}

1. 双击Client Context的“标记云”部分。 此时将打开对话框，您可以在此处选择标记：

   ![标记云对话框](assets/clientcontext_tagselection.png)

1. 单击“确定”以加载到Client Context中。

## 编辑客户端上下文 {#editing-the-client-context}

编辑客户端上下文可用于设置（或重置）某些属性的值，添加新属性或删除不再需要的属性。

### 编辑属性详细信息 {#editing-property-details}

编辑客户端上下文可用于设置（或重置）某些属性的值。 这让您可以测试特定场景（尤其有用） [分段](/help/sites-administering/campaign-segmentation.md) 和 [营销活动](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md))。

![编辑客户端上下文](assets/clientcontext_alisonparker_edit.png)

### 添加属性组件 {#adding-a-property-component}

打开 **ClientContext设计页面**，您还可以 **添加** 一个全新的属性，它使用了可用的组件(这些组件在sidekick或 **插入新组件** 对话框，该对话框在 **将组件或资源拖动到此处** 框)：

![将属性添加到“客户端上下文”窗口](assets/clientcontext_alisonparker_new.png)

### 删除属性组件 {#removing-a-property-component}

打开 **ClientContext设计页面**，您还可以 **移除** 属性（如果不再需要）。 这包括提供的现成属性； **重置** 如果它们被删除，将恢复这些文件。

## 通过JSONP在客户端上下文中存储数据 {#storing-data-in-client-context-via-jsonp}

按照此示例使用JSONP存储上下文存储组件将外部数据添加到客户端上下文。 然后，根据该数据中的信息创建区段。 此示例使用WIPmania.com提供的JSONP服务。 该服务根据Web客户端的IP地址返回地理位置信息。

此示例使用Geometrixx Outdoors示例网站来访问Client Context并测试创建的区段。 只要该页面启用了Client Context，您就可以使用其他网站。 (请参阅 [向页面添加客户端上下文](/help/sites-developing/client-context.md#adding-client-context-to-a-page).)

### 添加JSONP存储组件 {#add-the-jsonp-store-component}

将JSONP Store组件添加到Client Context，并使用它检索和存储有关Web客户端的地理位置信息。

1. 在AEM创作实例上打开Geometrixx Outdoors网站的英语主页。 ([https://localhost:4502/content/geometrixx-outdoors/en.html](https://localhost:4502/content/geometrixx-outdoors/en.html))。
1. 要打开Client Context，请按Ctrl-Alt-c (windows)或control-option-c (Mac)。
1. 单击Client Context顶部的编辑图标以打开Client Context Designer。

   ![“链接”图标](do-not-localize/chlimage_1.png)

1. 将JSONP存储组件拖动到Client Context。

   ![将JSONP存储组件拖放到客户端上下文中](assets/chlimage_1-4.jpeg)

1. 双击组件以打开“编辑”对话框。
1. 在“JSONP服务URL”框中，输入以下URL，然后单击“获取存储”：

   `https://api.wipmania.com/jsonp?callback=${callback}`

   该组件调用JSONP服务并列出返回数据包含的所有属性。 列表中的属性是将在客户端上下文中可用的属性。

   ![JSONP服务的属性](assets/chlimage_1-40.png)

1. 单击确定。
1. 返回“Geometrixx Outdoors”主页并刷新该页。 Client Context现在包含来自JSONP存储组件的信息。

   ![使用数据填充的JSONP组件示例](assets/chlimage_1-41.png)

### 创建区段 {#create-the-segment}

使用您通过JSONP存储组件创建的会话存储中的数据。 区段使用会话存储中的纬度和当前日期来确定是否是在客户端位置的冬季时间。

1. 在Web浏览器中打开“工具”控制台(`https://localhost:4502/miscadmin#/etc`)。
1. 在文件夹树中，单击Tools/Segmentation文件夹，然后单击“新建”>“新建文件夹”。 指定以下属性值，然后单击“创建”：

   * 名称：mysegments
   * 标题：我的区段

1. 选择“我的区段”文件夹，然后单击“新建”>“新建页面”：

   1. 对于“标题”，键入Winter。
   1. 选择区段模板。
   1. 单击创建。

1. 右键单击Winter区段，然后单击“打开”。
1. 将常规存储属性拖到默认的AND容器中。

   ![将组件添加到区段编辑器](assets/chlimage_1-5.jpeg)

1. 双击该组件以打开“编辑”对话框，指定以下属性值，然后单击“确定”：

   * 商店： wipmania
   * 属性名称： latitude
   * 运算符：大于
   * 属性值：30

1. 将脚本组件拖动到同一个AND容器中，然后打开其“编辑”对话框。 添加以下脚本，然后单击“确定”：

   `3 < new Date().getMonth() < 12`
