---
title: 表单管理简介
seo-title: 表单管理简介
description: AEM Forms提供了用于管理自适应表单和相关资产的工具。 本文向您介绍关键的表单管理功能和用户界面元素。
seo-description: AEM Forms提供了用于管理自适应表单和相关资产的工具。 本文向您介绍关键的表单管理功能和用户界面元素。
uuid: 2275a0b6-b31e-4d8e-8154-ccdfff3705aa
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: introduction
discoiquuid: c0e4c9bb-e12a-4f9a-a8fa-1a8ad41d3995
docset: aem65
translation-type: tm+mt
source-git-commit: 8e724af4d69cb859537dd088119aaca652ea3931

---


# 表单管理简介{#introduction-to-managing-forms}

AEM Forms提供简化而功能强大的用户界面，用于创建和管理表单、文档、主题、字母、文档片段、数据字典和相关资产。 它有助于管理表单、文档和相关资产的整个生命周期——从开发人员的桌面到在门户服务器上为最终用户提供。 您可以使用AEM Forms用户界面执行以下操作：

* 访问AEM Forms组件
* 访问AEM Forms配置

>[!NOTE]
>
>有关其他AEM工具和选项的详细信息，请参阅 [创作](/help/sites-authoring/author.md)。

## 访问AEM Forms组件 {#access-aem-forms-components}

除了创建表单、文档和相关资产的选项外，AEM还提供了创建站点、资产、管理AEM实例等选项。 您可以单击 ![adobeexperiencemanager](assets/adobeexperiencemanager.png) Experience manager徽标，导览至所有可用的工具。 除了指向其他组件控制台的链接外，它还包含AEM Forms的链接。 要导航到AEM Forms，请单击Experience Manager徽标 ![adobeexperiencemanager](assets/adobeexperiencemanager.png) >导航指南 ![>表单](assets/compass.png) 。 此时将显示以下控制台的链接：

* 表单和文档
* 主题
* 书信
* 文档片段
* 数据字典

![AEM Forms控制台](assets/aem_forms_console_new.png)

### 表单和文档  {#forms-documents}

“表单和文档”提供了用于创建交互式通信、自适应表单、自适应表单片段和表单集的选项。 仅对于JEE上的AEM Forms,“表单和文档”提供了一个选项，用于从本地存储导入文件并将AEM Forms资产与Workbench同步。

创建按钮是创建或上传AEM Forms资产的过程的起始点。 它为您提供了创建以下内容的选项：

* **交互通信**:交互式通信是基于HTML的个性化、交互式和设备友好型数字通信、声明或文档。 交互通信本质上是响应式的，并根据用户设备和设置自动更改布局和设计。 有关详细信息，请参阅交 [互通信概述](/help/forms/using/interactive-communications-overview.md)

* **** 自适应表单：自适应表单是一种引人入胜的响应式表单。 您可以根据用户响应、设备或工作环境添加或删除表单部分，创作自适应表单以动态适应用户输入。 自适 [应表单创作介绍文章](../../forms/using/introduction-forms-authoring.md) ，提供了有关自适应表单的详细信息。

* **** 自适应表单片段：虽然每个表单都是为特定用途而设计的，但大多数表单中都有一些常见的细分，例如提供个人详细信息，如姓名和地址、家庭详细信息、收入详细信息等。 您可以为这些部分创建单个资产。 这些可重用的独立细分称为自适应表单片段。 有关详细信息，请参阅自 [适应表单片段文章](../../forms/using/adaptive-form-fragments.md) 。

* **** 表单集：表单集是一组HTML5表单，这些表单分组在一起，并作为一组表单呈现给最终用户。 当最终用户开始填写表单集时，表单将从一个表单无缝地转换为另一个表单。 最后，用户只需单击一下，即可将所有表单作为单个实体提交。 有关详细信息，请参 [阅AEM Forms中的表单集](../../forms/using/formset-in-aem-forms.md)。

* **** 文件夹：AEM Forms用户界面使用文件夹来排列资产。 它支持两种类型的文件夹：

   * **** 常规文件夹：这些文件夹用于在AEM Forms用户界面中创建的资产。 这些文件夹没有严格的文件夹结构。 您可以重命名子文件夹，并存储这些文件夹中的自适应表单、交互通信、自适应表单片段、表单模板(XDP)、PDF表单、文档和相关资源。
   * **** Forms Workflow文件夹：在迁移Workbench进程（LiveCycle存档）并与AEM Forms用户界面同步时，将创建表单工作流文件夹。 不允许重命名、创建子文件夹、创建交互式通信、自适应表单片段或交互式通信。 此外，不允许删除版本文件夹或创建和上传与版本文件夹平行的自适应表单、自适应表单片段或交互式通信。

![文件夹](assets/folders.png)

******答：常规文**&#x200B;件夹B。Forms Workflow文件夹

“表单和文档”面板还提供以下选项：

* **** 从本地存储导入文件：您可以导入PDF表单和文档、表单模板（XFA表单）和其他资源（XSD的图像和XML架构）。 有关分步说明，请参阅将资 [产导入和导出到AEM Forms](../../forms/using/import-export-forms-templates.md)。
* **** 将AEM Forms资产与Workbench同步：您可以使用“从工作台中的文件”选项在AEM Forms用户界面和Workbench之间同步资产。 它可确保在AEM Forms用户界面和Workbench的crx-repository资产选择中提供所有资产。

### 主题  {#themes}

主题包含组件和面板的样式详细信息。 主题具有独立身份。 因此，您可以在多个自适应表单上重复使用一个主题。 您可以指定组件的样式，或修改表单中使用的各种组件的CSS属性。 样式包括背景颜色、状态颜色、透明度和大小等属性。 您可以在主题中保存自定义，并将自定义作为预设移植到表单的组件上。 将主题添加到表单时，指定的样式会反映在表单的相应组件上。 借助AEM 6.2 Forms，您可以创建主题并将其应用于表单。

有关创建和使用主题的信息，请参阅AEM [表单中的主题](../../forms/using/themes.md)。

### 书信  {#letters}

AEM表单信函是一种安全、个性化和交互式通信。 您可以使用AEM Forms以简化的流程快速组合来自预先批准和自定义创作内容的字母（也称为通信）。

有关创建和使用字母的信息，请参阅 [创建字母](../../forms/using/create-letter.md)。

### 文档片段 {#document-fragments}

文档片段是可重用的部分或通信的组件，您可以使用这些组件编写字母。 文档片段的类型为文本、列表、条件和布局片段。 有关创建和使用文档片段的信息，请参阅 [创建文档片段](/help/forms/using/document-fragments.md)。

### 数据字典 {#data-dictionaries}

通常，商业用户不需要有关元数据表示法(如XSD（XML架构）和Java类)的知识。 但是，他们通常需要访问这些数据结构和属性才能构建解决方案。 AEM Forms使用数据字典，使商业用户能够使用后端数据源中的信息，而无需了解有关其基础数据模型的技术详细信息。

有关创建和使用数据字典的信息，请参阅创建数 [据字典文章](../../forms/using/data-dictionary.md)

## 访问AEM Forms配置 {#accessing-aem-forms-configurations}

AEM工具面板包含用于各种组件的工具。 要导航到特定于AEM Forms的工具，请单击Experience manager徽标 ![adobe Experience Manager](assets/adobeexperiencemanager.png) >工具 ![锤子](assets/hammer.png) >表单。 此时将显示用于执行以下功能的工具：

* **** 配置监视文件夹：管理员可以配置网络文件夹（称为监视文件夹），这样，当用户将文件（如PDF文件）放置到监视文件夹时，将启动预配置的操作并处理该文件。 有关详细信息，请参 [阅创建和配置监视的文件夹](/help/forms/using/creating-configure-watched-folder.md)。
* **** 配置表单应用程序脱机服务：AEM Forms应用程序脱机服务会缓存表单中使用的资源的路径或URL。 缓存表单中使用的资源路径或URL可提高服务器端性能。 要配置AEM Forms应用程序的服务器端脱机组件，请参阅 [在脱机模式下工作](/help/forms/using/work-offline-mode.md)。

![AEM Forms工具](assets/aem_forms_tools_new.png)

* **** 配置PDF生成器：管理员可以配置AEM Forms PDF Generator设置、添加用户帐户以及将配置导入或导出到PDF Generator。
* **** 发布对应管理资产：通过AEM Forms，您可以同时发布来自创作实例的所有字母、文档片段和数据字典以及相关依赖关系。 已发布的资产包括所有Correponse Management资产和相关依赖关系。 有关详细信息，请参 [阅发布和取消发布表单和文档](../../forms/using/publishing-unpublishing-forms.md#publishallthecorrespondencemanagementassets)。
* **** 导出通信管理资产：您可以从AEM表单实例将所有Correponsement Management资产和相关依赖关系作为包下载。 有关详细步骤，请参 [阅将资产导入和导出到AEM Forms](../../forms/using/import-export-forms-templates.md#importandexportassetsincorrespondencemanagement)

## 用户界面的常用元素 {#commonelements}

* **** 左边栏：您可以单击左边栏图标 ![左边栏](assets/railleftpng.png) ，以显示AEM Forms的“时间轴”和“引用”功能。

   * **** 时间轴：您可以在时间轴中添加和查看可供审核的资产评论。 有关详细说明，请参 [阅创建和管理表单中资产的审阅](../../forms/using/create-reviews-forms.md)。
   * **** 参考：AEM Forms资产可用于多个AEM Forms资产。 例如，文档片段可以用于多个字母。 引用是选定资产所使用的资产（其他表单或资源）列表，也是选定资产所使用的其他资产列表。

* **** 痕迹导航：痕迹导航表示当前控制台或文件夹的标题。 单击痕迹导航选项可在层次结构中较高的文件夹级别之间导航。
* **** 视图切换器：单击“视图切换器”图标 ![viewlist](assets/viewlist.png) ，或 ![viewcard](assets/viewcard.png) ，可在列表和卡片视图之间快速切换。 有关常用用户界面组件的详细信息，请参阅 [创作](/help/sites-authoring/author.md)。
* **** 搜索：搜索选项 ![搜索](assets/search.png) ，可快速查找并跳转到所需的内容和工具。 键入内容名称或产品功能，然后从建议中进行选择，例如，键入“文档”，快速查找并导航到“表单和文档”或“文档片段”控制台。 有关搜索的详细信息，请参阅AEM 6.2搜索 [文章](/help/sites-authoring/search.md)

* **操作工具栏**:选择资产时，操作工具栏会显示在资产列表的上方。 它包含选定资产的所有管理工具。 可将鼠标悬停在工具图标上以查看描述其功能的工具提示

>[!NOTE]
>
>当用户执行任何“表单和文档”控制台的搜索时，边栏仅包含“过滤 **器和选项”**。 您可以使用“过滤器和选项”来执行高级搜索。

* **操作工具栏**:选择资产时，操作工具栏会显示在资产列表的上方。 它包含选定资产的所有管理工具。 可将鼠标悬停在工具图标上以查看描述其功能的工具提示

![自适应表单的操作工具栏](assets/action_toolbar_new.png)

自适应表单的操作工具栏

