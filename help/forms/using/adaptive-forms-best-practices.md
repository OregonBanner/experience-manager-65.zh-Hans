---
title: 使用自适应表单的最佳实践
seo-title: Best practices for working with adaptive forms
description: 介绍设置AEM Forms项目、开发自适应表单和优化AEM Forms系统性能的最佳实践。
seo-description: Explains best practices for setting up an AEM Forms project, developing adaptive forms, and optimizing the performance for AEM Forms system.
uuid: ed95fc64-56b3-4ea1-a5ba-2e96953fca56
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 43c431e4-5286-4f4e-b94f-5a7451c4a22c
feature: Adaptive Forms
exl-id: 5c75ce70-983e-4431-a13f-2c4c219e8dde
source-git-commit: f05ddd2fb72258b7de5d361eb87f5e68e7ddd7ff
workflow-type: tm+mt
source-wordcount: '4529'
ht-degree: 0%

---

# 使用自适应表单的最佳实践 {#best-practices-for-working-with-adaptive-forms}

## 概述 {#overview}

Adobe Experience Manager (AEM)表单可以帮助您将复杂的交易转换为简单、愉快的数字体验。 但是，它需要协调一致的努力，以实施、构建、执行和维持高效且富有成效的AEM Forms生态系统。

本文档提供了表单管理员、作者和开发人员在使用AEM Forms（尤其是自适应表单组件）时可能会从中受益的准则和建议。 它讨论了从设置表单开发项目到配置、自定义、创作和优化AEM Forms的最佳实践。 这些最佳实践共同为AEM Forms生态系统的整体性能做出了贡献。

此外，以下是一些一般AEM最佳实践的建议阅读：

* [最佳实践：部署和维护AEM](/help/sites-deploying/best-practices.md)
* [最佳实践：创作内容](/help/sites-authoring/best-practices.md)
* [最佳实践：管理AEM](/help/sites-administering/administer-best-practices.md)
* [最佳实践：开发解决方案](/help/sites-developing/best-practices.md)

## 设置和配置AEM Forms {#set-up-and-configure-aem-forms}

### 设置表单开发项目 {#setting-up-forms-development-project}

简化和标准化的项目结构可以显着减少开发和维护工作。 Apache Maven是用于构建AEM项目的推荐的开源工具。

* 使用Apache Maven `aem-project-archetype` 创建和管理AEM项目的结构。 它可为您的AEM项目创建推荐的结构和模板。 此外，它还提供构建自动化和变更控制系统以帮助管理项目。

   * 使用maven `archetype:generate` 命令生成初始结构。
   * 使用maven `eclipse:eclipse` 命令生成eclipse项目文件并将项目导入eclipse。

有关更多信息，请参阅 [如何使用Apache Maven构建AEM项目](/help/sites-developing/ht-projects-maven.md).

* FileVault工具或VLT可帮助您将CRX或AEM实例的内容映射到文件系统。 它提供变更控制管理操作，例如AEM项目内容的签入和签出。 参见 [如何使用VLT工具](/help/sites-developing/ht-vlttool.md).

* 如果您使用集成了Eclipse的开发环境，则可以使用AEM开发人员工具将Eclipse IDE与AEM实例无缝集成，以创建AEM应用程序。 有关详细信息，请参阅 [适用于Eclipse的AEM开发人员工具](/help/sites-developing/aem-eclipse.md).

* 请勿在/libs文件夹中存储任何内容或修改任何内容。 在/app文件夹中创建叠加以扩展或覆盖默认功能。

* 在创建包以移动内容时，请确保包过滤器路径正确，并且只提到所需的路径。

* 请勿在/libs文件夹中存储任何内容或修改任何内容。 在/app文件夹中创建叠加以扩展或覆盖默认功能。

* 为软件包定义正确的依赖关系，以强制预先确定的安装顺序/顺序。

* 请勿在/libs或/apps中创建任何可引用的节点。

### 规划创作环境 {#planning-for-authoring-environment}

设置AEM项目后，定义用于创作和自定义自适应表单模板和组件的策略。

* 自适应表单模板是一种专门的AEM页面，用于定义自适应表单的结构和页眉 — 页脚信息。 模板具有预配置的自适应表单布局、样式和基本结构。 AEM Forms提供可用于创作自适应表单的现成模板和组件。 但是，您可以根据需要创建自定义模板和组件。 建议收集您在自适应表单中所需的其他模板和组件的要求。 有关详细信息，请参阅 [自定义自适应表单和组件](/help/forms/using/adaptive-forms-best-practices.md#customize-components).
* AEM Forms允许您基于以下表单模型创建自适应表单。 表单模型用作表单与AEM系统之间数据交换的接口，并为自适应表单内外的数据流提供基于XML的结构。 此外，表单模型以模式和XFA约束的形式对自适应表单施加规则和约束。

   * **无**：使用此选项创建的自适应表单不使用任何表单模型。 从此类表单生成的数据 XML 具有带字段和相应值的平面结构。
   * **XML或JSON架构**： XML和JSON架构表示组织中的后端系统生成或使用数据的结构。 您可以将架构关联到自适应表单，并使用其元素将动态内容添加到自适应表单。 架构的元素在内容浏览器的数据模型对象选项卡中可用，用于创作自适应表单。 您可以拖放架构元素来构建表单。
   * **XFA表单模板**：如果您在基于XFA的HTML5表单中有投资，则它是理想的表单模型。 它提供了一种将您的基于XFA的表单转换为自适应表单的直接方法。 任何现有的XFA规则都会保留在关联的自适应表单中。 生成的自适应表单支持XFA构造，例如验证、事件、属性和模式。
   * **表单数据模型**：如果您希望集成后端系统(如数据库、Web服务和AEM用户配置文件)，以预填充自适应表单并将提交的表单数据写回后端系统，则它是首选表单模型。 利用表单数据模型编辑器，可在可用于创建自适应表单的表单数据模型中定义和配置实体和服务。 有关更多信息，请参阅 [AEM Forms数据集成](/help/forms/using/data-integration.md).

请务必仔细选择数据模型，该模型不仅适合您的要求，而且可以扩展您对XFA和XSD资产的现有投资（如果有）。 建议使用XSD模型创建表单模板，因为生成的XML包含架构定义的每个XPATH的数据。 使用XSD模型作为表单数据模型的默认选择也很有帮助，因为它将表单设计和处理和使用数据的后端系统分离，并且由于表单字段的一对一映射，它提高了表单的性能。 此外，还可以将该字段的BindRef设置为其数据值在XML中的XPATH。

有关更多信息，请参阅 [创建自适应表单](/help/forms/using/creating-adaptive-form.md).

* 自适应表单中包含一些常见部分。 您可以标识这些内容并定义策略以促进内容重用。 利用自适应表单，可创建独立片段并在各个表单中重复使用它们。 您还可以将自适应表单中的面板另存为片段。 片段中的任何更改都会反映在所有关联的表单中。 它有助于减少创作时间并确保表单之间的一致性。 此外，使用片段使自适应表单变得轻量级，从而改进了创作体验，尤其是大型表单的创作体验。 有关更多信息，请参阅 [自适应表单片段](/help/forms/using/adaptive-form-fragments.md).

### 自定义自适应表单和组件 {#customize-components}

* AEM Forms提供可用于创建自适应表单的现成自适应表单模板。 您还可以创建自己的模板。 AEM提供静态和可编辑的模板。

   * 静态模板由开发人员定义和配置。
   * 可编辑模板由作者使用模板编辑器创建。 利用模板编辑器，可在模板中定义基本结构和初始内容。 结构层中的任何修改都会反映在使用该模板的所有表单中。 初始内容可包括预配置的主题、预填充服务、提交操作等。 但是，可以使用表单编辑器为表单修改这些设置。 有关更多信息，请参阅 [自适应表单模板](/help/forms/using/template-editor.md).

* 要设置特定字段或面板实例的样式，请使用 [内联样式](/help/forms/using/inline-style-adaptive-forms.md). 或者，您也可以在CSS文件中定义类，并在组件的CSS Class属性中指定类名称。
* 在组件中包含客户端库，以便在使用该组件的自适应表单或片段中始终应用样式。 有关更多信息，请参阅 [创建自适应表单页面组件](/help/forms/using/custom-adaptive-forms-templates.md).
* 通过在自适应表单容器属性的CSS文件路径字段中指定客户端库的路径，应用客户端库中定义的样式来选择自适应表单。
* 要创建样式的客户端库，您可以在主题编辑器基本clientlib或表单容器属性中配置自定义CSS文件。
* 自适应表单提供面板布局（如响应式、选项卡式、折叠和向导），以控制表单组件在面板中的布局方式。 您可以创建自定义面板布局，并使其可供表单作者使用。 有关更多信息，请参阅 [创建自适应表单的自定义布局组件](/help/forms/using/custom-layout-components-forms.md).
* 您还可以自定义特定的自适应表单组件，如字段和面板布局。

   * 使用 [叠加](/help/sites-developing/overlays.md) AEM的功能，用于修改组件的副本。 建议不要修改默认组件。
   * 要在/libs中自定义现成自适应表单组件的布局，请执行以下操作 [创建自定义布局组件](/help/forms/using/custom-layout-components-forms.md) 除了 [默认版面](/help/forms/using/layout-capabilities-adaptive-forms.md).
   * 通过创建自定义小部件或外观引入自定义交互。 建议不要修改默认组件。 有关更多信息，请参阅 [外观框架](/help/forms/using/introduction-widgets.md).

* 参见 [处理个人身份信息](/help/forms/using/adaptive-forms-best-practices.md#p-handling-personally-identifiable-information-p) 以获取有关处理PII数据的建议。

### 创建表单模板

您可以使用中启用的表单模板创建自适应表单 **配置浏览器**. 要启用表单模板，请参阅 [创建自适应表单模板](https://experienceleague.adobe.com/docs/experience-manager-learn/forms/creating-your-first-adaptive-form/create-adaptive-form-template.html?lang=en).

表单模板也可以从在另一台作者计算机上创建的自适应表单包上传。 通过安装提供表单模板 [aemforms-references-*包](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=en). 推荐的一些最佳实践包括：
* 此 **nosamplecontent** 仅作者建议使用运行模式，而不建议发布节点使用运行模式。
* 自适应表单、主题、模板或云配置等资产的创作仅通过创作节点执行，并且可在配置的发布节点中发布。
有关更多信息，请参阅 [发布和取消发布表单和文档](https://experienceleague.adobe.com/docs/experience-manager-65/forms/publish-process-aem-forms/publishing-unpublishing-forms.html?lang=en)
* 创作和发布操作需要Forms附加组件包，才能支持文档服务操作；因此，可以将其视为依赖项。
如果您只想要Forms相关的示例模板、主题和DOR包，则可以从 [aemforms-references-*包](https://experienceleague.adobe.com/docs/experience-manager-65/forms/publish-process-aem-forms/publishing-unpublishing-forms.html?lang=en).

有关详细信息，请参阅 [自适应表单创作简介](/help/forms/using/introduction-forms-authoring.md).

## 创作自适应表单 {#author-adaptive-forms}

### 使用触控优化的UI进行创作 {#using-touch-optimized-ui-for-authoring}

* 使用侧栏中的对象浏览器快速访问表单层次结构中下层的字段。 您可以使用搜索框搜索表单或对象树中的对象，以便从一个对象导航到另一个对象。
* 要在侧栏的组件浏览器中查看和编辑组件的属性，请选择该组件并单击 ![cmppr-1](assets/cmppr-1.png). 您还可以双击组件以在属性浏览器中查看其属性。
* 使用键盘快捷键对表单执行快速操作。 参见 [AEM Forms键盘快捷键](/help/forms/using/keyboard-shortcuts.md).

* 建议仅将自适应表单组件用于自适应表单页面。 组件依赖于其父层次结构。 因此，请勿在AEM页面中使用它们。

另请参阅中的组件描述和最佳实践。 [自适应表单创作简介](/help/forms/using/introduction-forms-authoring.md).

### 在自适应表单中使用规则 {#using-rules-in-adaptive-forms}

AEM Forms提供 [规则编辑器](/help/forms/using/rule-editor.md) 允许您创建规则以将动态行为添加到自适应表单组件。 使用这些规则，您可以评估条件并触发组件上的操作，例如显示或隐藏字段、计算值、动态更改下拉列表等。

规则编辑器提供了用于编写规则的可视编辑器和代码编辑器。 使用代码编辑器模式编写规则时，请考虑以下事项：

* 为表单字段和组件使用有意义且唯一的名称，以避免在编写规则时可能产生的任何冲突。
* 使用 `this` 运算符，组件在规则表达式中引用自身。 它可确保即使组件名称发生更改，规则仍保持有效。 例如：`field1.valueCommit script: this.value > 10`。

* 引用其他表单组件时，请使用组件名称。 使用 `value` 属性以获取字段或组件的值。 例如：`field1.value`。

* 按相对唯一层次结构引用组件以避免任何冲突。 例如：`parentName.fieldName`。

* 处理复杂或常用规则时，请考虑将业务逻辑作为函数写入单独的客户端库中，您可以在自适应表单中指定并重用该库。 客户端库应为自包含库，并且不应具有任何外部依赖项，但jQuery和Underscore.js上除外。 您还可以使用客户端库来强制 [服务器端重新验证](/help/forms/using/configuring-submit-actions.md#server-side-revalidation-in-adaptive-form) 表单数据的URL路径。
* 自适应表单提供了一组API，您可以使用这些API与自适应表单通信并对自适应表单执行操作。 一些关键API如下所示。 有关更多信息，请参阅 [自适应Forms的JavaScript库API参考](https://adobe.com/go/learn_aemforms_documentation_63).

   * `guideBridge.reset()`：重置表单。
   * `guideBridge.submit()`：提交表单。
   * `guideBridge.setFocus(somExp, focusOption, runCompletionExp)`：将焦点设置为字段。
   * `guideBridge.validate(errorList, somExpression, focus)`：验证表单。
   * `guideBridge.getDataXML(options)`：以XML格式获取表单数据。
   * `guideBridge.resolveNode(somExpression)`：获取表单对象。
   * `guideBridge.setProperty(somList, propertyName, valueList)`：设置表单对象的属性。
   * 此外，您还可以使用以下字段属性：

      * `field.value` 以更改字段的值。
      * `field.enabled` 以启用/禁用字段。
      * `field.visible` 更改字段的可见性。

* 自适应表单作者可能需要编写JavaScript代码，才能在表单中构建业务逻辑。 虽然JavaScript功能强大且有效，但它很可能降低安全预期。 因此，您必须确保表单作者是受信任的角色，并且存在在表单投入生产之前审查和批准JavaScript代码的流程。 管理员可以根据用户组的角色或功能，限制用户组对规则编辑器的访问权限。 参见 [向选定的用户组授予规则编辑器访问权限](/help/forms/using/rule-editor-access-user-groups.md).
* 您可以在规则中使用表达式来使自适应表单成为动态表单。 所有表达式都是有效的JavaScript表达式，并且使用自适应表单脚本模型API。 这些表达式返回某些类型的值。 有关表达式及其周围最佳实践的更多信息，请参阅 [自适应表单表达式](/help/forms/using/adaptive-form-expressions.md).

### 使用主题 {#working-with-themes}

通过主题自适应，您可以创建可重复使用的样式，这些样式可以跨表单应用，以实现一致的外观和样式。 建议使用主题来定义表单组件和面板的样式。 围绕主题的一些最佳实践如下：

* 使用资产库快速应用文本样式、背景和图像。 将样式添加到资产库时，该样式可用于其他主题和表单编辑器的样式模式。
* 使用页面级别选择器应用字体和页面背景等全局设置。
* 使用客户端库将现有样式或高级样式导入主题。
* 可以覆盖表单样式图层中的特定字段、面板或按钮的样式。
* 如果主题不符合样式要求，则可以使用预定义类（如guideFieldNode、guideFieldLabel、guideFieldWidget和guidePanelNode）跨表单应用通用样式。

有关更多信息，请参阅 [主题](/help/forms/using/themes.md).

### 优化大型和复杂表单的性能 {#optimizing-performance-of-large-and-complex-forms}

在创作模式下或运行时加载大型表单时，表单作者和最终用户通常面临性能问题。 随着表单中对象（字段和面板）数量的增加，创作和运行时体验开始降级。 它还阻止多个作者同时协作和创作表单。

请考虑以下最佳实践，以解决大型表单的性能问题：

* 建议使用XSD表单数据模型创建自适应表单，即使可能的情况下也将XFA转换为自适应表单。
* 在自适应表单中仅包括从用户捕获信息的那些字段和面板。 可以考虑将静态内容保持在最小值，或者使用URL在单独的窗口中打开它们。
* 虽然每个表单都针对特定目的而设计，但大多数表单中都存在一些通用区段。 例如，个人详细信息、地址、雇用详细信息等。 创建 [自适应表单片段](/help/forms/using/adaptive-form-fragments.md) 用于常见表单元素和节，并在表单间使用它们。 您还可以将现有表单中的面板另存为片段。 片段中的任何更改都会反映在所有关联的自适应表单中。 它促进了协作创作，因为多个作者可以同时处理构成表单的不同片段。

   * 与自适应表单类似，建议使用片段容器对话框在客户端库中定义所有特定于片段的样式和自定义脚本。 此外，尝试创建不依赖于外部对象的自给自足的片段。
   * 避免使用跨片段脚本。 如果片段外有任何您必须引用的对象，请尝试将该对象作为父表单的一部分。 如果对象必须仍然驻留在另一个片段中，请在脚本中按其名称引用它。

* 使用自动保存并恢复可定期保存自适应表单，并允许用户稍后重新访问以完成表单。
* 将片段配置为延迟加载。 在运行时，标记为延迟加载的片段仅在需要时呈现。 它显着缩短了大型表单的加载时间。 带有可重复面板的片段也支持此功能。 有关更多信息，请参阅 [配置延迟加载](/help/forms/using/lazy-loading-adaptive-forms.md).

   * 请勿在响应式网格布局或第一个面板中配置对片段的延迟加载。
   * 延迟加载的片段不支持文件附件和条款和条件组件。
   * 如果延迟加载面板中的某个值在表单的其他部分中使用，请将该值标记为“全局使用值”，以便在卸载包含的面板时可以使用该值。
   * 考虑为应根据条件显示或隐藏的片段编写可见性规则。
* 设置值 **每个请求的调用数** 在 **Apache Sling主Servlet** 相当多的人。 它允许Forms服务器进行其他调用。 配置显示默认值1500。 值1500调用用于其他Experience Manager组件，如Sites和Assets。 自适应表单的默认值集为20000。 如果您遇到 `too many calls` 日志中有错误或表单无法呈现，请尝试将值增大到较大的数字来解决问题。 如果调用数超过20000，则意味着表单很复杂，可能需要一些时间才能在浏览器中呈现表单。 这仅在首次加载表单时发生，之后缓存表单，并且缓存表单后，对性能没有重大影响。

### 预填自适应表单 {#prefilling-adaptive-forms}

您可以使用从后端获取的数据预填充自适应表单字段，以帮助用户快速填写表单并避免键入错误。

* AEM Forms提供预填充服务，用于从预定义的数据XML文件读取数据，并使用预填充XML文件中的内容预填充自适应表单的字段。
* 预填充数据XML必须与与自适应表单关联的表单模型的架构兼容。
* 包括 `afBoundedData` 和 `afUnBoundedData` 预填充XML中的部分来预填充自适应表单中的绑定和未绑定字段。

* 对于基于表单数据模型的自适应表单，AEM Forms提供现成的表单数据模型预填充服务。 预填充服务在自适应表单中查询数据模型对象的数据源，并在渲染表单时预填充字段值。
* 您还可以使用文件、crx、服务或http协议预填充自适应表单。
* AEM Forms支持自定义预填充服务，您可以将这些服务作为OSGi服务插入以预填充自适应表单。

有关更多信息，请参阅 [预填自适应表单字段](/help/forms/using/prepopulate-adaptive-form-fields.md).

### 签名和提交自适应表单 {#signing-and-submitting-adaptive-forms}

自适应表单需要提交操作来处理用户指定的数据。 提交操作确定使用自适应表单提交的数据上执行的任务。

* 在自适应表单中，有多个现成的提交操作。 有关详细信息，请参阅 [配置提交操作](/help/forms/using/configuring-submit-actions.md).
* 如果默认提交操作不符合您的用例，则可以编写自定义提交操作。 有关更多信息，请参阅 [为自适应表单编写自定义提交操作](/help/forms/using/custom-submit-action-form.md).
* 包括服务器端验证，以防止提交无效数据。

您可以在自适应表单中利用Adobe Sign的多签名体验。 在自适应表单中配置Adobe Sign时，请考虑以下事项。 有关详细信息，请参阅 [在自适应表单中使用Adobe Sign](/help/forms/using/working-with-adobe-sign.md).

* 仅在所有签名者对表单签名后，才提交支持Adobe Sign的自适应表单。 在所有签名者对表单进行签名之前，Forms会一直处于待处理签名状态。
* 您可以在提交时配置表单内签名体验或将签名者重定向到签名页面。
* 根据需要配置顺序或并行签名体验。

### 生成记录文档 {#generating-document-of-record}

记录文档(DoR)是自适应表单的拼合PDF版本，您可以打印、签名或存档。

* 根据自适应表单所基于的表单数据模型，您可以为DoR配置模板，如下所示：

   * **XFA表单模板**：使用关联的XDP文件作为DoR模板。
   * **XSD架构**：使用与自适应表单使用相同XML架构的关联XFA模板。
   * **无**：使用自动生成的DoR。

* 直接从自适应表单编辑器的“记录文档”选项卡配置页眉、页脚、图像、颜色、字体等。
* 使用 `DoRService` 以编程方式生成DoR。
* 从记录文档排除隐藏字段。
* 使用 `afAcceptLang` 请求参数以在其他区域设置中查看DoR。

### 调试和测试自适应表单 {#debugging-and-testing-adaptive-forms}

[AEM Chrome插件](https://adobe-consulting-services.github.io/acs-aem-tools/aem-chrome-plugin/) 是Google Chrome的浏览器扩展，提供调试自适应表单的工具。 表单作者和开发人员可以使用这些工具执行以下操作：

* 确定瓶颈并优化表单渲染性能
* 表单中的调试关键字和bindRef错误
* 启用和配置日志
* 调试表单中的规则和脚本
* 探索和了解guideBridge API

有关更多信息，请参阅 [AEM Chrome插件 — 自适应表单](https://adobe-consulting-services.github.io/acs-aem-tools/aem-chrome-plugin/adaptive-form/).

### 验证AEM服务器上的自适应表单 {#validating-adaptive-forms-on-aem-server}

需要服务器端验证，以防止任何绕过客户端验证的尝试以及任何可能危及数据提交和业务规则违规的行为。 服务器端验证通过加载所需的客户端库在服务器上执行。

* 在客户端库中包含用于验证自适应表单中表达式的函数，并在自适应表单容器对话框中指定客户端库。 有关更多信息，请参阅 [服务器端重新验证](/help/forms/using/configuring-submit-actions.md#p-server-side-revalidation-in-adaptive-form-p).
* 服务器端验证验证表单模型。 建议为验证创建单独的客户端库，并且不要在同一客户端库中将其与HTML样式和DOM操作等其他内容混合。

### 本地化自适应表单 {#localizing-adaptive-forms}

AEM提供可用于本地化自适应表单的翻译工作流。 有关信息，请参阅 [使用AEM翻译工作流将自适应表单本地化](/help/forms/using/using-aem-translation-workflow-to-localize-adaptive-forms.md).

本地化自适应表单时的一些最佳实践如下：

* 将自适应表单片段用于表单中的通用元素并将片段本地化。 它确保您将片段本地化一次，并在使用本地化片段的所有表单中反映出来。
* 任何修改（如添加新组件或以本地化的形式应用脚本）都不会自动本地化。 因此，在本地化表单之前必须先完成该表单，以避免多个本地化周期。
* 使用 `afAcceptLang` 请求参数覆盖浏览器区域设置并以指定的区域设置呈现表单。 例如，无论浏览器设置中指定的区域设置如何，以下URL将强制以日语区域设置呈现表单：

   `https://'[server]:[port]'/<contextPath>/<formFolder>/<formName>.html?wcmmode=disabled&afAcceptLang=ja`

* AEM Forms当前支持英语(en)、西班牙语(es)、法语(fr)、意大利语(it)、德语(de)、日语(ja)、葡萄牙语 — 巴西语(pt-BR)、中文(zh-CN)、中文 — 台湾(zh-TW)和韩语(ko-KR)语言环境的自适应表单内容本地化。 但是，您可以在运行时为自适应表单添加新区域设置支持。 有关更多信息，请参阅 [支持自适应表单本地化的新区域设置](/help/forms/using/supporting-new-language-localization.md).

## 准备表单项目以进行生产 {#prepare-forms-project-for-production}

### 添加表单处理服务器 {#adding-forms-processing-server}

您可以配置驻留在防火墙后面的安全区域中的其他AEM Forms服务器实例。 您可以将此实例用于：

* **批处理**：以重负载批次方式定期或计划的作业。 例如，打印语句，生成对应，以及使用PDF生成器、输出和汇编器等文档服务。
* **存储PII数据**：将PII数据保存在处理服务器上。 如果您已在使用自定义存储提供程序存储PII数据，则不需要使用此功能。

### 将项目移动到其他环境 {#moving-project-to-another-environment}

您通常需要将AEM项目从一个环境移动到另一个环境。 迁移时需要记住的一些关键事项如下：

* 备份现有客户端库、自定义代码和配置。
* 在新环境中以指定的顺序手动部署产品软件包和修补程序。
* 手动部署项目特定的代码包和捆绑包，并将其作为单独的包或捆绑包部署到新的AEM服务器上。
* (*仅限JEE上的AEM Forms*)在Forms Workflow服务器上手动部署LCA和DSC。
* 使用 [Export-Import](/help/forms/using/import-export-forms-templates.md) 用于将资源移动到新环境的功能。 您还可以配置复制代理并发布资产。
* 升级时，请使用新的API和功能替换所有已弃用的API和功能。

### 配置AEM {#configuring-aem}

以下是配置AEM以提高整体性能的一些最佳实践：

* 从Felix控制台为JavaScript和CSS启用HTML客户端库压缩。
* 将所有客户端库都缓存到 `/etc.clientlibs/fd` 以及AEM Dispatcher上的任何其他自定义客户端库，以提高已发布表单的响应速度和安全性。 有关更多信息，请参阅 [调度程序](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html).

* 不缓存 `/content/forms/af/` 和 `/content/dam/formsanddocuments/*` 路径。 有关配置自适应表单缓存的详细信息，请参阅 [缓存自适应表单](/help/forms/using/configure-adaptive-forms-cache.md).

* 通过Web服务器HTML模块启用压缩。 有关更多信息，请参阅 [AEM Forms服务器的性能优化](/help/forms/using/performance-tuning-aem-forms.md).
* 增加大型表单的每个请求配置的调用数。 参见 [优化大型和复杂表单的性能](/help/forms/using/adaptive-forms-best-practices.md#optimizing-performance-of-large-and-complex-forms).
* 创建 [错误处理程序显示的自定义错误页面](https://experienceleague.adobe.com/docs/experience-manager-65/developing/platform/customizing-errorhandler-pages.html).
* 安全的AEM Forms服务器。

   * 使用 `nosamplecontent` 运行模式以确保生产服务器上没有部署示例内容和示例用户。 参见 [在生产就绪模式下运行AEM](/help/sites-administering/production-ready.md).

* 将栈大小保持为最小8 GB。 有关其他设置，请参阅 [AEM Forms服务器的性能优化](/help/forms/using/performance-tuning-aem-forms.md).
* 使用服务用户会话而不是管理会话来执行服务级别任务。 有关更多信息，请参阅 [服务身份验证](https://sling.apache.org/documentation/the-sling-engine/service-authentication.html).

>[!VIDEO](https://vimeo.com/)

### 为草稿和提交的表单数据配置外部存储 {#external-storage}

在生产环境中，建议不要将提交的表单数据存储在AEM存储库中。 Forms Portal Store、Store Content和StorePDF提交操作的默认实施将表单数据存储在AEM存储库中。 这些提交操作仅用于演示目的。 此外，默认情况下，“保存并恢复”和“自动保存”功能使用入口存储。 因此，请考虑以下建议：

* **存储草稿数据**：如果您使用自适应表单的草稿功能，则应实施自定义服务提供接口(SPI)，以将草稿数据存储到更安全的存储区，如数据库。 有关更多信息，请参阅 [将草稿和提交组件与数据库集成的示例](/help/forms/using/integrate-draft-submission-database.md).

* **存储提交数据**：如果您使用表单门户提交存储，则应当实施自定义SPI以将提交数据存储到数据库中。 参见 [将草稿和提交组件与数据库集成的示例](/help/forms/using/integrate-draft-submission-database.md) （了解示例集成）。

   您还可以编写自定义提交操作，将表单数据和附件存储在安全存储中。 参见 [为自适应表单编写自定义提交操作](/help/forms/using/custom-submit-action-form.md) 了解更多信息。

* **草稿标识的长度**：将自适应表单另存为草稿时，将生成草稿ID以唯一标识草稿。 草稿ID字段的最小长度值为26个字符。 Adobe建议将草稿ID长度设置为26个或更多字符。

### 处理个人身份信息 {#handling-personally-identifiable-information}

组织面临的主要挑战之一是如何处理个人身份识别(PII)数据。 以下是将帮助您处理此类数据的一些最佳实践：

* 使用安全的外部存储（如数据库）存储草稿和已提交表单中的数据。 参见 [为草稿和提交的表单数据配置外部存储](/help/forms/using/adaptive-forms-best-practices.md#external-storage).
* 使用条款和条件表单组件，在启用自动保存之前获得用户的明确同意。 在这种情况下，仅当用户同意条款和条件组件中的条件时才启用自动保存。


