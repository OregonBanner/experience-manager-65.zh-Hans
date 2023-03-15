---
title: 开发Forms（经典UI）
seo-title: Developing Forms (Classic UI)
description: 了解如何开发表单
seo-description: Learn how to develop forms
uuid: 33859f29-edc5-4bd5-a634-35549f3b5ccf
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 6ee3bd3b-51d1-462f-b12e-3cbe24898b85
docset: aem65
exl-id: f43e9491-aa8f-40af-9800-123695142559
source-git-commit: b886844dc80482ae4aae5fc7ce09e466efecc3bd
workflow-type: tm+mt
source-wordcount: '1940'
ht-degree: 17%

---

# 开发Forms（经典UI）{#developing-forms-classic-ui}

表单的基本结构是：

* 表单开始
* 表单元素
* 表单结尾

所有这些功能都通过一系列默认设置实现 [表单组件](/help/sites-authoring/default-components.md#form)，在标准AEM安装中提供。

除此之外 [开发新组件](/help/sites-developing/developing-components-samples.md) 要在表单上使用，您还可以：

* [使用值预加载表单](#preloading-form-values)
* [预加载（特定）具有多个值的字段](#preloading-form-fields-with-multiple-values)
* [开发新操作](#developing-your-own-form-actions)
* [制定新的限制](#developing-your-own-form-constraints)
* [显示或隐藏特定表单字段](#showing-and-hiding-form-components)

[使用脚本](#developing-scripts-for-use-with-forms) 以根据需要扩展功能。

>[!NOTE]
>
>本文档重点介绍如何使用开发表单 [基础组件](/help/sites-authoring/default-components-foundation.md) 在经典UI中。 Adobe建议利用新的 [核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hans) 和 [隐藏条件](/help/sites-developing/hide-conditions.md) 用于触屏UI中的表单开发。

## 预载表单值 {#preloading-form-values}

表单开始组件为 **加载路径**，指向存储库中节点的可选路径。

加载路径是指向节点属性的路径，用于将预定义值加载到表单上的多个字段中。

这是指定库中节点的路径的可选字段。如果此节点具有与字段名称相匹配的属性，则表单上的相应字段将随这些属性的值预加载。如果不存在任何匹配，则字段将包含默认值。

>[!NOTE]
>
>A [表单操作](#developing-your-own-form-actions) 还可以设置从中加载初始值的资源。 可使用以下方式完成 `FormsHelper#setFormLoadResource` 内部 `init.jsp`.
>
>仅当未设置时，才会从作者在起始表单组件中设置的路径填充表单。

### 预载具有多个值的表单字段 {#preloading-form-fields-with-multiple-values}

各种表单字段还具有 **项目加载路径**，同样是指向存储库中节点的可选路径。

此 **项目加载路径** 是节点属性的路径，用于将预定义值加载到表单上的特定字段中，例如， [下拉列表](/help/sites-authoring/default-components-foundation.md#dropdown-list)， [复选框组](/help/sites-authoring/default-components-foundation.md#checkbox-group) 或 [单选按钮组](/help/sites-authoring/default-components-foundation.md#radio-group).

#### 示例 — 预载具有多个值的下拉列表 {#example-preloading-a-dropdown-list-with-multiple-values}

可以使用选择的值范围配置下拉列表。

此 **项目加载路径** 可用于从存储库中的文件夹访问列表，并将这些列表预加载到字段中：

1. 创建新的sling文件夹( `sling:Folder`)例如， `/etc/designs/<myDesign>/formlistvalues`

1. 添加新属性(例如， `myList`)类型为多值字符串( `String[]`)以包含下拉项目的列表。 内容也可以使用脚本导入，例如通过JSP脚本或shell脚本中的cURL导入。

1. 在中使用完整路径 **项目加载路径** 字段：例如， `/etc/designs/geometrixx/formlistvalues/myList`

请注意，如果 `String[]` 的格式如下所示：

* `AL=Alabama`
* `AK=Alaska`
* 以此类推。

则AEM将生成列表为：

* `<option value="AL">Alabama</option>`
* `<option value="AK">Alaska</option>`

例如，可以在多语言设置中很好地使用此功能。

### 开发您自己的表单操作 {#developing-your-own-form-actions}

一个表单需要一项操作。操作定义随用户数据提交表单时执行的操作。

标准AEM安装中提供了一系列操作，这些操作可在以下位置查看：

`/libs/foundation/components/form/actions`

和 **操作类型** 列表 **表单** 组件：

![chlimage_1-8](assets/chlimage_1-8.png)

本节介绍如何开发您自己的表单操作以包含在此列表中。

您可在下添加自己的操作 `/apps` 如下所示：

1. 创建节点类型 `sling:Folder`. 指定反映要实施的操作的名称。

   例如：

   `/apps/myProject/components/customFormAction`

1. 在此节点上定义以下属性，然后单击 **全部保存** 要保留更改，请执行以下操作：

   * `sling:resourceType`  — 设置为 `foundation/components/form/action`

   * `componentGroup`  — 定义为 `.hidden`

   * 可选：

      * `jcr:title`  — 指定您选择的标题，该标题将显示在下拉选择列表中。 如果未设置，则会显示节点名称

      * `jcr:description`  — 输入所选内容的描述

1. 在文件夹中创建对话框节点：

   1. 添加字段，以便在选择操作后，作者可以编辑表单对话框。

1. 在文件夹中，创建：

   1. 后处理脚本。
脚本的名称为 `post.POST.<extension>`，例如 `post.POST.jsp`
提交表单以处理表单时会调用后脚本，该脚本包含处理从表单到达的数据的代码 
`POST`。

   1. 添加在提交表单时调用的转发脚本。
脚本的名称为 `forward.<extension`>，例如 `forward.jsp`
此脚本可以定义路径。 然后，当前请求将转发到指定的路径。
   必要的调用是 `FormsHelper#setForwardPath` （2种变体）。 典型的情况是执行一些验证或逻辑来查找目标路径，然后转发到该路径，让默认的SlingPOSTservlet在JCR中执行实际存储。

   还可以有另一个servlet执行实际处理，在这种情况下，表单操作和 `forward.jsp` 只能作为“胶水”代码。 例如，以下位置的mail操作 `/libs/foundation/components/form/actions/mail`，可将详细信息转发到 `<currentpath>.mail.html`邮件servlet所在的位置。

   那么：

   * a `post.POST.jsp` 对于完全由操作本身完成的小型操作非常有用
   * 而 `forward.jsp` 在只需要委派时非常有用。

   脚本的执行顺序为：

   * 呈现表单时( `GET`)：

      1. `init.jsp`
      1. 对于所有字段的约束： `clientvalidation.jsp`
      1. 表单的validationRT： `clientvalidation.jsp`
      1. 表单通过加载资源加载（如果已设置）
      1. `addfields.jsp` 在内部渲染时 `<form></form>`
   * 处理表单时 `POST`：

      1. `init.jsp`
      1. 对于所有字段的约束： `servervalidation.jsp`
      1. 表单的validationRT： `servervalidation.jsp`
      1. `forward.jsp`
      1. 如果已设置正向路径( `FormsHelper.setForwardPath`)，转发请求，然后调用 `cleanup.jsp`

      1. 如果未设置转发路径，则调用 `post.POST.jsp` (到此结束，否 `cleanup.jsp` called)




1. 再次在文件夹中（可选）添加：

   1. 用于添加字段的脚本。
脚本的名称为 `addfields.<extension>`，例如 `addfields.jsp`
An 
`addfields` 在写入表单起始HTML后，将立即调用脚本。 这允许操作在表单中添加自定义输入字段或其他此类HTML。

   1. 初始化脚本。
脚本的名称为 `init.<extension>`，例如 `init.jsp`
此脚本在渲染表单时调用。 它可用于初始化操作细节。

   1. 清理脚本。
脚本的名称为 `cleanup.<extension>`，例如 `cleanup.jsp`
此脚本可用于执行清理。

1. 使用 **Forms** parsys中的组件。 此 **操作类型** 下拉列表现在将包含您的新操作。

   >[!NOTE]
   >
   >要查看属于产品一部分的默认操作，请执行以下操作：
   >
   >
   >`/libs/foundation/components/form/actions`

### 开发您自己的表单限制 {#developing-your-own-form-constraints}

可在两个级别施加约束：

* 对象 [单个字段（请参阅以下过程）](#constraints-for-individual-fields)
* 作为 [表单全局验证](#form-global-constraints)

#### 单个字段的约束 {#constraints-for-individual-fields}

您可以为单个字段添加自己的约束(在 `/apps`)，如下所示：

1. 创建节点类型 `sling:Folder`. 指定反映要实施的约束的名称。

   例如：

   `/apps/myProject/components/customFormConstraint`

1. 在此节点上定义以下属性，然后单击 **全部保存** 要保留更改，请执行以下操作：

   * `sling:resourceType`  — 设置为 `foundation/components/form/constraint`

   * `constraintMessage`  — 自定义消息，在提交表单时，如果字段无效（根据约束），将显示该消息

   * 可选：

      * `jcr:title`  — 指定您选择的标题，该标题将显示在选择列表中。 如果未设置，则会显示节点名称
      * `hint`  — 用户有关如何使用字段的其他信息

1. 在此文件夹内，可能需要以下脚本：

   * 客户端验证脚本：脚本的名称为 `clientvalidation.<extension>`，例如 `clientvalidation.jsp`
在渲染表单字段时调用此项。 它可用于创建客户端javascript，以验证客户端上的字段。

   * 服务器验证脚本：脚本的名称为 `servervalidation.<extension>`，例如 `servervalidation.jsp`
在提交表单时会调用此项。 提交字段后，可使用它验证服务器上的字段。

>[!NOTE]
>
>示例约束可见于：
>
>`/libs/foundation/components/form/constraints`

#### 表单全局约束 {#form-global-constraints}

通过配置起始表单组件( `validationRT`)。 例如：

`apps/myProject/components/form/validation`

然后，您可以定义：

* a `clientvalidation.jsp`  — 在字段的客户端验证脚本之后插入
* 和 `servervalidation.jsp`  — 也在对进行单个字段服务器验证后调用 `POST`.

### 显示和隐藏表单组件 {#showing-and-hiding-form-components}

您可以根据表单中其他字段的值配置表单以显示或隐藏表单组件。

当仅在特定条件下才需要表单字段时，更改表单字段的可见性很有用。例如，在反馈表单中，有一个问题询问客户是否希望通过电子邮件向他们发送产品信息。选择“是”时，随即显示一个文本字段让客户键入他们的电子邮件地址。

使用 **编辑显示/隐藏规则** 对话框指定显示或隐藏表单组件的条件。

![showhideeditor](assets/showhideeditor.png)

使用对话框顶部的字段可指定以下信息：

* 您是否指定用于隐藏或显示组件的条件。
* 是否需要满足任何或所有条件才能显示或隐藏组件。

这些字段下显示一个或多个条件。条件将其他表单组件（同一表单上）的值与某个值进行比较。如果字段中的实际值满足条件，那么条件为真。条件包括以下信息：

* 测试表单字段的标题。
* 运算符。
* 要与字段值进行比较的值。

例如，标题为的单选按钮组组件 `Receive email notifications?`* *包含 `Yes` 和 `No` 单选按钮。 标题为的文本字段组件 `Email Address` 使用以下条件，使其在以下情况下可见： `Yes` 已选中：

![光照条件](assets/showhidecondition.png)

在 Javascript 中，条件使用元素名称属性的值引用字段。在上一个示例中，单选按钮组组件的Element Name属性为 `contact`. 下面的代码是该示例等效的 Javascript 代码：

`((contact == "Yes"))`

**要显示或隐藏表单组件，请执行以下操作：**

1. 编辑特定的表单组件。

1. 选择 **显示/隐藏** 以打开 **编辑显示/隐藏规则** 对话框：

   * 在第一个下拉列表中，选择 **显示** 或 **隐藏** 以指定您的条件是否决定显示或隐藏组件。

   * 在顶行末尾的下拉列表中，选择：

      * **所有**  — 如果所有条件都必须为true才能显示或隐藏组件
      * **任意**  — 如果只有一个或多个条件必须为true以显示或隐藏组件
   * 在条件行（默认显示一个）中，选择组件、运算符，然后指定一个值。
   * 如果需要，通过单击 **添加条件**.

   例如：

   ![chlimage_1-9](assets/chlimage_1-9.png)

1. 单击 **确定** 以保存定义。

1. 保存定义后， **编辑规则** 链接显示在旁边 **显示/隐藏** 选项。 单击此链接以打开 **编辑显示/隐藏规则** 对话框进行更改。

   单击 **确定** 以保存所有更改。

   ![chlimage_1-10](assets/chlimage_1-10.png)

   >[!CAUTION]
   >
   >可以查看和测试“显示/隐藏”定义的效果：
   >
   >* 在 **预览** 创作环境上的模式（首次切换到预览时需要重新加载页面）
   >
   >* 在发布环境中


#### 处理损坏的组件引用 {#handling-broken-component-references}

显示/隐藏条件使用元素名称属性值引用表单中的其他组件。当任何条件引用了已删除或已更改Element Name属性的组件时，显示/隐藏配置无效。 出现这种情况时，您需要手动更新条件，否则加载表单时会发生错误。

当“显示/隐藏”配置无效时，该配置仅以JavaScript代码的形式提供。 编辑代码以更正问题。该代码使用最初用于引用组件的Element Name属性。

### 开发用于Forms的脚本 {#developing-scripts-for-use-with-forms}

有关编写脚本时可以使用的API元素的更多信息，请参阅 [与表单相关的javadoc](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/foundation/forms/package-summary.html).

您可以将其用于各种操作，例如在提交表单之前调用服务，并在服务失败时取消服务：

* 定义验证资源类型
* 包含用于验证的脚本：

   * 在您的 JSP 中，调用您的 Web 服务并创建一个包含您的错误消息的 `com.day.cq.wcm.foundation.forms.ValidationInfo` 对象。如果存在错误，将不会发布表单数据。
