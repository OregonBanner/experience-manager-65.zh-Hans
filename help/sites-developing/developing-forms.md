---
title: 开发Forms（经典UI）
seo-title: 开发Forms（经典UI）
description: 了解如何开发表单
seo-description: 了解如何开发表单
uuid: 33859f29-edc5-4bd5-a634-35549f3b5ccf
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 6ee3bd3b-51d1-462f-b12e-3cbe24898b85
docset: aem65
exl-id: f43e9491-aa8f-40af-9800-123695142559
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1952'
ht-degree: 17%

---

# 开发Forms（经典UI）{#developing-forms-classic-ui}

表单的基本结构是：

* 表单开始
* 表单元素
* 表单结尾

所有这些操作都通过一系列默认的[表单组件](/help/sites-authoring/default-components.md#form)实现，这些组件可在标准AEM安装中使用。

除了[开发新组件](/help/sites-developing/developing-components-samples.md)以在表单上使用外，您还可以：

* [预载包含值的表单](#preloading-form-values)
* [预加载（某些）具有多个值的字段](#preloading-form-fields-with-multiple-values)
* [开发新操作](#developing-your-own-form-actions)
* [开发新限制](#developing-your-own-form-constraints)
* [显示或隐藏特定表单字段](#showing-and-hiding-form-components)

[根据需要](#developing-scripts-for-use-with-forms) 使用脚本扩展功能。

>[!NOTE]
>
>本文档重点介绍如何在经典UI中使用[Foundation Components](/help/sites-authoring/default-components-foundation.md)开发表单。 Adobe建议利用新的[核心组件](https://docs.adobe.com/content/help/zh-Hans/experience-manager-core-components/using/introduction.html)和[隐藏条件](/help/sites-developing/hide-conditions.md)在触屏优化UI中进行表单开发。

## 预加载表单值{#preloading-form-values}

表单开始组件为&#x200B;**加载路径**&#x200B;提供了一个字段，该路径是指向存储库中节点的可选路径。

Load Path是用于将预定义值加载到表单上多个字段中的节点属性的路径。

这是指定库中节点的路径的可选字段。如果此节点具有与字段名称相匹配的属性，则表单上的相应字段将随这些属性的值预加载。如果不存在任何匹配，则字段将包含默认值。

>[!NOTE]
>
>[表单操作](#developing-your-own-form-actions)还可以设置从中加载初始值的资源。 这是在`init.jsp`内使用`FormsHelper#setFormLoadResource`完成的。
>
>仅当未设置时，作者才会从开始表单组件中设置的路径填充表单。

### 预加载具有多个值{#preloading-form-fields-with-multiple-values}的表单字段

各种表单字段还具有&#x200B;**项目加载路径**，这同样是指向存储库中节点的可选路径。

**Items Load Path**&#x200B;是节点属性的路径，用于将预定义值加载到表单上的特定字段中，例如[下拉列表](/help/sites-authoring/default-components-foundation.md#dropdown-list)、[复选框组](/help/sites-authoring/default-components-foundation.md#checkbox-group)或[单选按钮组](/help/sites-authoring/default-components-foundation.md#radio-group)。

#### 示例 — 预加载具有多个值{#example-preloading-a-dropdown-list-with-multiple-values}的下拉列表

可以使用选择的值范围配置下拉列表。

**项目加载路径**&#x200B;可用于从存储库中的文件夹访问列表，并将这些列表预载到字段中：

1. 创建新的sling文件夹(`sling:Folder`)
例如，`/etc/designs/<myDesign>/formlistvalues`

1. 添加类型为多值字符串(`String[]`)的新属性（例如`myList`），以包含下拉项目列表。 也可以使用脚本导入内容，例如使用JSP脚本或Shell脚本中的cURL。

1. 在&#x200B;**Items Load Path**字段中使用完整路径：
例如，`/etc/designs/geometrixx/formlistvalues/myList`

请注意，如果`String[]`中的值的格式如下：

* `AL=Alabama`
* `AK=Alaska`
* *以此类推。*

然后，AEM将生成列表，如下所示：

* `<option value="AL">Alabama</option>`
* `<option value="AK">Alaska</option>`

例如，此功能可在多语言设置中得到良好使用。

### 开发您自己的表单操作{#developing-your-own-form-actions}

一个表单需要一项操作。操作定义在随用户数据提交表单时执行的操作。

标准AEM安装提供了一系列操作，这些操作可在下面查看：

`/libs/foundation/components/form/actions`

和&#x200B;**Form**&#x200B;组件的&#x200B;**Action Type**&#x200B;列表中的：

![chlimage_1-8](assets/chlimage_1-8.png)

本节介绍如何开发您自己的表单操作以包含在此列表中。

您可以在`/apps`下添加自己的操作，如下所示：

1. 创建类型为`sling:Folder`的节点。 指定反映要实施的操作的名称。

   例如：

   `/apps/myProject/components/customFormAction`

1. 在此节点上定义以下属性，然后单击&#x200B;**Save All**&#x200B;以保留更改：

   * `sling:resourceType`  — 设置为  `foundation/components/form/action`

   * `componentGroup`  — 定义为  `.hidden`

   * 可选：

      * `jcr:title`  — 指定您选择的标题，该标题将显示在下拉选择列表中。如果未设置，则会显示节点名称

      * `jcr:description`  — 输入您选择的描述

1. 在文件夹中，创建一个对话框节点：

   1. 添加字段，以便作者在选择操作后可以编辑表单对话框。

1. 在文件夹中创建以下任一项：

   1. 帖子脚本。
脚本的名称为`post.POST.<extension>`，例如`post.POST.jsp`
提交表单以处理表单时，将调用post脚本，该脚本包含用于处理从表单到达的数据的代码 
`POST`。

   1. 添加在提交表单时调用的转发脚本。
脚本的名称为`forward.<extension`>，例如`forward.jsp`
此脚本可定义路径。 然后，将当前请求转发到指定的路径。
   必需的调用是`FormsHelper#setForwardPath`（2个变体）。 典型情况是执行一些验证或逻辑，以查找目标路径，然后转发到该路径，从而让默认的SlingPOSTServlet在JCR中执行实际存储。

   还可能有另一个执行实际处理的Servlet，在这种情况下，表单操作和`forward.jsp`将仅充当“glue”代码。 例如，`/libs/foundation/components/form/actions/mail`上的邮件操作会将详细信息转发到邮件servlet所在的`<currentpath>.mail.html`。

   因此：

   * `post.POST.jsp`对于操作本身完全完成的小操作非常有用
   * 而`forward.jsp`在仅需要委派时很有用。

   脚本的执行顺序为：

   * 在呈现表单(`GET`)时：

      1. `init.jsp`
      1. 对于所有字段的约束：`clientvalidation.jsp`
      1. 表单的validationRT:`clientvalidation.jsp`
      1. 如果已设置，则通过加载资源加载表单
      1. `addfields.jsp` 在内部渲染  `<form></form>`
   * 处理`POST`表单时：

      1. `init.jsp`
      1. 对于所有字段的约束：`servervalidation.jsp`
      1. 表单的validationRT:`servervalidation.jsp`
      1. `forward.jsp`
      1. 如果设置了前进路径(`FormsHelper.setForwardPath`)，请转发请求，然后调用`cleanup.jsp`

      1. 如果未设置前向路径，请调用`post.POST.jsp`（此处结束，未调用`cleanup.jsp`）




1. 在文件夹中再次选择添加：

   1. 用于添加字段的脚本。
脚本的名称为`addfields.<extension>`，例如`addfields.jsp`
在写入表单开始的HTML后，会立即调用addfields脚本。 这允许操作在表单中添加自定义输入字段或其他此类HTML。

   1. 初始化脚本。
脚本的名称为`init.<extension>`，例如`init.jsp`
在呈现表单时将调用此脚本。 它可用于初始化操作特定信息。&quot;

   1. 清理脚本。
脚本的名称为`cleanup.<extension>`，例如`cleanup.jsp`
此脚本可用于执行清理。

1. 在parsys中使用&#x200B;**Forms**&#x200B;组件。 **操作类型**&#x200B;下拉列表现在将包含您的新操作。

   >[!NOTE]
   >
   >要查看产品中的默认操作，请执行以下操作：
   >
   >
   >`/libs/foundation/components/form/actions`

### 开发您自己的表单约束{#developing-your-own-form-constraints}

可在两个级别施加限制：

* 对于[单个字段（请参阅以下过程）](#constraints-for-individual-fields)
* 作为[form-global validation](#form-global-constraints)

#### 单个字段{#constraints-for-individual-fields}的约束

您可以为单个字段（在`/apps`下）添加您自己的约束，如下所示：

1. 创建类型为`sling:Folder`的节点。 指定反映要实施的约束的名称。

   例如：

   `/apps/myProject/components/customFormConstraint`

1. 在此节点上定义以下属性，然后单击&#x200B;**Save All**&#x200B;以保留更改：

   * `sling:resourceType`  — 设置为  `foundation/components/form/constraint`

   * `constraintMessage`  — 根据约束条件，在提交表单时，如果字段无效，将显示自定义消息

   * 可选：

      * `jcr:title`  — 指定您选择的标题，该标题将显示在选择列表中。如果未设置，则会显示节点名称
      * `hint`  — 有关如何使用字段的其他信息，请向用户提供

1. 在此文件夹中，您可以需要以下脚本：

   * 客户端验证脚本：
脚本的名称为`clientvalidation.<extension>`，例如`clientvalidation.jsp`
在呈现表单字段时，将调用此调用。 它可用于创建客户端javascript以验证客户端上的字段。

   * 服务器验证脚本：
脚本的名称为`servervalidation.<extension>`，例如`servervalidation.jsp`
在提交表单时，将调用此调用。 该字段可用于在提交后验证服务器上的字段。

>[!NOTE]
>
>示例约束可在以下位置查看：
>
>`/libs/foundation/components/form/constraints`

#### 表单 — 全局约束{#form-global-constraints}

表单全局验证是通过在开始表单组件(`validationRT`)中配置资源类型来指定的。 例如：

`apps/myProject/components/form/validation`

然后，您可以定义：

* `clientvalidation.jsp` — 插入到字段的客户端验证脚本之后
* 和`servervalidation.jsp` — 在对`POST`进行单个字段服务器验证后，也会调用。

### 显示和隐藏表单组件{#showing-and-hiding-form-components}

您可以配置表单，以根据表单中其他字段的值显示或隐藏表单组件。

当仅在特定条件下才需要表单字段时，更改表单字段的可见性很有用。例如，在反馈表单中，有一个问题询问客户是否希望通过电子邮件向他们发送产品信息。选择“是”时，随即显示一个文本字段让客户键入他们的电子邮件地址。

使用&#x200B;**编辑显示/隐藏规则**&#x200B;对话框指定在哪些条件下显示或隐藏表单组件。

![showhideeditor](assets/showhideeditor.png)

使用对话框顶部的字段可指定以下信息：

* 您是否指定用于隐藏或显示组件的条件。
* 是否需要满足任何或所有条件才能显示或隐藏组件。

这些字段下显示一个或多个条件。条件将其他表单组件（同一表单上）的值与某个值进行比较。如果字段中的实际值满足条件，那么条件为真。条件包括以下信息：

* 测试表单字段的标题。
* 运算符。
* 要与字段值进行比较的值。

例如，标题为`Receive email notifications?`* *的单选按钮组组件包含`Yes`和`No`单选按钮。 标题为`Email Address`的文本字段组件使用以下条件，以便在选择`Yes`时可见该组件：

![肖美德](assets/showhidecondition.png)

在 Javascript 中，条件使用元素名称属性的值引用字段。在上一个示例中，单选按钮组组件的“元素名称”属性为`contact`。 下面的代码是该示例等效的 Javascript 代码：

`((contact == "Yes"))`

**要显示或隐藏表单组件，请执行以下操作：**

1. 编辑特定的表单组件。

1. 选择&#x200B;**显示/隐藏**&#x200B;以打开&#x200B;**编辑显示/隐藏规则**&#x200B;对话框：

   * 在第一个下拉列表中，选择&#x200B;**Show**&#x200B;或&#x200B;**Hide** ，以指定条件确定是显示还是隐藏组件。

   * 在顶行末尾的下拉列表中，选择：

      * **all**  — 如果所有条件都必须为true才能显示或隐藏组件
      * **any**  — 如果只有一个或多个条件必须为true才能显示或隐藏组件
   * 在条件行（一个显示为默认值）中，选择组件、运算符，然后指定一个值。
   * 如果需要，可通过单击&#x200B;**Add Condition**&#x200B;添加更多条件。

   例如：

   ![chlimage_1-9](assets/chlimage_1-9.png)

1. 单击&#x200B;**确定**&#x200B;以保存定义。

1. 保存定义后，表单组件属性中的&#x200B;**显示/隐藏**&#x200B;选项旁边会显示一个&#x200B;**编辑规则**&#x200B;链接。 单击此链接可打开&#x200B;**编辑显示/隐藏规则**&#x200B;对话框以进行更改。

   单击&#x200B;**确定**&#x200B;以保存所有更改。

   ![chlimage_1-10](assets/chlimage_1-10.png)

   >[!CAUTION]
   >
   >可以查看和测试显示/隐藏定义的效果：
   >
   >
   >
   >    * 在&#x200B;**预览**&#x200B;模式下（首次切换到预览时需要重新加载页面）
      >
      >    
   * 在发布环境中


#### 处理损坏的组件引用{#handling-broken-component-references}

显示/隐藏条件使用元素名称属性值引用表单中的其他组件。当任何条件引用的组件已删除或已更改Element Name属性时，显示/隐藏配置无效。 出现这种情况时，您需要手动更新条件，否则加载表单时会发生错误。

当显示/隐藏配置无效时，该配置仅作为JavaScript代码提供。 编辑代码以更正问题。代码使用最初用于引用组件的元素名称属性。

### 开发用于Forms的脚本{#developing-scripts-for-use-with-forms}

有关在编写脚本时可使用的API元素的更多信息，请参阅与forms](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/foundation/forms/package-summary.html)相关的[javaoc。

您可以将此操作用于各种操作，例如在提交表单之前调用服务，并在表单失败时取消服务：

* 定义验证资源类型
* 包含验证脚本：

   * 在您的 JSP 中，调用您的 Web 服务并创建一个包含您的错误消息的 `com.day.cq.wcm.foundation.forms.ValidationInfo` 对象。如果存在错误，将不会发布表单数据。
