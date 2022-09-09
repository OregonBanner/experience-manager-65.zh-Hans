---
title: 建立组件数据与 Adobe Analytics 属性的映射
seo-title: Mapping Component Data with Adobe Analytics Properties
description: 了解如何使用SiteCatalyst属性映射组件数据。
seo-description: Learn how to map component data with SiteCatalyst properties.
uuid: b08ab37f-ad58-4c04-978f-8e21a3823ae8
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 6c1f8869-62d9-4fac-aa0d-b99bb0e86d6b
docset: aem65
exl-id: c7c0c705-ec16-40f5-ad08-193f82d01263
source-git-commit: 58594be73372e128ba999a8290615fbcb447084e
workflow-type: tm+mt
source-wordcount: '1445'
ht-degree: 1%

---

# 建立组件数据与 Adobe Analytics 属性的映射{#mapping-component-data-with-adobe-analytics-properties}

向框架中添加用于收集数据以发送到Adobe Analytics的组件。 用于收集分析数据的组件将数据存储在相应的 **CQ变量**. 在将此类组件添加到框架时，框架会显示CQ变量列表，以便您可以将每个变量添加到相应的 **Analytics变量**.

![aa-11](assets/aa-11.png)

当 **AEM视图** 打开后，内容查找器中会显示Analytics变量。

![aa-12](assets/aa-12.png)

您可以使用相同的 **CQ变量**.

![chlimage_1-68](assets/chlimage_1-68.png)

加载页面并满足以下条件时，会将映射的数据发送到Adobe Analytics:

* 页面与框架关联。
* 页面使用添加到框架中的组件。

请按照以下过程将CQ组件变量映射到Adobe Analytics报表属性。

1. 在 **AEM视图**，将跟踪组件从Sidekick拖动到框架上。 例如，将 **页面** 组件组件 **常规** 类别。

   ![aa-13](assets/aa-13.png)

   有几个默认组件组： **常规**, **商务**, **社区**&#x200B;和 **其他**. 您的AEM实例可配置为显示不同的组和组件。

1. 要将Adobe Analytics变量与组件中定义的变量映射，请拖动 **Analytics变量** 从内容查找器到跟踪组件上的字段。 例如，拖动 `Page Name (pageName)` to `pagedata.title`.

   ![aa-14](assets/aa-14.png)

   >[!NOTE]
   >
   >为框架选择的报表包ID(RSID)可确定内容查找器中显示的Adobe Analytics变量。

1. 对其他组件和变量重复上述两个步骤。

   >[!NOTE]
   >
   >您可以映射多个Analytics变量(例如， `props`, `eVars`, `events`)到同一CQ变量(例如， `pagedata.title`)

   >[!CAUTION]
   >
   >强烈建议：
   >
   >* `eVars` 和 `props` 映射到以下任一值开头的CQ变量 `pagedata.X` 或 `eventdata.X`
   >* 而事件应映射到以 `eventdata.events.X`


1. 要使框架在网站的发布实例上可用，请打开 **页面** 选项卡，然后单击 **激活框架。**

## 映射产品相关变量 {#mapping-product-related-variables}

AEM使用命名与产品相关的变量和事件的约定，这些变量和事件将映射到与Adobe Analytics产品相关的属性：

| CQ变量 | Analytics变量 | 描述 |
|--- |--- |--- |
| `product.category` | `product.category` （转化变量） | 产品类别。 |
| `product.sku` | `product.sku` （转化变量） | 产品SKU。 |
| `product.quantity` | `product.quantity` （转化变量） | 要购买的产品数量。 |
| `product.price` | `product.price` （转化变量） | 产品价格。 |
| `product.events.<eventName>` | 要与报表中的产品关联的成功事件。 | `product.events` 是命名事件的前缀 *eventName。* |
| `product.evars.<eVarName>` | 转化变量( `eVar`)与产品关联。 | `product.evars` 是名为的eVar变量的前缀 *eVarName。* |

一些AEM Commerce组件使用这些变量名称。

>[!NOTE]
>
>请勿将Adobe Analytics产品属性映射到CQ变量。 如表中所述，配置与产品相关的映射实际上等同于映射产品变量。

### 检查Adobe Analytics上的报表 {#checking-reports-on-adobe-analytics}

1. 使用提供给Adobe Analytics的相同凭据登录AEM网站。
1. 确保所选的RSID是前面步骤中使用的RSID。
1. 在 **报表** （位于页面左侧）选择 **自定义转化**，则 **自定义转化1-10** ，然后选择对应的变量 `eVar7`

1. 根据您使用的Adobe Analytics版本，您需要平均等待45分钟，才能使用所使用的搜索词更新报表；例如示例中的茄子

## 在Adobe Analytics框架中使用内容查找器(cf#) {#using-the-content-finder-cf-with-adobe-analytics-frameworks}

最初，当您打开Adobe Analytics框架时，内容查找器包含下面的预定义Analytics变量：

* 流量
* 转化
* 事件

选择RSID后，所有属于该RSID的变量都将添加到列表中。\
的 `cf#` 需要将Analytics变量映射到不同跟踪组件上存在的CQ变量。 请参阅设置基本跟踪框架。

根据为框架选择的视图，内容查找器将由Analytics变量(在AEM视图中)或CQ变量（在Analytics视图中）填充。

可以通过以下方式处理列表：

1. 在 **AEM视图**，则可以根据使用3个过滤器按钮选择的变量类型来过滤列表：

   * 如果 *“无”按钮* ，则列表会显示完整列表。
   * 如果 **流量** 按钮时，该列表将仅显示属于“流量”部分的变量。
   * 如果 **转化** 按钮时，该列表将仅显示属于“转化”部分的变量。
   * 如果 **事件** 按钮时，该列表将仅显示属于“事件”部分的变量。

   >[!NOTE]
   >
   >一次只能有一个过滤器按钮处于活动状态。

   1. 该列表还具有搜索功能，该功能可根据在搜索字段中输入的文本筛选元素。
   1. 如果在搜索列表中的元素时激活了过滤器选项，则显示的结果也会根据活动按钮进行过滤。
   1. 您可以随时使用旋转箭头按钮重新加载列表。
   1. 如果在框架上选择了多个RSID，则列表中的所有变量都将使用所选RSID中使用的所有标签来显示。


1. 在Adobe Analytics视图中，内容查找器显示所有属于在CQ视图中拖动的跟踪组件的CQ变量。

   * 例如，在 **下载组件** 是 *只拖一个* 在CQ视图中（具有两个可映射的变量） *eventdata.downloadLink* 和 *eventdata.events.startDownload*)，则在切换到Adobe Analytics视图时，内容查找器将如下所示：

   ![aa-22](assets/aa-22.png)

   * 可将这些变量拖放到属于这3个变量部分中任一部分(**流量**, **转化** 和 **事件**)。

   * 在CQ视图中将新跟踪组件拖动到框架上时，属于该组件的CQ变量将自动添加到Adobe Analytics视图的内容查找器(cf#)中。
   >[!NOTE]
   >
   >在任何给定时间，都只能将一个CQ变量映射到Adobe Analytics变量。

## 使用AEM视图和Analytics视图 {#using-aem-view-and-analytics-view}

在任何给定时间，用户都可以选择在框架页面上查看Adobe Analytics映射的两种方式之间切换。 这两个视图从两个不同的角度提供了框架内映射的更好概述。

### AEM视图 {#aem-view}

![aa-23](assets/aa-23.png)

以上图为例， **AEM视图** 具有以下属性：

1. 这是打开框架时的默认视图。
1. 左侧：内容查找器(cf#)由Adobe Analytics变量根据所选的RSID来填充。
1. 制表符标题(**AEM视图** 和 **Analytics视图**):使用这些图标可在两个视图之间切换。

1. **AEM视图**:

   1. 如果框架具有从其父级继承的组件，则这些组件将列在此处，以及映射到这些组件的变量。

      1. 继承的组件已锁定。
      1. 要解锁继承的组件，只需双击该组件名称旁边的挂锁
      1. 要还原继承，必须删除已解锁的组件；之后，它将重新获得锁定状态。
   1. **将组件拖动到此处，以将其包含在分析框架中**:可以从Sidekick中拖放组件。
   1. 您可以找到当前包含在分析框架中的所有组件：

      1. 要添加组件，请从Sidekick的“组件”选项卡中拖动一个组件
      1. 要删除组件及其所有映射，请从组件的上下文菜单中选择删除，然后在确认对话框中接受删除。
      1. 请记住，组件只能从其中创建的框架中删除，而不能从传统意义上的子框架中删除（只能覆盖它们）。


### Analytics视图 {#analytics-view}

![aa-24](assets/aa-24.png)

1. 通过切换到 **Analytics视图** 选项卡。
1. 左侧：内容查找器(cf#)由CQ变量根据CQ视图中拖动到框架中的组件进行填充。
1. 制表符标题(**AEM视图** 和 **Analytics视图**):使用这些图标可在两个视图之间切换。

1. 三个表（流量、转化、事件）列出了所有可用的Adobe Analytics变量。 属于所选RSID。 此处显示的映射应与AEM视图中的映射相同：

   * **流量**:

      * 流量变量( `prop1`)映射到CQ变量( `eventdata.downloadLink`)

      * 当组件旁边有一个挂锁图标时，这意味着它继承自父框架，因此无法编辑
   * **转化**:

      * 转化变量( `eVar1`)映射到CQ变量( `pagedata.title`)

      * 转化变量( `eVar3`)映射到通过双击CQ变量字段并手动输入代码而添加的内联javascript表达式
   * **Event**:

      * 事件变量( `event1`)映射到CQ事件( `eventdata.events.pageView`)



>[!NOTE]
>
>通过双击字段并向其添加文本，也可以内嵌填充任何表的CQ变量列。 这些字段接受javascript作为输入。
>
>例如， `prop3` 您可以添加：
>     `'`* `Adobe:'+pagedata.title+':'+pagedata.sitesection`\
发送 *标题* 与其连接的页面 *站点区域* 使用 *:* （冒号）和前缀为 *Adobe* as `prop3`

>[!CAUTION]
在任何给定时间，都只能将一个CQ变量映射到Adobe Analytics变量。
