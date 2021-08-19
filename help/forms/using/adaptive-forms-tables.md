---
title: 自适应表单中的表
seo-title: 自适应表单中的表
description: 通过AEM Forms中的表组件，您可以在自适应表单中创建对移动设备布局具有响应的表，并且还允许使用XDP表组件。
seo-description: 通过AEM Forms中的表组件，您可以在自适应表单中创建对移动设备布局具有响应的表，并且还允许使用XDP表组件。
uuid: 03436c81-42f0-430f-9e52-14a4ab0e877d
topic-tags: author
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: fc418da9-496f-4a2b-bfe4-2add3ac4f468
docset: aem65
feature: 自适应表单
exl-id: 1a139530-27bd-44da-8bf4-5b375e75cf32
source-git-commit: 840ea373537799af995c3b8ce0c8bf575752775b
workflow-type: tm+mt
source-wordcount: '2430'
ht-degree: 0%

---

# 自适应表单中的表{#tables-in-adaptive-forms}

使用表格是一种有效、简化且有组织的呈现复杂数据的方式。 它有助于用户容易地识别信息并以行和列的有序排列提供输入。 金融服务和政府组织的大多数表单都需要大型数据表来填写数字并执行计算。

AEM Forms在组件浏览器的侧栏中提供了一个表组件，通过该组件，您可以在自适应表单中创建表。 它提供的一些关键功能包括：

* 移动设备上的响应式布局
* 可配置的行和列
* 在运行时动态添加和删除行
* 合并或合并和拆分单元格
* 可由屏幕阅读器访问
* 使用CSS的自定义布局
* 与XDP表组件兼容并映射
* 支持使用XSD复杂类型元素添加行或单元格
* 合并XML文件中的数据

## 创建表 {#create-a-table}

要创建表，请从自适应表单的Sidekick的组件浏览器中拖放表组件。 默认情况下，表包含两列和三行，包括标题行。

![AEM侧栏中的表组件](assets/sidebar-tables.png)

### 关于标题和正文单元格 {#about-header-and-body-cells}

标题单元格是文本字段。 要更改标题的标签，请右键单击标题单元格，然后单击&#x200B;**编辑**。 在“编辑”对话框中，更新&#x200B;**Value**&#x200B;字段中的标签，然后单击&#x200B;**OK**。

默认情况下，主体单元格是文本框。 您可以将正文单元格替换为Sidekick中提供的任何其他自适应表单组件，例如数字框、日期选取器或下拉列表。

例如，下表中的第一个正文行包含文本框、日期选取器和作为单元格的下拉列表组件。

![row-cell-types](assets/row-cell-types.png)

通过选择要合并的单元格，右键单击并选择&#x200B;**Merge**，可以合并两个或多个主体单元格。 此外，您还可以通过右键单击合并的单元格并选择&#x200B;**拆分单元格**&#x200B;来拆分合并的单元格。

### 添加、删除、移动行和列 {#add-delete-move-rows-and-columns}

您可以添加和删除行或列，以及在表中上下移动行。

要添加或删除行或列或移动行，请单击行或列中的任意单元格。 列顶部和行左侧将显示一个下拉菜单。 顶部的菜单提供了添加或删除列的选项，而左侧的菜单则允许您添加、删除或移动行。

* “添加”操作会在下面添加一行，或在所选行或列的右侧添加一列。
* 删除操作将删除所选行或列。
* “上移和下移”操作可上下移动选定的行。

该行的下拉菜单还提供了编辑操作，用于编辑行属性、设置和样式选项。

![add-delete-move-row-column](assets/add-delete-move-row-column.png)

>[!NOTE]
>
>虽然可以在表中添加任意数量的行，但可添加的列数上限为六列。 此外，您也无法从表中删除标题行。

### 添加表描述 {#add-table-description}

您可以添加表的描述，以说明屏幕阅读器如何解释和读出信息。 要添加描述，请执行以下操作：

1. 选择表，然后点按![cmppr](assets/cmppr.png)以在侧栏中查看其属性。
1. 在“辅助功能”选项卡中指定摘要。
1. 单击&#x200B;**完成**。

### 对表中的列进行排序 {#sortcolumnstable}

您可以根据自适应表单中表格中的任意列对数据进行排序。 列中的值可以按升序或降序排序。

排序可应用于包含以下项的表列：

* 静态文本
* 数据模型对象属性
* 静态文本和数据模型对象属性的组合

要对表列应用排序，表列单元格必须包含以下任意组件：数字框、数字步进器、日期输入字段、日期选取器、文本或文本框。

要启用排序，请执行以下操作：

1. 选择表，然后点按![configure_icon](assets/configure_icon.png)(Configure)。 您还可以使用交互式通信Sidekick中的&#x200B;**Content**&#x200B;浏览器选择表。
1. 选择&#x200B;**启用排序**。
1. 点按![done_icon](assets/done_icon.png)以保存表属性。 列标题中的排序图标（上箭头和下箭头）表示排序已启用。

   ![启用排序](assets/enable_sorting_new.png)

1. 切换到&#x200B;**预览**&#x200B;模式以查看输出。 表格会根据表格的第一列自动排序。
1. 单击列标题可根据列对值进行排序。

   带有向上箭头的列标题表示表是根据该列排序的。 此外，列中的值以升序显示。

   ![按升序排序](assets/sorting_ascending_new.png)

   同样，带有向下箭头的列标题表示列中的值以降序显示。

   您还可以在&#x200B;**预览**&#x200B;模式下对表进行更改，然后再次单击列标题以对列值进行排序。

## 设置表的列宽 {#set-column-width}

执行以下步骤为表设置列宽：

1. 在&#x200B;**[!UICONTROL 内容]**&#x200B;选项卡中，点按&#x200B;**[!UICONTROL 表]**&#x200B;组件，然后点按配置（![配置](assets/configure-icon.svg)）图标。

1. 在&#x200B;**[!UICONTROL 列宽]**&#x200B;字段中输入以逗号分隔的值列表，以指定表中每列的相应宽度。 例如，对于包含3列的表，在&#x200B;**[!UICONTROL 列宽]**&#x200B;字段中指定2,4,6作为值会导致将列宽设置为第一列的2/12，将第二列的4/12，将第三列的6/12。 2/12表示，第一列的宽度是表宽度的六分之一。 同样，4/12将第二列宽度设置为表宽度的三分之一，6/12将第三列宽度设置为表宽度的一半。

## 配置表样式 {#configure}

您可以使用页面工具栏中的样式模式来定义表的样式。 执行以下步骤以切换到样式模式并编辑表样式

1. 在页面工具栏的“预览”之前，点按![canvas-drop-down](assets/canvas-drop-down.png) > **Style**。

1. 在侧栏中选择表，然后点按编辑按钮![edit-button](assets/edit-button.png)。
您可以在侧栏中看到样式属性。

![表的样式属性](assets/style-table.png)

>[!NOTE]
>
>您可以通过更改LESS变量的值来更改标题行和正文行的颜色主题。 有关更多信息，请参阅AEM Forms](/help/forms/using/themes.md)中的[主题。

## 动态添加或删除行 {#add-or-delete-a-row-dynamically}

表格为在运行时动态添加或删除行提供开箱即用支持。

1. 选择表行，然后点按![cmppr](assets/cmppr.png)。
1. 在“重复设置”选项卡中，指定最小和最大计数以限制表中的行数。
1. 单击&#x200B;**完成**。

在运行时，您将看到&#x200B;**+**&#x200B;和&#x200B;*-*&#x200B;按钮以添加或删除行。

![add-delete-rows-dynamicaly](assets/add-delete-rows-dynamically.png)

>[!NOTE]
>
>左移动表格布局的标题中不支持动态添加或删除行。

## 表中的表达式 {#expressions-in-a-table}

自适应表单中的表允许您使用JavaScript编写表达式来诱导行为，如显示或隐藏表或行、将所有数字相加并在单元格中显示总数、启用或禁用单元格、验证用户输入等。 这些表达式使用自适应表单脚本模型API。

虽然表和行仅支持可见性表达式，以便根据表达式返回的值控制其可见性，但单元格支持以下表达式：

* **初始化脚本：** 对字段的初始化执行操作。
* **值提交脚本：** 在字段的值发生更改后更改表单的组件。

>[!NOTE]
>
>如果XFA更改/退出脚本也应用于同一字段，则XFA更改/退出脚本将在值提交脚本之前执行。

* **计算表达式**:自动计算字段值。
* **验证表达式**:验证字段。
* **访问表达式**:启用/禁用字段。
* **可见性表达式**:以控制字段和面板的可见性。

表或行的可见性表达式可以在相应编辑组件对话框的面板属性选项卡中定义。 单元格的表达式可在其编辑组件对话框的脚本选项卡中定义。

有关自适应表单类、事件、对象和公共API的完整列表，请参阅[自适应表单的JavaScript库API引用](https://helpx.adobe.com/experience-manager/6-5/forms/javascript-api/index.html)。

## 移动设备布局 {#mobile-layouts}

自适应表单中的表格因其流畅且响应迅速的布局功能，可提供无与伦比的移动设备体验。 AEM Forms为表格提供了两种类型的移动布局 — 左列和可折叠列的标题。

您可以从表编辑组件对话框的样式选项卡中为表配置移动布局。

### 左侧的标题 {#headers-on-left}

在左侧布局的标题中，表中的标题在左侧换位，只有一个单元格显示在标题上。 此布局中的每一行都显示为一个不同的部分。 以下图像将桌面上的表格与移动设备上的表格进行比较。

![桌面视图](assets/desktopview_new.png)

左侧布局上带有标题的表的桌面视图

![左侧的标题](assets/headersontheleft_new.png)

左侧布局上带有标题的表的移动视图

### 可折叠的列布局 {#collapsible-columns-layout}

在可折叠列布局中，表中的列会折叠以显示一列或两列，具体取决于设备大小，而其他列则会折叠。 您可以单击折叠/展开图标以查看表中的其他列。

>[!NOTE]
>
>虽然可折叠列布局已针对移动设备进行了优化，但如果可用的宽度不足以显示表中的所有列，则该布局也将在桌面上工作。

下图比较了表格在具有折叠和展开列的设备上的显示方式。

![折叠列](assets/collapsed-column.png)

表格的折叠列，在移动设备上仅显示两列

![collablise_column](assets/collapsible_column.png)

移动设备上表格的扩展列

## 合并表中的数据 {#merge-data-in-a-table}

自适应表单中的表允许您在运行时使用XML文件中的数据填充表。 数据XML文件可以位于运行AEM Forms服务器的计算机的本地文件系统中，也可以位于CRX存储库中。

让我们以下面的银行交易汇总表为例，我们希望用XML文件中的数据来填充该表。

![数据合并表](assets/data-merge-table.png)

在本例中，为以下对象提供的Element name属性：

* 该行为&#x200B;**Row1**
* 交易日期下的body单元格为&#x200B;**tableItem1**
* “Description”（描述）下的body单元格为&#x200B;**tableItem2**
* Transaction type下的body单元格为&#x200B;**type**
* 以USD表示的“金额”下方的正文单元格为&#x200B;**tableItem3**

包含以下格式的数据的XML文件：

```xml
<?xml version="1.0" encoding="UTF-8"?><afData>
  <afUnboundData>
    <data>
 <typeSelect>0</typeSelect>
 <Row1>
      <tableItem1>2015-01-08</tableItem1>
      <tableItem2>Purchase laptop</tableItem2>
      <type>0</type>
      <tableItem3>12000</tableItem3>
 </Row1>
 <Row1>
      <tableItem1>2015-01-05</tableItem1>
      <tableItem2>Transport expense</tableItem2>
      <type>0</type>
      <tableItem3>120</tableItem3>
 </Row1>
 <Row1>
      <tableItem1>2014-01-08</tableItem1>
      <tableItem2>Laser printer</tableItem2>
      <type>0</type>
      <tableItem3>500</tableItem3>
 </Row1>
 <Row1>
      <tableItem1>2014-12-08</tableItem1>
      <tableItem2>Credit card payment</tableItem2>
      <type>0</type>
      <tableItem3>300</tableItem3>
 </Row1>
 <Row1>
      <tableItem1>2015-01-06</tableItem1>
      <tableItem2>Interest earnings</tableItem2>
      <type>1</type>
      <tableItem3>12000</tableItem3>
 </Row1>
 <Row1>
      <tableItem1>2015-01-05</tableItem1>
      <tableItem2>Payment from a client</tableItem2>
      <type>1</type>
      <tableItem3>500</tableItem3>
 </Row1>
 <Row1>
      <tableItem1>2015-01-08</tableItem1>
      <tableItem2>Food expense</tableItem2>
      <type>0</type>
      <tableItem3>120</tableItem3>
 </Row1>
 </data>
  </afUnboundData>
  <afBoundData>
    <data/>
  </afBoundData>
  <afBoundData/>
</afData>
```

在示例XML中，某行的数据由`<Row1>`标记定义，该标记是表中该行的元素名称。 在`<Row1>`标记中，每个单元格的数据在标记中为其元素名称定义，如`<tableItem1>`、`<tableItem2>`、`<tableItem3>`和`<type>`。

要在运行时将此数据与表合并，我们需要将包含表的自适应表单指向禁用wcmmode的绝对XML位置。 例如，如果自适应表单位于&#x200B;*https://localhost:4502/myForms/bankTransaction.html*，而数据XML文件保存在&#x200B;*C:/myTransactions/bankSummary.xml*，则可以在以下URL查看包含数据的表：

*https://localhost:4502/myForms/bankTransaction.html?dataRef=file:///*

![数据合并表](assets/data-merged-table.png)

## 使用XDP组件和XSD复杂类型 {#use-xdp-components-and-xsd-complex-types}

如果您基于XFA表单模板创建了自适应表单，则AEM内容查找器的“数据模型”选项卡中会提供XFA元素。 您可以以自适应形式拖放这些XFA元素（包括表）。

XFA表元素已映射到表组件，并可在自适应表单中现成使用。 将XDP表移入自适应表单后，将保留该表的所有属性和功能，您可以像使用本机自适应表单表一样对其执行任何操作。 例如，如果XDP表中的某行被标记为可重复，则它也会在拖放到自适应表单中时重复。

此外，您还可以拖放XDP子表单以在表中添加新行。 但是，请注意，删除嵌套子表单不起作用。

>[!NOTE]
>
>没有标题行的XDP表将不会映射到自适应表单表组件。 而是会通过流畅布局映射到自适应表单面板组件。 此外，当您将嵌套表从XDP添加到自适应表单时，外表将转换为面板，同时保留内表。

此外，还可以拖放一组XSD复杂类型元素以创建表行。 将在放置元素的行的正下方创建一个新行。 使用XSD复杂类型元素创建的单元格将维护对XSD的绑定引用。 您还可以将主体单元格拖放到单元格中，从而将其替换为XSD复杂类型元素。

>[!NOTE]
>
>XDP表组件、子表单或XSD复杂类型中的元素数量不能超过行中的单元格数量。 例如，不能在一个只有三个单元格的行中放置四个元素。 这将导致错误。
>
>如果元素数少于行中的单元格数，则新行会先根据元素添加单元格，然后添加默认单元格以填充行中的其余单元格。 例如，如果在一行中放置一组由三个元素组成的元素，这些元素具有四个单元格，则前三个单元格将基于您放置的元素，其余一个单元格将是默认的表单元格。

## 主要注意事项 {#key-considerations}

* 如果在创作基于XSD的表时上下移动行，则在提交表单时生成的数据XML中会看到表行中的一些数据丢失。
* 默认表中的每个正文单元格都有一个与其关联的预定义元素名称。 如果在自适应表单中添加其他表，则新表中的默认主体单元格将与第一个表中的元素名称相同。 在这种情况下，提交表单时生成的数据将仅包含在其中一个表的默认正文单元格中。 因此，请确保重命名默认主体单元格的元素名称，以使它们在各个表中保持唯一，并避免数据丢失。

   请注意，这仅适用于默认的主体单元格。 如果向表中添加更多行或列，则会自动为非默认主体单元格生成唯一的元素名称。
