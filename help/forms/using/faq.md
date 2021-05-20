---
title: HTML5表单的常见问题解答(FAQ)
seo-title: HTML5表单的常见问题解答(FAQ)
description: 有关HTML5表单的布局、脚本支持和范围的常见问题解答(FAQ)。
seo-description: 有关HTML5表单的布局、脚本支持和范围的常见问题解答(FAQ)。
uuid: 398e31de-3e46-4288-b3cd-39d51fa17abc
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 4b676e7e-191f-4a19-8b8f-fc3e30244b59
docset: aem65
feature: 移动设备表单
exl-id: 85c9315e-1bc8-44a9-937e-af6fc7cf54d1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1972'
ht-degree: 0%

---

# HTML5表单的常见问题解答(FAQ){#frequently-asked-questions-faq-for-html-forms}

有关HTML5表单的布局、脚本支持和范围的一些常见问题(FAQ)。

## 布局 {#layout}

1. 为什么中的条形码和签名字段未显示在我的表单中？

   答案：条码和签名字段与HTML或移动设备方案无关。 这些字段显示为非交互区域。 但是，AEM Forms Designer提供了一个新的签名潦草字段，可以用它代替签名字段。 您还可以为条形码添加[自定义小组件](../../forms/using/custom-widgets.md)并集成它。

1. XFA文本字段是否支持富文本？

   答案：不支持在AEM Forms Designer中允许富内容的XFA字段，该字段呈现为普通文本，而不支持从用户界面为文本设置样式。 此外，具有梳状属性的XFA字段显示为正常字段，尽管根据梳状位数的值，仍对允许的字符数存在限制。

1. 有关使用可重复子表单的任何限制？

   答案：可重复子表单的初始计数应为1个或更多。 不支持初始计数为零的可重复子表单。 您还可以选择使用可重复的子表单，而不会在加载表单时显示该子表单。 要实现用例，请执行以下操作：

   1. 将可重复子表单的初始计数设置为1。

      ![初数](assets/intial-count.png)

   1. 使用表单的初始化事件来隐藏子表单的主实例。 例如，下面的代码在表单初始化时隐藏子表单的主实例。 它还会验证应用程序类型，以确保脚本仅在客户端执行：

      ```javascript
      if ((xfa.host.appType == "HTML 5" || xfa.host.appType == "Exchange-Pro" || xfa.host.appType == "Reader")&&(_RepeatSubform.count == 1)&&(form1.Page1.Subform1.RepeatSubform.Key.rawValue == null)) {
      RepeatSubform.presence = "hidden";
      }
      ```

   1. 打开用于添加子表单实例以进行编辑的脚本。 添加如下所示的代码，以添加子表单脚本的实例。

      以下代码会检查子表单的隐藏实例。 如果找到子表单的隐藏实例，请删除子表单的隐藏实例，并插入子表单的新实例。 如果未找到子表单的隐藏实例，则只需插入该子表单的新实例即可。

      ```javascript
      if (RepeatSubform.presence == "hidden")
      {
      RepeatSubform.instanceManager.insertInstance(0);
      RepeatSubform.instanceManager.removeInstance(1);
      }
      else
      {
      RepeatSubform.instanceManager.addInstance(1);
      }
      ```

   1. 打开用于删除子表单实例的脚本以进行编辑。 添加如下所示的代码以删除子表单脚本的实例。

      该代码检查子表单的计数。 如果子表单的计数达到1，则代码将隐藏子表单，而不是删除子表单。

      ```javascript
      if (RepeatSubform.instanceManager.count == 1) {
      RepeatSubform.presence = "hidden";
      } else {
      RepeatSubform.instanceManager.removeInstance(RepeatSubform.instanceManager.count - 1);
      }
      ```

   1. 打开表单的预提交事件进行编辑。 将以下脚本添加到事件，以在编辑之前删除该脚本的隐藏实例。 它可防止在提交时发送隐藏子表单的数据。

      ```javascript
      if(RepeatSubform.instanceManager.count == 1 && RepeatSubform.presence == "hidden") {
      RepeatSubform.instanceManager.removeInstance(0);
      }
      ```

1. 有关使用隐藏子表单的任何限制？

   答案：具有复杂层次结构且跨页面拆分的隐藏子表单会导致布局问题。 解决方法是：将子表单标记为最初可见，然后根据某些逻辑或数据在初始化脚本中隐藏该子表单。

1. 为什么某些文本会被截断或在HTML5中显示不正确？

   答案：如果“绘制”或“题注”文本元素没有足够的空间来显示内容，则文本在移动设备表单呈现中会被截断。 此截断在AEM Forms Designer的“设计”视图中也可见。 尽管此截断可以在PDF中处理，但无法在HTML5表单中处理。 要避免出现此问题，请提供足够的空间来绘制或描述文本，以便它不会在AEM Forms Designer的设计模式中被截断。

1. 我正在观察与缺少内容或内容重叠相关的布局问题。 原因何在？

   答案：如果在同一位置（如矩形）有一个“绘制文本”或“绘制图像”元素以及另一个重叠元素，则如果“绘制文本”内容稍后按文档顺序排列(在AEM Forms Designer“层次结构”视图中)，则不显示该内容。 PDF支持透明分层，但HTML/浏览器不支持透明分层。

1. 为什么HTML表单中显示的某些字体与设计表单时使用的字体不同？

   答案：HTML5表单不嵌入字体(与将字体嵌入到表单中的PDF forms相反)。 要使表单的HTML版本按预期呈现，请确保XDP中指定的字体在服务器和客户端计算机上可用。 如果服务器上没有所需的字体，则使用回退字体。 此外，如果您在表单模板中使用客户端设备上不可用的字体，则将使用浏览器的默认字体来呈现文本。

1. HTML表单中是否支持vAlign和hAlign属性？

   是，支持vAlign和hAlign属性。 Internet Explorer和多行字段中不支持vAlign属性。

1. HTML5表单是否支持希伯来语字符？

   除Microsoft Internet Explorer外，所有浏览器中的HTML5表单都支持希伯来语字符。

1. HTML5表单对数字字段有任何限制吗？

   答案：是，HTML5表单存在一些限制。 如果位数大于picture子句中指定的计数，则数字不会本地化，并以英语区域设置显示。

1. 为何HTML表单的大小大于PDF forms?

   在HTML表单中渲染XDP时，需要大量中间数据结构和对象（如表单dom、数据dom和布局dom）。

   对于PDF forms,Adobe Acrobat具有内置的XTG引擎，用于创建中间数据结构和对象。 Acrobat还负责布局和脚本。

   对于HTML5表单，浏览器没有内置的XTG引擎来创建中间数据结构，以及来自原始XDP字节的对象。 因此，对于HTML5表单，中间结构在服务器上生成并发送到客户端。 在客户端，基于JavaScript的脚本和布局引擎使用这些中间结构。

   中间结构的大小取决于原始XDP的大小以及与XDP合并的数据。

1. 在xdp中使用表有任何限制吗？

   答案：复杂表在渲染时导致问题。

   * 不支持表内的节（子表单集）。
   * 某些表中的页眉或页脚行会标记为重复。 在多个页面中拆分此类表可能会遇到一些问题。

1. 辅助表有任何限制吗？

   答案：是，辅助表具有以下限制：

   * 不支持表内的嵌套表和子表单。
   * 仅表格的顶行或左列支持标题。 中间表元素不支持标头。 您可以将标题应用于多个行标题，并且支持所有此类行和列以及表最顶部的行或最左侧的列。
   * `Rowspan`不支持 `colspan`从表内的随机位置访问和。

   * 不能动态添加或删除包含行跨值大于1的元素的行实例。

1. 屏幕阅读器的工具提示和标题的阅读顺序是什么？

   * 如果同时存在标题和工具提示，则只会读取标题。 如果标题不可用，则会读取工具提示。 您还可以使用表单设计器指定在XDP中读取的优先级
   * 将鼠标悬停在某个元素上时，会显示工具提示。 如果工具提示不可用，则显示语音文本。 如果语音文本不可用，则显示字段名称。

1. 将鼠标悬停在字段上时，会显示工具提示。 如何禁用它？

   要在悬停时禁用工具提示，请在Designer的“辅助功能”面板中选择“无”。

1. 在Designer中，用户可以配置单选按钮和复选框的自定义外观属性。 在渲染表单时，HTML5表单是否会考虑此类自定义外观属性？

   答案：HTML5表单会忽略单选按钮和复选框的自定义外观属性。 单选按钮和复选框将根据基础浏览器的规范显示。

1. 在支持的浏览器中打开HTML5表单时，相邻放置的字段的边框未正确对齐或子表单出现重叠。 在Forms Designer中预览同一HTML5表单时，字段和布局不会出现错位现象，子表单显示在正确的位置。 如何修复该问题？

   当子表单设置为流内容，并且子表单具有隐藏的边框元素时，相邻放置的字段的边框不正确对齐或子表单出现重叠。 要解决此问题，您可以从相应的XDP中删除或注释隐藏的&lt;border>元素。 例如，以下&lt;border>元素被标记为注释：

   ```xml
               <!--<border>
                  <edge presence="hidden"/>
                  <corner thickness="0.175mm" presence="hidden"/>
               </border> -->
   ```

1. 为什么屏幕阅读器无法正确使用日期/时间字段对象？

   屏幕阅读器不支持日期/时间字段。 但是，您可以手动在字段中输入日期/时间，以便屏幕阅读器读取该日期/时间。 使用工具提示或屏幕阅读器文本来指示用户手动选择字段的日期/时间。

1. HTML5表单是否支持浮动字段的显示模式？

   答案：HTML5表单不支持浮动字段的显示模式。

### 脚本 {#scripting}

1. HTML Forms的JavaScript实施中是否存在任何限制？

   答案:

   * 对xfa.connectionSet脚本的支持有限。 对于connectionSet，仅支持Web服务的服务器端调用。 有关详细信息，请参阅[脚本支持](/help/forms/using/scripting-support.md)。
   * 客户端脚本中不支持$record和$data。 但是，如果脚本是以formReady、layoutReady块编写的，则脚本仍然有效，因为这些事件在服务器端运行。
   * 不支持XFA Draw元素特定的脚本，例如更改Draw文本（或字段中的标题文本）。

1. 使用formCalc有任何限制吗？

   答案：当前只实施formCalc脚本的子集。 有关详细信息，请参阅[脚本支持](/help/forms/using/scripting-support.md)。

1. 是否有任何推荐的命名约定？是否有任何需要避免的保留关键词？

   * 在AEM Forms Designer中，建议不要在对象（如子表单或文本字段）的名称开头带下划线(_)。 要在名称的开头使用下划线，请在下划线后面添加前缀_&lt;prefix>&lt;objectname>。
   * 所有HTML5表单API都是保留的关键字。 对于自定义API/函数，请使用与[HTML5表单API](/help/forms/using/scripting-support.md)不相同的名称。

1. HTML5表单是否支持浮动字段？

   是，HTML5 Forms支持浮动字段。 要启用浮动字段，请将以下属性添加到渲染配置文件：

   >[!NOTE]
   >
   >默认情况下，不为浮动启用字段。 您可以使用Forms Designer设置字段的浮动属性。

   1. 打开CRXde lite并导航到`/content/xfaforms/profiles/default`节点。
   1. 添加类型为String的属性`mfDataDependentFloatingField`，并将该属性的值设置为`true`。
   1. 单击&#x200B;**Save All**。 现在，可使用更新的呈现配置文件为HTML Forms启用浮动字段。

      >[!NOTE]
      >
      >要在不更新呈现配置文件的情况下为特定表单启用浮动字段，请将mfDataDependentFloatingField=true属性作为URL参数进行传递。

1. HTML5表单是否会多次执行初始化脚本和表单就绪事件？

   是，初始化脚本和表单就绪事件会多次执行，至少一次在服务器上执行，一次在客户端执行。 建议根据某些业务逻辑（表单或字段数据）编写诸如初始化或form:ready事件之类的脚本，以便根据数据和幂等状态（如果数据相同）执行操作。

### 设计XDP {#designing-xdp}

1. HTML5表单中是否有任何保留的关键词？

   答案：所有HTML5表单API都是保留的关键字。 对于自定义API/函数，请使用与[HTML5表单API](/help/forms/using/scripting-support.md)不相同的名称。 除保留的关键字外，如果您使用以下划线(_)开头的对象名称，建议在下划线后面添加唯一前缀。 添加前缀有助于避免与HTML5表单内部API发生任何可能的冲突。 例如，`_fpField1`
