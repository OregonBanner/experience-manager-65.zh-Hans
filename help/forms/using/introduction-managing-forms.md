---
title: 管理表单简介
seo-title: Introduction to managing forms
description: AEM Forms提供了用于管理自适应Forms和相关资源的工具。 本文介绍了关键表单管理功能和用户界面元素。
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

AEM [!DNL Forms] 提供了简化但功能强大的用户界面，用于创建和管理表单、文档、主题、信件、文档片段、数据字典和相关资产。 它有助于管理表单、文档和相关资产的完整生命周期 — 从开发人员的桌面到在门户服务器上为最终用户提供。 您可以使用AEM [!DNL Forms] 用户界面：

* 访问AEM [!DNL Forms] 组件
* 访问AEM [!DNL Forms] 配置

>[!NOTE]
>
>有关其他AEM工具和选项的详细信息，请参阅 [创作](/help/sites-authoring/author.md).

## 访问AEM Forms组件 {#access-aem-forms-components}

除了创建表单、文档和相关资产选项之外，AEM还提供了创建站点、资产、管理AEM实例等选项。 您可以单击 ![adobeexperiencemanager](assets/adobeexperiencemanager.png) Experience Manager徽标，可导航到所有可用的工具。 除了指向其他组件控制台的链接之外，它还包含AEM的链接 [!DNL Forms]. 导航到AEM [!DNL Forms]，单击Experience Manager徽标 ![adobeexperiencemanager](assets/adobeexperiencemanager.png) >导航 ![指南针](assets/compass.png) > **[!UICONTROL Forms]**. 将显示以下控制台的链接：

* 表单和文档
* 主题
* 书信
* 文档片段
* 数据字典

   ![AEM Forms控制台](assets/aem_forms_console_new.png)

### 表单和文档  {#forms-documents}

Forms &amp; Documents提供了创建交互式通信、自适应表单、自适应表单片段和表单集的选项。 仅适用于AEM [!DNL Forms] 在JEE上，Forms &amp; Documents提供了一个选项，用于从本地存储导入文件并同步AEM [!DNL Forms] 使用Workbench处理资产。

“创建”按钮是创建或上传AEM过程的起点 [!DNL Forms] 资产。 它为您提供了创建以下内容的选项：

* **交互式通信**：交互式通信是一种基于HTML的个性化、交互式且设备友好的数字通信、声明或文档。 交互式通信本质上是响应式的，可根据用户设备和设置自动更改布局和设计。 有关详细信息，请参阅 [交互式通信概述](/help/forms/using/interactive-communications-overview.md)

* **自适应表单：** 自适应表单是一种吸引人且响应式表单。 您可以创作自适应表单，以根据用户响应、设备或工作环境添加或删除表单部分，从而动态适应用户输入。 此 [自适应表单创作简介](../../forms/using/introduction-forms-authoring.md) 文章提供了有关自适应表单的详细信息。

* **自适应表单片段：** 虽然每个表单都是为特定目的而设计的，但大多数表单中都存在一些通用区段，例如提供个人详细信息，如姓名和地址、家庭详细信息、收入详细信息等。 您可以为此类部分创建单个资源。 这些可重用的独立区段称为自适应表单片段。 有关详细信息，请参阅 [自适应表单片段](../../forms/using/adaptive-form-fragments.md) 文章。

* **表单集：** 表单集是分组在一起的HTML5表单的集合，作为单个表单集提供给最终用户。 当最终用户开始填写表单集时，表单会无缝地从一个表单转换为另一个表单。 最后，用户只需单击一下即可作为单个实体提交所有表单。 有关详细信息，请参阅 [AEM Forms中的表单集](../../forms/using/formset-in-aem-forms.md).

* **文件夹：** AEM [!DNL Forms] 用户界面使用文件夹排列资产。 它支持两种类型的文件夹：

   * **常规文件夹：** 这些文件夹用于在AEM中创建的资源 [!DNL Forms] 用户界面。 这些文件夹没有严格的文件夹结构。 您可以重命名、创建子文件夹，并将自适应表单、交互式通信、自适应表单片段、表单模板(XDP)、PDF forms、文档和相关资源存储在这些文件夹中。
   * **Forms Workflow文件夹：** Forms工作流文件夹是在Workbench流程(LiveCycle存档)迁移并与AEM同步时创建的 [!DNL Forms] 用户界面。 不允许重命名、创建子文件夹、创建交互式通信、自适应表单片段或交互式通信。 还不允许删除版本文件夹，也不允许创建和上传与版本文件夹平行的自适应表单、自适应表单片段或交互式通信。

   ![文件夹](assets/folders.png)

   **答：** 常规文件夹 **B.** Forms Workflow文件夹

Forms和“文档”面板还提供以下选项：

* **从本地存储导入文件：** 您可以导入PDF forms和文档、表单模板（XFA表单）和其他资源（XSD的图像和XML架构）。 有关分步说明，请参阅 [将资源导入和导出到AEM Forms](../../forms/using/import-export-forms-templates.md).
* **将AEM Forms资源与Workbench同步：** 您可以使用“来自Workbench的文件”选项在AEM Forms用户界面和Workbench之间同步资产。 它确保所有资源在AEM中均可用 [!DNL Forms] 用户界面和Workbench的crx存储库资产选择。

### 主题  {#themes}

主题包含组件和面板的样式详细信息。 主题具有独立的标识。 因此，您可以在多个自适应表单上重用主题。 您可以为组件指定样式，或修改表单中使用的各种组件的CSS属性。 样式包括诸如背景颜色、状态颜色、透明度和大小等属性。 可将自定义项保存在主题中，并将其作为预设移植到表单的组件上。 将主题添加到表单时，指定的样式会反映在表单的相应组件上。 使用AEM 6.2 [!DNL Forms]，您可以创建主题并将其应用到表单。

有关创建和使用主题的信息，请参阅 [AEM Forms中的主题](../../forms/using/themes.md).

### 书信  {#letters}

AEM [!DNL Forms] 信件是一种安全、个性化的交互式通信。 您可以使用AEM [!DNL Forms] 以通过简化的流程从预批准和自定义内容中快速汇编信件（也称为信件）。

有关创建和使用字母的信息，请参阅 [创建书信](../../forms/using/create-letter.md).

### 文档片段 {#document-fragments}

文档片段是可重用的通信部分或组件，可用于撰写信件。 文档片段的类型为文本、列表、条件和布局片段。 有关创建和使用文档片段的信息，请参阅 [创建文档片段](/help/forms/using/document-fragments.md).

### 数据字典 {#data-dictionaries}

通常，商业用户不需要了解元数据表示法，例如XSD（XML架构）和Java类。 但是，它们通常需要访问这些数据结构和属性才能构建解决方案。 AEM [!DNL Forms] 使用数据字典，使商业用户能够使用来自后端数据源的信息，而无需了解其基础数据模型的技术详细信息。

有关创建和使用数据字典的信息，请参阅创建 [数据字典文章](../../forms/using/data-dictionary.md)

## 访问AEM [!DNL Forms] 配置 {#accessing-aem-forms-configurations}

“AEM工具”面板包含用于各种组件的工具。 要导航到特定于AEM Forms的工具，请单击Experience Manager徽标 ![adobeexperiencemanager](assets/adobeexperiencemanager.png) >工具 ![锤子](assets/hammer.png) > **[!UICONTROL Forms]**. 将显示用于执行以下功能的工具：

* **配置Watched文件夹：** 管理员可以配置网络文件夹（称为watched文件夹），以便当用户将文件(如PDF文件)放入watched文件夹时，将启动预配置的操作并操作该文件。 有关详细信息，请参阅 [创建和配置watched文件夹](/help/forms/using/creating-configure-watched-folder.md).
* **配置Forms App离线服务：** AEM [!DNL Forms] app offline service可缓存表单中使用的资源的路径或URL。 缓存表单中使用的资源的路径或URL可提高服务器端性能。 要配置AEM Forms应用程序的服务器端离线组件，请参阅 [在脱机模式下工作](/help/forms/using/work-offline-mode.md).

   ![AEM Forms工具](assets/aem_forms_tools_new.png)

* **配置PDF生成器：** 管理员可以配置AEM [!DNL Forms] PDF生成器设置、添加用户帐户以及将配置导入或导出到PDF生成器。
* **发布相应的管理资产：** AEM [!DNL Forms] 允许您一次从创作实例发布所有字母、文档片段和数据字典及相关依赖项。 已发布的资产包括所有相应的管理资产和相关依赖项。 有关详细信息，请参阅 [发布和取消发布表单和文档](../../forms/using/publishing-unpublishing-forms.md#publishallthecorrespondencemanagementassets).
* **导出相应的管理资产：** 您可以从AEM中作为包下载所有Correspondence Management资源和相关依赖项 [!DNL Forms] 实例。 有关详细步骤，请参阅 [将资源导入和导出到AEM Forms](../../forms/using/import-export-forms-templates.md#importandexportassetsincorrespondencemanagement)

## 用户界面的常见元素 {#commonelements}

* **左边栏：** 您可以单击左边栏图标 ![railleftpng](assets/railleftpng.png) 显示AEM的时间轴和引用功能 [!DNL Forms].

   * **时间轴：** 您可以在时间线中添加和查看可用于审阅的资产评论。 有关详细说明，请参阅 [在表单中创建和管理资产审核](../../forms/using/create-reviews-forms.md).
   * **引用：** AEM [!DNL Forms] 资源可以在多个AEM中使用 [!DNL Forms] 资产。 例如，一个文档片段可以在多个字母中使用。 引用是所选资产使用的资产（其他表单或资源）列表，也是所选资产正在使用的其他资产列表。

* **痕迹导航：** 痕迹导航表示当前控制台或文件夹的标题。 您可以单击痕迹导航选项，以在层次结构中较高的文件夹级别之间导航。
* **视图切换器：** 您可以单击视图切换器图标 ![视图列表](assets/viewlist.png) 或 ![viewcard](assets/viewcard.png) 在列表视图和卡片视图之间快速切换。 有关常见用户界面组件的详细信息，请参见 [创作](/help/sites-authoring/author.md).
* **搜索：** 搜索选项 ![搜索](assets/search.png) 提供快速查找和跳转到您需要的内容和工具的功能。 键入内容或产品功能的名称，然后从建议中进行选择，例如，键入“文档”可快速查找和导航到 **[!UICONTROL Forms和文档]** 或文档片段控制台。 有关搜索的详细信息，请参阅AEM 6.2 [搜索](/help/sites-authoring/search.md) 文章

* **“操作”工具栏**：选择资源时，操作工具栏显示在资源列表上方。 它包含选定资源的所有管理工具。 您可以将鼠标悬停在工具图标上以查看描述其功能的工具提示

>[!NOTE]
>
>当用户执行Forms和文档的任意控制台搜索时，边栏仅包含 **筛选器和选项**. 您可以使用“筛选器和选项”来执行高级搜索。

* **“操作”工具栏**：选择资源时，操作工具栏显示在资源列表上方。 它包含选定资源的所有管理工具。 您可以将鼠标悬停在工具图标上以查看描述其功能的工具提示

   ![自适应表单的操作工具栏](assets/action_toolbar_new.png)

   自适应表单的操作工具栏
