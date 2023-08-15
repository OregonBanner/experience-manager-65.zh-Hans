---
title: AEM Forms中的表单集
seo-title: Form set in AEM Forms
description: 本文介绍了表单集，并说明了如何通过将HTML5表单拼合在一起来创建表单集。 本文还介绍如何将xml数据预填充到表单集，以及如何在流程管理中使用表单集。
seo-description: This article introduces form set and explains how to create form sets by stitching together HTML5 forms. This article also explains how you can prefill xml data to a form set and how you can use form sets in process management.
uuid: a1a2f267-26a9-4f45-bcfc-dbdedad95973
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 80e3eec4-95e0-4731-a0e5-a617e9bcb069
docset: aem65
feature: Mobile Forms
exl-id: 039afdf3-013b-41b2-8821-664d28617f61
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '2813'
ht-degree: 0%

---

# AEM Forms中的表单集{#form-set-in-aem-forms}

## 概述 {#overview}

您的客户通常需要提交多个表单来申请服务或权益。 它需要找到所有相关表单；然后分别填写、提交和跟踪这些表单。 此外，还要求他们跨表单多次填写常见详细信息。 如果涉及大量表单，则整个过程会变得繁琐且容易出错。 在这种情况下，AEM Forms的表单集功能有助于简化用户体验。

表单集是HTML5表单的集合，这些表单分组在一起，作为一组表单提供给最终用户。 当最终用户开始填写表单集时，他们将无缝地从一个表单转换为另一个表单。 最后，用户只需一次单击即可提交所有表单。

AEM Forms为表单作者提供了一个直观的用户界面，用于创建、配置和管理表单集。 作为作者，您可以按照您希望最终用户遵循的特定顺序对表单进行排序。 此外，您还可以对单个表单应用条件或资格表达式，以根据用户输入控制其可见性。 例如，您可以将配偶详细信息表单配置为仅在婚姻状况指定为“已婚”时显示。

此外，您可以配置不同表单中的常用字段以共享常用数据绑定。 在设置了适当的数据绑定后，最终用户只需填写一次在后续表单中自动填写的常用信息。

AEM Forms应用程序也支持表单集，允许字段工作人员离线获取表单集、访问客户、输入数据，并稍后与AEM Forms服务器同步以将表单数据提交到业务流程。

## 创建和管理表单集 {#creating-and-managing-form-set}

您可以将多个XDP或使用设计器创建的表单模板关联到表单集中。 然后，可使用表单集根据用户在初始表单及其用户档案中输入的值有选择地渲染XDP。

使用 [AEM Forms用户界面](../../forms/using/introduction-managing-forms.md) 以管理所有表单、表单集和相关资源。

### 创建表单集 {#create-a-form-set}

要创建表单集，请执行以下操作：

1. 选择Forms > Forms和文档。
1. 选择“创建”>“表单集”。

1. 在“添加属性”页中，添加以下详细信息，然后单击“下一步”。

   * 标题：指定文档的标题。 标题可帮助您识别AEM Forms用户界面中的表单集。
   * 描述：指定有关文档的详细信息。
   * 标记：指定用于唯一标识表单集的标记。 标记有助于搜索表单集。 要创建标记，请在“标记”框中键入新标记名称。
   * 提交URL：指定在表单集独立演绎版(非AEM Forms应用程序用例)的情况下发布所提交数据的URL。 数据将作为带有以下请求参数的multipart/formdata提交到此端点：
   * dataXML：此参数包含提交的表单集数据的XML表示形式。 如果表单集中的所有表单都使用公共架构，则根据该架构生成XML。 否则，XML根标记将包含表单集中每个已填写表单的子标记，该表单包含表单附件的数据。
   * formsetPath： CRXDE中已提交的表单集的路径。
   * HTML渲染配置文件：您可以配置某些选项，如浮动字段、附件和草稿支持（适用于独立表单集演绎版），以自定义表单集的外观、行为和交互。 您可以自定义或扩展现有配置文件以更改任何HTML表单配置文件设置。

   ![表单集：添加属性](assets/createformset1.png)

1. 选择表单屏幕显示可用的XDP表单或XDP文件。 搜索并选择要包含在表单集中的表单，然后单击“添加到表单集”。 如有必要，请再次搜索要添加的表单。 将所有表单添加到表单集后，单击下一步。

   >[!NOTE]
   >
   >确保XDP表单中的字段名称不包含点字符。 否则，任何尝试解析字段的脚本（带有点字符）无法解析它们。

1. 在“配置表单”页中，可以执行以下操作：

   * 表单顺序：拖放表单以对其进行重新排序。 表单顺序定义在AEM Forms应用程序和独立演绎版中向最终用户显示表单的顺序。
   * 表单标识符：为要用于资格表达式的表单指定唯一标识。
   * 数据根：对于表单集中的每个表单，作者可以配置XPATH，其中特定表单的数据位于提交的XML中。 默认情况下，该值为/。 如果表单集中的所有表单都绑定了架构并共享相同的XML架构，则可以更改此值。 建议表单中的每个字段都具有XDP中指定的正确数据绑定。 如果两个不同表单中的字段共享公共数据绑定，则第二个表单中的字段显示来自第一个表单的预填充值。 不要将内部内容相同的两个子表单绑定到同一XML节点。 有关表单集的XML结构的详细信息，请参阅 [为表单集预填充XML](../../forms/using/formset-in-aem-forms.md#p-prefill-xml-for-form-set-p).
   * 合格表达式：指定用于计算布尔值并指示表单集中的表单是否适于填写的JavaScript表达式。 如果为false，则不会要求用户填写表单，甚至不会向用户显示要填写的表单。 通常，表达式基于在此表单之前捕获的字段值。 表达式还包含对表单集API fs.valueOf的调用，以提取用户在表单集的表单的字段中填充的值：

   *fs.valueOf(&lt;form identifier=&quot;&quot;>， &lt;fieldsom expression=&quot;&quot;>) > &lt;value>*

   例如，如果表单集中有两个表单：业务费用和差旅费，则可以在资格表达式字段中为这两个表单添加一个JavaScript代码片段，以检查用户在表单中输入的费用类型。 如果用户选择“业务费用”，则“业务费用”表单将呈现给最终用户。 或者，如果用户选择差旅费，则会向最终用户呈现不同的表单。 有关更多信息，请参阅资格表达式。

   此外，作者还可以选择使用每行右角显示的“删除”图标从表单集中删除表单，或使用“**+**&#x200B;工具栏中的“ ”图标。 此&#39;**+**”图标会将用户引导回向导中的上一步，该步骤用于“选择表单”。 现有选择将得到维护，并且必须使用该页上的添加到表单集图标将所做的任何其他选择添加到表单集。

   ![表单集：配置表单](assets/createformset2.png)

   >[!NOTE]
   >
   >表单集中使用的所有表单都由AEM Forms用户界面管理。

### 管理表单集 {#managing-a-form-set}

创建表单集后，您可以对该表单集执行以下操作：

* 单击：创建表单集并将其列在主资产页面时，您可以单击表单集以查看该表单集。 表单集随即会打开并显示该表单集中的所有表单模板(XDP)。
* 编辑：在选择表单集后单击编辑时，将打开配置表单屏幕，该屏幕如上面创建表单集的步骤中所示。 您可以执行此处所述的所有功能。
* 复制+粘贴：通过此功能，您可以从一个位置复制整个表单集，并将其粘贴到同一位置或任何其他位置或文件夹。
* 下载：您可以下载表单集及其所有依赖项。
* 开始/管理审核：创建表单集后，您可以通过单击“开始审核”来设置其审核。 表单集的审核启动后，管理审核选项即会向用户显示。 在管理审阅屏幕上，您可以更新/结束审阅。 对于添加的审阅，您可以检查审阅并在必要时添加注释。
* 删除：删除完整的表单集。 已删除表单集中的表单保留在存储库中。
* 发布/取消发布：发布/取消发布表单集，以及它包含的所有表单和这些表单的相关资源。
* 预览：预览提供两个选项：作为HTML预览（无数据）和使用示例数据自定义预览。
* 查看/编辑属性：您可以查看/编辑所选表单集的元数据属性。

![createformset3](assets/createformset3.png)

### 编辑表单集 {#edit-a-form-set}

要编辑表单集，请执行以下操作：

1. 选择Forms > Forms和文档。
1. 找到要编辑的表单集。 将鼠标悬停在其上并选择编辑( ![编辑](assets/editicon.png))。
1. 在“配置表单”页中，可以编辑以下内容：

   * 表单顺序
   * 表单标识符
   * 数据根
   * 合格表达式

   您还可以单击相关的“删除”图标以从表单集中删除表单。

## 流程管理中的表单集 {#form-set-in-process-management}

使用AEM Forms Management用户界面创建表单集后，您可以在“起点”中使用表单集，或使用Workbench在“分配任务”活动中使用表单集。

### 在任务或起点中使用表单集 {#using-form-set-in-task-or-start-point}

1. 设计流程时，在“分配任务/起点”的“呈现和数据”部分下，选择 **使用CRX资源**. 此时会显示CRX资产浏览器。

   ![设计流程：使用CRX资产](assets/formsetinprocessmgmt1.png)

1. 选择表单集以筛选AEM存储库(CRX)中的表单集。

   ![设计流程：选择表单资产对话框](assets/formsetinprocessmgmt2.png)

1. 选择表单集，然后单击“确定”。

## 合格表达式 {#eligibility-expressions}

表单集中的合格表达式用于定义和动态控制向用户显示的表单。 例如，仅当用户属于特定年龄组时才显示特定表单。 使用表单管理器指定和编辑合格表达式。

合格表达式可以是返回布尔值的任何有效JavaScript语句。 JavaScript代码片段中的最后一个语句被视为布尔值，该值根据JavaScript代码片段的其余部分（上一行）中的处理来确定表单的资格。 如果表达式的值为true，则表单符合向用户显示的条件。 此类表单称为合格表单。

>[!NOTE]
>
>不执行表单集中第一个表单的资格表达式。 无论合格表达式如何，始终显示第一个表单。

除了标准JavaScript函数之外，表单集还公开fs.valueOf API，此API提供对表单集中表单字段值的访问。 使用此API访问表单集中表单字段的值。 API语法为fs.valueOf (formUid， fieldSOM)，其中：

* formUid（字符串）：表单集中表单的唯一ID。 您可以在表单管理器用户界面中创建表单集时指定它。 默认情况下，这是表单名称。
* fieldSOM（字符串）：采用formUid指定的表单的字段的SOM表达式。 SOM表达式或脚本对象模型表达式用于引用特定文档对象模型(DOM)中的值、属性和方法。 选择字段时，您可以在表单设计器中的“脚本”选项卡下查看它。

>[!NOTE]
>
>formUid和fieldSOM参数都必须为字符串文字。

### 示例 {#examples}

API的有效用法：

`fs.valueOf("form1", "xfa.form.form1.subform1.field1")`

API的用法无效：

```javascript
var formUid = "form1";
 var fieldSOM = "xfa.form.form1.subform1.field1"; fs.valueOf(formUid, fieldSOM);
```

## 为表单集预填充XML {#prefill-xml-for-form-set}

表单集是包含相同或不同架构的多个HTML5表单的集合。 表单集支持使用XML文件预填充表单字段。 您可以将XML文件与表单集关联，以便在打开表单集中的表单时，会预填充表单中的一些字段。

使用表单集URL的dataRef参数指定预填充XML文件。 dataRef参数指定与表单集合并的数据XML文件的绝对路径。

例如，您在表单集中有三个表单（form1、form2和form3），具有以下结构：

form1

字段表单1字段

form2

字段表单2字段

form3

字段表单3字段

每个表单都有一个名为“field”的通用命名字段和一个名为“formfield”的唯一命名字段。

可以使用具有以下结构的XML预填充此表单集：

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
>XML根标记可以具有任何名称，但对应于字段的元素标记必须与字段具有相同的名称。 XML的层次结构必须模拟表单的层次结构，这意味着XML必须具有用于封装子表单的相应标记。

上述XML代码片段显示了表单集的预填充XML是各个表单的预填充XML代码片段的并集。 如果不同表单中的某些字段具有相似的数据层次结构/架构，则会使用相同的值预填充这些字段。 在此示例中，所有三个表单都预填充了公共字段“field”的相同值。 这是一种将数据从一个表单传递到下一个表单的简单方法。 这也可以通过将字段绑定到相同的架构或数据引用来实现。 如果您要根据表单的架构分离表单集数据。 这可以通过在表单集创建期间指定表单的“数据根”属性来实现（默认值为“/”，该值映射到表单集根标记）。

在上一个示例中，如果您为三个表单分别指定数据根“/form1”、“/form2”和“/form3”，则需要使用以下结构的预填充XML：

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
>如果存在两个数据根重叠的表单，或一个表单的元素层次结构与另一个表单的数据根层次结构重叠，则在预填充xml中，将合并重叠元素的值。 提交XML具有与预填充XML相似的结构，但提交XML具有更多的包装器标记以及一些表单集上下文数据标记。

### 预填充XML元素说明 {#prefill-xml-elements-description}

创建预填充XML文件的语法规则：

* parent elements：元素，可以是其父元素，其中null表示该元素可以位于XML的根目录下。
* 基数：描述元素在其父元素内可以使用的次数。
* submitXML：指示元素在提交XML中始终存在(P)还是可选(O)。
* prefillXML：指示元素在预填充XML中是必需的(R)还是可选的(O)。
* 子项：指示哪些元素可以是其子项。

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

基数： [1]

submitXML： P

prefillXML： O

`children: xdp:xdp/rootElement`

子树指示表单集中表单的数据。 只有在表单集元素不存在时，预填充XML中的元素才可选

### XDP：XDP {#xdp-xdp}

`parent elements: fs_data/null`

`cardinality: [0,1]`

`submitXML: O`

`prefillXML: O`

`children: xfa:datasets`

此标记指示HTML5表单XML的开头。 如果预填充XML中存在或没有预填充XML，则会将此内容添加到提交XML中。 可以从预填充XML中删除此标记。

### XFA：数据集 {#xfa-datasets}

`parent elements: xdp:xdp`

`cardinality: [1]`

`submitXML: O`

`prefillXML: O`

`children: xfa:data`

### XFA：DATA {#xfa-data}

`parent elements: xfa:datasets`

`cardinality: [1]`

`submitXML: O`

`prefillXML: O`

`children: rootElement`

### ROOTELEMENT {#rootelement}

`parent elements: xfa:datasets/fs_data/null`

`cardinality: [0,1]`

`submitXML: P`

`prefillXML: O`

`children: controlled by the Forms in Form set`

名称rootElement只是占位符。 实际名称是从表单集中使用的表单中挑选的。 以rootElement开头的子树包含表单集中Forms内字段和子表单的数据。 有多个因素可决定rootElement及其子项的结构。

在预填充XML中，此标记是可选的，但如果缺少此标记，则忽略整个XML。

根元素标记的名称

如果预填充XML中存在根元素，则该元素的名称也会包含在提交XML中。 如果没有预填充xml，则rootElement的名称为表单集中第一个表单的根子表单的名称，该表单的dataRoot属性设置为“/”。 如果没有此类表单，则rootElement名称为 **fs_dummy_root**，这是保留关键词。

## AEM Forms应用程序中的表单集 {#formset-in-workspace-app}

AEM Forms应用程序允许现场工作人员将其移动设备与AEM Forms服务器同步并处理其任务。 通过将数据保存在设备本地，即使设备处于脱机状态，该应用程序也能正常工作。 利用诸如照片之类的注释功能，现场工作人员可以提供准确的信息以集成到业务流程中。

<!-- Update link as it is a 404 - For more information on AEM Forms app, see [AEM Forms app overview](/help/forms/using/mobile-workspace-overview.md).-->

## 已知限制 — 表单集中不完全支持模式 {#known-limitations-patterns-not-fully-supported-in-form-set}

表单集中不完全支持以下数据模式：

<table>
 <tbody>
  <tr>
   <td><strong>表单集中不完全支持模式</strong></td>
   <td><strong>示例</strong></td>
  </tr>
  <tr>
   <td>输入大小和图案大小不匹配</td>
   <td><p>当模式= num{z，zzz}时</p> <p>输入=</p> <p>12,345或</p> <p>1,23</p> </td>
  </tr>
  <tr>
   <td>带括号“(”“)”的Picture子句模式</td>
   <td>数字{(zz，zzz)}</td>
  </tr>
  <tr>
   <td>多个数据模式</td>
   <td>num{zz，zzz} |数字{z，zzz，zzz}</td>
  </tr>
  <tr>
   <td>速记模式 </td>
   <td><p>num.integer{},</p> <p>num.decimal{},</p> <p>数字。%{}，或</p> <p>num.currency{}</p> </td>
  </tr>
 </tbody>
</table>
