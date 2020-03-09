---
title: 使用自适应表单的最佳实践
seo-title: 使用自适应表单的最佳实践
description: 解释设置AEM Forms项目、开发自适应表单以及优化AEM Forms系统性能的最佳实践。
seo-description: 解释设置AEM Forms项目、开发自适应表单以及优化AEM Forms系统性能的最佳实践。
uuid: ed95fc64-56b3-4ea1-a5ba-2e96953fca56
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 43c431e4-5286-4f4e-b94f-5a7451c4a22c
translation-type: tm+mt
source-git-commit: dbfadb0b49c83c38aa2cb55c32517ad70bbd79d0

---


# 使用自适应表单的最佳实践 {#best-practices-for-working-with-adaptive-forms}

## 概述 {#overview}

Adobe Experience Manager(AEM)表单可以帮助您将复杂的交易转变为简单、愉悦的数字体验。 但是，它需要共同努力来实施、构建、执行和维护一个高效、高效的AEM Forms生态系统。

本文档提供了管理员、作者和开发人员在使用AEM Forms（尤其是自适应表单组件）时可从中受益的准则和建议。 它讨论了从设置表单开发项目到配置、自定义、创作和优化AEM表单的最佳实践。 这些最佳做法集中有助于AEM Forms生态系统的整体性能。

此外，以下是一些针对一般AEM最佳实践的建议读取内容：

* [最佳实践：部署和维护AEM](/help/sites-deploying/best-practices.md)
* [最佳实践：创作内容](/help/sites-authoring/best-practices.md)
* [最佳实践：管理AEM](/help/sites-administering/administer-best-practices.md)
* [最佳实践：开发解决方案](/help/sites-developing/best-practices.md)

## 设置和配置AEM表单 {#set-up-and-configure-aem-forms}

### 设置表单开发项目 {#setting-up-forms-development-project}

简化和标准化的项目结构可以显着减少开发和维护工作。 Apache Maven是建立AEM项目时推荐的开放源代码工具。

* 使用Apache Maven `aem-project-archetype` 为AEM项目创建和管理结构。 它为您的AEM项目创建推荐的结构和模板。 此外，它还提供构建自动化和更改控制系统以帮助管理项目。

   * 使用maven命 `archetype:generate` 令生成初始结构。
   * 使用maven `eclipse:eclipse` 命令生成Eclipse项目文件并将项目导入Eclipse。

有关详细信息，请 [参阅如何使用Apache Maven构建AEM项目](/help/sites-developing/ht-projects-maven.md)。

* FileVault工具或VLT可帮助您将CRX或AEM实例的内容映射到文件系统。 它提供了更改控制管理操作，如AEM项目内容的登记和注销。 请参 [阅如何使用VLT工具](/help/sites-developing/ht-vlttool.md)。

* 如果您使用Eclipse集成的开发环境，则可以使用AEM开发人员工具将Eclipse IDE与AEM实例无缝集成以创建AEM应用程序。 有关详细信息，请参 [阅适用于Eclipse的AEM开发人员工具](/help/sites-developing/aem-eclipse.md)。

### 创作环境规划 {#planning-for-authoring-environment}

设置AEM项目后，请定义用于创作和自定义自适应表单模板和组件的策略。

* 自适应表单模板是一个专用的AEM页面，它定义自适应表单的结构和页眉和页脚信息。 模板具有预配置的布局、样式和自适应表单的基本结构。 AEM Forms提供现成的模板和组件，您可以使用它们创作自适应表单。 但是，您可以根据需要创建自定义模板和组件。 建议收集您在自适应表单中需要的其他模板和组件的要求。 有关详细信息，请参 [阅自定义自适应表单和组件](/help/forms/using/adaptive-forms-best-practices.md#customize-components)。
* AEM Forms允许您根据以下表单模型创建自适应表单。 表单模型用作表单与AEM系统之间数据交换的接口，并为自适应表单内外的数据流提供基于XML的结构。 另外，表单模型以模式和XFA约束的形式对自适应表单施加规则和约束。

   * **无**:使用此选项创建的自适应表单不使用任何表单模型。 从这种表单生成的数据XML具有带字段和相应值的平面结构。
   * **XML或JSON架构**:XML和JSON架构表示组织中后端系统生成或使用数据的结构。 您可以将架构与自适应表单关联，并使用其元素将动态内容添加到自适应表单。 此架构的元素位于内容浏览器的“数据模型对象”选项卡中，可用于创作自适应表单。 您可以拖放架构元素以构建表单。
   * **XFA表单模板**:如果您对基于XFA的HTML5表单有投资，那么它是理想的表单模型。 它提供了一种将基于XFA的表单转换为自适应表单的直接方式。 任何现有的XFA规则都会保留在关联的自适应表单中。 生成的自适应表单支持XFA构造，如验证、事件、属性和模式。
   * **表单数据模型**:如果您希望集成后端系统（如数据库、Web服务和AEM用户配置文件）以预填自适应表单并将提交的表单数据写入后端系统，则这是首选的表单模型。 表单数据模型编辑器允许您在表单数据模型中定义和配置实体和服务，以便用于创建自适应表单。 有关详细信息，请参 [阅AEM Forms数据集成](/help/forms/using/data-integration.md)。

请务必仔细选择不仅符合您的要求，而且扩展您在XFA和XSD资产中的现有投资（如果有）的数据模型。 建议使用XSD Model创建表单模板，因为生成的XML包含由架构定义的每个XPATH的数据。 使用XSD模型作为表单数据模型的默认选择也有助于实现，因为它将表单设计从处理和消费数据的后端系统分离出来，并且它由于表单字段的一对一映射而提高了表单的性能。 此外，字段的BindRef可以作为XML中其数据值的XPATH。

有关详细信息，请参 [阅创建自适应表单](/help/forms/using/creating-adaptive-form.md)。

* 自适应表单中有一些常见部分。 您可以识别这些内容并定义策略以促进内容重用。 自适应表单允许您创建独立的片段并跨表单重复使用它们。 您还可以将自适应表单中的面板另存为片段。 片段中的任何更改都会反映在所有关联的表单中。 它有助于您缩短创作时间并确保表单之间的一致性。 此外，片段的使用使自适应表单变得轻量化，从而改善了创作体验，尤其是大型表单。 有关详细信息，请参 [阅自适应表单片段](/help/forms/using/adaptive-form-fragments.md)。

### 自定义自适应表单和组件 {#customize-components}

* AEM Forms提供现成的自适应表单模板，您可以使用这些模板创建自适应表单。 您还可以创建自己的模板。 AEM提供静态和可编辑的模板。

   * 静态模板由开发人员定义和配置。
   * 可编辑的模板由作者使用模板编辑器创建。 模板编辑器允许您在模板中定义基本结构和初始内容。 结构层中的任何修改都会反映在使用该模板的所有表单中。 初始内容可以包括预配置的主题、预填充服务、提交操作等。 但是，可以使用表单编辑器为表单修改这些设置。 有关详细信息，请参阅自 [适应表单模板](/help/forms/using/template-editor.md)。

* 要设置特定字段或面板实例的样式，请使用内 [联样式](/help/forms/using/inline-style-adaptive-forms.md)。 或者，也可以在CSS文件中定义类，并在组件的“CSS类”属性中指定类名。
* 在组件中包括客户端库，以跨使用该组件的自适应表单或片段一致地应用样式。 有关详细信息，请参 [阅创建自适应表单页面组件](/help/forms/using/custom-adaptive-forms-templates.md)。
* 通过在自适应表单容器属性的CSS文件路径字段中指定到客户端库的路径，应用在客户端库中定义的样式以选择自适应表单。
* 要创建样式的客户端库，可以在“主题编辑器”基本clientlib或“表单容器”属性中配置自定义CSS文件。
* 自适应表单提供面板布局，如响应式、选项卡式、折叠式和向导，以控制表单组件在面板中的布局方式。 您可以创建自定义面板布局并使它们可供表单作者使用。 有关详细信息，请参 [阅为自适应表单创建自定义布局组件](/help/forms/using/custom-layout-components-forms.md)。
* 您还可以自定义特定的自适应表单组件，如字段和面板布局。

   * 使用 [AEM的](/help/sites-developing/overlays.md) Overlay功能可修改组件的副本。 不建议修改默认组件。
   * 要在/libs中自定义现成自适应表单组件的布局，除了默认布局外，还 [要创建自定义布局组](/help/forms/using/custom-layout-components-forms.md) 件 [](/help/forms/using/layout-capabilities-adaptive-forms.md)。
   * 通过创建自定义构件或外观引入自定义交互活动。 不建议修改默认组件。 有关详细信息，请参阅 [外观框架](/help/forms/using/introduction-widgets.md)。

* 有关 [处理PII数据的建议](/help/forms/using/adaptive-forms-best-practices.md#p-handling-personally-identifiable-information-p) ，请参阅处理个人识别信息。

## 创作自适应表单 {#author-adaptive-forms}

### 使用触屏优化UI进行创作 {#using-touch-optimized-ui-for-authoring}

* 使用提要栏中的对象浏览器快速访问表单层次结构中的深层字段。 您可以使用搜索框在表单或对象树中搜索对象，以便从一个对象导航到另一个对象。
* 要在提要栏中的组件浏览器中查看和编辑组件的属性，请选择该组件，然后单击 ![cmppr-1](assets/cmppr-1.png)。 您还可以双击组件以在属性浏览器中查看其属性。
* 使用键盘快捷键对表单执行快速操作。 请参 [阅AEM Forms键盘快捷键](/help/forms/using/keyboard-shortcuts.md)。

* 建议仅在自适应表单页面中使用自适应表单组件。 这些组件对其父层次具有依赖关系。 因此，请勿在AEM页面中使用它们。

另请参阅创作自适应表单的简介中 [的组件描述和最佳实践](/help/forms/using/introduction-forms-authoring.md)。

### 在自适应表单中使用规则 {#using-rules-in-adaptive-forms}

AEM Forms提供了规则编 [辑器](/help/forms/using/rule-editor.md) ，允许您创建规则以向自适应表单组件添加动态行为。 使用这些规则，您可以评估条件并触发对组件的操作，如显示或隐藏字段、计算值、动态更改下拉列表等。

规则编辑器提供了一个可视编辑器和一个用于编写规则的代码编辑器。 使用代码编辑器模式编写规则时，请考虑以下事项：

* 为表单字段和组件使用有意义的唯一名称，以避免在编写规则时出现任何可能的冲突。
* 使用 `this` 组件的运算符在规则表达式中引用自身。 它可确保规则保持有效，即使组件名称发生更改也是如此。 For example, `field1.valueCommit script: this.value > 10`.

* 在引用其他表单组件时使用组件名称。 使用 `value` 属性获取字段或组件的值。 For example, `field1.value`.

* 按相对唯一的层次结构引用组件，以避免任何冲突。 For example, `parentName.fieldName`.

* 在处理复杂或常用的规则时，请考虑将业务逻辑编写为一个单独的客户端库中的函数，您可以在自适应表单中指定和重用该函数。 客户端库应为自包含库，除jQuery和Endrower.js外，不应具有任何外部依赖关系。 您还可以使用客户端库强制对已提 [交的表单数据进行](/help/forms/using/configuring-submit-actions.md#server-side-revalidation-in-adaptive-form) 服务器端重新验证。
* 自适应表单提供一组API，您可以使用这些API与自适应表单通信并对自适应表单执行操作。 一些关键API如下所示。 有关详细信息，请参 [阅自适应表单的JavaScript库API参考](https://adobe.com/go/learn_aemforms_documentation_63)。

   * `guideBridge.reset()`:重置表单。
   * `guideBridge.submit()`:提交表单。
   * `guideBridge.setFocus(somExp, focusOption, runCompletionExp)`:将焦点设置到字段。
   * `guideBridge.validate(errorList, somExpression, focus)`:验证表单。
   * `guideBridge.getDataXML(options)`:将表单数据作为XML获取。
   * `guideBridge.resolveNode(somExpression)`:获取表单对象。
   * `guideBridge.setProperty(somList, propertyName, valueList)`:设置表单对象的属性。
   * 此外，您还可以使用以下字段属性：

      * `field.value` 更改字段的值。
      * f启 `ield.enabled` 用／禁用字段。
      * `field.visible` 更改字段的可见性。

* 自适应表单作者可能需要编写JavaScript代码才能在表单中构建业务逻辑。 虽然JavaScript功能强大且高效，但它可能会在安全预期上做出妥协。 因此，您必须确保表单作者是可信任的角色，并且在将表单投入生产之前，需要审核和批准JavaScript代码的进程。 管理员可以根据用户组的角色或功能限制对规则编辑器的访问权限。 请参 [阅授予规则编辑器对选定用户组的访问权限](/help/forms/using/rule-editor-access-user-groups.md)。
* 您可以在规则中使用表达式来使自适应表单变为动态表单。 所有表达式都是有效的JavaScript表达式，并使用自适应表单脚本模型API。 这些表达式返回某些类型的值。 有关表达式及其周围的最佳实践的更多信息，请参 [阅自适应表单表达式](/help/forms/using/adaptive-form-expressions.md)。

### 使用主题 {#working-with-themes}

主题自适应允许您创建可跨表单应用的可重用样式，以实现一致的外观和样式。 建议使用主题为表单组件和面板定义样式。 围绕主题的一些最佳实践如下：

* 使用资源库快速应用文本样式、背景和图像。 当样式添加到资源库中时，该样式可用于其他主题，也可用于表单编辑器的样式模式。
* 使用页面级选择器应用全局设置，如字体和页面背景。
* 使用客户端库将现有或高级样式导入到主题中。
* 您可以在表单样式层中覆盖特定字段、面板或按钮的样式。
* 如果某个主题不满足您的样式要求，您可以使用预定义的类（如guideFieldNode、guideFieldLabel、guideFieldWidget和guidePanelNode）跨表单应用通用样式。

有关详细信息，请参阅 [主题](/help/forms/using/themes.md)。

### 优化大型和复杂表单的性能 {#optimizing-performance-of-large-and-complex-forms}

表单作者和最终用户通常在创作模式下或运行时加载大型表单时会遇到性能问题。 随着表单中对象（字段和面板）数量的增加，创作和运行时体验开始降级。 它还防止多个作者同时协作和创作表单。

请考虑以下最佳做法，以克服大型表单的性能问题：

* 建议使用XSD表单数据模型创建自适应表单，即使将XFA转换为自适应表单（如果可能）也是如此。
* 在自适应表单中仅包括那些从用户处捕获信息的字段和面板。 请考虑将静态内容保持为最小，或使用URL在单独的窗口中打开它们。
* 虽然每个表单都是为特定用途而设计的，但大多数表单中都有一些常见的细分。 例如，个人详细信息、地址、雇佣详细信息等。 为常 [见表单元素和章节创建自适应表单片段](/help/forms/using/adaptive-form-fragments.md) ，并跨表单使用它们。 您还可以将现有表单中的面板另存为片段。 片段中的任何更改都会反映在所有关联的自适应表单中。 由于多个作者可以同时处理组成表单的不同片段，因此它促进了协作创作。

   * 与自适应表单类似，建议使用片段容器对话框在客户端库中定义所有片段特定的样式和自定义脚本。 此外，尝试创建不依赖外部对象的自足片段。
   * 避免使用跨片段脚本。 如果片段外有任何您必须引用的对象，请尝试将该对象作为父表单的一部分。 如果该对象仍必须位于另一个片段中，请在脚本中按其名称引用它。

* 使用“保存并恢复并自动保存”定期保存自适应表单，使用户能够稍后重新访问以完成表单。
* 配置片段以松散加载。 在运行时，标记为松散加载的片段仅在需要时才呈现。 它显着缩短了大型表单的加载时间。 在具有可重复面板的片段中也支持该功能。 有关详细信息，请参阅 [配置延迟加载](/help/forms/using/lazy-loading-adaptive-forms.md)。

   * 请勿在响应式网格布局中或在第一个面板中配置片段的延迟加载。
   * 松散加载的片段不支持文件附件和条款和条件组件。
   * 如果延迟加载面板中的值在表单的其他部分中使用，则将该值标记为全局使用值，以便在卸载包含面板时该值可用。
   * 考虑为应根据条件显示或隐藏的片段编写可见性规则。

### 预填自适应表单 {#prefilling-adaptive-forms}

您可以使用从后端获取的数据预填自适应表单字段，以帮助用户快速填写表单并避免键入错误。

* AEM Forms提供预填服务，用于从预定义的数据XML文件读取数据，并使用预填XML文件中的内容预填自适应表单的字段。
* 预填数据XML必须与与自适应表单关联的表单模型的模式兼容。
* 在预 `afBoundedData` 填XML中包 `afUnBoundedData` 括和部分，以在自适应表单中预填绑定字段和未绑定字段。

* 对于基于表单数据模型的自适应表单，AEM表单提供现成的表单数据模型预填服务。 预填充服务查询自适应表单中数据模型对象的数据源并在呈现表单时预填充字段值。
* 您还可以使用文件、crx、服务或http协议预填自适应表单。
* AEM Forms支持自定义预填服务，您可以将其作为OSGi服务插入以预填自适应表单。

有关详细信息，请参阅预 [填自适应表单字段](/help/forms/using/prepopulate-adaptive-form-fields.md)。

### 签名和提交自适应表单 {#signing-and-submitting-adaptive-forms}

自适应表单要求提交操作以处理用户指定的数据。 “提交”操作可确定使用自适应表单对提交的数据执行的任务。

* 自适应表单中有几种现成的提交操作。 有关详细信息，请参 [阅配置提交操作](/help/forms/using/configuring-submit-actions.md)。
* 如果默认的提交操作不符合您的用例，您可以编写自定义提交操作。 有关详细信息，请参 [阅编写自适应表单的自定义提交操作](/help/forms/using/custom-submit-action-form.md)。
* 包括服务器端验证，以防止提交无效的数据。

您可以在自适应表单中利用Adobe Sign的多签名体验。 在自适应表单中配置Adobe Sign时，请考虑以下事项。 有关详细信息，请 [参阅在自适应表单中使用Adobe Sign](/help/forms/using/working-with-adobe-sign.md)。

* 只有在所有签名者都对表单进行了签名后，才会提交启用了Adobe Sign的自适应表单。 表单以“待签名”状态显示，直到表单由所有签名者签名。
* 您可以配置表单内签名体验，或在提交时将签名者重定向到签名页面。
* 根据需要配置顺序或并行签名体验。

### 生成记录文档 {#generating-document-of-record}

记录文档(DoR)是自适应表单的拼合PDF版本，您可以打印、签署或存档它。

* 根据自适应表单所基于的表单数据模型，您可以按如下方式为DoR配置模板：

   * **XFA表单模板**:使用关联的XDP文件作为DoR模板。
   * **XSD架构**:使用关联的XFA模板，该模板使用与自适应表单使用的相同XML架构。
   * **无**:使用自动生成的DoR。

* 直接从自适应表单编辑器的“记录文档”选项卡中配置页眉、页脚、图像、颜色、字体等。
* 使用 `DoRService` 以编程方式生成DoR。
* 从DoR中排除隐藏字段。
* 使用 `afAcceptLang` 请求参数可在其他区域设置中查看DoR。

### 调试和测试自适应表单 {#debugging-and-testing-adaptive-forms}

[AEM Chrome插件是Google Chrome的浏览器扩展](https://adobe-consulting-services.github.io/acs-aem-tools/aem-chrome-plugin/) ，它提供了调试自适应表单的工具。 表单作者和开发人员可以使用这些工具：

* 找出瓶颈并优化表单渲染的性能
* 调试表单中的关键字和bindRef错误
* 启用和配置日志
* 调试表单中的规则和脚本
* 浏览并了解指南Bridge API

有关详细信息，请参 [阅AEM Chrome插件——自适应表单](https://adobe-consulting-services.github.io/acs-aem-tools/aem-chrome-plugin/adaptive-form/)。

Calvin SDK是一个实用程序API，供Adaptive Forms开发人员测试Adaptive Forms。 Calvin SDK构建在 [Hobbes.js测试框架之上](https://docs.adobe.com/docs/en/aem/6-3/develop/ref/test-api/index.html)。 您可以使用框架测试以下内容：

* 自适应表单的再现体验
* 自适应表单的预填体验
* 提交自适应表单的体验
* 表达式规则
* 验证
* 延迟加载

有关详细信息，请参 [阅自动测试自适应表单](/help/forms/using/calvin.md)。

### 验证AEM服务器上的自适应表单 {#validating-adaptive-forms-on-aem-server}

需要服务器端验证，以防止任何尝试绕过客户端上的验证以及任何可能危及数据提交和违反业务规则的行为。 通过加载所需的客户端库在服务器上执行服务器端验证。

* 在客户端库中包含用于验证自适应表单中表达式的函数，并在自适应表单容器对话框中指定客户端库。 有关详细信息，请参 [阅服务器端重新验证](/help/forms/using/configuring-submit-actions.md#p-server-side-revalidation-in-adaptive-form-p)。
* 服务器端验证可验证表单模型。 建议为验证创建单独的客户端库，但不要将它与同一客户端库中的HTML样式和DOM操作等内容混合使用。

### 本地化自适应表单 {#localizing-adaptive-forms}

AEM提供了翻译工作流程，您可以使用这些工作流来本地化自适应表单。 有关信息，请参 [阅使用AEM翻译工作流程本地化自适应表单](/help/forms/using/using-aem-translation-workflow-to-localize-adaptive-forms.md)。

本地化自适应表单时的一些最佳实践如下：

* 将自适应表单片段用于表单中的常见元素并本地化片段。 它确保您对片段进行本地化一次，它反映在使用本地化片段的所有表单中。
* 任何修改（如添加新组件或在本地化表单中应用脚本）都不会自动本地化。 因此，您必须在将表单本地化之前完成表单的定制，以避免多个本地化周期。
* 使用 `afAcceptLang` request参数可覆盖浏览器区域设置，并在指定的区域设置中呈现表单。 例如，以下URL将强制以日语区域设置呈现表单，而不管浏览器设置中指定的区域设置如何：

   `https://[server]:[port]/<contextPath>/<formFolder>/<formName>.html?wcmmode=disabled&afAcceptLang=ja`

* AEM Forms目前支持以英语(en)、西班牙语(es)、法语(fr)、意大利语(it)、德语(de)、日语(ja)、葡萄牙语——巴西语(pt-BR)、中文(zh-CN)、中文——台湾语(zh-TW)和韩语(ko-KR)区域设置的自适应表单内容本地化。 但是，您可以在运行时为自适应表单添加新区域设置支持。 有关详细信息，请参 [阅支持自适应表单本地化的新区域设置](/help/forms/using/supporting-new-language-localization.md)。

## 为生产准备表单项目 {#prepare-forms-project-for-production}

### 添加表单处理服务器 {#adding-forms-processing-server}

您可以配置位于安全区域中防火墙后的AEM Forms服务器的其他实例。 您可以将此实例用于：

* **批处理**:重负载成批重复或计划的作业。 例如，打印语句、生成对应内容和使用文档服务（如PDF Generator、Output和Assembler）。
* **存储PII数据**:将PII数据保存到处理服务器上。 如果您已经使用自定义存储提供程序存储PII数据，则不需要此设置。

### 将项目移至其他环境 {#moving-project-to-another-environment}

您通常需要将AEM项目从一个环境移到另一个环境。 移动时要记住的一些关键事项如下：

* 备份现有客户端库、自定义代码和配置。
* 在新环境中按指定顺序手动部署产品包和修补程序。
* 手动部署特定于项目的代码包和捆绑包，并将它们作为单独的包或捆绑包部署到新的AEM服务器上。
* (仅&#x200B;*限JEE上的AEM Forms*)在Forms Workflow服务器上手动部署LCA和DSC。
* 使 [用“导出](/help/forms/using/import-export-forms-templates.md) -导入”功能将资产移至新环境。 您还可以配置复制代理并发布资产。

### 配置AEM {#configuring-aem}

配置AEM以改进总体性能的一些最佳实践如下：

* 从Felix Console中为JavaScript和CSS启用HTML客户端库压缩。 请参 [阅示例说明的Clientlibs](https://blogs.adobe.com/experiencedelivers/experience-management/clientlibs-explained-example/)。
* 在AEM调度程序上缓存 `/etc.clientlibs/fd` 所有客户端库和任何其他自定义客户端库，以提高已发布表单的响应性和安全性。 有关详细信息，请参 [阅Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html)。

* 请勿缓存 `/content/forms/af/` 和路 `/content/dam/formsanddocuments/*` 径。 有关配置自适应表单缓存的详细信息，请参阅 [缓存自适应表单](/help/forms/using/configure-adaptive-forms-cache.md)。

* 通过Web服务器压缩模块启用HTML。 有关详细信息，请参 [阅AEM Forms服务器的性能调整](/help/forms/using/performance-tuning-aem-forms.md)。
* 增加大型表单的每个请求配置的调用数。 请参 [阅优化大型和复杂表单的性能](/help/forms/using/adaptive-forms-best-practices.md#optimizing-performance-of-large-and-complex-forms)。
* 创建 [由错误处理程序显示的自定义错误页](https://helpx.adobe.com/experience-manager/6-2/sites-developing/customizing-errorhandler-pages.html)。
* 保护AEM Forms服务器。

   * 使用 `nosamplecontent` 运行模式确保生产服务器上没有部署的示例内容和示例用户。 请参 [阅在生产就绪模式下运行AEM](/help/sites-administering/production-ready.md)。

* 将堆大小保持为最小8 GB。 有关其他设置，请参 [阅AEM Forms服务器的性能调整](/help/forms/using/performance-tuning-aem-forms.md)。
* 使用服务用户会话而不是管理员会话来执行服务级别任务。 有关详细信息，请参阅 [服务身份验证](https://sling.apache.org/documentation/the-sling-engine/service-authentication.html)。

>[!VIDEO](https://vimeo.com/)

### 为草稿和提交的表单数据配置外部存储 {#external-storage}

在生产环境中，建议不要将提交的表单数据存储在AEM存储库中。 Forms Portal Store、Store Content和Store PDF提交操作的默认实现将表单数据存储在AEM存储库中。 这些提交操作仅用于演示目的。 此外，默认情况下，“保存并恢复”和“自动保存”功能使用门户存储。 因此，请考虑以下建议：

* **存储草稿数据**:如果您使用自适应表单的“草稿”功能，则应实现自定义服务提供接口(SPI)，以将草稿数据存储在更安全的存储中，如数据库。 有关详细信息，请参 [阅将草稿和提交组件与数据库集成的示例](/help/forms/using/integrate-draft-submission-database.md)。

* **存储提交数据**:如果您使用表单门户提交存储，则应实施自定义SPI以在数据库中存储提交数据。 有关 [示例集成，请参阅将草稿和提交组件与数据库集成](/help/forms/using/integrate-draft-submission-database.md) 的示例。

   您还可以编写一个自定义提交操作，将表单数据和附件存储在安全存储中。 有关更 [多信息，请参阅编写自适应表单的自定义提交操作](/help/forms/using/custom-submit-action-form.md) 。

### 处理个人身份识别信息 {#handling-personally-identifiable-information}

组织面临的一个关键挑战是如何处理个人识别(PII)数据。 有助于处理此类数据的一些最佳实践如下：

* 使用安全的外部存储（如数据库）存储草稿和提交的表单中的数据。 请参 [阅为草稿和提交的表单数据配置外部存储](/help/forms/using/adaptive-forms-best-practices.md#external-storage)。
* 使用“条款和条件”表单组件在启用自动保存之前征得用户的明确同意。 在这种情况下，仅当用户同意条款和条件组件中的条件时，才启用自动保存。

