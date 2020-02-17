---
title: ClientContext
seo-title: ClientContext
description: 了解如何在AEM中使用Client Context。
seo-description: 了解如何在AEM中使用Client Context。
uuid: 82b2f976-cb41-42f8-ad4b-3a5cd23cc5f5
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 7a3322fe-554e-479e-a27c-4259cdd3ba2e
docset: aem65
translation-type: tm+mt
source-git-commit: 684d2d5f73d571a15c8155e7870134c28dc892b7

---


# ClientContext{#client-context}

>[!NOTE]
>
>Client Context已被ContextHub取代。 有关详细信息，请参阅相关 [配置](/help/sites-administering/contexthub-config.md) 和开 [发人员文档](/help/sites-developing/contexthub.md) 。

Client Context是一种机制，可为您提供有关当前页面和访客的特定信息。 可以使用 **Ctrl-Alt-c** (Windows)或 **control-option-c** (Mac)打开它：

![](assets/clientcontext_alisonparker.png)

在发布和 [创作环境中，它都显示有关](#propertiesavailableintheclientcontext) :

* 访客；根据您的实例，会请求或派生某些信息。
* 页面标记和当前访客访问这些标记的次数（当您将鼠标移到特定标记上时显示）。
* 页面信息。
* 技术环境信息；如IP地址、浏览器和屏幕分辨率。
* 当前已解析的任何区段。

图标（仅在创作环境中可用）允许您配置Client Context的详细信息：

![](do-not-localize/clientcontext_icons.png)

* **编辑**&#x200B;此时将打开一个新页面，允许您 [编辑、添加或删除配置文件属性](#editingprofiledetails)。

* **加载**&#x200B;您可 [以从配置文件列表中选择并加载要测试的配置文件](#loading-a-new-user-profile) 。

* **重置**&#x200B;您可 [以将配置文件重置为当前用户的配置文件](#resetting-the-profile-to-the-current-user) 。

## 可用的Client Context组件 {#available-client-context-components}

Client Context可显示以下属性(取[决于使用“编辑”选择的内容](#adding-a-property-component)):

**Surfer信息** ：显示以下客户端信息：

* IP **地址**
* **用于搜索引擎** 引用的关键字
* 使 **用的浏览器**
* 使 **用的OS** （操作系统）
* 屏幕分辨 **率**
* 鼠标 **X位置**
* 鼠标 **Y位置**

**活动流** ：提供用户在不同平台上的社交活动信息；例如，AEM论坛、博客、评级等。

**营销活动** -允许作者模拟营销活动的特定体验。 此组件覆盖了常规的营销活动分辨率和体验选择，以便能够测试各种组合。

营销活动解决方案通常基于营销活动的优先级属性。 体验通常根据细分进行选择。

**购物车** 显示购物车信息，包括产品条目（标题、数量、价格已格式化等）、已解析的促销（标题、消息等）和优惠券（代码、说明等）。

购物车会话商店还使用ClientContextCartServlet通知服务器已解决的促销更改（基于分段更改）。

**通用商店** -显示商店内容的通用组件。 它是通用商店属性组件的低级版本。

通用商店必须配置JS呈示器，以自定义方式显示数据。

**通用商店属性** -显示商店内容的通用组件。 它是通用商店组件的更高级别版本。

通用商店属性组件包含一个默认渲染器，它列出已配置的属性（以及缩略图）。

**地理位置** 显示客户端的纬度和经度。 它使用HTML5地理位置API查询浏览器的当前位置。 这会导致向访客显示一个弹出窗口，浏览器会询问他们是否同意共享其位置。

当在Context cloud中显示时，该组件使用Google API将地图显示为缩略图。 该组件受Google API使用限制 [的约束](https://developers.google.com/maps/documentation/staticmaps/intro#Limits)。

>[!NOTE]
>
>在AEM 6.1中，Geolocation商店不再提供反向地理编码功能。 因此，Geolocation存储不再检索有关当前位置的详细信息，如城市名称或国家／地区代码。 使用此存储数据的区段无法正常工作。 Geolocation存储区只包含位置的纬度和经度。

**JSONP Store** A component that displays content that is dependent on your installation.

JSONP标准是对JSON的补充，它允许规避相同的源策略（使Web应用程序无法与位于另一个域上的服务器通信）。 它包括将JSON对象封装在函数调用中，以便能够从另一个域加载它（这是同一源策略允许的例外）。 `<script>`

JSONP Store与任何其他存储一样，但它加载来自另一个域的信息，而无需为当前域上的信息设置代理。 请参阅通过JSONP在 [Client Context中存储数据中的示例](/help/sites-administering/client-context.md#storing-data-in-client-context-via-jsonp)。

>[!NOTE]
>
>JSONP Store不缓存Cookie中的信息，但会在每页加载时检索该数据。

**个人资料数据** -显示在用户个人资料中收集的信息。 例如，性别、年龄、电子邮件地址等。

**已解析的区段** -显示当前解析的区段（通常取决于Client Context中显示的其他信息）。 这在配置营销活动时很有意义。

例如，鼠标当前位于窗口的左手部分还是右手部分上。 此区段主要用于测试，因为更改可立即看到。

**社交图** -显示用户的好友和关注者的社交图。

>[!NOTE]
>
>目前，这是一个演示功能，它依赖于我们演示用户的配置文件节点上的预配置数据集。 例如，请参阅：
>
>`/home/users/geometrixx/aparker@geometrixx.info/profile` =>朋友财产

**标记云** -显示在当前页面上设置的标记以及在浏览网站时收集的标记。 将鼠标移到标记上会显示当前用户访问包含该特定标记的页面的次数。

>[!NOTE]
在DAM资产上设置的标记在所访问的页面上显示将不会计数。

**Technographics Store** This component is dependent on your installation.

**已查看的产品** -跟踪购物者已查看的产品。 可以查询最近查看的产品或最近查看的产品（不在购物车中）。

此会话存储没有默认的客户端上下文组件。

有关其他信息，请参阅详 [细信息中的Client Context](/help/sites-developing/client-context.md)。

>[!NOTE]
页面数据不再作为默认组件存在于Client Context中。 如果需要，您可以通过编辑Client Context，添加“通用商店属性”组 **件** ，然后将其配置为将 **Store** 定义为 `pagedata`。

## 更改Client Context配置文件 {#changing-the-client-context-profile}

Client Context允许您以交互方式更改详细信息：

* 更改Client Context中使用的配置文件允许您查看不同用户在当前页面看到的不同体验。
* 除了更改用户配置文件之外，您还可以更改一些配置文件详细信息，以查看在不同条件下页面体验的差异。

### 加载新用户配置文件 {#loading-a-new-user-profile}

您可以通过以下任一方式更改配置文件：

* [使用加载图标](#loading-a-new-visitor-profile-with-the-load-profile-icon)
* [使用选择滑块](#loadinganewvisitorprofilewiththeselectionslider)

完成后，您可以 [重置配置文件](#resetting-the-profile-to-the-current-user)。

#### 使用加载配置文件图标加载新的访客配置文件 {#loading-a-new-visitor-profile-with-the-load-profile-icon}

1. 单击“加载配置文件”图标：

   ![](do-not-localize/clientcontext_loadprofile.png)

1. 此操作将打开对话框，您可以在此选择要加载的配置文件：

   ![](assets/clientcontext_profileloader.png)

1. Click **OK** to load.

#### 使用选择滑块加载新用户配置文件 {#loading-a-new-user-profile-with-the-selection-slider}

您还可以使用选择滑块选择配置文件：

1. 双击表示当前用户的图标。 选择器将打开，使用箭头导航并查看可用的配置文件：

   ![](assets/clientcontext_profileselector.png)

1. 单击要加载的配置文件。 加载详细信息后，请在选择器外部单击以关闭。

#### 将配置文件重置为当前用户 {#resetting-the-profile-to-the-current-user}

1. 使用重置图标将Client context中的配置文件返回到当前用户的配置文件：

   ![](do-not-localize/clientcontext_resetprofile.png)

### 更改浏览器平台 {#changing-the-browser-platform}

1. 双击表示浏览器平台的图标。 选择器将打开，使用箭头导航并查看可用的平台／浏览器：

   ![](assets/clientcontext_browserplatform.png)

1. 单击要加载的平台浏览器。 加载详细信息后，请在选择器外部单击以关闭。

### 更改地理位置 {#changing-the-geolocation}

1. 双击地理位置图标。 此时将打开一个扩展的地图，您可以在此将标记拖动到新位置：

   ![](assets/clientcontext_geomocationrelocate.png)

1. 在地图外部单击可关闭。

### 更改标记选择 {#changing-the-tag-selection}

1. 双击Client Context的“标记云”部分。 此时将打开对话框，您可以在此选择标记：

   ![](assets/clientcontext_tagselection.png)

1. 单击确定以加载到Client Context中。

## 编辑Client Context {#editing-the-client-context}

编辑Client Context可用于设置（或重置）某些属性的值、添加新属性或删除不再需要的属性。

### 编辑属性详细信息 {#editing-property-details}

编辑Client Context可用于设置（或重置）某些属性的值。 这允许您测试特定方案(对于分段和营销活动 [尤其](/help/sites-administering/campaign-segmentation.md)[有用](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md))。

![](assets/clientcontext_alisonparker_edit.png)

### 添加属性组件 {#adding-a-property-component}

在打开 **ClientContext设计页面后**，您还可以使用可用的组件(组件列在Sidekick上或从 **Insert New Component** （插入新组件）对话框中，该对话框在 ******** Drag组件或此处的资产框上双击后打开)添加全新的属性：

![](assets/clientcontext_alisonparker_new.png)

### 删除属性组件 {#removing-a-property-component}

打开ClientContext设计页 **面后**，如果不再需要，还可以 **删除属性** 。 这包括现成提供的属性；如 **果删除** ,“重置”将恢复这些设置。

## 通过JSONP在Client context中存储数据 {#storing-data-in-client-context-via-jsonp}

请按照此示例使用JSONP Store上下文存储组件将外部数据添加到Client Context。 然后，根据该数据中的信息创建区段。 该示例使用WIPmania.com提供的JSONP服务。 该服务基于该Web客户端的IP地址返回地理位置信息。

此示例使用Geometrixx Outdoors示例网站访问Client Context并测试创建的区段。 只要页面启用了Client Context，您就可以使用其他网站。 (请参 [阅将Client Context添加到页面](/help/sites-developing/client-context.md#adding-client-context-to-a-page)。)

### 添加JSONP商店组件 {#add-the-jsonp-store-component}

将JSONP store组件添加到Client Context，然后使用它检索和存储有关Web客户端的地理位置信息。

1. 打开AEM作者实例上Geometrixx Outdoors站点的英文主页。 ([https://localhost:4502/content/geometrixx-outdoors/en.html](https://localhost:4502/content/geometrixx-outdoors/en.html))。
1. 要打开Client Context，请按Ctrl-Alt-c(Windows)或control-option-c(Mac)。
1. 单击Client Context顶部的编辑图标以打开Client Context Designer。

   ![](do-not-localize/chlimage_1.png)

1. 将JSONP Store组件拖动到Client Context。

   ![](assets/chlimage_1-4.jpeg)

1. 双击组件以打开编辑对话框。
1. 在“JSONP服务URL”框中，输入以下URL，然后单击“提取商店”:

   `https://api.wipmania.com/jsonp?callback=${callback}`

   该组件调用JSONP服务并列出返回数据包含的所有属性。 列表中的属性是那些将在Client Context中可用的属性。

   ![](assets/chlimage_1-40.png)

1. 单击“确定”。
1. 返回Geometrixx Outdoors主页并刷新该页面。 Client Context现在包括JSONP store组件中的信息。

   ![](assets/chlimage_1-41.png)

### 创建区段 {#create-the-segment}

使用您使用JSONP存储组件创建的会话存储中的数据。 区段使用会话商店的纬度和当前日期来确定是否是客户端位置的冬季时间。

1. 在Web浏览器()中打开工具控`https://localhost:4502/miscadmin#/etc`制台。
1. 在文件夹树中，单击“工具／分段”文件夹，然后单击“新建”>“新建文件夹”。 指定以下属性值，然后单击创建：

   * 名称：mysegments
   * 标题：我的细分

1. 选择“我的区段”文件夹，然后单击“新建”>“新建页面”:

   1. 在“标题”中，键入Winter。
   1. 选择区段模板。
   1. 单击创建。

1. 右键单击“冬季”区段，然后单击打开。
1. 将“通用商店属性”拖动到默认的AND容器。

   ![](assets/chlimage_1-5.jpeg)

1. 双击组件以打开编辑对话框，指定以下属性值，然后单击确定：

   * 商店：wipmania
   * 属性名称：纬度
   * 运营商：大于
   * 属性值：30

1. 将“脚本”组件拖至同一AND容器，然后打开其编辑对话框。 添加以下脚本，然后单击“确定”:

   `3 < new Date().getMonth() < 12`

