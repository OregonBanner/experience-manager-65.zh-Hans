---
title: 建立组件数据与 Adobe Analytics 属性的映射
description: 了解如何使用SiteCatalyst属性映射组件数据。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
docset: aem65
exl-id: c7c0c705-ec16-40f5-ad08-193f82d01263
source-git-commit: 260f71acd330167572d817fdf145a018b09cbc65
workflow-type: tm+mt
source-wordcount: '1440'
ht-degree: 1%

---

# 建立组件数据与 Adobe Analytics 属性的映射{#mapping-component-data-with-adobe-analytics-properties}

将组件添加到框架中以收集要发送到Adobe Analytics的数据。 用于收集Analytics数据的组件会将数据存储到适当的 **CQ变量**. 当您将此类组件添加到框架时，该框架会显示CQ变量列表，以便您可以将每个变量添加到相应的变量中 **Analytics变量**.

![aa-11](assets/aa-11.png)

当 **AEM视图** 打开，则Analytics变量会显示在内容查找器中。

![aa-12](assets/aa-12.png)

您可以使用相同的 **CQ变量**.

![chlimage_1-68](assets/chlimage_1-68.png)

当页面加载并满足以下条件时，映射的数据将被发送到Adobe Analytics：

* 该页面与框架关联。
* 该页面使用添加到框架中的组件。

使用以下过程可将CQ组件变量与Adobe Analytics报表属性进行映射。

1. 在 **AEM视图**，将跟踪组件从sidekick拖动到框架上。 例如，拖动 **页面** 组件来自 **常规** 类别。

   ![aa-13](assets/aa-13.png)

   有几个默认的组件组： **常规**， **商务**， **Communities**、和 **其他**. 您的AEM实例可以配置为显示不同的组和组件。

1. 要将Adobe Analytics变量与组件中定义的变量进行映射，请拖动 **Analytics变量** 从内容查找器转到跟踪组件上的字段。 例如，拖动 `Page Name (pageName)` 到 `pagedata.title`.

   ![aa-14](assets/aa-14.png)

   >[!NOTE]
   >
   >为框架选择的报表包ID (RSID)决定了显示在内容查找器中的Adobe Analytics变量。

1. 对其他组件和变量重复前两个步骤。

   >[!NOTE]
   >
   >您可以映射多个Analytics变量(例如， `props`， `eVars`， `events`)，以匹配相同的CQ变量(例如， `pagedata.title`)

   >[!CAUTION]
   >
   >强烈建议：
   >
   >* `eVars` 和 `props` 映射到以以下任一开头的CQ变量： `pagedata.X` 或 `eventdata.X`
   >* 而事件应映射到以开头的变量 `eventdata.events.X`

1. 要使框架在网站的发布实例上可用，请打开 **页面** 选项卡，然后单击 **激活框架。**

## 映射产品相关的变量 {#mapping-product-related-variables}

AEM使用约定来命名与产品相关的变量和事件，这些变量和事件旨在映射到Adobe Analytics产品相关的属性：

| CQ变量 | Analytics变量 | 描述 |
|--- |--- |--- |
| `product.category` | `product.category` （转化变量） | 产品类别。 |
| `product.sku` | `product.sku` （转化变量） | 产品sku。 |
| `product.quantity` | `product.quantity` （转化变量） | 正在购买的产品数。 |
| `product.price` | `product.price` （转化变量） | 产品价格。 |
| `product.events.<eventName>` | 要与报表中的产品关联的成功事件。 | `product.events` 是命名事件的前缀 *eventName。* |
| `product.evars.<eVarName>` | 转化变量( `eVar`)，以关联产品。 | `product.evars` 是名为的eVar变量的前缀 *eVarName。* |

多个AEM Commerce组件使用这些变量名称。

>[!NOTE]
>
>请勿将Adobe Analytics Products资产映射到CQ变量。 如表中所述配置产品相关映射实际上等同于映射Products变量。

### 检查Adobe Analytics上的报告 {#checking-reports-on-adobe-analytics}

1. 使用提供给AEM的相同凭据登录Adobe Analytics网站。
1. 确保选定的RSID是前面步骤中使用的RSID。
1. In **报告** （在页面的左侧）选择 **自定义转换**，则 **自定义转换1-10** 并选择对应的变量 `eVar7`

1. 根据您使用的Adobe Analytics版本，您平均需要等待45分钟，以便使用使用的搜索词更新报告；例如，示例中的茄子

## 在Adobe Analytics框架中使用内容查找器(cf#) {#using-the-content-finder-cf-with-adobe-analytics-frameworks}

最初，在打开Adobe Analytics框架时，内容查找器在下包含预定义的Analytics变量：

* 流量
* 转化
* 事件

选择RSID后，属于该RSID的所有变量都会添加到列表中。\
此 `cf#` 需要将Analytics变量映射到不同跟踪组件上存在的CQ变量。 请参阅为基本跟踪设置框架。

根据为框架选择的视图，内容查找器将由Analytics变量(在AEM视图中)或CQ变量（在Analytics视图中）填充。

可通过以下方式操作列表：

1. 时间 **AEM视图**&#x200B;之后，可以根据使用三个筛选按钮选择的变量类型对列表进行筛选：

   * 如果 *无按钮* 选中时，列表会显示完整列表。
   * 如果 **流量** 按钮时，列表将仅显示属于流量部分的变量。
   * 如果 **转化** 按钮时，列表将仅显示属于转化部分的变量。
   * 如果 **事件** 按钮时，列表将仅显示属于事件部分的变量。

   >[!NOTE]
   >
   >一次只能激活一个筛选器按钮。

   1. 列表还具有搜索功能，该功能根据在搜索字段中输入的文本筛选元素。
   1. 如果在搜索列表中的元素时激活了筛选器选项，则显示的结果也将根据活动按钮进行筛选。
   1. 可以使用“旋转箭头”按钮随时重新加载列表。
   1. 如果在框架中选择了多个RSID，则列表中的所有变量将使用选定RSID内使用的所有标签显示。

1. 在Adobe Analytics视图中时，内容查找器显示属于在CQ视图中拖动的跟踪组件的所有CQ变量。

   * 例如，如果 **下载组件** 是 *只有一个拖动* 在CQ视图（具有两个可映射变量）中 *eventdata.downloadLink* 和 *eventdata.events.startDownload*)，则当切换到Adobe Analytics视图时，内容查找器将如下所示：

   ![aa-22](assets/aa-22.png)

   * Adobe Analytics可以将变量拖放到属于三个变量部分(**流量**， **转化** 和 **事件**)。

   * 在CQ视图中将新跟踪组件拖动到框架上时，属于该组件的CQ变量会自动添加到Adobe Analytics视图中的内容查找器(cf#)。

   >[!NOTE]
   >
   >在任意给定时间，只能将一个CQ变量映射到Adobe Analytics变量。

## 使用AEM视图和Analytics视图 {#using-aem-view-and-analytics-view}

在任何给定时间，用户可以在框架页面上以两种方式查看Adobe Analytics映射。 从两个不同的角度来看，这两种视图提供了框架中映射的更好概述。

### AEM视图 {#aem-view}

![aa-23](assets/aa-23.png)

以上图为例， **AEM视图** 具有以下属性：

1. 这是框架打开时的默认视图。
1. 左侧：内容查找器(cf#)由基于所选RSID的Adobe Analytics变量填充。
1. 选项卡标题(**AEM视图** 和 **Analytics视图**)：使用这些选项可在两个视图之间切换。

1. **AEM视图**：

   1. 如果框架具有从其父框架继承的组件，则在此处列出这些组件，以及映射到这些组件的变量。

      1. 继承的组件将被锁定。
      1. 要解锁继承的组件，请双击该组件名称旁边的挂锁
      1. 要恢复继承，请删除已解锁的组件；之后，该组件将重新获得其锁定状态。

   1. **将组件拖动到此处以包含在分析框架中**：组件可以从Sidekick中拖动并放置在此处。
   1. 您可以找到当前包含在分析框架中的所有组件：

      1. 要添加组件，请从Sidekick的“组件”选项卡中拖动一个组件
      1. 要删除组件及其所有映射，请从组件的上下文菜单中选择删除，然后在确认对话框上接受删除。
      1. 请记住，组件只能从在其中创建的框架中删除，而不能从传统意义上的子框架中删除（它们只能被覆盖）。

### Analytics视图 {#analytics-view}

![aa-24](assets/aa-24.png)

1. 通过切换到 **Analytics视图** 选项卡。
1. 左侧：由CQ变量填充的内容查找器(cf#)基于在CQ视图中拖动到框架上的组件。
1. 选项卡标题(**AEM视图** 和 **Analytics视图**)：使用这些选项可在两个视图之间切换。

1. 三个表（流量、转化、事件）列出了所有可用的Adobe Analytics变量。 属于选定的RSID。 此处显示的映射应该与AEM视图中的映射相同：

   * **流量**:

      * 流量变量( `prop1`)映射到CQ变量( `eventdata.downloadLink`)

      * 当组件旁边有挂锁时，这意味着该组件继承自父框架，因此无法编辑

   * **转化**:

      * 转化变量( `eVar1`)映射到CQ变量( `pagedata.title`)

      * 转化变量( `eVar3`)，通过双击CQ变量字段并手动输入代码，映射到内联添加的JavaScript表达式

   * **Event**:

      * 事件变量( `event1`)映射到CQ事件( `eventdata.events.pageView`)

>[!NOTE]
>
>也可以内联填充任何表的CQ变量列，方法是双击该字段并向其添加文本。 这些字段接受JavaScript作为输入。
>
>例如，在 `prop3` 您可以添加：
>     `'`* `Adobe:'+pagedata.title+':'+pagedata.sitesection`\
发送 *标题* 与其连接的页面的 *sitesection* 使用 *：* （冒号）和前缀 *Adobe* 作为 `prop3`
>

>[!CAUTION]
>
在任意给定时间，只能将一个CQ变量映射到Adobe Analytics变量。
