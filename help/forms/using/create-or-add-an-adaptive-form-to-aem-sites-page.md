---
title: 创建自适应表单或将自适应表单添加到 AEM Sites 页面
description: 了解如何轻松创建自适应表单或将自适应表单无缝添加到 AEM Sites 页面。分步学习将动态且可自定义的表单集成到您的网站中并优化您的数字体验以尽量提高影响力的方法和最佳实践。
Keywords: AEM Forms in sites, AF in Sites editor, af in aem sites, aem sites af, add af to a sites page, af aem sites, af sites, create af in a sites page, adaptive form in aem sites, forms aem sites, add form to a sites page, adaptive forms aem sites, add adaptive forms to aem page, create forms in an aem sites page
feature: Adaptive Forms
exl-id: 1813ccfc-87ce-46fa-a1d5-5edffd91efb0
source-git-commit: 3649df0e2a2672bc1742b3c02386f12ff6991935
workflow-type: tm+mt
source-wordcount: '2888'
ht-degree: 24%

---

# 创建自适应表单或将自适应表单添加到 AEM Sites 页面 {#create-or-add-an-adaptive-form-to-aem-sites-page}

<span class="preview">Adobe 建议使用现代、可扩展的数据捕获[核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)，以[创建新的自适应表单](/help/forms/using/create-an-adaptive-form-core-components.md)或[将自适应表单添加到 AEM Sites 页面](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)。这些组件代表有关创建自适应表单的重大改进，确保实现令人印象深刻的用户体验。本文介绍了使用基础组件创作自适应表单的旧方法。</span>

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | 本文 |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/create-or-add-an-adaptive-form-to-aem-sites-page.html) |

借助 AEM Forms，您可以将自适应表单无缝整合到您的网页中。这使得您的访问者无需离开其所在的页面，即可方便地填写和提交表格。这样，他们即可在主动与表单交互的同时轻松地与网站的其他元素保持互动。

您可以使用AEM页面编辑器快速创建多个表单并将其添加到AEM Sites页面。 使用AEM页面编辑器，内容作者可以使用自适应表单组件的强大功能（包括动态行为、验证、数据集成、生成记录文档和业务流程自动化），在Sites页面中创建无缝的数据捕获体验。 它还允许您使用AEM Sites页面的各种功能，例如，版本控制、定位、翻译和多站点管理器。

AEM Forms 会提供自适应表单容器和自适应表单嵌入组件。您可以使用自适应表单容器在体验片段或AEM Sites页面中创建新表单，而自适应Forms — 嵌入组件允许您添加现有自适应表单或使用自适应Forms编辑器创建新表单。

![站点页面中的自适应表单](/help/forms/using/assets/adaptive-form-in-sites-page.png)

## 在AEM页面编辑器或体验片段中使用自适应表单容器组件的好处

通过在AEM页面编辑器中使用自适应表单容器，您可以使用自适应Forms组件的强大功能（包括动态行为、验证、数据集成、生成记录文档和业务流程自动化）在Sites页面中创建无缝的数据捕获体验。 它还允许您使用AEM Sites页面的各种功能，如版本控制、定位、翻译和多站点管理器，从而改善整体表单创建和管理体验。 让我们来探索一下其中的一些功能：

* **版本控制：** AEM Sites pages选件 [强大的版本控制功能](/help/sites-authoring/working-with-page-versions.md)，允许您跟踪和管理表单的不同版本。 这使您能够对表单进行更改和增强，同时保持根据需要回滚到以前版本的能力。 版本控制可确保采用受控且有条理的方法来形成开发和演变。
* **定位(与Adobe Target集成)：** 利用AEM Sites页面定位功能，您还可以 [为不同受众个性化表单体验](/help/sites-administering/target.md). 利用用户区段和定位标准，您可以根据特定用户组定制表单的内容、设计或行为。 这使您能够提供个性化且相关的表单体验，从而提高参与度和转化率。
* **翻译：** AEM Sites [与翻译服务无缝集成](/help/sites-administering/translation.md)，可轻松地将表单翻译成多种语言。 此功能简化了本地化过程，确保全球受众能够访问您的表单。 您可以在AEM翻译项目中高效地管理翻译，从而减少多语言表单支持所需的时间和工作量。 有关翻译的更多信息，请参阅注意事项部分。
* **多站点管理和Live Copy：** AEM Sites提供强大的 [多站点管理和实时复制功能](/help/sites-administering/msm.md)，使您能够在一个环境中创建和管理多个网站。 此功能现在允许您跨不同站点重用表单，确保一致性并减少重复工作。 通过集中化的控制和管理，您可以跨多个网站高效地维护和更新表单。
* **主题：** AEM Sites页面提供了一个框架，用于跨多个网页设计和维护一致的可视样式。 它们定义了颜色、字体、样式表和其他对网站整体外观和体验有所贡献的可视元素。 [您可以将为AEM Sites页面设计的主题用于自适应表单，从而节省时间和精力](/help/sites-authoring/style-system.md).
* **标记：** AEM Sites页面允许您 [为页面、资产或其他内容分配标记或标签](/help/sites-authoring/tags.md). 标记是关键字或元数据标签，它们提供了一种根据特定标准对内容进行分类和整理的方法。 您可以为AEM中的页面、资源或任何其他内容项分配一个或多个标记，以改进搜索并对资源分类。
* **锁定和解锁内容：** AEM Sites允许用户 [控制对页面的访问和修改](/help/sites-authoring/editing-content.md#locking-a-page-locking-a-page) 在AEM Sites环境中。 锁定页面时，即表示页面不会遭到其他用户未经授权的更改或编辑。 只有锁定了内容的用户或指定的管理员才能解锁内容以允许修改。


## 在AEM页面编辑器中添加自适应表单的各种选项

可使用以下选项充分利用此功能：

* **[将自定义自适应表单添加到AEM Sites页面：](#create-an-adaptive-form-in-sites-editor)** 从头开始构建全新的表单，根据您的要求和设计偏好进行定制。

* **[向体验片段添加自定义自适应表单：](#create-an-adaptive-form-in-experience-fragment)** 通过将表单添加到AEM体验片段来扩展表单的覆盖范围，从而允许在多个页面或网站上无缝重用。

* **[将自适应表单转换为体验片段：](#convert-an-adaptive-form-in-sites-page-to-an-experience-fragment)** 将添加到AEM Sites页面的自适应表单转换为体验片段，以便在多个AEM Sites页面中重用该表单。

* **根据批准的模板创建表单并将其添加到AEM Sites页面：** 利用预批准的模板快速创建符合您组织的品牌准则和设计标准的表单。 选项仅适用于使用自适应Forms编辑器或自适应Forms — 嵌入组件创建的自适应Forms 。

* **将现有表单添加到AEM Sites页面：** 轻松将您已创建的表单集成到网站中，使访客能够直接与表单进行交互。 选项仅适用于使用自适应Forms编辑器或自适应Forms — 嵌入组件创建的自适应Forms 。

* **将多个表单添加到AEM Sites页面或体验片段：**  将多个表单添加到页面中，以根据用户的偏好和要求为其提供多个选择。 这些表单可以包括从头开始创建的全新表单和现有的表单。

## 注意事项 {#consideration}

* 当您使用自适应表单容器创建或添加表单时，该表单会通过 AEM Sites 翻译流程进行翻译和本地化。对于每种语言，系统都会生成网站页面和相应表单的单独副本（语言副本），而当内容作者修改父页面上表单中的规则时，必须在该表单的所有语言副本中进行相同的更改。自适应表单容器还允许您使用AEM Sites页面的各种功能，例如，版本控制、定位、翻译和多站点管理器。

* 当您使用自适应表单嵌入组件创建或添加表单时，该表单会使用 AEM Forms 翻译流程进行翻译和本地化。在这种情况下，Sites 页面的所有语言副本中会维护和引用一个表单。无法通过自适应表单嵌入组件使用 AEM Sites 页面的多种功能，例如版本控制、定位、翻译和多站点管理器等。


## 开始之前 {#before-you-start}

+++  为您的环境启用自适应表单核心组件

确保 [为您的环境启用了自适应Forms核心组件](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/quick-setup/enable-headless-adaptive-forms-and-core-components.html?lang=en).

+++

+++  将自适应Forms客户端库添加到AEM Sites页面和体验片段页面组件

要启用自适应表单容器组件的完整功能，请使用部署管道将 Customheaderlibs 和 Customfooterlibs 客户端库添加到 AEM Sites 页面。要添加库：

1. 登录您的AEM创作实例并打开CRX DE。 本地运行的创作实例的默认URL为 `http://localhost:4502/crx/de`.

1. 打开 `/apps/[your-sites-project]/components/page/customheaderlibs.html` 文件并将以下代码添加到该文件中：

   ```
       //Customheaderlibs.html
       <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-call="${clientlib.css @ categories='core.forms.components.runtime.all'}"/>
       </sly> 
   ```

1. 打开 `/apps/[your-sites-project]/components/page/customfooterlibs.html` 文件并将以下代码添加到该文件中：

   ```
       //customfooterlibs.html
       <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-test="${!wcmmode.edit}" data-sly-call="${clientlib.js @ categories='core.forms.components.runtime.all', async=true}"/>
       </sly> 
   ```

1. 打开 `/apps/[your-sites-project]/components/xfpage/customheaderlibs.html` 文件并将以下代码添加到该文件中：

   ```
       //Customheaderlibs.html
       <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-call="${clientlib.css @ categories='core.forms.components.runtime.all'}"/>
       </sly> 
   ```

1. 打开 `/apps/[your-sites-project]/components/customfooterlibs.html` 文件并将以下代码添加到该文件中：

   ```
       //customfooterlibs.html
       <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-test="${!wcmmode.edit}" data-sly-call="${clientlib.js @ categories='core.forms.components.runtime.all', async=true}"/>
       </sly> 
   ```

1. 重复以上步骤，以在您的环境中创建所有创作实例和发布实例。

+++

+++ 启用自适应Forms容器

若要启用模板策略中的[!UICONTROL 自适应表单容器]组件，请执行以下步骤：

1. 打开AEM Sites页面或体验片段进行编辑。 若要打开要编辑的页面，请选择该页面并点击“编辑”。
1. 打开站点或体验片段页面的模板。 要打开模板，请转到[!UICONTROL 页面信息]![页面信息](/help/forms/using/assets/Smock_Properties_18_N.svg) > [!UICONTROL 编辑模板。] 它会在模板编辑器中打开相应的模板。
1. 在结构视图中，单击菜单栏中的&#x200B;**[!UICONTROL 策略]**![策略](/help/forms/using/assets/Smock_FeedManagement_18_N.svg)图标。在&#x200B;**[!UICONTROL 允许的组件]**&#x200B;列出中，选择 **[AEM 原型项目名称] - 自适应表单**&#x200B;下的&#x200B;**[!UICONTROL 自适应表单容器]**&#x200B;复选框。
1. 单击&#x200B;**[!UICONTROL 完成]**。

>[!VIDEO](https://video.tv.adobe.com/v/3419370?quality=12&learn=on)

+++

## 创建自适应表单 {#create-an-adaptive-form-in-sites-editor-or-experience-fragment}

您可以直接从头开始创建全新的表单，直接在AEM Sites页面或体验片段中根据您的要求和设计首选项对其进行自定义。 对于一次性表单，建议直接创作到AEM Sites页面，而体验片段则适用于需要在网站上的多个页面中重用的表单。

* [在 AEM Sites 页面中创建一个表单](#create-an-adaptive-form-in-sites-editor)
* [在体验片段中创建一个表单](#create-an-adaptive-form-in-experience-fragment)
* [将AEM Sites页面中的自适应表单转换为体验片段](#convert-an-adaptive-form-in-sites-page-to-an-experience-fragment)

### 在 AEM Sites 页面中创建一个表单 {#create-an-adaptive-form-in-sites-editor}

您可以使用AEM页面编辑器中的自适应表单容器组件来创建自定义表单。 利用组件，可通过拖放表单组件来创建表单。 表单组件基于核心组件。您可以根据组织的要求轻松地对其进行自定义。

>[!VIDEO](https://video.tv.adobe.com/v/3419284?quality=12&learn=on)

要在 Sites 页面创建自适应表单：

1. 以编辑模式打开 AEM Sites 页面。
1. 将&#x200B;**[!UICONTROL 自适应表单容器]**&#x200B;组件从组件浏览器拖放到 Sites 页面。它会在页面上为表单创建一个空间。您可以使用布局模式来更改容器空间的大小。
1. 将自适应表单核心组件拖放到该容器空间，以创建表单。
1. 添加“提交”按钮。

接下来，您 [设置提交操作](#configure-submit-action-for-form) 和高级属性。

### 在体验片段中创建一个表单 {#create-an-adaptive-form-in-experience-fragment}

您可以通过将表单添加到 AEM 体验片段来扩展表单的范围，从而允许跨多个页面或站点无缝重用。例如，您可以在体验片段中加入新闻稿注册表单。这使您能够方便地在网站的多个页面中重用片段，而无需重复重新创建表单。 对体验片段中新闻稿注册表单所做的任何更新或修改都会自动传播到其使用的所有页面。 这简化了流程，并确保无缝的用户体验，同时简化了对网站表单的管理。

要在体验片段中创建自适应表单：

1. 打开体验片段。
1. 拖放 **[!UICONTROL 自适应Forms容器]** 从组件浏览器到体验片段的组件。
1. 将自适应表单核心组件拖放到体验片段中的容器空间以创建表单。
1. 添加“提交”按钮。

接下来，您 [设置提交操作](#configure-submit-action-for-form) 和高级属性。

### 将AEM Sites页面中的自适应表单转换为体验片段 {#convert-an-adaptive-form-in-sites-page-to-an-experience-fragment}

您可以在站点页面编辑器中将现有的自适应表单转换为体验片段，以在多个页面或站点中重用该表单。

要将AEM Sites页面中的自适应表单转换为体验片段，请执行以下操作：

1. 在编辑模式下打开包含自适应表单的AEM Sites页面(在自适应Forms容器组件中)。
1. 打开内容树，然后选择 **[!UICONTROL 自适应Forms容器]** ，用于托管您的自适应表单。 一个AEM Sites页面可以托管多个自适应Forms。 因此，请仔细选择正确的自适应Forms容器。
1. 在菜单栏上，选择 ![“转换为体验片段变量”图标](/help/forms/using/assets/Smock_FilingCabinet_18_N.svg) “转换为体验片段变量”图标。
   ![将站点页面中的表单转换为体验片段](/help/forms/using/assets/convert-form-in-sites-page-to-an-experience-fragment.png)

   出现一个对话框，用于将自适应表单容器转换为新的体验片段或添加到现有的体验片段
1. 在转换为体验片段变体对话框中，设置以下选项的值：

   * **操作：** 选择以创建新体验片段或添加到现有体验片段。
   * **父级路径：** 指定要承载体验片段的文件夹的路径。 选项仅适用于创建新体验片段。
   * **模板：** 指定体验片段模板的路径。 如果您没有体验片段模板， [创建它](/help/sites-developing/experience-fragments.md). 选项仅可用于将自适应表单添加到现有体验片段。
   * **片段标题：** 指定体验片段的标题。 标题唯一标识体验片段


## 配置表单的提交操作 {#configure-submit-action-for-form}

提交操作让您选择通过自适应表单捕获的数据的目标。当用户单击自适应表单上的提交按钮时，将触发此操作。自适应表单包括一些现成的提交操作。 您还可以扩展默认提交操作以创建自己的自定义提交操作。 要为表单配置提交操作，请执行以下操作：

1. 打开包含自适应表单的AEM页面编辑器或体验片段。
1. 打开内容树，然后选择 **[!UICONTROL 自适应Forms容器]** ，用于托管您的自适应表单。 一个AEM Sites页面可以托管多个自适应Forms。 因此，请仔细选择正确的自适应Forms容器。
1. 单击自适应表单容器属性 ![自适应表单容器属性](/help/forms/using/assets/configure-icon.svg) 图标。 此时将打开用于配置提交操作的自适应表单容器对话框。
   ![自适应表单容器](/help/forms/using/assets/adaptive-forms-container.png)
1. 根据要求选择并配置提交操作。有关提交操作的详细信息，请参阅 [自适应表单提交操作](configuring-submit-actions.md)


## 为表单配置架构或表单数据模型 {#configure-schema-or-data-model-for-form}

您可以使用表单数据模型将表单连接到数据源，以根据用户操作发送和接收数据。 您还可以将表单连接到JSON架构，以预定义格式接收提交的数据。

将表单连接到架构或表单数据模型之前

* [创建JSON架构并上传到您的环境](adaptive-form-json-schema-form-model.md)
* [创建表单数据模型](create-form-data-models.md)

要为表单配置JSON架构或表单数据模型，请执行以下操作：

1. 打开包含自适应表单的AEM页面编辑器或体验片段。
1. 打开内容树，然后选择 **[!UICONTROL 自适应Forms容器]** ，用于托管您的自适应表单。 一个AEM Sites页面可以托管多个自适应Forms。 因此，请仔细选择正确的自适应Forms容器。
1. 单击自适应表单容器属性 ![自适应表单容器属性](/help/forms/using/assets/configure-icon.svg) 图标。 此时将打开用于配置数据模型的自适应表单容器对话框。
   ![表单数据模型自适应表单容器](/help/forms/using/assets/form-data-model-adaptive-forms-container.png)
1. 根据您的要求，选择并配置JSON架构或表单数据模型。 有关提交操作的详细信息，请参阅 [自适应表单提交操作](configuring-submit-actions.md).

   * 当您选择 **[!UICONTROL 表单模型]** 选项，使用 **[!UICONTROL 选择表单数据模型]** 用于选择预配置的表单数据模型的选项。
   * 当您选择 **[!UICONTROL 架构]** 选项，使用 **[!UICONTROL 架构]** 选项来为您的表单选择JSON架构。

1. 单击&#x200B;**[!UICONTROL 完成]**。

## 为表单配置预填充服务 {#configure-prefill-service-for-form}

您可以使用预填充服务使用现有数据自动填充自适应表单的字段。 当用户打开表单时，这些字段的值会预先填充。 您可以：

* [创建自定义预填充服务](prepopulate-adaptive-form-fields.md)
* [使用表单数据模型预填充服务](#fdm-prefill-service)

### 使用表单数据模型预填充服务 {#fdm-prefill-service}

您可以使用表单数据模型预填充服务使用配置的表单数据模型预填充表单的字段。 表单数据模型预填充服务使用 [获取已配置表单数据模型的服务](work-with-form-data-model.md#add-data-model-objects-and-services-add-data-model-objects-and-services) 以检索数据。 要对自适应表单使用表单数据模型预填充服务，请执行以下操作：

1. 打开包含自适应表单的AEM页面编辑器或体验片段。
1. 打开内容树，然后选择 **[!UICONTROL 自适应Forms容器]** ，用于托管您的自适应表单。 一个AEM Sites页面可以托管多个自适应Forms。 因此，请仔细选择正确的自适应Forms容器。
1. 单击自适应表单容器属性 ![自适应表单容器属性](/help/forms/using/assets/configure-icon.svg) 图标。 此时将打开用于配置数据模型的自适应表单容器对话框。
   ![预填充服务fdm aem sites页面编辑器](/help/forms/using/assets/prefill-service-fdm-aem-sites-page-editor.png)
1. 选择表单数据模型. 打开 **[!UICONTROL 基本]** 选项卡。 在预填充服务中，选择 **[!UICONTROL Forms Portal草稿预填充服务]**.
1. 单击&#x200B;**[!UICONTROL 完成]**。

## 在提交表单时将用户重定向到新用户或显示感谢消息

在提交表单时，您可以将用户重定向到其他网页或消息。 要重定向用户或配置感谢消息，请执行以下操作：

1. 打开包含自适应表单的AEM页面编辑器或体验片段。
1. 打开内容树，然后选择 **[!UICONTROL 自适应Forms容器]** ，用于托管您的自适应表单。 一个AEM Sites页面可以托管多个自适应Forms。 因此，请仔细选择正确的自适应Forms容器。
1. 单击自适应表单容器属性 ![自适应表单容器属性](/help/forms/using/assets/configure-icon.svg) 图标。 此时将打开用于配置数据模型的自适应表单容器对话框。
1. 打开 **[!UICONTROL 提交]** 选项卡。

   * 要配置重定向URL，请在提交时为选项选择重定向到URL选项，并提供绝对地址、重定向URL或AEM Sites页面的相对路径。

   * 要配置自定义或感谢消息，请在“提交时”选项中选择显示消息选项，然后在“消息内容”框中提供消息。 它是一个富文本框，您可以使用全屏选项查看所有可用的富文本项。
