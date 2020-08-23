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
translation-type: tm+mt
source-git-commit: 80b8571bf745b9e7d22d7d858cff9c62e9f8ed1e
workflow-type: tm+mt
source-wordcount: '1952'
ht-degree: 17%

---


# 开发Forms（经典UI）{#developing-forms-classic-ui}

表单的基本结构是：

* 表单开始
* 表单元素
* 表单结尾

所有这些都通过一系列默认的表单组 [件实现](/help/sites-authoring/default-components.md#form)，标准AEM安装中提供这些组件。

除了开发 [新组件](/help/sites-developing/developing-components-samples.md) （用于表单上）外，您还可以：

* [预载包含值的表单](#preloading-form-values)
* [预载具有多个值的（某些）字段](#preloading-form-fields-with-multiple-values)
* [开发新操作](#developing-your-own-form-actions)
* [开发新约束](#developing-your-own-form-constraints)
* [显示或隐藏特定表单字段](#showing-and-hiding-form-components)

[在必要时](#developing-scripts-for-use-with-forms) ，使用脚本扩展功能。

>[!NOTE]
>
>此文档侧重于在经典UI中 [使用基础组](/help/sites-authoring/default-components-foundation.md) 件开发表单。 Adobe建议在触屏 [优化UI中](https://docs.adobe.com/content/help/zh-Hans/experience-manager-core-components/using/introduction.html) , [利用新的核心组](/help/sites-developing/hide-conditions.md) 件和隐藏条件，进行表单开发。

## 预加载表单值 {#preloading-form-values}

表单开始组件为加载路径提 **供了字段**，这是指向存储库中节点的可选路径。

加载路径是用于将预定义值加载到表单上多个字段的节点属性的路径。

这是指定库中节点的路径的可选字段。如果此节点具有与字段名称相匹配的属性，则表单上的相应字段将随这些属性的值预加载。如果不存在任何匹配，则字段将包含默认值。

>[!NOTE]
>
>表 [单操作](#developing-your-own-form-actions) 还可设置加载初始值时要从的资源。 这是使用内部 `FormsHelper#setFormLoadResource` 完成的 `init.jsp`。
>
>仅当未设置此设置时，作者才会从开始表单组件中设置的路径填充表单。

### Preloading Form Fields with Multiple Values {#preloading-form-fields-with-multiple-values}

各种表单字段还具有“ **项目加载路径**”，也是指向存储库中节点的可选路径。

项目 **加载路径** ，是用于将预定义值加载到表单上的特定字段中的节点属性的路径，例如，下拉 [列表](/help/sites-authoring/default-components-foundation.md#dropdown-list)、复选框组 [或单选按钮组](/help/sites-authoring/default-components-foundation.md#checkbox-group)[](/help/sites-authoring/default-components-foundation.md#radio-group)的。

#### 示例——预载具有多个值的下拉列表 {#example-preloading-a-dropdown-list-with-multiple-values}

可以使用选择的值范围配置下拉列表。

项目 **加载路径** ，可用于从存储库中的文件夹访问列表，并将这些内容预载到字段中：

1. 新建一个sling文件 `sling:Folder`夹()，例如 `/etc/designs/<myDesign>/formlistvalues`

1. 添加多值字符串() `myList`类型的新属性( `String[]`例如)以包含下拉项的列表。 还可以使用脚本导入内容，如使用JSP脚本或shell脚本中的cURL。

1. Use the full path in the **Items Load Path** field:
for example, `/etc/designs/geometrixx/formlistvalues/myList`

请注意，如果中的值 `String[]` 的格式如下：

* `AL=Alabama`
* `AK=Alaska`
* *以此类推。*

然后AEM将生成列表为：

* `<option value="AL">Alabama</option>`
* `<option value="AK">Alaska</option>`

例如，此功能可在多语言设置中得到很好的使用。

### 开发您自己的表单操作 {#developing-your-own-form-actions}

一个表单需要一项操作。操作定义在随用户数据提交表单时执行的操作。

标准AEM安装提供了一系列操作，这些操作可在以下位置查看：

`/libs/foundation/components/form/actions`

和在表 **单组件的** “操作类 **型”列表** 中：

![chlimage_1-8](assets/chlimage_1-8.png)

本节介绍如何开发自己的表单操作以包含在此列表中。

您可以在下面添加您自己的 `/apps` 操作：

1. 创建类型的节点 `sling:Folder`。 指定反映要实施的操作的名称。

   例如：

   `/apps/myProject/components/customFormAction`

1. 在此节点上定义以下属性，然后单 **击“全部保** 存”以保留更改：

   * `sling:resourceType` -设置为 `foundation/components/form/action`

   * `componentGroup` -定义为 `.hidden`

   * 可选：

      * `jcr:title` -指定您选择的标题，此标题将显示在下拉选择列表中。 如果未设置，则显示节点名称

      * `jcr:description` -输入您选择的说明

1. 在文件夹中，创建一个对话框节点：

   1. 添加字段，以便作者在选择操作后可以编辑表单对话框。

1. 在文件夹中，创建以下任一项：

   1. 帖子脚本。
脚本的名称是 `post.POST.<extension>`，例如，提 `post.POST.jsp`交表单以处理表单时将调用后台脚本，它包含处理从表单到达的数据的代码 
`POST`。

   1. 添加提交表单时调用的前向脚本。
脚本的名称为>, `forward.<extension`例如，此脚 `forward.jsp`本可以定义路径。 然后，当前请求将转发到指定路径。
   必要的调用 `FormsHelper#setForwardPath` 是（2个变体）。 典型情况是执行一些验证或逻辑，以查找目标路径，然后转发到该路径，让默认的SlingPOSTservlet在JCR中执行实际存储。

   还可能有另一个Servlet进行实际处理，在这种情况下，表单操作 `forward.jsp` 和只充当“粘合”代码。 例如，上的邮件操作 `/libs/foundation/components/form/actions/mail`将详细信息转 `<currentpath>.mail.html`发到mail servlet所在的位置。

   因此：

   * a对 `post.POST.jsp` 于由操作本身完全完成的小操作很有用
   * 而只 `forward.jsp` 需委托时，此功能非常有用。

   脚本的执行顺序为：

   * 呈现表单( `GET`)时：

      1. `init.jsp`
      1. for all field&#39;s constraints: `clientvalidation.jsp`
      1. 表单的validationRT: `clientvalidation.jsp`
      1. 如果设置了表单，则通过加载资源加载
      1. `addfields.jsp` 在内渲染 `<form></form>`
   * 处理表单时 `POST`:

      1. `init.jsp`
      1. for all field&#39;s constraints: `servervalidation.jsp`
      1. 表单的validationRT: `servervalidation.jsp`
      1. `forward.jsp`
      1. 如果设置了前进路径(), `FormsHelper.setForwardPath`请转发请求，然后调用 `cleanup.jsp`

      1. 如果未设置前进路径，请调 `post.POST.jsp` 用(在此结束，不 `cleanup.jsp` 调用)




1. 再次在文件夹中选择添加：

   1. 用于添加字段的脚本。
脚本的名称是 `addfields.<extension>`，例如， `addfields.jsp`在为表单开始写入HTML后，会立即调用addfields脚本。 这允许操作在表单中添加自定义输入字段或其他类似HTML。

   1. 初始化脚本。
脚本的名称是 `init.<extension>`，例如， `init.jsp`在呈现表单时将调用此脚本。 它可用于初始化操作特定信息。&quot;

   1. 清理脚本。
脚本的名称 `cleanup.<extension>`为，例如， `cleanup.jsp`此脚本可用于执行清除。

1. 在parsys **中使** 用Forms组件。 操 **作类型** (Action Type)下拉框现在将包含您的新操作。

   >[!NOTE]
   >
   >要查看属于产品的默认操作：
   >
   >
   >`/libs/foundation/components/form/actions`

### 开发您自己的表单约束 {#developing-your-own-form-constraints}

可以在两个级别施加限制：

* 对于 [单个字段（请参阅以下过程）](#constraints-for-individual-fields)
* 作为 [表单全局验证](#form-global-constraints)

#### 单个字段的约束 {#constraints-for-individual-fields}

您可以按如下方式为单个字段（在下）添 `/apps`加您自己的约束：

1. 创建类型的节点 `sling:Folder`。 指定反映要实现的约束的名称。

   例如：

   `/apps/myProject/components/customFormConstraint`

1. 在此节点上定义以下属性，然后单 **击“全部保** 存”以保留更改：

   * `sling:resourceType` -设置为 `foundation/components/form/constraint`

   * `constraintMessage` -根据约束条件，在提交表单时显示的自定义消息（如果字段无效）

   * 可选：

      * `jcr:title` -指定您选择的标题，此标题将显示在选择列表中。 如果未设置，则显示节点名称
      * `hint` -用户有关如何使用该字段的其他信息

1. 在该文件夹中，您可以需要以下脚本：

   * 客户端验证脚本：脚本的名称是 `clientvalidation.<extension>`，例如， `clientvalidation.jsp`在呈现表单字段时将调用此名称。 它可用于创建客户端javascript以验证客户端上的字段。

   * 服务器验证脚本：脚本的名称是 `servervalidation.<extension>`，例如提 `servervalidation.jsp`交表单时将调用此名称。 它可用于在提交后验证服务器上的字段。

>[!NOTE]
>
>示例约束可在以下位置查看：
>
>`/libs/foundation/components/form/constraints`

#### 表单全局约束 {#form-global-constraints}

通过在开始表单组件()中配置资源类型来指定表单全局验 `validationRT`证。 例如：

`apps/myProject/components/form/validation`

然后，您可以定义：

* a `clientvalidation.jsp` -在字段的客户端验证脚本之后注入
* 和a `servervalidation.jsp` -也在单个字段服务器验证后调用 `POST`。

### Showing and Hiding Form Components {#showing-and-hiding-form-components}

您可以配置表单以根据表单中其他字段的值显示或隐藏表单组件。

当仅在特定条件下才需要表单字段时，更改表单字段的可见性很有用。例如，在反馈表单中，有一个问题询问客户是否希望通过电子邮件向他们发送产品信息。选择“是”时，随即显示一个文本字段让客户键入他们的电子邮件地址。

Use the **Edit Show/Hide Rules** dialog box to specify the conditions under which a form component is shown or hidden.

![showhideeditor](assets/showhideeditor.png)

使用对话框顶部的字段可指定以下信息：

* 您是否指定用于隐藏或显示组件的条件。
* 是否需要满足任何或所有条件才能显示或隐藏组件。

这些字段下显示一个或多个条件。条件将其他表单组件（同一表单上）的值与某个值进行比较。如果字段中的实际值满足条件，那么条件为真。条件包括以下信息：

* 测试表单字段的标题。
* 运算符。
* 要与字段值进行比较的值。

例如，标题为* *的单选按钮组 `Receive email notifications?`件包含 `Yes` 和单选按钮 `No` 。 A Text Field component with the title of `Email Address` uses the following condition so that it is visible if `Yes` is selected:

![狂魔](assets/showhidecondition.png)

在 Javascript 中，条件使用元素名称属性的值引用字段。In the previous example, the Element Name property of the Radio Group component is `contact`. 下面的代码是该示例等效的 Javascript 代码：

`((contact == "Yes"))`

**显示或隐藏表单组件：**

1. 编辑特定表单组件。

1. 选择 **显示／隐藏** ，打开编辑显 **示／隐藏规则对话框** :

   * 在第一个下拉列表中，选 **择显示** 或隐 **藏** ，以指定条件确定是显示还是隐藏组件。

   * 在顶行末尾的下拉列表中，选择：

      * **all** —— 如果必须满足所有条件才能显示或隐藏组件
      * **any** —— 如果必须满足一个或多个条件才能显示或隐藏组件
   * 在条件行（一个显示为默认值）中，选择组件、运算符，然后指定值。
   * 根据需要，通过单击添加条件来添 **加更多条件**。

   例如：

   ![chlimage_1-9](assets/chlimage_1-9.png)

1. Click **OK** to save the definition.

1. After you saved your definition, an **Edit Rules** link appears next to the **Show / Hide** option in the form component properties. Click this link to open the **Edit Show / Hide Rules** dialog box to make changes.

   Click **OK** to save all changes.

   ![chlimage_1-10](assets/chlimage_1-10.png)

   >[!CAUTION]
   >
   >可以查看和测试显示／隐藏定义的效果：
   >
   >
   >
   >    * 在 **预览** 模式下(首次切换到预览时需要重新加载页面)
      >
      >    
   * 在发布环境


#### Handling Broken Component References {#handling-broken-component-references}

显示/隐藏条件使用元素名称属性值引用表单中的其他组件。当任何条件引用已删除或已更改元素名称属性的组件时，显示／隐藏配置无效。 出现这种情况时，您需要手动更新条件，否则加载表单时会发生错误。

当显示／隐藏配置无效时，该配置仅作为JavaScript代码提供。 编辑代码以纠正问题。代码使用最初用于引用组件的元素名称属性。

### 开发用于Forms的脚本 {#developing-scripts-for-use-with-forms}

有关在编写脚本时可使用的API元素的详细信息，请参阅与 [表单相关的javadoc](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/foundation/forms/package-summary.html)。

您可以将此功能用于以下操作：在提交表单之前调用服务，如果服务失败，则取消服务：

* 定义验证资源类型
* 包含验证脚本：

   * 在您的 JSP 中，调用您的 Web 服务并创建一个包含您的错误消息的 `com.day.cq.wcm.foundation.forms.ValidationInfo` 对象。如果存在错误，将不会发布表单数据。
