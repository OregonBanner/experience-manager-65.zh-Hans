---
title: 创建和添加模板和组件
seo-title: 创建和添加模板和组件
description: 可查看本页以了解有关创建模板和组件并将其添加到应用程序的信息。 该页面使用Geometrixx Unlimited应用程序作为包含示例应用程序模板和页面模板的应用程序。
seo-description: 可查看本页以了解有关创建模板和组件并将其添加到应用程序的信息。 该页面使用Geometrixx Unlimited应用程序作为包含示例应用程序模板和页面模板的应用程序。
uuid: 3a93017c-8094-413f-a01c-9b72025a2b20
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
discoiquuid: ec4ada04-e429-4ad4-a060-2dccac847cf0
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1198'
ht-degree: 0%

---


# 创建和添加模板和组件{#creating-and-adding-templates-and-components}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如，React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md).

AEM Mobile点播提供完全配置的应用程序模板、文章模板和文章组件。

We.Unlimited App是一个范例模板，它代表一个完全可配置和可管理的AEM Mobile点播应用程序的外壳。

创建新应用程序时选择此示例模板可提供AEM Mobile功能的丰富仪表板。

![chlimage_1-70](assets/chlimage_1-70.png)

>[!NOTE]
>
>要从AEM Mobile应用控制中心管理您的应用程序和移动应用程序内容，请参阅[AEM Mobile应用程序仪表板](/help/mobile/mobile-apps-ondemand-application-dashboard.md)。

## 创建应用程序模板{#creating-app-templates}

应用程序模板用于创建新应用程序并充当页面模板和组件的集合，这些模板和组件代表应用程序的基线或基础。 模板会标记一些基本属性，以便以适当的方式引导应用程序。 一般而言，客户总体不会创建太多应用程序。

应用程序模板提供了一种轻松的方法，可利用开发人员创建的现有设计，用于在AEM内创建新应用程序。

根据其他应用程序的模板创建新应用程序时，您将获得一个应用程序，其起点代表从中创建该应用程序的应用程序。

根据应用程序模板创建新应用程序的步骤：

1. 导航到AEM Mobile应用程序目录：*&lt;server url>/aem/apps.html/content/mobileapps*
1. 选择&#x200B;**创建** —> **应用**，如下所示

使用此模板创建应用程序后，即可向应用程序添加文章、横幅和集合。 要重新访问、创建文章、横幅和集合，请参阅[内容管理操作](/help/mobile/mobile-apps-ondemand-manage-content-ondemand.md)。

>[!NOTE]
>
>或者，您也可以选择AEM开发人员为您提供的示例应用程序模板，例如&#x200B;**We.Unlimited**&#x200B;应用程序。 如果您将此示例模板用于您的应用程序，您将获得一些示例文章和集合以供处理。 您可以选择使用示例模板和组件、自定义现有模板和组件，或为应用程序创建新模板和组件。

>[!CAUTION]
>
>设置&#x200B;***redirectTarget***&#x200B;属性
>
>使用其中一个应用程序模板时，开发人员定义应用程序的内容。 但是，开发人员必须知道在jcr中创建应用程序的位置以及&#x200B;***redirectTarget***&#x200B;属性的值。
>
>***redirectTarget***&#x200B;是作为创建应用程序操作的一部分计算的，并尝试解析路径（如果有redirectTarget属性作为应用程序模板的一部分可用），且redirectTarget的值定义为相对值。 当创建应用程序进程在应用程序模板中找到redirectTarget的相对值时，该值将附加到创建应用程序的已解析位置。
>
>例如，如果应用程序模板定义值为“*lanugage-masters/en*”的&#x200B;***redirectTarget***，并且该应用程序是在“*/content/mobileapps/fooApp*”中创建的，则创建应用程序后redirectTarget的最终值为“*”/content/mobileapps/fooApp/language-masters/en*&quot;。


## 创建内容模板{#creating-content-templates}

每个实体类型都有两个现成的模板。 这四个关键原则分别是：

* **默认模板：** 用于创建具有适用默认属性／结构的内容
* **导入的模板：** 用于从具有适用默认属性／结构的AEM Mobile导入内容

### 文章模板{#article-templates}

“无限制文章”是表示典型AEM Mobile点播文章布局的示例模板。

1. 单击&#x200B;**管理文章**&#x200B;中的&#x200B;**+**&#x200B;以创建新文章。 您可以选择&#x200B;**无限制文章**&#x200B;或&#x200B;**富文本文章**。 下图显示了一个选项，通过该选项，您可以从以下两个文章模板中的任何一个中进行选择。

1. 单击&#x200B;**Next**&#x200B;可定义文章元数据，如文章名称／标题、描述、作者、摘要、部门、缩略图、文章访问等。
1. 单击&#x200B;**下一步**&#x200B;以填写广告属性。
1. 单击&#x200B;**下一步**&#x200B;以输入文章图像或社交媒体图像
1. 单击&#x200B;**下一步**&#x200B;以选择此新文章所指向的集合链接。
1. 单击&#x200B;**下一步**&#x200B;以输入社交共享的详细信息。
1. 单击&#x200B;**创建**&#x200B;以完成使用示例创建文章的过程。 单击&#x200B;**完成**&#x200B;或&#x200B;**编辑文章**&#x200B;以编辑本文的属性。

![chlimage_1-71](assets/chlimage_1-71.png)

### 将组件添加到文章{#adding-components-to-article}

创建后，作者可以通过添加文本和图像等组件来编辑文章的内容。 文章是AEM页面模板的扩展。

选择一篇文章，要编辑，然后单击&#x200B;**编辑**&#x200B;以向文章添加组件。

![chlimage_1-72](assets/chlimage_1-72.png) ![chlimage_1-73](assets/chlimage_1-73.png)

选择左面板上的“**+**”，向文章添加组件。

![chlimage_1-74](assets/chlimage_1-74.png)

### 创建现成模板{#creating-out-of-the-box-templates}

没有现成的文章模板，但是自定义模板应该扩展的默认模板，请参阅Geometrixx Unlimited应用程序的[文章模板示例](http://localhost:4502/crx/de/index.jsp#/apps/geometrixx-unlimited-app/templates/article)。

超出常规AEM模板的关键属性需要包括；

***dps-resourceType=&quot;dps:Article&quot;***

此属性可确保将AEM页面识别为AEM Mobile目标文章页面。

与AEM模板一样，您可以向模板的&#x200B;***jcr:content***&#x200B;添加任何默认属性或子节点。

### 横幅和集合模板{#banner-and-collection-templates}

>[!CAUTION]
>
>横幅和集合没有内容，因此其创建不支持自定义模板。

## 创建和添加组件{#creating-and-adding-components}

组件使用和允许访问构件，这些构件用于呈现内容。

代码存储库中包含一个简单组件，其源位于AEM中。 随后，也可以在本地以CRXDE Lite打开它。

>[!NOTE]
>
>目前没有为AEM Mobile提供现成的组件。


您可以向页面添加组件。 任何组件都可用于AEM Mobile应用程序，但应用后可能无法正常呈现。

但是，如果没有在AEM中渲染的自定义导出内容同步处理程序，自定义组件可能无法正确导出并上传到AEM Mobile On-demand Services。

在AEM页面中包含该组件以及其他几个构建块组件后，您可以向页面添加其他组件或编辑现有组件。

**要向页面添加其他组件，请执行以下操作：**

1. 选择该页面，并确保您处于编辑模式（通过编辑器标题右上方的下拉菜单）
1. 使用编辑器标题中最左侧的图标切换侧面板
1. 选择&#x200B;**组件**&#x200B;选项卡
1. 将其中一个可用组件拖放到页面上

![chlimage_1-75](assets/chlimage_1-75.png)

**要编辑现有组件，请执行以下操作：**

1. 选择该页面，确保处于&#x200B;**编辑**&#x200B;模式并选择组件
1. 点按扳手图标以配置组件

>[!NOTE]
>
>可以在AEM中创建一个组件，并使用[使用CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md)进行开发自定义相同组件。 根据需要自定义现有组件后，您可以使用上图所示的“管理文章”下的&#x200B;**编辑**&#x200B;选项将其添加到页面中。****

>[!NOTE]
>
>请参阅AEM Mobile的[模板和组件开发的最佳实践](/help/mobile/best-practices-aem-mobile.md)。

### 后续步骤 {#the-next-steps}

* [使用内容属性导出内容](/help/mobile/on-demand-content-properties-exporting.md)
* [内容同步的移动设备](/help/mobile/mobile-ondemand-contentsync.md)