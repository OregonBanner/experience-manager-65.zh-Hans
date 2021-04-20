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
feature: Interactive Communication
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2648'
ht-degree: 2%

---


# 在Interactive Communications{#using-charts-in-interactive-communications}中使用图表

图表或图表是数据的可视表示形式。 它将大量信息浓缩为易于理解的可视格式，使交互式通信的收件人能够更好地可视化、解释和分析复杂数据。

在创建交互式通信时，您可以添加图表以可视方式表示来自交互式通信的表单数据模型的二维数据。 图表组件允许您添加和配置以下类型的图表：饼图、列图、圆环图、条形图、线图、线图和点图、点图、面积图和象限图。

## 在交互通信{#add-and-configure-chart-in-an-interactive-communication}中添加和配置图表

执行以下步骤以在交互通信中添加和配置图表：

1. 从交互式通信的Sidekick中点按&#x200B;**组件**。
1. 将&#x200B;**Chart**&#x200B;组件拖放到以下组件之一：

   * 打印渠道:目标区域或图像字段
   * Web渠道:面板或目标区域

1. 点按交互式通信编辑器中的图表组件，然后从组件工具栏中选择&#x200B;**[!UICONTROL 配置(]** ![configure_icon](assets/configure_icon.png))。

   图表属性显示在左窗格中。

   ![打印渠道中折线图的基本属性](assets/chart_properties_print_new.png)

   打印渠道中折线图的基本属性

   ![Web渠道中折线图的基本属性](assets/chart_properties_web_new.png)

   Web渠道中折线图的基本属性

1. 根据渠道类型配置[图表属性](../../forms/using/chart-component-interactive-communications.md#configure-chart-properties)。
1. (仅打印渠道)在&#x200B;**[!UICONTROL 代理设置]**&#x200B;中，指定代理是否必须使用此图表。 如果代理必须使用&#x200B;**[!UICONTROL ，未选择此图表]**&#x200B;选项，则代理可点击代理UI的&#x200B;**[!UICONTROL 内容]**&#x200B;选项卡中图表的眼睛图标以显示或隐藏图表。

   ![chart_agent属性](assets/chart_agentproperties.png)

1. 点按![done_icon](assets/done_icon.png)以保存图表属性。

   点按&#x200B;**[!UICONTROL 预览]**&#x200B;以视图与图表关联的外观和数据。 点按&#x200B;**[!UICONTROL 编辑]**&#x200B;以重新配置图表的属性。

## 配置图表属性{#configure-chart-properties}

在为打印和Web渠道创建图表时配置以下属性：

<table>
 <tbody>
  <tr>
   <td>字段</td>
   <td>描述</td>
   <td>渠道类型</td>
  </tr>
  <tr>
   <td>名称</td>
   <td>图表元素的标识符。 在此字段中指定的图表名称在图表上不可见。 当引用来自其他组件、脚本和SOM表达式的元素时，会使用它。</td>
   <td>印刷和Web</td>
  </tr>
  <tr>
   <td>图表类型</td>
   <td>要生成的图表类型。 可用选项有饼图、列、圆环、条、线、线和点、点和区域。</td>
   <td>印刷和Web</td>
  </tr>
  <tr>
   <td>“系列”&gt;“多系列”</td>
   <td>选择以为在X轴和Y轴上绘制的表单数据模型集合项添加多个系列。</td>
   <td>印刷和Web</td>
  </tr>
  <tr>
   <td>“系列”&gt;“数据模型对象”</td>
   <td>用于向图表添加多个系列的表单数据模型集合项的名称。<br /> 为在X轴和Y轴上绘制的属性选择父表单数据模型对象属性，以形成有意义的系列。绑定的数据模型对象必须为Number、String或Date类型。</td>
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
   <td><p>要在X轴上绘制的表单数据模型收集项的名称。</p> <p>选择同一父级数据模型对象的两个集合/数组类型属性，这些属性相互有意义，可在图表的X轴和Y轴上绘制。 绑定的数据模型对象必须为Number、String或Date类型。</p> </td>
   <td>印刷和Web</td>
  </tr>
  <tr>
   <td>Y轴&gt;标题</td>
   <td>Y轴的标题。 </td>
   <td>印刷和Web</td>
  </tr>
  <tr>
   <td>Y轴&gt;数据模型对象</td>
   <td><p>在Y轴上绘制的表单数据模型收集项。 在“打印”渠道中，Y轴的数据模型对象应为“编号”类型。</p> <p>选择同一父级数据模型对象的两个集合/数组类型属性，这些属性相互有意义，可在图表的X轴和Y轴上绘制。 </p> </td>
   <td>印刷和Web</td>
  </tr>
  <tr>
   <td>Y轴&gt;函数</td>
   <td>用于计算y轴上值的统计/自定义函数。</td>
   <td>印刷和Web</td>
  </tr>
  <tr>
   <td>隐藏对象</td>
   <td>选择以在最终输出中隐藏图表。</td>
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
   <td>图表的宽度（以像素为单位）。您可以使用样式图层或通过应用主题来控制Web渠道中图表的宽度。</td>
   <td>打印</td>
  </tr>
  <tr>
   <td>之前必填分页符</td>
   <td>选择以在图表前添加一个必填的分页符，并将图表放在新页面的顶部。 </td>
   <td>打印</td>
  </tr>
  <tr>
   <td>之后必填分页符</td>
   <td>选择此项可在图表后添加强制分页符，并将图表后的内容放在新页面的顶部。 </td>
   <td>打印</td>
  </tr>
  <tr>
   <td>缩进</td>
   <td>从页面左侧缩进图表。 </td>
   <td>打印</td>
  </tr>
  <tr>
   <td>工具提示</td>
   <td><p>工具提示显示在Web渠道中图表中数据点上的鼠标悬停上的格式。 默认值为${x}(${y})。 根据图表类型，当您将鼠标指向图表中的点、条或切片时，变量${x}和${y}将动态替换为X轴和Y轴上的相应值，并显示在工具提示中。</p> <p>要禁用工具提示，请将<span class="uicontrol">工具提示</code>字段留空。 此选项不适用于线图和面积图。 例如，请参阅<a href="#chartoutputprintweb">示例1:打印和Web</a>中的图表输出。</code></p> </td>
   <td>Web</td>
  </tr>
  <tr>
   <td>图表特定的配置</td>
   <td><p>除了常见配置之外，还提供以下特定于图表的配置：</p>
    <ul>
     <li><strong>显示图例： </strong>启用时显示饼图或圆环图的图例。</li>
     <li><strong>图例位置： </strong>指定图例相对于图表的位置。可用选项有“右”、“左”、“上”和“下”。 建议在打印渠道中使用右侧图例。</li>
     <li><strong>内半径</strong>:可用于圆环图指定图表中内圆的半径（以像素为单位）。</li>
     <li><strong>线条颜色</strong>:可用于折线图、折线图、点图和面积图，以指定图表中折线的颜色。</li>
     <li><strong>点颜色</strong>:可用于点图和线图和点图表，以指定图表中点的颜色。<br /> </li>
     <li><strong>区域颜色</strong>:面积图可用于指定图表中线条下方区域的颜色。</li>
     <li><strong>参考点&gt;绑定类型： </strong>可用于象限图<strong> </strong>表指定参考点的绑定类型。使用静态文本或数据模型对象属性为参考点定义值。</li>
     <li><strong>参照点&gt; X轴： </strong>如果从“绑定类型”下拉 <span class="uicontrol"></code> 列表中选择“状态”以指定参考点的X轴值，则可用于象限图表。</code></li>
     <li><strong>参照点&gt; Y轴： </strong>如果从“绑定类型”下拉 <span class="uicontrol"></code> 列表中选择“状态”以指定参考点的Y轴值，则可用于象限图表。</code></li>
     <li><strong>“参考点”&gt;“系列的数据模型对象”： </strong>如果从“绑定类型”下拉列表中选 <span class="uicontrol">择“数</code> 据模型对象”，则可用于多个系列象限图表。定义表单数据模型对象属性以确定参考点的系列. </code></li>
     <li><strong>“参考点”&gt;“系列的数据模型对象值”： </strong>如果从“绑定类型”下拉列表中选 <span class="uicontrol">择“数</code> 据模型对象”，则可用于多个系列象限图表。使用系列的表单数据模型对象属性和此字段中定义的值标识参考点的系列。</code></li>
     <li><strong>“参考点”(Reference Point)&gt;“参考点的数据模型对象”(Data Model Object for Reference Point): </strong>如果从“绑定类型”下拉 <span class="uicontrol">列表中</code> 选择“数据模型对象”，则可用于象限图表。定义一个表单数据模型对象属性，该属性是在X轴和Y轴上绘制的属性的同级。 此外，对于多个系列，定义一个数据模型对象属性，该属性是为该系列定义的数据模型对象属性的子实体。</code></li>
     <li><strong>“参考点”(Reference Point)&gt;“参考点的数据模型对象值”(Data Model Object Value for Reference Point): </strong>如果从“绑定类型”下拉 <span class="uicontrol">列表中</code> 选择“数据模型对象”，则可用于象限图表。使用引用点的表单数据模型对象属性和此字段中定义的值来标识图表的引用点。<br /> <strong>象限标签&gt;左上图：</strong> 可用于象限图表，以指定左上图的名称。</code></li>
     <li><strong>象限标签&gt;右上图：</strong> 可用于象限图表，以指定右上图的名称。</li>
     <li><strong>象限标签&gt;右下： </strong>可用于象限图表以指定右下象限的名称。</li>
     <li><strong>象限标签&gt;左下： </strong>可用于象限图表以指定左下象限的名称。</li>
    </ul> </td>
   <td>印刷和Web</td>
  </tr>
 </tbody>
</table>

## 在图表{#use-functions-in-chart}中使用函数

您可以配置图表以使用统计函数从源数据计算值，以便在图表上绘图。 通过应用图表中的函数，可以绘制表单数据模型不直接提供的数据。

![图表中的函数](assets/functions_charts_new.png)

虽然图表组件包含一些内置函数，但您可以编写[自定义函数](#customfunctionsweb)并使它们可用于Web渠道的图表配置中。

图表组件默认提供以下功能：

**平均值(平** 均值)返回X或Y轴上其它轴上给定值的平均值。

**Sum** 返回X轴或Y轴上另一个轴上某个给定值的所有值的和。

**最** 大值返回X轴或Y轴上另一个轴上给定值的最大值。

**频** 率返回X轴或Y轴上另一个轴上给定值的值数。

**范** 围返回X轴或Y轴上其它轴上给定值的最大值与最小值之差。

**中** 值返回在X轴或Y轴上为另一轴上的给定值分隔高值和低值的值。

**最小** 值返回X轴或Y轴上其它轴上给定值的最小值。

**模** 式返回在X或Y轴上出现次数最多的值，该值在另一个轴上显示给定值。

有关详细信息，请参阅[示例2:在折线图](#applicationsumfrequency)中应用“和”和“频率”函数。

### Web渠道{#customfunctionsweb}中的自定义函数

除了使用图表中的默认函数外，您还可以在JavaScript™中编写自定义函数，并在“图表”组件中的列表中使这些函数可用于Web渠道。

函数将数组或值和类别名称作为输入并返回值。 例如：

```javascript
Multiply(valueArray, category) {
 var val = 1;
 _.each(valueArray, function(value) {
 val = val * value;
 });
 return val;
}
```

编写自定义函数后，请执行以下操作以使其可用于图表配置：

1. 在与相关交互通信关联的客户端库中添加自定义函数。 有关详细信息，请参阅[配置提交操作](/help/forms/using/configuring-submit-actions.md)和[使用客户端库](/help/sites-developing/clientlibs.md)。

1. 要在“函数”下拉菜单中显示自定义函数，请在CRXDe Lite中，使用以下属性在apps文件夹中创建一个`nt:unstructured`节点：

   * 添加属性`guideComponentType`，其值为`fd/af/reducer`。 (mandatory)

   * 将属性`value`添加到自定义JavaScript™函数的完全限定名。 （必填），将其值设置为自定义函数的名称，如“乘号”。
   * 添加属性`jcr:description`，其值要显示为“函数”下拉列表中显示的自定义函数的名称。 例如，**Multiply**。

   * 添加属性`qtip`，其值将是自定义函数的简短描述。 当将指针悬停在&#x200B;**Function**&#x200B;下拉列表中的函数名称上时，它将显示为工具提示。

1. 单击&#x200B;**保存全部**&#x200B;以保存配置。

该函数现在可在图表中使用。

## 示例1:打印和Web中的图表输出{#chartoutputprintweb}

在“基本”选项卡中，您定义图表类型、包含数据的源表单数据模型属性、要在图表的X轴和Y轴上绘制的标签，以及（可选）用于计算在图表上绘制的值的统计函数。

让我们借助使用交互式通信生成的卡声明来详细了解基本属性中所需的最低信息。 请考虑您要生成一个图表来描述报表中不同费用的金额。 您希望使用不同类型的图表来打印和Web输出交互通信。

### 打印{#columnchartprint}的柱状图

要完成此操作，请指定以下属性：

* **[!UICONTROL 名称]**  — 指定图表的名称。
* **[!UICONTROL 图表类型]**  — 从 **** 下拉列表中选择列。
* **[!UICONTROL 标题]**  — 为X轴指定费用类型，为Y轴指定事务处理金额。
* **[!UICONTROL 数据模型对象]**  — 选择数据模型对象属性，为X轴（支出类型）和Y轴（事务处理金额）创建数据绑定。

![交互式通信的打印渠道中的柱状图](assets/sample_chart_print_column_new.png)

交互式通信的打印渠道中的柱状图

### Web {#donutchartweb}的圆环图

要完成此操作，请指定以下属性：

* **[!UICONTROL 名称]**  — 指定图表的名称。
* **[!UICONTROL 图表类型]**  — 从 **** 下拉式列表中选择“下载”。
* **[!UICONTROL 数据模型对象]**  — 选择数据模型对象属性，为X轴（支出类型）和Y轴（事务处理金额）创建数据绑定。
* **[!UICONTROL 内半径]**  — 将“内半径”值指定为150，以指定图表中内圆的半径（以像素为单位）。
* **[!UICONTROL 工具]** 提示 — 使用${x}(${y})默认格式显示工具提示。工具提示显示为：费用类型（事务处理金额）。 示例：比特币的借记(10000)。

![交互式通信的Web渠道中的圆环图](assets/sample_chart_web_new.png)

交互式通信的Web渠道中的圆环图

## 示例2:求和函数和频率函数在线图{#applicationsumfrequency}中的应用

通过应用图表中的函数，可以绘制表单数据模型不直接提供的数据。 在此示例中，我们使用信用卡对帐单示例来了解如何将Sum和Frequency函数应用到图表。

![无函数的折线图，包含两个“AirBnB借项”交易](assets/line_chart_web_new.png)

无函数的折线图，包含两个“AirBnB借项”交易

### Sum函数{#sum-function}

您可以应用sum函数来累加同一数据属性的多个实例的值，并且只显示一次。 例如，在下图中，在Y轴上应用Sum函数，将AirBnB交易（2050和1050）的两个借项金额相加，并仅显示一个交易(3100)。

Sum函数可让图表在您希望对相同数据属性的许多实例进行拼贴和显示sum时更有用。

![折线图和](assets/line_chart_web_sum_new.png)

### 频率函数{#frequency-function}

Frequency函数返回另一个轴上给定值的Y轴值数。 通过在Y轴（事务处理金额）上应用“频率”功能，该图表显示，AirBnB事务处理发生了两次借项事件，其余事务类型发生了一次。

![折线图频率](assets/line_chart_web_functions_frequency_new.png)

## 示例3:Web {#example-multi-series-quadrant-chart-in-web}中的多系列象限图

图表以图表形式显示在特定日期范围内执行的事务处理的金额。 象限图表提供了将图表区域分为四个标记部分的功能。 该字符对X轴和Y轴使用静态参考点。 使用多系列功能根据银行名称隔离数据。

要完成此操作，请指定以下属性：

* **名称：** 指定图表的名称。
* **图表类型：** 从 **** 下拉式列表中选择象限。

* 选中&#x200B;**多系列**&#x200B;复选框。
* **数据模型对象**:指定系列的数据模型对象属性。银行名称的数据模型对象属性是在X轴和Y轴中绘制的数据模型对象属性的父项。
* **数据模型对** 象：选择数据模型对象属性，为X轴（事务日期）和Y轴（事务金额）创建数据绑定。
* 在&#x200B;**参考点**&#x200B;部分，选择&#x200B;**静态**&#x200B;作为绑定类型。

* 指定X轴和Y轴参照点的值。
* 指定“左上”、“右上”、“右下”和“左下”象限的象限标签。
* 选中&#x200B;**显示图例**&#x200B;复选框，以显示库名称的颜色代码。

![象限图](assets/charts_quadrant_example_new.png)

