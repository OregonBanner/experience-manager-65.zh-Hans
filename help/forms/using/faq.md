---
title: HTML5表单常见问题解答(FAQ)
description: 有关HTML5表单布局、脚本支持和范围的常见问题解答(FAQ)。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
docset: aem65
feature: Mobile Forms
exl-id: 85c9315e-1bc8-44a9-937e-af6fc7cf54d1
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '2007'
ht-degree: 0%

---


# HTML5表单常见问题解答(FAQ){#frequently-asked-questions-faq-for-html-forms}

存在关于HTML5表单布局、脚本支持和范围的常见问题解答(FAQ)。

## 布局 {#layout}

1. 为什么中的条形码和签名字段未显示在我的表单中？

   答案：条形码和签名字段在HTML或移动场景中无关。 这些字段显示为非交互区域。 但是，AEM Forms Designer提供了一个新的签名涂写字段，该字段可用于代替签名字段。 您也可以添加 [自定义构件](../../forms/using/custom-widgets.md) 用于条形码，并将它集成。

1. XFA文本字段是否支持富文本？

   答案： XFA字段允许在AEM Forms Designer中使用丰富内容，该字段不受支持，并且会呈现为普通文本，而不支持从用户界面为文本设置样式。 此外，具有梳状属性的XFA字段会显示为普通字段，尽管根据梳状位数的值，仍对允许的字符数存在限制。

1. 使用可重复子表单是否存在任何限制？

   回答：可重复子表单的初始计数应为1或大于1。 不支持初始计数为零的可重复子表单。 您还可以选择使用可重复的子表单，并在加载表单时不显示它。 要实现用例，请执行以下操作：

   1. 将可重复子表单的初始计数设置为1。

      ![初始计数](assets/intial-count.png)

   1. 使用窗体的初始化事件来隐藏子窗体的主实例。 例如，下面的代码在表单初始化时隐藏子表单的主要实例。 它还会验证应用程序类型，以确保脚本仅在客户端执行：

      ```javascript
      if ((xfa.host.appType == "HTML 5" || xfa.host.appType == "Exchange-Pro" || xfa.host.appType == "Reader")&&(_RepeatSubform.count == 1)&&(form1.Page1.Subform1.RepeatSubform.Key.rawValue == null)) {
      RepeatSubform.presence = "hidden";
      }
      ```

   1. 打开用于添加子表单实例的脚本以进行编辑。 添加如下所示的代码以添加子表单脚本的实例。

      下面的代码检查子表单的隐藏实例。 如果找到子表单的隐藏实例，请删除该子表单的隐藏实例，并插入该子表单的新实例。 如果找不到子表单的隐藏实例，则只需插入子表单的新实例。

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

   1. 打开用于移除子表单实例的脚本以进行编辑。 添加如下代码以删除Subform脚本的实例。

      该代码检查子表单的计数。 如果子表单的数量达到1，则代码会隐藏子表单，而不是删除子表单。

      ```javascript
      if (RepeatSubform.instanceManager.count == 1) {
      RepeatSubform.presence = "hidden";
      } else {
      RepeatSubform.instanceManager.removeInstance(RepeatSubform.instanceManager.count - 1);
      }
      ```

   1. 打开表单的预提交事件进行编辑。 将以下脚本添加到事件中，以在编辑之前删除脚本的隐藏实例。 它可防止在提交时发送隐藏子表单的数据。

      ```javascript
      if(RepeatSubform.instanceManager.count == 1 && RepeatSubform.presence == "hidden") {
      RepeatSubform.instanceManager.removeInstance(0);
      }
      ```

1. 有关使用隐藏子表单是否有任何限制？

   答案：具有复杂层次结构的隐藏子表单被拆分为多个页面，这会导致布局问题。 解决方法是将子表单标记为最初可见，然后根据某些逻辑或数据将其隐藏在初始化脚本中。

1. 为什么某些文本被截断或在HTML5中显示不正确？

   回答：如果为绘制或题注文本元素提供的空间不足以显示内容，则在移动设备表单呈现版本中，文本会显示为截断。 此截断在AEM Forms Designer的“设计”视图中也可见。 虽然此截断可在PDF中处理，但在HTML5表单中无法处理。 要避免出现此问题，请为Draw或Caption Text提供足够的空间，以便在AEM Forms Designer的设计模式下不会截断文本。

1. 我观察到与缺少内容或内容重叠相关的布局问题。 原因是什么？

   回答：如果在同一位置有一个绘制文本或绘制图像元素以及另一个重叠元素（例如矩形），则绘制文本内容在文档顺序的后面显示(在AEM Forms Designer层次结构视图中)时不可见。 PDF支持透明分层，但HTML/浏览器不支持透明分层。

1. 为什么在HTML表单中显示的某些字体与设计表单时使用的字体不同？

   回答：HTML5 Forms不允许嵌入字体(与字体嵌入到表单中的PDF forms相反)。 要使表单的HTML版本按预期呈现，请确保AEM Forms服务器的CRX存储库(AEM Content Repository)中以及安装了AEM Designer的计算机上的字体可用。 当AEM Forms服务器的CRX存储库中或AEM Designer的安装位置中无法使用这些字体时，表单将渲染为回退字体。

1. HTML表单中是否支持vAlign和hAlign属性？

   回答：是，支持vAlign和hAlign属性。 Internet Explorer和多行字段中不支持vAlign属性。

1. HTML5表单是否支持希伯来字符？

   答案：除Microsoft Internet Explorer之外，HTML5表单在所有浏览器中均支持希伯来字符。

1. HTML5表单对数值字段是否有任何限制？

   回答：是，HTML5表单存在一些限制。 如果位数大于picture子句中指定的计数，则这些数字不会本地化，而是以英语区域设置显示。

1. 为什么HTML表单的大小大于PDF forms？

   答案：要将XDP呈现为HTML表单，需要大量中间数据结构和对象，例如表单dom、数据dom和布局dom。

   对于PDF forms，Adobe Acrobat具有内置的XTG引擎，可用于创建中间数据结构和对象。 Acrobat还负责布局和脚本。

   对于HTML5表单，浏览器没有内置的XTG引擎来创建中间数据结构，以及从原始XDP字节创建对象。 因此，对于HTML5表单，中间结构在服务器上生成并发送到客户端。 在客户端，基于JavaScript的脚本和布局引擎使用这些中间结构。

   中间结构的大小取决于原始XDP和与XDP合并的数据的大小。

1. 在xdp中使用表是否存在任何限制？

   答案：复杂的表会导致渲染时出现问题。

   * 不支持表内的节(SubformSet)。
   * 某些表中的页眉行或页脚行标记为重复。 在多个页面中拆分此类表格可能会遇到一些问题。

1. 辅助表是否有任何限制？

   回答：是，可访问的表具有以下限制：

   * 不支持嵌套表格和表格内的子表单。
   * 仅表的顶行或左列支持标头。 中间表元素不支持标头。 如果所有行与列与表的最顶行或最左侧的列一起使用，则可以将标题应用于多个支持行和列标题。
   * `Rowspan`和 `colspan`不支持来自表中的随机位置。

   * 无法动态添加或删除包含rowspan值大于1的元素的行的实例。

1. 屏幕阅读器的工具提示和说明的阅读顺序是什么？

   回答：
   * 如果同时存在标题和工具提示，则仅读取标题。 如果标题不可用，则阅读工具提示。 您还可以使用表单设计器指定在XDP中读取的优先级
   * 当您将光标悬停在元素上时，将显示工具提示。 如果工具提示不可用，则会显示语音文本。 如果语音文本不可用，则显示字段名称。

1. 将光标悬停在字段上时，将显示工具提示。 如何禁用它？

   回答：要在悬停鼠标时禁用工具提示，请在设计器的辅助功能面板中选择“无”。

1. 在Designer中，用户可以配置单选按钮和复选框的自定义外观属性。 在渲染表单时，HTML5表单是否考虑此类自定义外观属性？

   回答：HTML5表单忽略单选按钮和复选框的自定义外观属性。 单选按钮和复选框将按照基础浏览器的规范显示。

1. 在支持的浏览器中打开HTML5表单时，相邻放置字段的边框未正确对齐或子表单显示重叠。 在Forms Designer中预览同一HTML5表单时，字段和布局不会出现不对齐，并且子表单会显示在正确的位置。 如何修复此问题？

   答案：当子表单设置为流动内容并且子表单具有隐藏的边框元素时，相邻放置字段的边框未正确对齐或子表单显示重叠。 要解决此问题，您可以移除或注释隐藏的 &lt;border> 元素对应的扩展dp中。 例如，以下各项 &lt;border> 元素被标记为注释：

   ```xml
               <!--<border>
                  <edge presence="hidden"/>
                  <corner thickness="0.175mm" presence="hidden"/>
               </border> -->
   ```

1. 为什么屏幕阅读器无法正确处理日期/时间字段对象？

   答案：屏幕阅读器不支持日期/时间字段。 但是，您可以在字段中手动输入日期/时间，以使屏幕阅读器能够阅读该字段。 使用工具提示或屏幕阅读器文本指示用户手动选择字段的日期/时间。

1. HTML5表单是否支持浮动字段的显示模式？

   答案：HTML5表单不支持浮动字段的显示模式。

1. HTML5 Forms中日期字段的格式是什么？

答案：日期字段接受ISO格式，YYYY-MM-DD。 如果以某种其他格式指定日期，则在用户退出该字段之前，日期字段不接受格式。

### 脚本 {#scripting}

1. 在用于HTMLForms的JavaScript实施中是否有任何限制？

   回答：

   * xfa.connectionSet脚本的支持有限。 对于connectionSet，仅支持在服务器端调用Web服务。 有关详细信息，请参阅 [脚本支持](/help/forms/using/scripting-support.md).
   * 客户端脚本不支持$record和$data。 但是，如果脚本是在formReady、layoutReady块中编写的，则脚本仍然有效，因为这些事件在服务器端运行。
   * 不支持特定于XFA Draw元素的脚本，例如更改Draw文本（如果存在字段，则更改Caption文本）。

1. 使用formCalc是否有任何限制？

   回答：当前仅实现了formCalc脚本的子集。 有关详细信息，请参阅 [脚本支持](/help/forms/using/scripting-support.md).

1. 是否有任何推荐的命名惯例以及要避免的保留关键字？

   回答：
   * 在AEM Forms Designer中，建议不要以下划线(_)。 要在名称开头使用下划线，请在下划线后添加前缀，_&lt;prefix>&lt;objectname>.
   * 所有HTML5 Forms API都是保留关键词。 对于自定义API/函数，请使用与不同的名称 [HTML5 Forms API](/help/forms/using/scripting-support.md).

1. HTML5表单是否支持浮动字段？

   回答：是，HTML5 Forms支持浮动字段。 要启用浮动字段，请将以下属性添加到渲染配置文件：

   >[!NOTE]
   >
   >默认情况下，这些字段不启用浮动显示。 您可以使用Forms Designer设置字段的浮动属性。

   1. 打开CRXde Lite并导航到 `/content/xfaforms/profiles/default` 节点。
   1. 添加属性 `mfDataDependentFloatingField`类型为字符串并将属性的值设置为 `true`.
   1. 单击 **全部保存**. 现在，使用更新的渲染配置文件为HTMLForms启用了浮动字段。

      >[!NOTE]
      >
      >要在不更新渲染配置文件的情况下为特定表单启用浮动字段，请将mfDataDependentFloatingField=true属性作为URL参数传递。

1. HTML5表单是否多次执行初始化脚本和表单就绪事件？

   回答：是，初始化脚本和表单就绪事件会执行多次，在服务器上至少执行一次，在客户端执行一次。 建议基于某些业务逻辑（表单或字段数据）编写初始化或表单：ready事件等脚本，以便基于数据和幂等状态（如果数据相同）执行操作。

### 设计XDP {#designing-xdp}

1. HTML5表单中是否有保留关键词？

   答案：所有HTML5 Forms API都是保留关键词。 对于自定义API/函数，请使用与不同的名称 [HTML5 Forms API](/help/forms/using/scripting-support.md). 除了保留的关键字之外，如果您使用以下划线(_)开头的对象名称，建议在下划线后添加唯一的前缀。 添加前缀有助于避免与HTML5表单内部API发生任何可能的冲突。 例如，`_fpField1`
