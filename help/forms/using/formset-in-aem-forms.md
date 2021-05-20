---
title: 在AEM Forms中设置表单
seo-title: 在AEM Forms中设置表单
description: 本文介绍了表单集，并说明了如何通过将HTML5表单拼合在一起来创建表单集。 本文还介绍如何将xml数据预填充到表单集，以及如何在流程管理中使用表单集。
seo-description: 本文介绍了表单集，并说明了如何通过将HTML5表单拼合在一起来创建表单集。 本文还介绍如何将xml数据预填充到表单集，以及如何在流程管理中使用表单集。
uuid: a1a2f267-26a9-4f45-bcfc-dbdedad95973
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 80e3eec4-95e0-4731-a0e5-a617e9bcb069
docset: aem65
feature: 移动设备表单
exl-id: 039afdf3-013b-41b2-8821-664d28617f61
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2862'
ht-degree: 0%

---

# 在AEM Forms中设置的表单{#form-set-in-aem-forms}

## 概述 {#overview}

客户通常需要提交多个表单才能申请服务或福利。 它涉及找到所有相关表格；并单独填写、提交和跟踪这些内容。 此外，还需要在表单中多次填写常见详细信息。 如果整个过程涉及大量表单，则会变得麻烦且容易出错。 AEM Forms的表单集功能有助于简化此类情况下的用户体验。

表单集是HTML5表单的集合，分组在一起，以单个表单集的形式向最终用户显示。 当最终用户开始填写表单集时，他们会从一个表单无缝地转换到另一个表单。 最后，他们只需单击一次即可提交所有表单。

AEM Forms为表单作者提供了直观的用户界面，用于创建、配置和管理表单集。 作为作者，您可以按您希望最终用户遵循的特定顺序对表单进行排序。 此外，您还可以对单个表单应用条件或资格表达式，以根据用户输入控制其可见性。 例如，您可以将配偶详细信息表单配置为仅在婚姻状态指定为“已婚”时显示。

此外，您还可以配置不同表单中的常用字段以共享常用数据绑定。 在适当的数据绑定到位后，最终用户只需在后续表单中自动填写通用信息一次，即可填写通用信息。

AEM Forms应用程序还支持表单集，允许您的现场员工脱机创建表单集、访问客户、输入数据，并稍后与AEM Forms服务器同步，以将表单数据提交到业务流程。

## 创建和管理表单集{#creating-and-managing-form-set}

可以将使用Designer创建的多个XDP或表单模板关联到表单集中。 然后，可以使用表单集根据用户在初始表单中输入的值及其配置文件有选择地渲染XDP。

使用[AEM Forms用户界面](../../forms/using/introduction-managing-forms.md)管理您的所有表单、表单集和相关资产。

### 创建表单集{#create-a-form-set}

要创建表单集，请执行以下操作：

1. 选择Forms > Forms和文档。
1. 选择创建>表单集。

1. 在添加属性页面中，添加以下详细信息，然后单击下一步。

   * 标题：指定文档的标题。 标题可帮助您识别AEM Forms用户界面中设置的表单。
   * 描述：指定有关文档的详细信息。
   * 标记：指定用于唯一标识表单集的标记。 标记有助于搜索表单集。 要创建标记，请在“标记”框中键入新的标记名称。
   * 提交URL:为表单集的独立呈现(非AEM Forms应用程序用例)指定在其中发布提交数据的URL。 数据将作为具有以下请求参数的multipart/formdata提交到此端点：
   * dataXML:此参数包含已提交表单集数据的XML表示形式。 如果表单集中的所有表单都使用通用架构，则会根据该架构生成XML。 否则，XML根标记将为表单集中每个已填写表单包含子标记，子标记包含表单附件的数据。
   * formsetPath:CRXDE中已提交的表单集路径。
   * HTML渲染配置文件：您可以配置某些选项，如浮动字段、附件和草稿支持（对于独立的表单集呈现），以自定义表单集的外观、行为和交互。 您可以自定义或扩展现有配置文件，以更改任何HTML表单配置文件设置。

   ![表单集：添加属性](assets/createformset1.png)

1. “选择表单”屏幕显示可用的XDP表单或XDP文件。 搜索并选择要包含在表单集中的表单，然后单击添加到表单集。 如有必要，请再次搜索要添加的表单。 将所有表单添加到表单集后，单击下一步。

   >[!NOTE]
   >
   >确保XDP表单中的字段名称不包含点字符。 否则，任何尝试解析字段的脚本（具有点字符）都无法解析它们。

1. 在“配置表单”页面中，您可以执行以下操作：

   * 表单顺序：拖放表单以对其重新排序。 表单顺序定义在AEM Forms应用程序和独立呈现版本中向最终用户显示表单的顺序。
   * 表单标识符：为要在资格表达式中使用的表单指定唯一标识。
   * 数据根：对于表单集中的每个表单，作者都可以配置XPATH，该特定表单的数据位于提交的XML中。 默认情况下，值为/。 如果表单集中的所有表单都绑定了架构，并且共享了相同的XML架构，则可以更改此值。 建议每个表单字段在XDP中指定适当的数据绑定。 如果两个不同表单中的字段共享通用数据绑定，则第二个表单中的字段显示第一个表单中的预填充值。 请勿将具有相同内部内容的两个子表单绑定到同一XML节点。 有关表单集的XML结构的详细信息，请参阅[为表单集预填充XML](../../forms/using/formset-in-aem-forms.md#p-prefill-xml-for-form-set-p)。
   * 资格表达式：指定一个JavaScript表达式，该表达式将计算布尔值并指示表单集中的表单是否符合填写条件。 如果为false，则不会要求用户填写，甚至不会向用户显示要填写的表单。 通常，表达式基于在此表单之前捕获的字段值。 表达式还包含对表单集API fs.valueOf的调用，以提取用户在表单集字段中填写的值：

   *fs.valueOf(&lt;form Identifier=&quot;&quot;>,  &lt;fieldsom expression=&quot;&quot;>)>  &lt;value>*

   例如，如果表单集中有两个表单：业务费用和差旅费用，您可以在资格表达式字段中为这两种表单添加JavaScript代码片段，以检查用户在表单中输入的费用类型。 如果用户选择“业务费用”，则“业务费用”表单会呈现给最终用户。 或者，如果用户选择差旅费用，则会向最终用户呈现其他表单。 有关更多信息，请参阅资格表达式。

   此外，作者还可以选择使用每行右角的“删除”图标从表单集中删除表单，或使用工具栏中的“**+**”图标添加另一组表单。 此“**+**”图标将用户引导回向导中用于“选择表单”的上一步。 将维护现有的选择，并且必须使用该页面上的“添加到表单集”图标将所做的任何其他选择添加到表单集。

   ![表单集：配置表单](assets/createformset2.png)

   >[!NOTE]
   >
   >表单集中使用的所有表单都由AEM Forms用户界面管理。

### 管理表单集{#managing-a-form-set}

创建表单集后，您可以对该表单集执行以下操作：

* 单击：在主资产页面上创建并列出表单集后，您可以单击表单集以查看该表单集。 此时会打开一个表单集，并显示该表单集中的所有表单模板(XDP)。
* 编辑：选择表单集后单击编辑时，将打开配置表单屏幕，该屏幕显示在创建表单集的步骤上方。 您可以执行其中描述的所有功能。
* 复制并粘贴：这样，您就可以从一个位置复制整个表单集，并将其粘贴到同一位置或任何其他位置或文件夹。
* 下载：您可以下载包含其所有依赖项的表单集。
* 开始/管理审阅：创建表单集后，可以单击“开始审阅”以设置其审阅。 开始对表单集进行审核后，将向用户显示“管理审核”选项。 在“管理审阅”屏幕上，您可以更新/结束审阅。 对于您添加的审阅，您可以检查审阅并根据需要添加注释。
* 删除：删除完整的表单集。 已删除表单集中的表单仍保留在存储库中。
* 发布/取消发布：这会发布/取消发布表单集及其包含的所有表单以及这些表单的相关资产。
* 预览：“预览”提供了两个选项：以HTML形式预览（不含数据），以及使用示例数据进行自定义预览。
* 查看/编辑属性：您可以查看/编辑选定表单集的元数据属性。

![createformset3](assets/createformset3.png)

### 编辑表单集{#edit-a-form-set}

要编辑表单集，请执行以下操作：

1. 选择Forms > Forms和文档。
1. 找到要编辑的表单集。 将鼠标悬停在该页面上，然后选择“编辑”(![editicon](assets/editicon.png))。
1. 在“配置表单”页面中，您可以编辑以下内容：

   * 表单顺序
   * 表单标识符
   * 数据根
   * 资格表达式

   您还可以单击相关的删除图标，从表单集中删除表单。

## 进程管理{#form-set-in-process-management}中的表单集

使用AEM Forms管理用户界面创建表单集后，您可以在开始点中使用表单集，或使用工作台分配任务活动。

### 使用任务或起始点{#using-form-set-in-task-or-start-point}中设置的表单

1. 在设计流程时，在分配任务/起点的演示和数据部分下，选择&#x200B;**使用CRX资产**。 出现CRX资产浏览器。

   ![设计流程：使用CRX资产](assets/formsetinprocessmgmt1.png)

1. 选择表单集以在AEM存储库(CRX)中筛选表单集。

   ![设计流程：选择表单资产对话框](assets/formsetinprocessmgmt2.png)

1. 选择表单集并单击“确定”。

## 资格表达式{#eligibility-expressions}

表单集中的资格表达式用于定义和动态控制向用户显示的表单。 例如，仅当用户属于某个特定年龄组时，才显示特定表单。 使用表单管理器指定和编辑资格表达式。

资格表达式可以是任何返回布尔值的有效JavaScript语句。 JavaScript代码片段中的最后一个语句将被视为布尔值，该值会根据JavaScript代码片段其余（前一行）中的处理情况确定表单的资格。 如果表达式的值为true，则表单有资格向用户显示。 此类表单称为合格表单。

>[!NOTE]
>
>不会执行表单集中第一个表单的资格表达式。 无论第一个表单的资格表达式如何，都会始终显示第一个表单。

除了标准JavaScript函数外，表单集还公开了fs.valueOf API，该API提供对表单集中表单字段值的访问。 使用此API访问表单集中表单字段的值。 API语法为fs.valueOf(formUid， fieldSOM)，其中：

* formUid（字符串）：表单集中表单的唯一ID。 您可以在表单管理器用户界面中创建表单集时指定它。 默认情况下，它是表单名称。
* 字段SOM（字符串）：字段的SOM表达式，其格式由formUid指定。 SOM表达式或脚本对象模型表达式用于引用特定文档对象模型(DOM)中的值、属性和方法。 选择字段后，您可以在表单设计器中的脚本选项卡下查看该字段。

>[!NOTE]
>
>formUid和fieldSOM参数都必须是字符串文字。

### 示例 {#examples}

API的有效用法：

`fs.valueOf("form1", "xfa.form.form1.subform1.field1")`

API的使用无效：

```javascript
var formUid = "form1";
 var fieldSOM = “xfa.form.form1.subform1.field1"; fs.valueOf(formUid, fieldSOM);
```

## 为表单集{#prefill-xml-for-form-set}预填充XML

表单集是多个HTML5表单的集合，这些表单具有共同或不同的架构。 表单集支持使用XML文件预填充表单字段。 您可以将XML文件与表单集关联，这样当您在表单集中打开表单时，表单中的某些字段就会被预填充。

预填充XML文件是使用表单集URL的dataRef参数指定的。 dataRef参数指定与表单集合并的数据XML文件的绝对路径。

例如，在具有以下结构的表单集中，您有三个表单（form1、form2和form3）：

form1

字段
form1field

form2

字段
form2field

form3

字段
form3field

每个表单都有一个名为“field”的通用命名字段和一个名为“form&lt;i>field”的唯一命名字段。

您可以使用具有以下结构的XML预填此表单集：

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<formSetRootTag>
 <field>common field value</field>
 <form1field>value1</form1field>
 <form2field>value2</form2field>
 <form3field>value3</form3field>
</formSetRootTag>
```

>[!NOTE]
>
>XML根标记可以具有任何名称，但与字段对应的元素标记必须与字段具有相同的名称。 XML的层次结构必须模拟表单的层次结构，这意味着XML必须具有用于封装子表单的相应标记。

上述XML代码片段显示，表单集的预填充XML是单个表单的预填充XML代码片段的并集。 如果不同表单中的某些字段具有相似的数据层次结构/架构，则这些字段会预填相同的值。 在本例中，所有三个表单都预填充了公用字段“field”的相同值。 这是一种将数据从一种形式转发到另一种形式的简单方法。 也可以通过将字段绑定到同一模式或数据引用来实现这一点。 如果要根据表单的架构来分隔表单集数据。 在表单集创建期间，通过指定表单的“数据根”属性（默认值为“/”，该值映射到表单集根标记），可实现此目的。

在上一个示例中，如果指定数据根：“/form1”、“/form2”和“/form3”分别用于这三种表单，您需要使用以下结构的预填充XML:

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<formSetRootTag>
 <form1>
  <field>field value1</field>
  <form1field>value1</form1field>
 </form1>
 <form2>
  <field>field value2</field>
  <form2field>value2</form2field>
 </form2>
 <form3>
  <field>field value3</field>
  <form3field>value3</form3field>
 </form3>
</formSetRootTag>
```

在表单集中，XML使用以下语法定义了XML架构：

```xml
<formset>
 <fs_data>
  <xdp:xdp xmlns:xdp="https://ns.adobe.com/xdp/">
  <xfa:datasets xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/">
   <xfa:data>
   <rootElement>
    ... data ....
   </rootElement>
   </xfa:data>
  </xfa:datasets>
  </xdp:xdp>
 </fs_data>
 <fs_draft>
  ... private data...
 </fs_draft>
</formset>
```

>[!NOTE]
>
>如果存在两个具有重叠数据根的表单，或者一个表单的元素层次结构与另一个表单的数据根目录层次结构重叠，则在预填充xml中，合并重叠元素的值。 提交XML的结构与预填充XML类似，但提交XML具有更多的包装标签，并且有些表单集上下文数据标签会附加在末尾。

### 预填充XML元素描述{#prefill-xml-elements-description}

用于创建预填充XML文件的语法规则：

* 父元素：元素（可以是其父元素），其中null表示元素可以位于XML的根。
* 基数：描述元素在其父元素中可使用的次数。
* submitXML:指示元素在提交XML中是始终存在(P)还是可选(O)。
* prefillXML:指示预填充XML中是required(R)还是optional(O)元素。
* 子项：指示哪些元素可以是其子元素。

### 表单集 {#formset}

`parent elements:`

`null`

`cardinality: [0,1]`

`submitXML: P`

`prefillXML: O`

`children: fs_data`

表单集XML的根元素。 建议不要将此词用作表单集中任何表单的rootSubform的名称。

### FS_DATA {#fs-data}

`parent elements:`

`formset`

基数：[1]

submitXML:P

prefillXML:O

`children: xdp:xdp/rootElement`

子树表示表单集中表单的数据。 仅当表单集元素不存在时，该元素在预填充XML中是可选的

### XDP:XDP {#xdp-xdp}

`parent elements: fs_data/null`

`cardinality: [0,1]`

`submitXML: O`

`prefillXML: O`

`children: xfa:datasets`

此标记表示HTML5表单XML的开始。 如果提交XML中存在预填充XML，或者没有预填充XML，则会在该XML中添加该XML。 可以从预填充XML中删除此标记。

### XFA：数据集{#xfa-datasets}

`parent elements: xdp:xdp`

`cardinality: [1]`

`submitXML: O`

`prefillXML: O`

`children: xfa:data`

### XFA:DATA {#xfa-data}

`parent elements: xfa:datasets`

`cardinality: [1]`

`submitXML: O`

`prefillXML: O`

`children: rootElement`

### 根部 {#rootelement}

`parent elements: xfa:datasets/fs_data/null`

`cardinality: [0,1]`

`submitXML: P`

`prefillXML: O`

`children: controlled by the Forms in Form set`

名称rootElement只是占位符。 实际名称是从表单集中使用的表单中选取的。 以rootElement开头的子树包含表单集中Forms内的字段和子表单的数据。 有多种因素可决定rootElement及其子元素的结构。

在预填充XML中，此标记是可选的，但如果缺少，则会忽略整个XML。

根元素标记的名称

如果预填充XML中有根元素，则该元素的名称也会在提交XML中采用。 如果没有预填充xml，则rootElement的名称是表单集中第一个表单的根子表单的名称，该表单集的dataRoot属性设置为“/”。 如果没有此类形式，则rootElement名称为&#x200B;**fs_dummy_root**，这是保留的关键字。

## 在AEM Forms应用程序中设置的表单{#formset-in-workspace-app}

AEM Forms应用程序允许现场工作人员将其移动设备与AEM Forms服务器同步并处理其任务。 即使设备处于脱机状态，应用程序也能通过将数据保存在设备本地而正常工作。 使用照片等注释功能，现场工作人员可以提供准确的信息以集成到业务流程中。

<!-- Update link as it is a 404 - For more information on AEM Forms app, see [AEM Forms app overview](/help/forms/using/mobile-workspace-overview.md).-->

## 已知限制 — 表单集{#known-limitations-patterns-not-fully-supported-in-form-set}中不完全支持模式

表单集中不完全支持以下数据模式：

<table>
 <tbody>
  <tr>
   <td><strong>表单集中不完全支持模式</strong></td>
   <td><strong>示例</strong></td>
  </tr>
  <tr>
   <td>输入大小和模式大小不匹配</td>
   <td><p>当pattern= num{z，zzz}时</p> <p>输入=</p> <p>12,345或</p> <p>1,23</p> </td>
  </tr>
  <tr>
   <td>带括号"(" ")"的图片子句模式</td>
   <td>num{(zz，zzz)}</td>
  </tr>
  <tr>
   <td>多个数据模式</td>
   <td>num{zz，zzz} | num{z，zzz，zzz}</td>
  </tr>
  <tr>
   <td>速记模式 </td>
   <td><p>num.integer{},</p> <p>num.decimal{},</p> <p>num.%{}或</p> <p>num.currency{}</p> </td>
  </tr>
 </tbody>
</table>
