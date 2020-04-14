---
title: 在Interactive Communications中使用图表
seo-title: Interactive Communications中的图表组件
description: 使用交互式通信中的图表，您可以将大量信息浓缩为易于分析的可视格式
seo-description: AEM Forms提供了一个图表组件，您可以使用它在交互式通信中创建图表。 本文档介绍图表组件的基本配置和代理配置。
uuid: 978aa431-9a5b-4964-b37c-7bfa8c3f49b9
content-type: reference
topic-tags: interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e21714ad-d445-4aff-b0db-d577061e0907
docset: aem65
translation-type: tm+mt
source-git-commit: 726163106ddb80600eaa7cc09b1a2e9b035a223e

---


# 在Interactive Communications中使用图表{#using-charts-in-interactive-communications}

图表或图表是数据的可视化表示形式。 它将大量信息浓缩为易于理解的可视格式，使交互式通信的收件人能够更好地可视化、解释和分析复杂数据。

在创建交互式通信时，您可以添加图表以可视方式表示来自交互式通信的表单数据模型的二维数据。 图表组件允许您添加和配置以下类型的图表：饼图、列图、圆环图、条形图、线图、线图和点图、点图、面积图和象限图。

## 在交互式通信中添加和配置图表 {#add-and-configure-chart-in-an-interactive-communication}

执行以下步骤以在交互式通信中添加和配置图表：

1. 从交 **互式通信** 的Sidekick点按组件。
1. 将“图表”组 **件拖放到** 下列组件之一：

   * 打印渠道:目标区域或图像字段
   * Web渠道:面板或目标区

1. 点按交互式通信编辑器中的图表组件，并从“组 **[!UICONTROL 件”工具栏]** 中选 ![择“配置”(configure_icon](assets/configure_icon.png))。

   图表属性显示在左窗格中。

   ![打印渠道中线型图表的基本属性](assets/chart_properties_print_new.png)

   打印渠道中线型图表的基本属性

   ![Web渠道中线型图表的基本属性](assets/chart_properties_web_new.png)

   Web渠道中线型图表的基本属性

1. 根据渠道 [类型配置图](../../forms/using/chart-component-interactive-communications.md#configure-chart-properties) 表属性。
1. (仅打印渠道)在“代 **[!UICONTROL 理设置]**”中，指定代理是否必须使用此图表。 如果代 **[!UICONTROL 理必须使用此图表]****** ，则未选择此图表选项，代理可点按代理UI内容选项卡中图表的眼睛图标以显示或隐藏图表。

   ![chart_agentproperties](assets/chart_agentproperties.png)

1. 点 ![按done_icon](assets/done_icon.png) 以保存图表属性。

   点按 **[!UICONTROL 预览]** ，以视图与图表关联的外观和数据。 点按 **[!UICONTROL 编辑]** ，重新配置图表的属性。

## 配置图表属性 {#configure-chart-properties}

在创建用于打印和Web渠道的图表时配置以下属性：

<table>
 <tbody>
  <tr>
   <td>字段</td>
   <td>描述</td>
   <td>渠道类型</td>
  </tr>
  <tr>
   <td>名称</td>
   <td>图表元素的标识符。 在此字段中指定的图表名称在图表上不可见。 它用于引用来自其他组件、脚本和SOM表达式的元素。</td>
   <td>印刷和Web</td>
  </tr>
  <tr>
   <td>图表类型</td>
   <td>要生成的图表类型。 可用的选项有饼图、列、圆环、条、线、线和点、点和区域。</td>
   <td>印刷和Web</td>
  </tr>
  <tr>
   <td>“系列”&gt;“多系列”</td>
   <td>选择此项可为在X轴和Y轴上绘制的表单数据模型集合项添加多个系列。</td>
   <td>印刷和Web</td>
  </tr>
  <tr>
   <td>“序列”&gt;“数据模型对象”</td>
   <td>用于向图表添加多个系列的表单数据模型集合项的名称。<br /> 为X轴和Y轴上绘制的属性选择父表单数据模型对象属性，以形成有意义的系列。 您绑定的数据模型对象必须为“数字”、“字符串”或“日期”类型。</td>
   <td>印刷和Web</td>
  </tr>
  <tr>
   <td>显示排列</td>
   <td>选择将各系列的数值排列程序。</td>
   <td>印刷和Web</td>
  </tr>
  <tr>
   <td>X轴&gt;标题</td>
   <td>X轴的标题。</td>
   <td>印刷和Web</td>
  </tr>
  <tr>
   <td>X轴&gt;数据模型对象</td>
   <td><p>要在X轴上绘制的表单数据模型集合项的名称。</p> <p>选择同一父数据模型对象的两个集合／数组类型属性，这些属性相互有意义，以在图表的X轴和Y轴上绘制。 您绑定的数据模型对象必须为“数字”、“字符串”或“日期”类型。</p> </td>
   <td>印刷和Web</td>
  </tr>
  <tr>
   <td>Y轴&gt;标题</td>
   <td>Y轴的标题。 </td>
   <td>印刷和Web</td>
  </tr>
  <tr>
   <td>Y轴&gt;数据模型对象</td>
   <td><p>要在Y轴上绘制的表单数据模型收集项。 在“打印”渠道中，Y轴的数据模型对象应为“编号”类型。</p> <p>选择同一父数据模型对象的两个集合／数组类型属性，这些属性相互有意义，以在图表的X轴和Y轴上绘制。 </p> </td>
   <td>印刷和Web</td>
  </tr>
  <tr>
   <td>Y轴&gt;函数</td>
   <td>用于计算Y轴上的值的统计／自定义函数。</td>
   <td>印刷和Web</td>
  </tr>
  <tr>
   <td>隐藏对象</td>
   <td>选择此项可在最终输出中隐藏图表。</td>
   <td>印刷和Web</td>
  </tr>
  <tr>
   <td>标题</td>
   <td>图表的标题。 </td>
   <td>打印</td>
  </tr>
  <tr>
   <td>高度</td>
   <td>图表的高度（以像素为单位）。</td>
   <td>打印</td>
  </tr>
  <tr>
   <td>宽度</td>
   <td>图表的宽度（以像素为单位）。您可以使用样式层或通过应用主题来控制Web渠道中图表的宽度。</td>
   <td>打印</td>
  </tr>
  <tr>
   <td>前面必填分页符</td>
   <td>选择此项可在图表前添加一个强制分页符，并将图表放在新页面的顶部。 </td>
   <td>打印</td>
  </tr>
  <tr>
   <td>之后必填分页符</td>
   <td>选择此项可在图表后添加一个强制分页符，并将图表后的内容放在新页面的顶部。 </td>
   <td>打印</td>
  </tr>
  <tr>
   <td>缩进</td>
   <td>从页面左侧缩进图表。 </td>
   <td>打印</td>
  </tr>
  <tr>
   <td>工具提示</td>
   <td><p>Web渠道中图表数据点上的鼠标悬停时显示工具提示的格式。 默认值是${x}(${y})。 根据图表类型，当您将鼠标指向图表中的点、条或切片时，变量${x}和${y}将动态替换为X轴和Y轴上的相应值，并显示在工具提示中。</p> <p>要禁用工具提示，请将“工具提 <span class="uicontrol">示</code> ”字段留空。 此选项不适用于线图和面积图。 例如，请参 <a href="#chartoutputprintweb">阅示例1:打印和Web中的图表输出</a>。</code></p> </td>
   <td>Web</td>
  </tr>
  <tr>
   <td>图表特定的配置</td>
   <td><p>除了常见配置之外，还提供以下特定于图表的配置：</p>
    <ul>
     <li><strong>显示图例：显 </strong>示启用时饼图或圆环图的图例。</li>
     <li><strong>图例位置：指 </strong>定图例相对于图表的位置。 可用选项有“右”、“左”、“上”和“下”。 建议在打印渠道中使用右侧图例。</li>
     <li><strong>内径</strong>:可用于圆环图以指定图表中内圆的半径（以像素为单位）。</li>
     <li><strong>线条颜色</strong>:可用于折线图、折线图、点图和面积图，以指定图表中折线的颜色。</li>
     <li><strong>点颜色</strong>:可用于点图和线图和点图以指定图表中点的颜色。<br /> </li>
     <li><strong>区域颜色</strong>:面积图可用于指定图表中线下区域的颜色。</li>
     <li><strong>“参照点”(Reference Point)&gt;“装订类型”(Binding Type):Quadrant </strong>图表可用于<strong></strong>指定参考点的绑定类型。 使用静态文本或数据模型对象属性为参考点定义值。</li>
     <li><strong>“参照点”(Reference Point)&gt;“X轴”(X-axis):如 </strong>果从“绑定类型”下拉列表中选择 <span class="uicontrol">“静态</code> ”(Static)来指定参考点的X轴值，则可用于象限图表。</code></li>
     <li><strong>“参照点”(Reference Point)&gt;“Y轴”(Y-axis):如 </strong>果从“绑定类型”( <span class="uicontrol">Binding Type</code> )下拉列表中选择“静态”(Static)，为参考点指定Y轴值，则此图表可用。</code></li>
     <li><strong>“参考点”&gt;“序列的数据模型对象”:如 </strong>果从“绑定类型”下拉列表中选 <span class="uicontrol">择“数据模型对象</code> ”，则可用于多个系列象限图表。 定义表单数据模型对象属性以确定参考点的系列. </code></li>
     <li><strong>“参考点”&gt;“序列的数据模型对象值”:如 </strong>果从“绑定类型”下拉列表中选 <span class="uicontrol">择“数据模型对象</code> ”，则可用于多个系列象限图表。 使用系列的表单数据模型对象属性和此字段中定义的值来标识参考点的系列。</code></li>
     <li><strong>“参照点”(Reference Point)&gt;“参照点的数据模型对象”(Data Model Object):如 </strong>果从“绑定类型”下拉列表 <span class="uicontrol">中选择“数据模型对象</code> ”，则可用于象限图表。 定义表单数据模型对象属性，该属性是X轴和Y轴上绘制的属性的同级属性。 此外，对于多个系列，定义一个数据模型对象属性，该属性是为系列定义的数据模型对象属性的子实体。</code></li>
     <li><strong>“参照点”(Reference Point)&gt;“数据模型对象值”(Data Model Object Value for Reference Point):如 </strong>果从“绑定类型”下拉列表 <span class="uicontrol">中选择“数据模型对象</code> ”，则可用于象限图表。 对参考点使用表单数据模型对象属性以及此字段中定义的值，以标识图表的参考点。<br /> 象限 <strong>标签&gt;左上角：</strong> 可用于象限图表以指定左上象限的名称。</code></li>
     <li><strong>象限标签&gt;右上：</strong> 可用于象限图表以指定右上象限的名称。</li>
     <li><strong>象限标签&gt;右下：可 </strong>用于象限图表以指定右下象限的名称。</li>
     <li><strong>象限标签&gt;左下：可 </strong>用于象限图表以指定左下象限的名称。</li>
    </ul> </td>
   <td>印刷和Web</td>
  </tr>
 </tbody>
</table>

## 在图表中使用函数 {#use-functions-in-chart}

您可以将图表配置为使用统计函数从源数据计算值以在图表上绘制。 通过在图表中应用函数，您可以绘制表单数据模型不直接提供的数据。

![图表中的函数](assets/functions_charts_new.png)

虽然“图表”组件包含一些内置函数，但您可以编写自定 [义函数](#customfunctionsweb) ，并使这些函数可用于Web渠道的图表配置中。

图表组件默认提供以下功能：

**平均值（平均值）** 返回X轴或Y轴上另一个轴上给定值的平均值。

**总和** 返回X轴或Y轴上另一个轴上给定值的所有值的总和。

**Maximum** （最大值）返回X轴或Y轴上另一个轴上给定值的最大值。

**频率** ：返回X轴或Y轴上另一个轴上给定值的值数。

**范围** ：返回X轴或Y轴上给定值在其它轴上的最大值与最小值之间的差值。

**中值** (Median)返回在X轴或Y轴上分隔较高值和较低值的值，该值在另一个轴上分隔给定值的一半。

**最小** ：为另一个轴上的给定值返回X轴或Y轴上的最小值。

**模式** ：返回在X轴或Y轴上出现次数最多的值，以表示在另一个轴上的给定值。

有关详细信息，请参 [阅示例2:求和和和频率函数在折线图中的应用](#applicationsumfrequency)。

### Web渠道中的自定义函数 {#customfunctionsweb}

除了使用图表中的默认函数外，您还可以使用JavaScript™编写自定义函数，并在“图表”组件中的函数列表中使其可用以进行Web渠道。

函数将数组或值以及类别名称作为输入并返回值。 例如：

```
Multiply(valueArray, category) {
 var val = 1;
 _.each(valueArray, function(value) {
 val = val * value;
 });
 return val;
}
```

编写自定义函数后，请执行以下操作以使其可用于图表配置：

1. 在与相关交互通信关联的客户端库中添加自定义函数。 有关详细信息，请参 [阅配置提交操作](/help/forms/using/configuring-submit-actions.md) 和 [使用客户端库](/help/sites-developing/clientlibs.md)。

1. 要在“函数”下拉菜单中显示自定义函数，请在CRXDe Lite中，使用以 `nt:unstructured` 下属性在apps文件夹中创建一个节点：

   * 添加 `guideComponentType` 值为的属 `fd/af/reducer`性。 (mandatory)

   * 将属性 `value` 添加到自定义JavaScript™函数的完全限定名称。 （必填），将其值设置为自定义函数的名称，如Multiply。
   * 添加 `jcr:description` 要显示为“函数”下拉列表中显示的自定义函数名称的值的属性。 例如， **Multiply**。

   * 添加 `qtip` 将简短描述自定义函数的值的属性。 将指针悬停在“函数”下拉列表中的函数名称上时，它将 **显示为** “工具提示”。

1. 单击 **全部保存** ，以保存配置。

该函数现在可在图表中使用。

## 示例1:打印和Web中的图表输出 {#chartoutputprintweb}

在“基本”选项卡中，您定义图表类型、包含数据的源表单数据模型属性、要在图表的X轴和Y轴上绘制的标签，以及（可选）用于计算在图表上绘制的值的统计函数。

让我们借助使用交互式通信生成的卡语句详细了解基本属性中的最低要求信息。 请考虑生成一个图表来描述报表中不同费用的金额。 您希望使用不同类型的图表来打印和Web输出交互通信。

### 用于打印的柱状图 {#columnchartprint}

要完成此操作，请指定以下属性：

* **[!UICONTROL 名称]** -指定图表的名称。
* **[!UICONTROL 图表类型]** -从下 **拉列表** 中选择列。
* **[!UICONTROL 标题]** -为X轴指定费用类型，为Y轴指定事务处理金额。
* **[!UICONTROL 数据模型对象]** -选择数据模型对象属性，为X轴（费用类型）和Y轴（事务处理金额）创建数据绑定。

![交互通信打印渠道中的柱状图](assets/sample_chart_print_column_new.png)

交互通信打印渠道中的柱状图

### Web圆环图 {#donutchartweb}

要完成此操作，请指定以下属性：

* **[!UICONTROL 名称]** -指定图表的名称。
* **[!UICONTROL 图表类型]** -从下 **** 拉列表中选择“圆环”。
* **[!UICONTROL 数据模型对象]** -选择数据模型对象属性，为X轴（费用类型）和Y轴（事务处理金额）创建数据绑定。
* **[!UICONTROL 内半径]** -将“内半径”值指定为150，以指定图表中内圆的半径（以像素为单位）。
* **[!UICONTROL 工具提示]** -使用${x}(${y})默认格式显示工具提示。 工具提示显示为：费用类型（事务处理金额）。 示例：比特币的借记(10000)。

![交互式通信Web渠道中的圆环图](assets/sample_chart_web_new.png)

交互式通信Web渠道中的圆环图

## 示例2:和频函数在线图中的应用 {#applicationsumfrequency}

通过在图表中应用函数，您可以绘制表单数据模型不直接提供的数据。 在此示例中，我们使用信用卡对帐单示例来了解如何将“和”和“频率”函数应用于图表。

![无函数的折线图，包含两个“AirBnB借记”交易](assets/line_chart_web_new.png)

无函数的折线图，包含两个“AirBnB借记”交易

### 和函数 {#sum-function}

您可以应用sum函数来添加同一数据属性的多个实例的值，并且只显示一次。 例如，在下图中，在Y轴上应用“和”函数，为AirBnB交易（2050和1050）加上两个“借项”的金额，并且只显示一个交易(3100)。

当您要对同一数据属性的许多实例进行拼合和显示和时，和函数可以使图形更有用。

![折线图和](assets/line_chart_web_sum_new.png)

### 频率函数 {#frequency-function}

Frequency函数返回另一个轴上给定值的Y轴数。 在Y轴上应用“频率”功能（“事务处理金额”）后，图表显示，AirBnB事务处理有两次发生借项，其余的事务类型有一次发生。

![折线图频率](assets/line_chart_web_functions_frequency_new.png)

## 示例3:Web中的多序列象限图 {#example-multi-series-quadrant-chart-in-web}

图表以曲线表示在特定日期范围内执行的事务处理金额。 象限图表提供了将图表区域分为四个标记部分的功能。 该字符对X轴和Y轴使用静态参考点。 使用多系列功能根据银行名称隔离数据。

要完成此操作，请指定以下属性：

* **名称：** 指定图表的名称。
* **图表类型：** 从 **下拉列表** 中选择象限。

* 选中“多 **个系列** ”复选框。
* **数据模型对象**:为系列指定数据模型对象属性。 库名称的数据模型对象属性是在X轴和Y轴中绘制的数据模型对象属性的父项。
* **数据模型对象：** 选择数据模型对象属性，为X轴（事务日期）和Y轴（事务金额）创建数据绑定。
* 在“参 **照点** ”(Reference Point **)部分，选择“** Static”（静态）作为“绑定类型”(Binding Type)。

* 指定X轴和Y轴参照点的值。
* 指定“左上”、“右上”、“右下”和“左下”象限的象限标签。
* 选中“显 **示图例** ”复选框可显示银行名称的颜色代码。

![象限图](assets/charts_quadrant_example_new.png)

