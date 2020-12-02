---
title: 使用自适应表单的最佳实践
seo-title: 使用自适应表单的最佳实践
description: 解释设置AEM Forms项目、开发自适应表单和优化AEM Forms系统性能的最佳实践。
seo-description: 解释设置AEM Forms项目、开发自适应表单和优化AEM Forms系统性能的最佳实践。
uuid: ed95fc64-56b3-4ea1-a5ba-2e96953fca56
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 43c431e4-5286-4f4e-b94f-5a7451c4a22c
translation-type: tm+mt
source-git-commit: 615b0db6da0986d7a74c42ec0d0e14bad7ede168
workflow-type: tm+mt
source-wordcount: '4296'
ht-degree: 0%

---


# 使用自适应表单的最佳实践 {#best-practices-for-working-with-adaptive-forms}

## 概述 {#overview}

Adobe Experience Manager(AEM)表单可以帮助您将复杂的交易转变为简单、愉悦的数字体验。 但是，它需要协调一致地努力来实施、建立、执行和维护一个高效和富有成效的AEM Forms生态系统。

本文档提供了管理员、作者和开发人员在与AEM Forms协作时可从中受益的准则和建议，尤其是自适应表单组件。 它讨论了从设置表单开发项目到配置、自定义、创作和优化AEM Forms的最佳实践。 这些最佳做法共同有助于AEM Forms生态系统的整体绩效。

此外，以下是一般AEM最佳实践的推荐读法：

* [最佳实践：部署和维护AEM](/help/sites-deploying/best-practices.md)
* [最佳实践：创作内容](/help/sites-authoring/best-practices.md)
* [最佳实践：管理AEM](/help/sites-administering/administer-best-practices.md)
* [最佳实践：开发解决方案](/help/sites-developing/best-practices.md)

## 设置和配置AEM Forms{#set-up-and-configure-aem-forms}

### 设置表单开发项目{#setting-up-forms-development-project}

简化和标准化的项目结构可以显着减少开发和维护工作。 Apache Maven是建立AEM项目时推荐的开放源码工具。

* 使用Apache Maven `aem-project-archetype`为AEM项目创建和管理结构。 它为AEM项目创建推荐的结构和模板。 此外，它还提供构建自动化和更改控制系统以帮助管理项目。

   * 使用主`archetype:generate`命令生成初始结构。
   * 使用maven `eclipse:eclipse`命令生成eclipse项目文件并将项目导入eclipse。

有关详细信息，请参阅[如何使用Apache Maven](/help/sites-developing/ht-projects-maven.md)构建AEM项目。

* FileVault工具或VLT可帮助您将CRX或AEM实例的内容映射到文件系统。 它提供变更控制管理操作，如AEM项目内容的登记和注销。 请参阅[如何使用VLT工具](/help/sites-developing/ht-vlttool.md)。

* 如果您使用Eclipse集成开发环境，则可以使用AEM开发人员工具将Eclipse IDE与AEM实例无缝集成以创建AEM应用程序。 有关详细信息，请参阅[用于Eclipse的AEM开发人员工具](/help/sites-developing/aem-eclipse.md)。

* 请勿在/libs文件夹中存储任何内容或进行任何修改。 在/app文件夹中创建叠加以扩展或覆盖默认功能。

* 创建包以移动内容时，请确保包过滤器路径正确，并且只提及所需的路径。

* 请勿在/libs文件夹中存储任何内容或进行任何修改。 在/app文件夹中创建叠加以扩展或覆盖默认功能。

* 为软件包定义正确的依赖关系，以强制预先确定的安装顺序／顺序。

* 请勿在/libs或/apps中创建任何可引用的节点。

### 计划创作环境{#planning-for-authoring-environment}

设置AEM项目后，请定义用于创作和自定义自适应表单模板和组件的策略。

* 自适应表单模板是一个专门的AEM页面，它定义自适应表单的结构和页眉和页脚信息。 模板具有预配置的自适应表单布局、样式和基本结构。 AEM Forms提供现成的模板和组件，您可以使用这些模板和组件创作自适应表单。 但是，您可以根据需要创建自定义模板和组件。 建议收集您在自适应表单中需要的其他模板和组件的要求。 有关详细信息，请参阅[自定义自适应表单和组件](/help/forms/using/adaptive-forms-best-practices.md#customize-components)。
* AEM Forms允许您根据以下表单模型创建自适应表单。 表单模型充当表单与AEM系统之间数据交换的接口，并为自适应表单内外的数据流提供基于XML的结构。 此外，表单模型以模式和XFA约束的形式对自适应表单施加规则和约束。

   * **无**:使用此选项创建的自适应表单不使用任何表单模型。从这种表单生成的数据XML具有带字段和相应值的平面结构。
   * **XML或JSON模式**:XML和JSON模式表示组织中的后端系统生成或使用数据的结构。您可以将模式与自适应表单关联，并使用其元素将动态内容添加到自适应表单。 模式的元素位于内容浏览器的“数据模型对象”选项卡中，用于创作自适应表单。 您可以拖放模式元素以构建表单。
   * **XFA表单模板**:如果您对基于XFA的HTML5表单有投资，它是理想的表单模型。它提供了一种将基于XFA的表单转换为自适应表单的直接方法。 任何现有的XFA规则都将保留在关联的自适应表单中。 生成的自适应表单支持XFA构造，如验证、事件、属性和模式。
   * **表单数据模型**:如果您希望集成后端系统(如数据库、Web服务和AEM用户用户档案)以预填自适应表单并将提交的表单数据写入后端系统，则它是首选的表单模型。表单数据模型编辑器允许您在表单数据模型中定义和配置实体和服务，您可以使用它创建自适应表单。 有关详细信息，请参阅[AEM Forms数据集成](/help/forms/using/data-integration.md)。

请务必仔细选择不仅符合您的要求，而且扩展您在XFA和XSD资产中的现有投资（如果有）的数据模型。 建议使用XSD模型创建表单模板，因为生成的XML包含由模式定义的XPATH的数据。 使用XSD模型作为表单数据模型的默认选择也有帮助，因为它将表单设计从后端系统分离出来，后端系统处理和消耗数据，并且由于表单字段的一到一映射，它改善了表单的性能。 此外，字段的BindRef可以作为XML中其数据值的XPATH。

有关详细信息，请参阅[创建自适应表单](/help/forms/using/creating-adaptive-form.md)。

* 自适应表单之间有一些常见部分。 您可以识别它们并定义策略来促进内容重用。 自适应表单允许您创建独立的片段并在表单之间重复使用它们。 您还可以将自适应表单中的面板另存为片段。 片段中的任何更改都会反映在所有关联的表单中。 它有助于您缩短创作时间并确保表单之间的一致性。 此外，片段的使用使自适应表单变得轻量，从而改善创作体验，尤其是大型表单。 有关详细信息，请参阅[自适应表单片段](/help/forms/using/adaptive-form-fragments.md)。

### 自定义自适应表单和组件{#customize-components}

* AEM Forms提供现成的自适应表单模板，您可以使用这些模板创建自适应表单。 您还可以创建自己的模板。 AEM提供静态和可编辑模板。

   * 静态模板由开发人员定义和配置。
   * 可编辑的模板由作者使用模板编辑器创建。 模板编辑器允许您定义模板中的基本结构和初始内容。 结构层中的任何修改都会反映在使用该模板的所有表单中。 初始内容可以包括预配置主题、预填服务、提交操作等。 但是，可以使用表单编辑器修改表单的这些设置。 有关详细信息，请参阅[自适应表单模板](/help/forms/using/template-editor.md)。

* 要设置特定字段或面板实例的样式，请使用[内联样式](/help/forms/using/inline-style-adaptive-forms.md)。 或者，您可以在CSS文件中定义类，并在组件的CSS类属性中指定类名。
* 在组件中包含一个客户端库，以便跨使用该组件的自适应表单或片段一致地应用样式。 有关详细信息，请参阅[创建自适应表单页面组件](/help/forms/using/custom-adaptive-forms-templates.md)。
* 通过在自适应表单容器属性的CSS文件路径字段中指定到客户端库的路径，应用在客户端库中定义的样式来选择自适应表单。
* 要创建样式的客户端库，可在“主题编辑器”基clientlib或“表单容器”属性中配置自定义CSS文件。
* 自适应表单提供面板布局，如响应式、选项卡式、折叠式和向导，以控制表单组件在面板中的布局方式。 您可以创建自定义面板布局并使它们可供表单作者使用。 有关详细信息，请参阅[为自适应表单创建自定义布局组件](/help/forms/using/custom-layout-components-forms.md)。
* 您还可以自定义特定的自适应表单组件，如字段和面板布局。

   * 使用AEM的[Overlay](/help/sites-developing/overlays.md)功能可修改组件的副本。 不建议修改默认组件。
   * 要在/libs中自定义现成自适应表单组件的布局，除了[默认布局](/help/forms/using/layout-capabilities-adaptive-forms.md)之外，[还要创建自定义布局组件](/help/forms/using/custom-layout-components-forms.md)。
   * 通过创建自定义构件或外观引入自定义交互活动。 不建议修改默认组件。 有关详细信息，请参阅[外观框架](/help/forms/using/introduction-widgets.md)。

* 有关处理PII数据的建议，请参阅[处理个人可识别信息](/help/forms/using/adaptive-forms-best-practices.md#p-handling-personally-identifiable-information-p)。

## 创作自适应表单{#author-adaptive-forms}

### 使用触屏优化UI进行创作{#using-touch-optimized-ui-for-authoring}

* 使用提要栏中的对象浏览器快速访问表单层次结构中的深层字段。 您可以使用搜索框在表单或对象树中搜索对象，以便从一个对象导航到另一个对象。
* 要在提要栏中的组件浏览器中视图和编辑组件的属性，请选择该组件，然后单击![cmppr-1](assets/cmppr-1.png)。 您还可以多次单击组件，在属性浏览器中视图其属性。
* 使用键盘快捷键对表单执行快速操作。 请参阅[AEM Forms键盘快捷键](/help/forms/using/keyboard-shortcuts.md)。

* 建议仅在自适应表单页面中使用自适应表单组件。 这些组件对其父层次结构具有依赖关系。 因此，请勿在AEM页面中使用它们。

另请参阅[创作自适应表单的简介](/help/forms/using/introduction-forms-authoring.md)中的组件说明和最佳实践。

### 在自适应表单中使用规则{#using-rules-in-adaptive-forms}

AEM Forms提供了一个[规则编辑器](/help/forms/using/rule-editor.md)，它允许您创建规则，将动态行为添加到自适应表单组件。 使用这些规则，您可以评估条件并触发对组件的操作，如显示或隐藏字段、计算值、动态更改下拉列表等。

规则编辑器提供了用于编写规则的可视编辑器和代码编辑器。 使用代码编辑器模式编写规则时，请考虑以下事项：

* 为表单字段和组件使用有意义的唯一名称，以避免在编写规则时出现任何可能的冲突。
* 对组件使用`this`运算符可在规则表达式中引用它自己。 它确保即使组件名称发生更改，规则仍然有效。 例如，`field1.valueCommit script: this.value > 10`。

* 引用其他表单组件时使用组件名称。 使用`value`属性获取字段或组件的值。 例如，`field1.value`。

* 按相对唯一层次结构引用组件以避免任何冲突。 例如，`parentName.fieldName`。

* 处理复杂或常用的规则时，请考虑将业务逻辑编写为单独的客户端库中的函数，您可以在自适应表单中指定和重用这些函数。 客户端库应为自包含库，除jQuery和Downloader.js外，不应具有任何外部依赖关系。 您还可以使用客户端库强制对提交的表单数据执行[服务器端重新验证](/help/forms/using/configuring-submit-actions.md#server-side-revalidation-in-adaptive-form)。
* 自适应表单提供一组API，您可以使用这些API与自适应表单通信并对其执行操作。 一些关键API如下。 有关详细信息，请参阅[适用于Adaptive Forms的JavaScript库API参考](https://adobe.com/go/learn_aemforms_documentation_63)。

   * `guideBridge.reset()`:重置表单。
   * `guideBridge.submit()`:提交表单。
   * `guideBridge.setFocus(somExp, focusOption, runCompletionExp)`:将焦点设置到字段。
   * `guideBridge.validate(errorList, somExpression, focus)`:验证表单。
   * `guideBridge.getDataXML(options)`:将表单数据获取为XML。
   * `guideBridge.resolveNode(somExpression)`:获取表单对象。
   * `guideBridge.setProperty(somList, propertyName, valueList)`:设置表单对象的属性。
   * 此外，您还可以使用以下字段属性：

      * `field.value` 更改字段的值。
      * f `ield.enabled`启用／禁用字段。
      * `field.visible` 更改字段的可见性。

* 自适应表单作者可能需要编写JavaScript代码才能在表单中构建业务逻辑。 虽然JavaScript功能强大且有效，但它可能会在安全预期上做出妥协。 因此，您必须确保表单作者是可信任的角色，在将表单投入生产之前，需要审核和批准JavaScript代码。 管理员可以根据用户组的角色或功能限制对规则编辑器的访问权限。 请参阅[授予规则编辑器对选择用户组的访问权限](/help/forms/using/rule-editor-access-user-groups.md)。
* 您可以在规则中使用表达式来使自适应表单变为动态表单。 所有表达式都是有效的JavaScript表达式，并使用自适应表单脚本模型API。 这些表达式返回某些类型的值。 有关表达式及其最佳实践的详细信息，请参阅[自适应表单表达式](/help/forms/using/adaptive-form-expressions.md)。

### 使用主题{#working-with-themes}

主题自适应功能允许您创建可跨表单应用的可重用样式，以实现一致的外观和样式。 建议使用主题定义表单组件和面板的样式。 围绕主题的一些最佳实践如下：

* 使用资源库快速应用文本样式、背景和图像。 当样式添加到资源库中时，其他主题在表单编辑器的样式模式下也可以使用该样式。
* 使用页面级选择器应用全局设置，如字体和页面背景。
* 使用客户端库将现有或高级样式导入主题。
* 您可以在表单样式层中覆盖特定字段、面板或按钮的样式。
* 如果某个主题不符合您的样式要求，您可以使用预定义的类（如guideFieldNode、guideFieldLabel、guideFieldWidget和guidePanelNode）在表单间应用通用样式。

有关详细信息，请参阅[主题](/help/forms/using/themes.md)。

### 优化大型和复杂表单的性能{#optimizing-performance-of-large-and-complex-forms}

表单作者和最终用户通常在创作模式下或运行时加载大型表单时会遇到性能问题。 随着表单中对象（字段和面板）数量的增加，创作和运行时体验开始会降低。 它还可防止多个作者同时协作和创作表单。

请考虑以下最佳实践，以克服大型表单的性能问题：

* 建议使用XSD表单数据模型创建自适应表单，即使将XFA转换为自适应表单（如果可能）也是如此。
* 在自适应表单中仅包括那些从用户处捕获信息的字段和面板。 请考虑将静态内容保持为最小值，或使用URL在单独的窗口中打开它们。
* 虽然每个表单都是为特定目的而设计的，但大多数表单中有一些常见的细分。 例如，个人详细信息、地址、雇佣详细信息等。 为常见表单元素和章节创建[自适应表单片段](/help/forms/using/adaptive-form-fragments.md)并在表单之间使用它们。 您还可以将现有表单中的面板另存为片段。 片段中的任何更改都会反映在所有关联的自适应表单中。 它促进协作创作，因为多个作者可以同时处理组成表单的不同片段。

   * 与自适应表单相似，建议使用片段容器对话框在客户端库中定义所有片段特定的样式和自定义脚本。 此外，尝试创建不依赖外部对象的自给自足片段。
   * 避免使用跨片段脚本。 如果片段外有任何您必须引用的对象，请尝试将该对象作为父表单的一部分。 如果对象仍必须驻留在另一个片段中，请在脚本中按其名称引用它。

* 使用“保存并恢复并自动保存”定期保存自适应表单，并允许用户以后重新访问以完成表单。
* 配置片段以延迟加载。 在运行时，标记为延迟加载的片段仅在需要时才呈现。 它显着缩短了大型表单的加载时间。 在具有可重复面板的片段中也支持此功能。 有关详细信息，请参阅[配置延迟加载](/help/forms/using/lazy-loading-adaptive-forms.md)。

   * 请勿在响应式网格布局或第一个面板中配置片段延迟加载。
   * 松散加载的片段不支持文件附件和条款和条件组件。
   * 如果在表单的其他部分中使用该值，则将延迟加载面板中的值标记为全局使用值，以便在卸载包含面板时使用该值。
   * 考虑为应根据条件显示或隐藏的片段编写可见性规则。

### 预填自适应表单{#prefilling-adaptive-forms}

您可以使用从后端获取的数据预填自适应表单字段，帮助用户快速填写表单并避免键入错误。

* AEM Forms提供预填服务，从预定义的数据XML文件读取数据，并使用预填XML文件中的内容预填自适应表单的字段。
* 预填数据XML必须与与自适应表单关联的表单模型的模式兼容。
* 在预填XML中包括`afBoundedData`和`afUnBoundedData`部分，以在自适应表单中预填绑定字段和未绑定字段。

* 对于基于表单数据模型的自适应表单，AEM Forms提供现成的表单数据模型预填服务。 预填服务查询自适应表单中数据模型对象的数据源，并在呈现表单时预填字段值。
* 您还可以使用文件、crx、服务或http协议预填自适应表单。
* AEM Forms支持自定义预填服务，您可以将其作为OSGi服务插入以预填自适应表单。

有关详细信息，请参阅[预填自适应表单字段](/help/forms/using/prepopulate-adaptive-form-fields.md)。

### 签署和提交自适应表单{#signing-and-submitting-adaptive-forms}

自适应表单需要提交操作才能处理用户指定的数据。 “提交”操作决定对您使用自适应表单提交的数据执行的任务。

* 自适应表单中有几种现成的提交操作。 有关详细信息，请参阅[配置提交操作](/help/forms/using/configuring-submit-actions.md)。
* 如果默认提交操作不符合您的用例，您可以编写自定义提交操作。 有关详细信息，请参阅[编写自适应表单的自定义提交操作](/help/forms/using/custom-submit-action-form.md)。
* 包括服务器端验证，以防止提交无效的数据。

您可以采用自适应表单来利用Adobe Sign的多签名体验。 在自适应表单中配置Adobe Sign时，请考虑以下事项。 有关详细信息，请参阅[以自适应形式使用Adobe Sign](/help/forms/using/working-with-adobe-sign.md)。

* Adobe Sign启用的自适应表单只有在所有签署者都已签署表单后才能提交。 Forms在表单由所有签名者签名之前一直处于“待签名”状态。
* 您可以在提交时配置表单内签名体验或将签名者重定向到签名页面。
* 根据需要配置顺序或并行签名体验。

### 生成记录{#generating-document-of-record}的文档

记录文档(DoR)是自适应表单的拼合PDF版本，您可以打印、签署或存档。

* 根据自适应表单所基于的表单数据模型，您可以按如下方式为DoR配置模板：

   * **XFA表单模板**:将关联的XDP文件用作DoR模板。
   * **XSD模式**:使用与自适应表单使用的相同XML模式的关联XFA模板。
   * **无**:使用自动生成的DoR。

* 直接从自适应表单编辑器的“记录”选项卡的“文档”中配置页眉、页脚、图像、颜色、字体等。
* 使用`DoRService`以编程方式生成DoR。
* 从DoR中排除隐藏字段。
* 使用`afAcceptLang`请求参数在其他区域设置中视图DoR。

### 调试和测试自适应表单{#debugging-and-testing-adaptive-forms}

[AEM Chrome插件是](https://adobe-consulting-services.github.io/acs-aem-tools/aem-chrome-plugin/) Google Chrome的浏览器扩展，提供调试自适应表单的工具。表单作者和开发人员可以使用这些工具：

* 找出瓶颈并优化表单渲染性能
* 调试表单中的关键字和bindRef错误
* 启用和配置日志
* 调试表单中的规则和脚本
* 浏览并了解指南Bridge API

有关详细信息，请参阅[AEM Chrome插件——自适应表单](https://adobe-consulting-services.github.io/acs-aem-tools/aem-chrome-plugin/adaptive-form/)。

Calvin SDK是供自适应Forms开发人员测试自适应Forms的实用程序API. Calvin SDK构建于[Hobbes.js测试框架](https://docs.adobe.com/docs/en/aem/6-3/develop/ref/test-api/index.html)之上。 您可以使用框架测试以下内容：

* 自适应表单的再现体验
* 自适应表单的预填体验
* 提交自适应表单的体验
* 表达式规则
* 验证
* 延迟加载

有关详细信息，请参阅[自动测试自适应表单](/help/forms/using/calvin.md)。

### 验证AEM服务器{#validating-adaptive-forms-on-aem-server}上的自适应表单

需要进行服务器端验证，以防止任何尝试绕过客户端上的验证，以及任何可能危及数据提交和业务规则违规的行为。 通过加载所需的客户端库，在服务器上执行服务器端验证。

* 在客户端库中包含用于验证自适应表单中表达式的函数，并在自适应表单容器对话框中指定客户端库。 有关详细信息，请参阅[服务器端重新验证](/help/forms/using/configuring-submit-actions.md#p-server-side-revalidation-in-adaptive-form-p)。
* 服务器端验证可验证表单模型。 建议为验证创建单独的客户端库，但不要将它与同一客户端库中的HTML样式和DOM处理等内容混合。

### 将自适应表单定位{#localizing-adaptive-forms}

AEM提供翻译工作流，您可以使用它来本地化自适应表单。 有关信息，请参阅[使用AEM转换工作流本地化自适应表单](/help/forms/using/using-aem-translation-workflow-to-localize-adaptive-forms.md)。

本地化自适应表单时的一些最佳实践如下：

* 将自适应表单片段用于表单中的常见元素，并本地化片段。 它确保您对片段进行一次本地化，它反映在使用本地化片段的所有表单中。
* 任何修改（如添加新组件或在本地化表单中应用脚本）不会自动本地化。 因此，您必须在将表单本地化之前完成表单的定版，以避免多个本地化周期。
* 使用`afAcceptLang`请求参数覆盖浏览器区域设置并在指定区域设置中呈现表单。 例如，以下URL将强制以日语区域设置呈现表单，而不管在浏览器设置中指定的区域设置如何：

   `https://'[server]:[port]'/<contextPath>/<formFolder>/<formName>.html?wcmmode=disabled&afAcceptLang=ja`

* AEM Forms目前支持本地化适应表单内容，语言版本有英语(en)、西班牙语(es)、法语(fr)、意大利语(it)、德语(de)、日语(ja)、巴西葡萄牙语(pt-BR)、中文(zh-CN)、中国台湾(zh-TW)和韩语(ko-KR)。 但是，您可以在运行时为自适应表单添加新区域设置支持。 有关详细信息，请参阅[支持自适应表单的新语言环境本地化](/help/forms/using/supporting-new-language-localization.md)。

## 准备用于生产的表单项目{#prepare-forms-project-for-production}

### 添加表单处理服务器{#adding-forms-processing-server}

您可以配置位于安全区域中防火墙后的AEM Forms服务器的其他实例。 您可以将此实例用于：

* **批处理**:重负荷批量重复或计划的作业。例如，打印语句、生成对应项以及使用文档服务（如PDF Generator、Output和Assembler）。
* **存储PII数据**:在处理服务器上保存PII数据。如果您已使用自定义存储提供程序存储PII数据，则不需要此设置。

### 将项目移到另一个环境{#moving-project-to-another-environment}

您通常需要将AEM项目从一个环境移到另一个。 移动时要记住的一些关键事项如下：

* 备份现有客户端库、自定义代码和配置。
* 在新环境中按指定顺序手动部署产品包和修补程序。
* 手动部署特定于项目的代码包和捆绑包，并作为单独的包或捆绑在新的AEM服务器上。
* (*AEM Forms仅在JEE上*)在Forms Workflow服务器上手动部署LCA和DSC。
* 使用[Export-Import](/help/forms/using/import-export-forms-templates.md)功能将资产移动到新环境。 您还可以配置复制代理并发布资产。
* 升级时，请用新的API和功能替换所有已弃用的API和功能。

### 配置AEM {#configuring-aem}

配置AEM以改进总体性能的一些最佳实践如下：

* 从Felix控制台启用JavaScript和CSS的HTML客户端库压缩。 请参见[Clientlibs，如示例](https://blogs.adobe.com/experiencedelivers/experience-management/clientlibs-explained-example/)说明。
* 将所有客户端库缓存在`/etc.clientlibs/fd`和AEM dispatcher上的任何其他自定义客户端库，以提高已发布表单的响应性和安全性。 有关详细信息，请参阅[ Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html)。

* 不缓存`/content/forms/af/`和`/content/dam/formsanddocuments/*`路径。 有关配置自适应表单缓存的详细信息，请参阅[缓存自适应表单](/help/forms/using/configure-adaptive-forms-cache.md)。

* 通过Web服务器压缩模块启用HTML。 有关详细信息，请参阅[AEM Forms服务器的性能调整](/help/forms/using/performance-tuning-aem-forms.md)。
* 增加大型表单的每个请求配置调用数。 请参阅[优化大型和复杂表单的性能](/help/forms/using/adaptive-forms-best-practices.md#optimizing-performance-of-large-and-complex-forms)。
* 创建由错误处理程序](https://helpx.adobe.com/experience-manager/6-2/sites-developing/customizing-errorhandler-pages.html)显示的[自定义错误页。
* 保护AEM Forms服务器。

   * 使用`nosamplecontent`运行模式确保生产服务器上没有部署示例内容和示例用户。 请参阅[在生产就绪模式下运行AEM](/help/sites-administering/production-ready.md)。

* 将堆大小保持为最小8 GB。 有关其他设置，请参阅[AEM Forms服务器的性能调整](/help/forms/using/performance-tuning-aem-forms.md)。
* 使用服务用户会话而不是管理员会话来执行服务级别任务。 有关详细信息，请参阅[服务身份验证](https://sling.apache.org/documentation/the-sling-engine/service-authentication.html)。

>[!VIDEO](https://vimeo.com/)

### 为草稿和已提交的表单存储配置外部数据{#external-storage}

在生产环境中，建议不要将提交的表单数据存储在AEM存储库中。 Forms门户商店、商店内容和商店PDF提交操作的默认实施将表单数据存储在AEM存储库中。 这些提交操作仅用于演示目的。 此外，默认情况下，“保存并恢复”和“自动保存”功能使用门户存储。 因此，请考虑以下建议：

* **存储草稿数据**:如果您使用自适应表单的“草稿”功能，则应实现自定义服务提供接口(SPI)，以将草稿存储存储在更安全的环境中，如数据库。有关详细信息，请参阅[将草稿和提交组件与数据库集成的示例](/help/forms/using/integrate-draft-submission-database.md)。

* **存储提交数据**:如果您使用表单门户提交存储，则应实现自定义SPI以将提交数据存储在数据库中。有关示例集成，请参阅[将草稿和提交组件与数据库](/help/forms/using/integrate-draft-submission-database.md)集成的示例。

   您还可以编写自定义提交操作，在安全存储中存储表单数据和附件。 有关详细信息，请参阅[编写自适应表单的自定义提交操作](/help/forms/using/custom-submit-action-form.md)。

* **草稿ID的长度**:将自适应表单另存为草稿时，将生成草稿ID以唯一标识草稿。草稿ID字段长度的最小值为26个字符。 Adobe建议将草稿ID长度设置为26个或更多字符。

### 处理个人可识别信息{#handling-personally-identifiable-information}

组织面临的一个主要挑战是如何处理个人身份识别(PII)数据。 帮助您处理此类数据的一些最佳实践如下：

* 使用安全、外部存储（如数据库）存储草稿和提交的表单中的数据。 请参阅[为草稿和提交的表单存储配置外部数据](/help/forms/using/adaptive-forms-best-practices.md#external-storage)。
* 使用“条款和条件”表单组件在启用自动保存之前征得用户的明确同意。 在这种情况下，仅当用户同意“条款和条件”组件中的条件时，才启用自动保存。

