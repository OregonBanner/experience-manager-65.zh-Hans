---
title: 管理表单简介
seo-title: Introduction to managing forms
description: AEM Forms提供了用于管理自适应Forms和相关资产的工具。 本文介绍了关键表单管理功能和用户界面元素。
seo-description: AEM Forms provides tools to manage Adaptive Forms and related assets. This article introduces you to the key forms management capabilities and user interface elements.
uuid: 2275a0b6-b31e-4d8e-8154-ccdfff3705aa
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager, introduction
discoiquuid: c0e4c9bb-e12a-4f9a-a8fa-1a8ad41d3995
docset: aem65
exl-id: 3e063456-7f96-483d-86a3-6a414746db8a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1564'
ht-degree: 1%

---

# 管理表单简介 {#introduction-to-managing-forms}

AEM [!DNL Forms] 提供了简化但功能强大的用户界面，用于创建和管理表单、文档、主题、信件、文档片段、数据字典和相关资产。 它有助于管理表单、文档和相关资产的完整生命周期 — 从开发人员的桌面到面向最终用户的门户服务器。 您可以使用AEM [!DNL Forms] 用户界面：

* 访问AEM [!DNL Forms] 组件
* 访问AEM [!DNL Forms] 配置

>[!NOTE]
>
>有关其他AEM工具和选项的详细信息，请参阅 [创作](/help/sites-authoring/author.md).

## 访问AEM Forms组件 {#access-aem-forms-components}

除了用于创建表单、文档和相关资产的选项之外，AEM还提供了用于创建站点、资产、管理AEM实例等选项。 您可以单击 ![adobeexperiencemanager](assets/adobeexperiencemanager.png) Experience Manager徽标，以导航到所有可用的工具。 除了指向其他组件控制台的链接之外，它还包含AEM的链接 [!DNL Forms]. 导航到AEM [!DNL Forms]，单击Experience Manager徽标 ![adobeexperiencemanager](assets/adobeexperiencemanager.png) >导航 ![指南](assets/compass.png) > **[!UICONTROL Forms]**. 将显示以下控制台的链接：

* 表单和文档
* 主题
* 书信
* 文档片段
* 数据字典

   ![AEM Forms控制台](assets/aem_forms_console_new.png)

### 表单和文档  {#forms-documents}

Forms &amp; Documents提供了用于创建交互式通信、自适应表单、自适应表单片段和表单集的选项。 仅限AEM [!DNL Forms] 在JEE上，“Forms &amp; Documents”提供了一个选项，用于从本地存储导入文件并同步AEM [!DNL Forms] 资产。

创建按钮是创建或上传AEM的过程起点 [!DNL Forms] 资产。 它为您提供了创建以下内容的选项：

* **交互式通信**:交互式通信是一种基于HTML的个性化、交互式且设备友好型数字通信、声明或文档。 交互式通信具有响应性，并可根据用户设备和设置自动更改布局和设计。 有关详细信息，请参阅 [交互式通信概述](/help/forms/using/interactive-communications-overview.md)

* **自适应表单：** 自适应表单是一种引人入胜且响应迅速的表单。 您可以创作自适应表单，以根据用户响应、设备或工作环境添加或删除表单部分，从而动态适应用户输入。 的 [创作自适应表单简介](../../forms/using/introduction-forms-authoring.md) 文章提供了有关自适应表单的详细信息。

* **自适应表单片段：** 虽然每个表单都是专门为特定目的而设计的，但大多数表单中都有一些常见的区段，例如，提供个人详细信息，如姓名和地址、家庭详细信息、收入详细信息等。 您可以为此类部分创建单个资产。 这些可重用的独立区段称为自适应表单片段。 有关详细信息，请参阅 [自适应表单片段](../../forms/using/adaptive-form-fragments.md) 文章。

* **表单集：** 表单集是HTML5个表单的集合，这些表单分组在一起，并以单个表单集的形式呈现给最终用户。 当最终用户开始填写表单集时，表单会从一个表单无缝地转换到另一个表单。 最终，用户只需单击一次，即可将所有表单作为单个实体提交。 有关详细信息，请参阅 [在AEM Forms中设置表单](../../forms/using/formset-in-aem-forms.md).

* **文件夹：** AEM [!DNL Forms] 用户界面使用文件夹来排列资产。 它支持两种类型的文件夹：

   * **常规文件夹：** 这些文件夹用于在AEM中创建的资产 [!DNL Forms] 用户界面。 这些文件夹没有严格的文件夹结构。 您可以在这些文件夹中重命名、创建子文件夹，并存储自适应表单、交互式通信、自适应表单片段、表单模板(XDP)、PDF forms、文档和相关资产。
   * **Forms Workflow文件夹：** Forms工作流文件夹是在迁移Workbench进程(LiveCycle存档)并与AEM同步时创建的 [!DNL Forms] 用户界面。 不允许重命名、创建子文件夹、创建交互式通信、自适应表单片段或交互式通信。 此外，还不允许删除版本文件夹或创建和上传与版本文件夹平行的自适应表单、自适应表单片段或交互式通信。

   ![文件夹](assets/folders.png)

   **A.** 常规文件夹 **B.** Forms Workflow文件夹

“Forms和文档”面板还提供了以下选项：

* **从本地存储导入文件：** 您可以导入PDF forms和文档、表单模板（XFA表单）以及其他资源（XSD的图像和XML架构）。 有关分步说明，请参阅 [将资产导入和导出到AEM Forms](../../forms/using/import-export-forms-templates.md).
* **将AEM Forms资产与Workbench同步：** 您可以使用“从Workbench中的文件”选项在AEM Forms用户界面和Workbench之间同步资产。 它可确保所有资产均在AEM中可用 [!DNL Forms] 用户界面和Workbench的crx-repository资产选择。

### 主题  {#themes}

主题包含组件和面板的样式详细信息。 主题具有独立的身份。 因此，您可以在多个自适应表单上重复使用一个主题。 您可以指定组件的样式，或修改表单中所用各种组件的CSS属性。 样式包括背景颜色、状态颜色、透明度和大小等属性。 您可以在主题中保存自定义项，并将它们作为预设插入到表单的组件中。 将主题添加到表单时，指定的样式将反映在表单的相应组件上。 使用AEM 6.2 [!DNL Forms]，则可以创建主题并将其应用于表单。

有关创建和使用主题的信息，请参阅 [AEM Forms主题](../../forms/using/themes.md).

### 书信  {#letters}

AEM [!DNL Forms] 信件是安全、个性化和交互式的通信。 您可以使用AEM [!DNL Forms] 以简化流程，从预批准和自定义创作的内容快速组合信件（也称为通信）。

有关创建和使用字母的信息，请参阅 [创建信件](../../forms/using/create-letter.md).

### 文档片段 {#document-fragments}

文档片段是可重复使用的部件或通信组件，您可以使用这些部件来撰写信件。 文档片段的类型为文本、列表、条件和布局片段。 有关创建和使用文档片段的信息，请参阅 [创建文档片段](/help/forms/using/document-fragments.md).

### 数据字典 {#data-dictionaries}

通常，业务用户不需要了解元数据表示法，如XSD（XML架构）和Java类。 但是，它们通常需要访问这些数据结构和属性才能构建解决方案。 AEM [!DNL Forms] 使用数据字典，使企业用户能够使用来自后端数据源的信息，而无需了解其基础数据模型的技术详细信息。

有关创建和使用数据字典的信息，请参阅创建 [数据字典文章](../../forms/using/data-dictionary.md)

## 访问AEM [!DNL Forms] 配置 {#accessing-aem-forms-configurations}

AEM“工具”面板包含用于各种组件的工具。 要导航到特定于AEM Forms的工具，请单击Experience Manager徽标 ![adobeexperiencemanager](assets/adobeexperiencemanager.png) >工具 ![锤子](assets/hammer.png) > **[!UICONTROL Forms]**. 将显示用于执行以下功能的工具：

* **配置监视文件夹：** 管理员可以配置网络文件夹（称为监视文件夹），以便当用户将文件(如PDF文件)放置在监视文件夹中时，将启动预配置操作并处理该文件。 有关详细信息，请参阅 [创建和配置监视文件夹](/help/forms/using/creating-configure-watched-folder.md).
* **配置Forms应用程序离线服务：** AEM [!DNL Forms] 应用程序离线服务会缓存表单中使用的资源的路径或URL。 缓存表单中所用资源的路径或URL可提高服务器端性能。 要配置AEM Forms应用程序的服务器端离线组件，请参阅 [在脱机模式下工作](/help/forms/using/work-offline-mode.md).

   ![AEM Forms工具](assets/aem_forms_tools_new.png)

* **配置PDF生成器：** 管理员可以配置AEM [!DNL Forms] PDF生成器设置、添加用户帐户，以及将配置导入或导出到PDF生成器。
* **发布通信管理资产：** AEM [!DNL Forms] 允许您同时发布创作实例中的所有字母、文档片段、数据字典和相关依赖项。 已发布的资产包括所有通信管理资产和相关依赖关系。 有关详细信息，请参阅 [发布和取消发布表单和文档](../../forms/using/publishing-unpublishing-forms.md#publishallthecorrespondencemanagementassets).
* **导出通信管理资产：** 您可以从AEM中将所有通信管理资产和相关依赖项下载为包 [!DNL Forms] 实例。 有关详细步骤，请参阅 [将资产导入和导出到AEM Forms](../../forms/using/import-export-forms-templates.md#importandexportassetsincorrespondencemanagement)

## 用户界面的常见元素 {#commonelements}

* **左边栏：** 您可以单击左边栏图标 ![raillefpng](assets/railleftpng.png) 显示AEM的时间轴和引用功能 [!DNL Forms].

   * **时间轴：** 您可以在时间轴中添加和查看可供审阅的资产评论。 有关详细说明，请参阅 [创建和管理表单中资产的审阅](../../forms/using/create-reviews-forms.md).
   * **引用：** AEM [!DNL Forms] 资产可用于多个AEM [!DNL Forms] 资产。 例如，文档片段可以用于多个字母。 引用是指所选资产所使用的资产（其他表单或资源）列表，也是选定资产所使用的其他资产列表。

* **痕迹导航：** 痕迹导航表示当前控制台或文件夹的标题。 您可以单击痕迹导航选项，在层次结构中较高的文件夹级别之间导航。
* **查看切换器：** 您可以单击“视图切换器”图标 ![视图列表](assets/viewlist.png) 或 ![视卡](assets/viewcard.png) 快速在列表视图和卡片视图之间切换。 有关常用用户界面组件的更多信息，请参阅 [创作](/help/sites-authoring/author.md).
* **搜索：** 搜索选项 ![搜索](assets/search.png) 提供了快速查找和跳转到所需内容和工具的功能。 键入内容或产品功能的名称并从建议中进行选择，例如，键入“文档”以快速查找并导航到 **[!UICONTROL Forms和文档]** 或“文档片段”控制台。 有关搜索的更多信息，请参阅AEM 6.2 [搜索](/help/sites-authoring/search.md) 文章

* **“操作”工具栏**:选择资产时，“操作”工具栏会显示在资产列表的上方。 它包含选定资产的所有管理工具。 您可以将鼠标悬停在工具图标上，以查看描述其功能的工具提示

>[!NOTE]
>
>当用户执行搜索任意控制台的Forms和文档时，边栏仅包含 **过滤器和选项**. 您可以使用过滤器和选项来执行高级搜索。

* **“操作”工具栏**:选择资产时，“操作”工具栏会显示在资产列表的上方。 它包含选定资产的所有管理工具。 您可以将鼠标悬停在工具图标上，以查看描述其功能的工具提示

   ![自适应表单的操作工具栏](assets/action_toolbar_new.png)

   自适应表单的操作工具栏
