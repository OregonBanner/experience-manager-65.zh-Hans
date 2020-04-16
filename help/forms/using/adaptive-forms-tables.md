---
title: 自适应表单中的表
seo-title: 自适应表单中的表
description: 通过AEM Forms中的表组件，您可以在自适应表单中创建对移动布局有响应的表，还允许使用XDP表组件。
seo-description: 通过AEM Forms中的表组件，您可以在自适应表单中创建对移动布局有响应的表，还允许使用XDP表组件。
uuid: 03436c81-42f0-430f-9e52-14a4ab0e877d
topic-tags: author
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: fc418da9-496f-4a2b-bfe4-2add3ac4f468
docset: aem65
translation-type: tm+mt
source-git-commit: f9389a06f9c2cd720919486765cee76257f272c3

---


# 自适应表单中的表{#tables-in-adaptive-forms}

使用表是一种有效、简化和有组织的呈现复杂数据的方法。 它帮助用户容易地识别信息并以行和列的有序排列提供输入。 金融服务和政府机构的大多数表单都需要大型数据表来填写数字和执行计算。

AEM Forms在组件浏览器的提要栏中提供一个表组件，允许您在自适应表单中创建表。 它提供的一些关键功能包括：

* 移动设备上的响应式布局
* 可配置的行和列
* 在运行时动态添加和删除行
* 合并或合并和拆分单元格
* 屏幕阅读器可访问
* 使用CSS的自定义布局
* 与XDP表组件兼容并映射
* 支持使用XSD复杂类型元素添加行或单元格
* 从XML文件合并数据

## 创建表 {#create-a-table}

要创建表，请从自适应表单的Sidekick中的组件浏览器中拖放表组件。 默认情况下，表包含两列和三行，包括标题行。

![AEM提要栏中的表组件](assets/sidebar-tables.png)

### 关于标题和正文单元格 {#about-header-and-body-cells}

标题单元格是文本字段。 要更改标题的标签，请右键单击标题单元格，然后单击“编 **辑”**。 在“编辑”对话框中，更新“值”字段中的标 **签** ，然后单击“ **确定”**。

主体单元格默认为文本框。 您可以将正文单元格替换为Sidekick中可用的任何其他自适应表单组件，如数字框、日期选取器或下拉列表。

例如，下表中的第一个正文行包括文本框、日期选取器和作为单元格的下拉列表组件。

![行单元格类型](assets/row-cell-types.png)

通过选择要合并的单元格，右键单击并选择“合并”，可以合并两个或多个正文单元 **格**。 此外，您还可以通过右键单击合并的单元格并选择拆分单元格来拆 **分该单元格**。

### 添加、删除、移动行和列 {#add-delete-move-rows-and-columns}

您可以添加和删除行或列，并在表中上下移动行。

要添加或删除行或列或移动行，请单击行或列中的任意单元格。 列顶部和行左侧将显示一个下拉菜单。 顶部的菜单提供添加或删除列的选项，而左侧的菜单允许您添加、删除或移动行。

* 添加操作会在选定行或列的右侧添加一行或一列。
* 删除操作将删除选定的行或列。
* “上移”和“下移”操作可上移和下移选定行。

该行的下拉菜单还提供了编辑操作，用于编辑行属性、设置和样式选项。

![add-delete-move-row-column](assets/add-delete-move-row-column.png)

>[!NOTE]
>
>虽然可以在表中添加任意数量的行，但最多可添加的列数为6。 此外，您也不能从表中删除标题行。

### 添加表说明 {#add-table-description}

您可以添加表的说明来说明屏幕阅读器如何解释和读出信息。 要添加说明，请执行以下操作：

1. 选择表并点按 ![cmppr](assets/cmppr.png) ，以在提要栏中查看其属性。
1. 在“辅助功能”选项卡中指定摘要。
1. 单击&#x200B;**完成**。

### 对表中的列进行排序 {#sortcolumnstable}

您可以根据自适应表单中表中的任意列对数据进行排序。 列中的值可以按升序或降序排序。

可以将排序应用于包含以下内容的表列：

* 静态文本
* 数据模型对象属性
* 静态文本和数据模型对象属性的组合

要对表列应用排序，表列单元格必须包含以下任何组件：数字框、数字步进器、日期输入字段、日期选取器、文本或文本框。

要启用排序，请执行以下操作：

1. 选择表并点按( ![](assets/configure_icon.png) 配置)。 您还可以使用交互式通信Sidekick中 **的** “内容”浏览器选择表。
1. 选择 **启用排序**。
1. 点 ![](assets/done_icon.png) 按以保存表属性。 列标题中的排序图标（向上和向下箭头）表示已启用排序。

   ![启用排序](assets/enable_sorting_new.png)

1. 切换到 **预览** 模式以视图输出。 表会根据表的第一列自动排序。
1. 单击列标题可根据列对值进行排序。

   带有向上箭头的列标题表示表将根据该列进行排序。 此外，列中的值会按升序显示。

   ![按升序排序](assets/sorting_ascending_new.png)

   同样，带有向下箭头的列标题表示列中的值以降序显示。

   您还可以在预览模式下对表进行 **更改** ，然后再次单击列标题以对列值进行排序。

## 配置表样式 {#configure}

您可以使用页面工具栏中的样式模式为表定义样式。 执行以下步骤切换到样式模式并编辑表样式

1. 在页面工具栏中，在预览之前，点 ![按画布下拉框](assets/canvas-drop-down.png) > **样式**。

1. 在提要栏中，选择表，然后点按编辑按 ![钮edit-button](assets/edit-button.png)。
您可以在提要栏中查看样式属性。

![表的样式属性](assets/style-table.png)

>[!NOTE]
>
>您可以通过更改LESS变量的值来更改标题行和正文行的颜色主题。 有关详细信息，请参 [阅AEM Forms中的主题](/help/forms/using/themes.md)[](/help/forms/using/creating-custom-adaptive-form-themes.md)。

## 动态添加或删除行 {#add-or-delete-a-row-dynamically}

表提供了开箱即用的支持，可在运行时动态添加或删除行。

1. 选择表行并点按 ![cmppr](assets/cmppr.png)。
1. 在“重复设置”选项卡中，指定最小和最大计数以限制表中的行数。
1. 单击&#x200B;**完成**。

在运行时，您将看到 **+***和——按* 钮来添加或删除行。

![add-delete-rows-dynamically](assets/add-delete-rows-dynamically.png)

>[!NOTE]
>
>左侧移动表布局的标题中不支持动态添加或删除行。

## 表达式表 {#expressions-in-a-table}

自适应表单中的表允许您使用JavaScript编写表达式，以感应诸如显示或隐藏表或行、将所有数字加起来并显示单元格中的总数、启用或禁用单元格、验证用户输入等行为。 这些表达式使用自适应表单脚本模型API。

虽然表和行仅支持可视性表达式以根据表达式返回的值控制其可见性，但单元格支持以下表达式:

* **初始化脚本：** 对字段的初始化执行操作。
* **值提交脚本：** 更改字段值后表单的组件。

>[!NOTE]
>
>如果XFA更改／退出脚本也应用于同一字段，则XFA更改／退出脚本在“值提交”脚本之前执行。

* **计算表达式**:自动计算字段的值。
* **验证表达式**:来验证字段。
* **访问表达式**:启用／禁用字段。
* **可见性表达式**:以控制字段和面板的可见性。

表或行的可见性表达式可以在相应编辑组件对话框的面板属性选项卡中定义。 单元格的表达式可在其“编辑”组件对话框的“脚本”选项卡中定义。

有关自适应表单类、事件、对象和公共API的完整列表，请参阅自适应表单的 [JavaScript库API参考](https://helpx.adobe.com/aem-forms/6/javascript-api/index.html)。

## 移动布局 {#mobile-layouts}

自适应表单中的表格因其流畅的响应式布局而提供了无与伦比的移动设备体验。 AEM Forms优惠了两种类型的表移动布局——左侧的标题和可折叠列。

您可以从表的编辑组件对话框的样式选项卡中为表配置移动布局。

### Headers on left {#headers-on-left}

在左侧布局的标题中，表格中的标题在左侧变换，只有一个单元格显示在标题上。 此布局中的每行显示为一个不同的部分。 以下图像将桌面上的表格与移动设备上的表格进行比较。

![桌面视图](assets/desktopview_new.png)

桌面视图左侧布局带有标题的表

![左侧的标题](assets/headersontheleft_new.png)

移动视图左侧布局带有标题的表

### 可折叠列布局 {#collapsible-columns-layout}

在“可折叠”列布局中，表中的列会折叠以显示一列或两列，具体取决于设备大小，而其他列则会折叠。 单击折叠／展开图标可视图表中的其他列。

>[!NOTE]
>
>虽然可折叠列布局针对移动设备进行了优化，但如果可用宽度不足以显示表中的所有列，它也将在桌面上工作。

以下图像比较了表格在具有折叠列和展开列的设备上的外观。

![collapsed-column](assets/collapsed-column.png)

表格的折叠列，在移动设备上仅显示两列

![collapsible_column](assets/collapsible_column.png)

移动设备上表的扩展列

## 将数据合并到表中 {#merge-data-in-a-table}

自适应表单中的表允许您使用XML文件中的数据在运行时填充表。 数据XML文件可以驻留在运行AEM Forms服务器的计算机的本地文件系统中或CRX存储库中。

让我们举下面的银行交易汇总表为例，我们希望用XML文件中的数据填充该表。

![数据合并表](assets/data-merge-table.png)

在此示例中，为以下对象使用元素名称属性：

* 第一行是第 **一行**
* 事务日期下的正文单元格是 **tableItem1**
* “说明”下的正文单元格 **是tableItem2**
* 事务类型下的正文单元格为类 **型**
* 以USD表示的正文单元格是 **tableItem3**

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

在示例XML中，行的数据由标记定义，该标 `<Row1>` 记是表中行的元素名称。 在标 `<Row1>` 记中，每个单元格的数据在标记中定义为其元素名称， `<tableItem1>`如、 `<tableItem2>`、 `<tableItem3>`和 `<type>`。

要在运行时将这些数据与表合并，我们需要将包含该表的自适应表单指向禁用wcmmode的绝对XML位置。 例如，如果自适应表单位于 *https://localhost:4502/myForms/bankTransaction.html* ，而数据XML文件保存在 *C:/myTransactions/bankSummary.xml*，则可以将表与位于以下URL的数据视图:

*https://localhost:4502/myForms/bankTransaction.html?dataRef=file:/// C:/myTransactions/bankSummary.xml&amp;wcmmode=disabled*

![数据合并表](assets/data-merged-table.png)

## 使用XDP组件和XSD复杂类型 {#use-xdp-components-and-xsd-complex-types}

如果您基于XFA表单模板创建了自适应表单，则XFA元素可在AEM内容查找器的“数据模型”选项卡中使用。 您可以在自适应表单中拖放这些XFA元素，包括表。

XFA表元素将映射到表组件，并在自适应表单中开箱即用。 XDP表的所有属性和功能在移入自适应表单时都会保留，您可以像处理本机自适应表单表一样对其执行任何操作。 例如，如果XDP表中的某行被标记为可重复，则在自适应表单中删除时也会重复该行。

此外，还可以拖放XDP子表单以在表中添加新行。 但是，请注意，删除嵌套子表单不起作用。

>[!NOTE]
>
>没有标题行的XDP表将不会映射到自适应表单表组件。 相反，它将映射到具有自适应布局的自适应表单面板组件。 此外，当您将嵌套表从XDP添加到自适应表单时，外表将转换为面板，同时保留内表。

此外，还可以拖放一组XSD复杂类型元素以创建表行。 将在放置元素的行的正下方创建一个新行。 使用XSD复杂类型元素创建的单元格将保留对XSD的绑定引用。 您还可以将正文单元格拖放到单元格上，从而将其替换为XSD复杂类型元素。

>[!NOTE]
>
>XDP表组件、子表单或XSD复杂类型中的元素数不能超过行中的单元格数。 例如，不能将四个元素放在只有三个单元格的行上。 这将导致错误。
>
>如果元素数少于行中的单元格数，则新行首先根据元素添加单元格，然后添加默认单元格以填充行中的其余单元格。 例如，如果将一组三个元素放入一个包含四个单元格的行中，则前三个单元格将基于您删除的元素，其余一个单元格将作为默认表单元格。

## 主要注意事项 {#key-considerations}

* 如果在创作基于XSD的表时上下移动行，则在提交表单时生成的数据XML中会看到表行中的一些数据丢失。
* 默认表中的每个正文单元格都有与之关联的预定义元素名称。 如果在自适应表单中添加另一个表，则新表中的默认正文单元格将与第一个表中的元素名称相同。 在这种情况下，提交表单时生成的数据将仅包含其中一个表的默认正文单元格中的数据。 因此，请确保重命名默认主体单元格的元素名称，以使它们在各个表中保持唯一，并避免数据丢失。

   请注意，这仅适用于默认的正文单元格。 如果向表中添加更多行或列，将为非默认主体单元格自动生成唯一的元素名称。

