---
title: 使用Adobe Analytics属性映射组件数据
seo-title: 使用Adobe Analytics属性映射组件数据
description: 了解如何使用SiteCatalyst属性映射组件数据。
seo-description: 了解如何使用SiteCatalyst属性映射组件数据。
uuid: b08ab37f-ad58-4c04-978f-8e21a3823ae8
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 6c1f8869-62d9-4fac-aa0d-b99bb0e86d6b
docset: aem65
translation-type: tm+mt
source-git-commit: 6f49e01aa3e9841c7b2917870593452b778667d2
workflow-type: tm+mt
source-wordcount: '1470'
ht-degree: 0%

---


# 使用Adobe Analytics属性映射组件数据{#mapping-component-data-with-adobe-analytics-properties}

将组件添加到框架中，以收集要发送到Adobe Analytics的数据。 旨在收集分析数据的组件将数据存储在相应的&#x200B;**CQ变量**&#x200B;中。 在将此类组件添加到框架时，框架会显示CQ变量的列表，以便您可以分别使用相应的&#x200B;**Analytics变量**。

![aa-11](assets/aa-11.png)

当&#x200B;**AEM视图**&#x200B;打开时，Analytics变量将显示在内容查找器中。

![aa-12](assets/aa-12.png)

可以使用相同的&#x200B;**CQ变量**&#x200B;映射多个Analytics变量。

![chlimage_1-68](assets/chlimage_1-68.png)

加载页面并满足以下条件时，将映射的数据发送到Adobe Analytics:

* 页面与框架关联。
* 该页面使用添加到框架的组件。

请按照以下过程将CQ组件变量与Adobe Analytics报表属性进行映射。

1. 在&#x200B;**AEM视图**&#x200B;中，将跟踪组件从Sidekick拖动到框架上。 例如，从&#x200B;**常规**&#x200B;类别中拖动&#x200B;**Page**&#x200B;组件组件。

   ![aa-13](assets/aa-13.png)

   有几个默认组件组：**一般**、**商务**、**社区**、**Search&amp;Promote**&#x200B;和&#x200B;**其它**。 您的AEM实例可配置为显示不同的组和组件。

1. 要将Adobe Analytics变量与组件中定义的变量进行映射，请将&#x200B;**Analytics变量**&#x200B;从内容查找器拖动到跟踪组件上的字段上。 例如，将`Page Name (pageName)`拖到`pagedata.title`。

   ![aa-14](assets/aa-14.png)

   >[!NOTE]
   >
   >为框架选择的报表包ID(RSID)决定内容查找器中显示的Adobe Analytics变量。

1. 对其他组件和变量重复上述两个步骤。

   >[!NOTE]
   >
   >您可以映射多个Analytics变量(例如，`props`、`eVars`、`events`)。`pagedata.title`

   >[!CAUTION]
   >
   >强烈建议：
   >    
   >    * `eVars` 并 `props` 映射到以或开头的CQ变 `pagedata.X` 量  `eventdata.X`
      >    
      >    
   * 而事件应映射到以`eventdata.events.X`开头的变量


1. 要使框架在站点的发布实例中可用，请打开Sidekick的&#x200B;**Page**&#x200B;选项卡，然后单击&#x200B;**激活框架。**

## 映射产品相关变量{#mapping-product-related-variables}

AEM使用一个约定来命名与产品相关的变量和事件，这些变量和应映射到与Adobe Analytics产品相关的属性：

| CQ变量 | 分析变量 | 描述 |
|---|---|---|
| `product.category` | `product.category` （转换变量） | 产品类别。 |
| `product.sku` | `product.sku` （转换变量） | 产品sku。 |
| `product.quantity` | `product.quantity` （转换变量） | 要购买的产品数。 |
| `product.price` | `product.price` （转换变量） | 产品价格。 |
| `product.events.<eventName>` | 要与报表中的产品关联的成功事件。 | `product.events` 是名为eventName的事件的 *前缀。* |
| `product.evars.<eVarName>` | 要与产品关联的转换变量(`eVar`)。 | `product.evars` 是名为eVarName的eVar变量的 *前缀。* |

几个AEM Commerce组件使用这些变量名称。

>[!NOTE]
>
>请勿将“Adobe Analytics产品”属性映射到CQ变量。 如表中所述配置与产品相关的映射与映射产品变量等效。

### 检查Adobe Analytics的报告{#checking-reports-on-adobe-analytics}

1. 使用提供给AEM的相同凭据登录Adobe Analytics网站。
1. 确保所选的RSID是前面步骤中使用的RSID。
1. 在&#x200B;**报告**（在页面左侧）中，选择&#x200B;**自定义转换**，然后选择&#x200B;**自定义转换1-10**&#x200B;并选择与`eVar7`对应的变量

1. 根据您使用的Adobe Analytics版本，您平均需要等待45分钟，才能使用所使用的搜索词更新报告；例如茄子

## 将内容查找器(cf#)与Adobe Analytics框架{#using-the-content-finder-cf-with-adobe-analytics-frameworks}结合使用

最初，打开Adobe Analytics框架时，内容查找器包含预定义的Analytics变量：

* 流量
* 转换
* 事件

选择RSID后，属于该RSID的所有变量都将添加到列表。\
需要`cf#`才能将Analytics变量映射到不同跟踪组件上存在的CQ变量。 请参阅设置用于基本跟踪的框架。

根据为框架选择的视图，内容查找器将由Analytics变量(在AEM视图中)或CQ变量(在Analytics视图中)填充。

列表可以通过以下方式进行操作：

1. 在&#x200B;**AEM视图**&#x200B;中时，可以根据使用3个筛选器按钮选择的变量类型来筛选列表:

   * 如果&#x200B;*未选择按钮*，则列表将显示完整列表。
   * 如果选择&#x200B;**Traffic**&#x200B;按钮，列表将仅显示属于“流量”部分的变量。
   * 如果选择&#x200B;**Conversion**&#x200B;按钮，列表将仅显示属于“转换”部分的变量。
   * 如果选择&#x200B;**事件**&#x200B;按钮，列表将仅显示属于事件部分的变量。

   >[!NOTE]
   >
   >一次只能有一个过滤器按钮处于活动状态。

   >[!NOTE]
   >
   >Search&amp;Promote变量也属于“转换”部分。

   1. 列表还具有搜索功能，该功能根据在搜索字段中输入的文本过滤器元素。
   1. 如果在搜索列表中的元素时激活了筛选选项，则显示的结果也会根据活动按钮进行筛选。
   1. 可随时使用漩涡箭头按钮重新加载列表。
   1. 如果在框架上选择了多个RSID，则列表中的所有变量将使用所选RSID内使用的所有标签显示。


1. 当处于Adobe Analytics视图时，内容查找器显示属于在CQ视图中拖动的跟踪组件的所有CQ变量。

   * 例如，如果&#x200B;**下载组件**&#x200B;是CQ视图中仅拖动的&#x200B;*一个*(它有两个映射变量&#x200B;*eventdata.downloadLink*&#x200B;和&#x200B;*eventdata.事件.startDownload*)，则内容查找器的外观将如此切换到Adobe Analytics视图时：

   ![aa-22](assets/aa-22.png)

   * 这些变量可以拖放到属于三个变量部分(**流量**、**转换**&#x200B;和&#x200B;**事件**)之一的任何Adobe Analytics变量上。

   * 在CQ视图中将新的跟踪组件拖到框架上时，属于该组件的CQ变量将自动添加到Adobe Analytics视图的内容查找器(cf#)中。
   >[!NOTE]
   >
   >一次只能将一个CQ变量映射到一个Adobe Analytics变量

## 使用AEM视图和分析视图{#using-aem-view-and-analytics-view}

在任何给定时间，用户都可以选择在框架页面上查看Adobe Analytics映射的两种方式之间切换。 2个视图从2个不同的角度提供了框架内映射的更好概述。

### AEM视图{#aem-view}

![aa-23](assets/aa-23.png)

以上图像为例，**AEM视图**&#x200B;具有以下属性：

1. 这是框架打开时的默认视图。
1. 左侧：内容查找器(cf#)由基于所选RSID的Adobe Analytics变量填充。
1. 选项卡标题(**AEM视图**&#x200B;和&#x200B;**分析视图**):使用这些在两个视图之间切换。

1. **AEM视图**:

   1. 如果框架具有从其父级继承的组件，则这些组件以及映射到这些组件的变量将在此列出。

      1. 继承的组件已锁定。
      1. 要解锁继承的组件，只需多次单击组件名称旁的挂锁
      1. 要还原继承，您必须删除已解锁的组件；之后，它将重新获得锁定状态。
   1. **将组件拖动到此处以将其包含在分析框架中**:可以从Sidekick中拖动组件并将其放在此处。
   1. 您可以找到分析框架中当前包含的所有组件：

      1. 要添加组件，请从Sidekick的“组件”选项卡中拖动一个组件
      1. 要删除组件及其所有映射，请从组件的上下文菜单中选择删除，然后在确认对话框上接受删除。
      1. 请记住，组件只能从创建时所用的框架中删除，而不能从子框架中传统地删除（只能覆盖它们）。


### 分析视图{#analytics-view}

![aa-24](assets/aa-24.png)

1. 可通过切换到框架上的&#x200B;**分析视图**&#x200B;选项卡来访问此视图。
1. 左侧：内容查找器(cf#)根据在CQ视图中拖动到框架上的组件由CQ变量填充。
1. 选项卡标题(**AEM视图**&#x200B;和&#x200B;**分析视图**):使用这些在两个视图之间切换。

1. 三个表(流量、转换、事件)列表所有可用的Adobe Analytics变量。 属于所选RSID。 此处显示的映射应与AEM视图中的映射相同：

   * **流量**:

      * 映射到CQ变量的流量变量(`prop1`)(`eventdata.downloadLink`)

      * 当组件旁边有一个挂锁，这意味着它是从父框架继承的，因此无法编辑
   * **转换**:

      * 映射到CQ变量(`pagedata.title`)的转换变量(`eVar1`)

      * 通过多次单击CQ变量字段并手动输入代码，映射到内嵌的javascript表达式的转换变量(`eVar3`)
   * **事件**:

      * 事件变量(`event1`)映射到CQ事件(`eventdata.events.pageView`)



>[!NOTE]
>
>任何表的CQ变量列也可以内嵌填写，方法是多次单击该字段并向其添加文本。 这些字段接受javascript作为输入。
>
>* 例如，在`prop3`旁边，您可以
>* `'`* `Adobe:'+pagedata.title+':'+pagedata.sitesection`\
   >  使用&#x200B;*:*（冒号）发送与其&#x200B;*sitesection*&#x200B;连接的页面的&#x200B;*标题*，前缀为&#x200B;*Adobe*`prop3`

>



>[!CAUTION]
>
>在任何给定时间，只能将一个CQ变量映射到Adobe Analytics变量。

