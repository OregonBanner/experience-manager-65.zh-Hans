---
title: ClientContext
seo-title: Client Context
description: 了解如何在AEM中使用Client Context。
seo-description: Learn how to use the Client Context in AEM.
uuid: 82b2f976-cb41-42f8-ad4b-3a5cd23cc5f5
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 7a3322fe-554e-479e-a27c-4259cdd3ba2e
docset: aem65
exl-id: 69c66c82-fbd6-406e-aefd-b85480a62109
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1878'
ht-degree: 0%

---

# ClientContext{#client-context}

>[!NOTE]
>
>Client Context已被ContextHub取代。 有关更多详细信息，请参阅相关 [配置]ch-configuring.md)和 [开发人员](/help/sites-developing/contexthub.md) 文档。

Client Context是一种机制，可为您提供有关当前页面和访客的特定信息。 可以使用 **Ctrl-Alt-c** (windows)或 **control-option-c** (Mac):

![](assets/clientcontext_alisonparker.png)

在 [发布和创作环境可显示信息](#propertiesavailableintheclientcontext) 关于：

* 访客；根据您的实例，会请求或派生某些信息。
* 页面标记和当前访客访问这些标记的次数（当您将鼠标移动到特定标记上时会显示此标记）。
* 页面信息。
* 技术环境信息；例如IP地址、浏览器和屏幕分辨率。
* 当前已解析的任何区段。

图标（仅在创作环境中可用）允许您配置Client Context的详细信息：

![](do-not-localize/clientcontext_icons.png)

* **编辑**
将打开一个新页面，允许您 [编辑、添加或删除配置文件属性](#editingprofiledetails).

* **加载**
您可以 [从用户档案列表中选择并加载用户档案](#loading-a-new-user-profile) 你要测试。

* **重置**
您可以 [重置用户档案](#resetting-the-profile-to-the-current-user) 到当前用户的ID。

## 可用的客户端上下文组件 {#available-client-context-components}

Client Context可显示以下属性([根据使用编辑选择的内容](#adding-a-property-component)):

**冲浪者信息** 显示以下客户端信息：

* the **IP地址**
* **关键词** 用于搜索引擎反向链接
* the **浏览器** 正在使用
* the **操作系统** （正在使用的操作系统）
* 屏幕 **resolution**
* the **鼠标X** 位置
* the **鼠标Y** 位置

**活动流** 这提供有关用户在各种平台上的社交活动的信息；例如，AEM论坛、博客、评级等。

**Campaign** 允许作者模拟营销活动的特定体验。 此组件会覆盖常规的促销活动分辨率和体验选择，以便能够测试各种排列。

营销活动解决方案通常基于营销活动的优先级属性。 体验通常根据区段进行选择。

**购物车** 显示购物车信息，包括产品条目（标题、数量、价格格式化等）、已解析的促销活动（标题、消息等） 和凭证（代码、说明等）。

购物车会话存储还使用ClientContextCartServlet通知服务器有关已解析的促销更改（基于分段更改）。

**通用商店** 是显示存储内容的通用组件。 它是通用存储属性组件的较低级别版本。

必须为通用商店配置JS渲染器，该渲染器将以自定义方式显示数据。

**一般存储属性** 是显示存储内容的通用组件。 它是通用存储组件的更高级别版本。

通用商店属性组件包含一个默认渲染器，其中列出了配置的属性（以及缩略图）。

**地理位置** 显示客户端的纬度和经度。 它使用HTML5地理位置API查询浏览器的当前位置。 这会导致向访客显示一个弹出窗口，浏览器会在该弹出窗口中询问访客是否同意共享其位置。

在Context Cloud中显示时，组件会使用Google API将地图显示为缩略图。 组件受Google API的约束 [使用限制](https://developers.google.com/maps/documentation/staticmaps/intro#Limits).

>[!NOTE]
>
>在AEM 6.1中，地理位置存储不再提供反向地理编码功能。 因此，地理位置存储不再检索有关当前位置的详细信息，如城市名称或国家/地区代码。 使用此存储数据的区段将无法正常运行。 地理位置存储仅包含位置的纬度和经度。

**JSONP商店** 显示依赖于安装的内容的组件。

JSONP标准是对JSON的补充，它允许规避同一源策略（使Web应用程序无法与位于其他域上的服务器通信）。 它包括在函数调用中封装JSON对象，以便能够将其作为 `<script>` 从另一个域（这是允许对同一源策略的例外）。

JSONP存储与任何其他存储一样，但它加载来自其他域的信息，而无需拥有有关当前域上该信息的代理。 请参阅 [通过JSONP在客户端上下文中存储数据](/help/sites-administering/client-context.md#storing-data-in-client-context-via-jsonp).

>[!NOTE]
>
>JSONP存储不会缓存Cookie中的信息，但会在每次页面加载时检索该数据。

**用户档案数据** 显示在用户配置文件中收集的信息。 例如，性别、年龄、电子邮件地址等。

**已解析的区段** 显示当前解析的区段（通常取决于客户端上下文中显示的其他信息）。 这在配置营销活动时很重要。

例如，鼠标当前位于窗口的左侧还是右侧部分。 此区段主要用于测试，因为更改可立即看到。

**社交图** 显示用户好友和关注者的社交图。

>[!NOTE]
>
>目前，这是一项演示功能，依赖于我们演示用户配置文件节点上的预配置数据集。 例如，请参阅：
>
>`/home/users/geometrixx/aparker@geometrixx.info/profile` =>好友属性

**标记云** 显示在当前页面上设置的标记以及在浏览网站时收集的标记。 将鼠标移动到标记上会显示当前用户访问包含该特定标记的页面的次数。

>[!NOTE]
在DAM资产中设置的标记在访问的页面上显示将不会被计数。

**Technographics商店** 此组件取决于您的安装。

**已查看的产品** 跟踪购物者已查看的产品。 可以查询最近查看的产品或购物车中尚未包含的最近查看的产品。

此会话存储没有默认的客户端上下文组件。

有关其他信息，请参阅 [Client Context详细信息](/help/sites-developing/client-context.md).

>[!NOTE]
页面数据不再作为默认组件显示在客户端上下文中。 如果需要，您可以通过编辑Client Context并添加 **一般存储属性** 组件，然后配置此组件以定义 **存储** as `pagedata`.

## 更改Client Context配置文件 {#changing-the-client-context-profile}

Client Context允许您以交互方式更改详细信息：

* 更改Client Context中使用的配置文件允许您查看不同用户在当前页面中将看到的不同体验。
* 除了更改用户配置文件之外，您还可以更改一些配置文件详细信息，以查看页面体验在各种情况下的差异。

### 加载新用户配置文件 {#loading-a-new-user-profile}

您可以通过以下任一方式更改用户档案：

* [使用加载图标](#loading-a-new-visitor-profile-with-the-load-profile-icon)
* [使用选择滑块](#loadinganewvisitorprofilewiththeselectionslider)

完成后，您可以 [重置用户档案](#resetting-the-profile-to-the-current-user).

#### 使用加载配置文件图标加载新访客配置文件 {#loading-a-new-visitor-profile-with-the-load-profile-icon}

1. 单击加载配置文件图标：

   ![](do-not-localize/clientcontext_loadprofile.png)

1. 此时将打开对话框，您可以在此处选择要加载的用户档案：

   ![](assets/clientcontext_profileloader.png)

1. 单击 **确定** 加载。

#### 使用选择滑块加载新用户配置文件 {#loading-a-new-user-profile-with-the-selection-slider}

您还可以使用选择滑块选择配置文件：

1. 双击表示当前用户的图标。 将打开选择器，使用箭头导航并查看可用的配置文件：

   ![](assets/clientcontext_profileselector.png)

1. 单击要加载的用户档案。 加载详细信息后，单击选择器外部以关闭。

#### 将用户档案重置为当前用户 {#resetting-the-profile-to-the-current-user}

1. 使用重置图标将Client Context中的配置文件返回到当前用户的配置文件：

   ![](do-not-localize/clientcontext_resetprofile.png)

### 更改浏览器平台 {#changing-the-browser-platform}

1. 双击表示浏览器平台的图标。 将打开选择器，使用箭头导航并查看可用的平台/浏览器：

   ![](assets/clientcontext_browserplatform.png)

1. 单击要加载的平台浏览器。 加载详细信息后，单击选择器外部以关闭。

### 更改地理位置 {#changing-the-geolocation}

1. 双击地理位置图标。 此时将打开一个展开的地图，您可以在此将标记拖到新位置：

   ![](assets/clientcontext_geomocationrelocate.png)

1. 单击映射外部以关闭。

### 更改标记选择 {#changing-the-tag-selection}

1. 双击Client Context的Tag Cloud部分。 此时将打开相应的对话框，您可以在此处选择标记：

   ![](assets/clientcontext_tagselection.png)

1. 单击确定以加载到Client Context中。

## 编辑客户端上下文 {#editing-the-client-context}

编辑客户端上下文可用于设置（或重置）某些属性的值、添加新属性或删除不再需要的属性。

### 编辑属性详细信息 {#editing-property-details}

编辑客户端上下文可用于设置（或重置）某些属性的值。 这允许您测试特定方案(对于 [分段](/help/sites-administering/campaign-segmentation.md) 和 [营销活动](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md))。

![](assets/clientcontext_alisonparker_edit.png)

### 添加属性组件 {#adding-a-property-component}

在您打开 **ClientContext设计页面**，您还可以 **添加** 使用可用组件(这些组件同时列在Sidekick上，或从 **插入新组件** 对话框，该对话框在 **将组件或资产拖动到此处** 框):

![](assets/clientcontext_alisonparker_new.png)

### 删除属性组件 {#removing-a-property-component}

在您打开 **ClientContext设计页面**，您还可以 **删除** 属性（如果不再需要）。 其中包括现成提供的属性； **重置** 如果删除了，将恢复这些值。

## 通过JSONP在客户端上下文中存储数据 {#storing-data-in-client-context-via-jsonp}

请按照此示例使用JSONP存储上下文存储组件将外部数据添加到Client Context。 然后，根据来自该数据的信息创建区段。 该示例使用WIPmania.com提供的JSONP服务。 该服务根据Web客户端的IP地址返回地理位置信息。

此示例使用Geometrixx Outdoors示例网站访问Client Context并测试创建的区段。 只要页面已启用Client Context，您就可以使用其他网站。 (请参阅 [向页面添加Client Context](/help/sites-developing/client-context.md#adding-client-context-to-a-page).)

### 添加JSONP存储组件 {#add-the-jsonp-store-component}

将JSONP存储组件添加到Client Context中，然后使用它检索和存储有关Web客户端的地理位置信息。

1. 在AEM创作实例上打开Geometrixx Outdoors网站的英文主页。 ([https://localhost:4502/content/geometrixx-outdoors/en.html](https://localhost:4502/content/geometrixx-outdoors/en.html))。
1. 要打开Client Context，请按Ctrl-Alt-c（窗口）或control-option-c(Mac)。
1. 单击Client Context顶部的编辑图标以打开Client Context Designer。

   ![](do-not-localize/chlimage_1.png)

1. 将JSONP存储组件拖到Client Context。

   ![](assets/chlimage_1-4.jpeg)

1. 双击组件以打开编辑对话框。
1. 在JSONP服务URL框中，输入以下URL，然后单击获取存储：

   `https://api.wipmania.com/jsonp?callback=${callback}`

   该组件调用JSONP服务并列出返回数据包含的所有属性。 列表中的属性是将在Client Context中可用的属性。

   ![](assets/chlimage_1-40.png)

1. 单击确定。
1. 返回Geometrixx Outdoors主页并刷新页面。 Client Context现在包含来自JSONP存储组件的信息。

   ![](assets/chlimage_1-41.png)

### 创建区段 {#create-the-segment}

使用使用JSONP存储组件创建的会话存储中的数据。 区段使用会话存储中的纬度和当前日期来确定客户端位置的冬季时间。

1. 在Web浏览器中打开工具控制台(`https://localhost:4502/miscadmin#/etc`)。
1. 在文件夹树中，单击“工具/分段”文件夹，然后单击“新建”>“新建文件夹”。 指定以下属性值，然后单击创建：

   * 名称：mysegments
   * 标题：我的区段

1. 选择My Segments文件夹，然后单击新建>新建页面：

   1. 对于标题，键入Winter。
   1. 选择区段模板。
   1. 单击创建。

1. 右键单击“Winter（冬季）”区段，然后单击“Open（打开）”。
1. 将通用存储属性拖到默认的AND容器。

   ![](assets/chlimage_1-5.jpeg)

1. 双击组件以打开编辑对话框，指定以下属性值，然后单击确定：

   * 商店：维马尼亚
   * 属性名称：latitude
   * 运算符：大于
   * 属性值：30

1. 将脚本组件拖到同一AND容器，然后打开其编辑对话框。 添加以下脚本，然后单击“确定”：

   `3 < new Date().getMonth() < 12`
