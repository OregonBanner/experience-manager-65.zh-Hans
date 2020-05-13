---
title: HTML5表单的常见问题解答(FAQ)
seo-title: HTML5表单的常见问题解答(FAQ)
description: 关于HTML5表单的布局、脚本支持和范围的常见问题解答(FAQ)。
seo-description: 关于HTML5表单的布局、脚本支持和范围的常见问题解答(FAQ)。
uuid: 398e31de-3e46-4288-b3cd-39d51fa17abc
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 4b676e7e-191f-4a19-8b8f-fc3e30244b59
docset: aem65
translation-type: tm+mt
source-git-commit: 407b4d0b86c6bcbff11a085ea10bd3bf90115257
workflow-type: tm+mt
source-wordcount: '1970'
ht-degree: 0%

---


# HTML5表单的常见问题解答(FAQ){#frequently-asked-questions-faq-for-html-forms}

有关HTML5表单的布局、脚本支持和范围的一些常见问题(FAQ)。

## 布局 {#layout}

1. 为什么条码和签名字段不显示在我的表单中？

   答案： 条码和签名字段与HTML或移动场景无关。 这些字段显示为非交互区域。 但是，AEM Forms Designer提供了一个新的签名涂抹字段，可以使用它代替签名字段。 您还可以为条码添 [加自定义](../../forms/using/custom-widgets.md) 构件并将其集成。

1. XFA文本字段是否支持富文本？

   答案： 不支持XFA字段（它允许AEM Forms Designer中的丰富内容），它将呈现为普通文本，而不支持从用户界面设置文本样式。 此外，具有梳状属性的XFA字段显示为普通字段，但根据梳状数字的值，仍对允许的字符数有限制。

1. 使用可重复子表单是否存在任何限制？

   答案： 可重复的子表单的初始计数应为1或更多。 不支持初始计数为零的可重复子表单。 您还可以选择使用可重复的子表单，而不是在加载表单时显示它。 要实现用例：

   1. 将可重复子表单的初始计数设置为1。

      ![初数](assets/intial-count.png)

   1. 使用表单的初始化事件隐藏子表单的主实例。 例如，下面的代码在表单初始化时隐藏子表单的主要实例。 它还验证应用程序类型以确保脚本仅在客户端执行：

      ```
      if ((xfa.host.appType == "HTML 5" || xfa.host.appType == "Exchange-Pro" || xfa.host.appType == "Reader")&&(_RepeatSubform.count == 1)&&(form1.Page1.Subform1.RepeatSubform.Key.rawValue == null)) {
      RepeatSubform.presence = "hidden";
      }
      ```

   1. 打开用于添加子表单实例的脚本进行编辑。 添加如下代码以添加子表单脚本的实例。

      下面的代码检查子表单的隐藏实例。 如果找到子表单的隐藏实例，请删除子表单的隐藏实例并插入子表单的新实例。 如果找不到子表单的隐藏实例，则只需插入子表单的新实例。

      ```
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

   1. 打开用于删除子表单实例的脚本进行编辑。 添加如下代码以删除子表单脚本的实例。

      代码检查子表单的计数。 如果子表单的计数达到1，则代码将隐藏子表单，而不是删除子表单。

      ```
      if (RepeatSubform.instanceManager.count == 1) {
      RepeatSubform.presence = "hidden";
      } else {
      RepeatSubform.instanceManager.removeInstance(RepeatSubform.instanceManager.count - 1);
      }
      ```

   1. 打开表单的预提交事件进行编辑。 将以下脚本添加到事件，以在编辑之前删除脚本的隐藏实例。 它可防止在提交时发送隐藏子表单的数据。

      ```
      if(RepeatSubform.instanceManager.count == 1 && RepeatSubform.presence == "hidden") {
      RepeatSubform.instanceManager.removeInstance(0);
      }
      ```

1. 使用隐藏子表单有任何限制吗？

   答案： 具有复杂层次结构的隐藏子表单会跨页面拆分，从而导致布局问题。 一种解决方法是将子表单标记为最初可见，然后根据某些逻辑或数据将其隐藏在初始化脚本中。

1. 为什么某些文本会被截断或在HTML5中显示不正确？

   答案： 如果“绘图”或“题注”文本元素没有足够的空间来显示内容，则文本在移动表单再现中会被截断。 此截断操作也可在AEM Forms Designer的设计视图中看到。 尽管此截断可在PDF中处理，但无法在HTML5表单中处理。 要避免此问题，请提供足够的空间来绘制或描述文本，以便它不会在AEM Forms Designer的设计模式中截断。

1. 我正在观察与缺失内容或重叠内容相关的布局问题。 原因何在？

   答案： 如果在同一位置（如矩形）存在“绘图文本”或“绘图图像”元素以及另一个重叠元素，则“绘图文本”内容稍后按文档顺序出现(在AEM Forms Designer层次结构视图中)时将不可见。 PDF支持透明分层，但HTML/浏览器不支持透明分层。

1. 为什么HTML表单中显示的某些字体与设计表单时使用的字体不同？

   答案： HTML5表单不嵌入字体（与字体嵌入在表单中的PDF表单相反）。 要使表单的HTML版本按预期呈现，请确保在XDP中指定的字体在服务器和客户端计算机上可用。 如果服务器上不提供所需的字体，则使用回退字体。 此外，如果您在表单模板中使用客户端设备上不可用的字体，则使用浏览器的默认字体来呈现文本。

1. HTML表单中是否支持vAlign和hAlign属性？

   是，支持vAlign和hAlign属性。 Internet Explorer和多行字段中不支持vAlign属性。

1. HTML5表单是否支持希伯来语字符？

   HTML5表单支持除Microsoft Internet Explorer外的所有浏览器中的希伯来语字符。

1. HTML5表单对数字字段是否有任何限制？

   答案： 是的，HTML5表单有一些限制。 如果数字数大于图片子句中指定的计数，则数字未本地化，并以英语区域设置显示。

1. 为什么HTML表单比PDF表单大？

   要将XDP渲染为HTML表单，需要许多中间数据结构和对象，如表单dom、数据dom和布局dom。

   对于PDF表单，Adobe Acrobat具有一个内置的XTG引擎，用于创建中间数据结构和对象。 Acrobat还负责布局和脚本。

   对于HTML5表单，浏览器没有内置的XTG引擎来创建中间数据结构和来自原始XDP字节的对象。 因此，对于HTML5表单，在服务器上生成中间结构并发送到客户端。 在客户端，基于javascript的脚本和布局引擎使用这些中间结构。

   中间结构的大小取决于原始XDP的大小以及与XDP合并的数据。

1. 在xdp中使用表是否存在任何限制？

   答案： 复杂表导致渲染中出现问题。

   * 不支持表中的节（子表单集）。
   * 某些表中的页眉或页脚行被标记为重复。 将这些表分割到多个页面可能会遇到一些问题。

1. 可访问的表是否有任何限制？

   答案： 是的，可访问表具有以下限制：

   * 不支持表中的嵌套表和子表单。
   * 表的顶行或左列仅支持标题。 中间表元素不支持标题。 您可以将标题应用于多个行并支持列标题，前提是所有此类行和列以及表的最顶行或最左列。
   * `Rowspan`并且 `colspan`不支持从表内的随机位置进行访问。

   * 不能动态添加或删除包含行跨值大于1的元素的行实例。

1. 屏幕阅读器的工具提示和题注的阅读顺序是什么？

   * 当同时存在题注和工具提示时，将读取唯一的题注。 如果描述不可用，则会读取工具提示。 您还可以使用表单设计器指定XDP中阅读的优先级
   * 悬停某个元素时，将显示工具提示。 如果工具提示不可用，则显示语音文本。 如果语音文本不可用，则显示字段名称。

1. 悬停字段时，将显示工具提示。 如何禁用它？

   要在悬停时禁用工具提示，请在设计器的“辅助功能”面板中选择“无”。

1. 在设计器中，用户可以配置单选按钮和复选框的自定义外观属性。 是否，在呈现表单时，HTML5表单会考虑此类自定义外观属性？

   答案： HTML5表单会忽略单选按钮和复选框的自定义外观属性。 单选按钮和复选框根据基础浏览器的规范显示。

1. 在支持的浏览器中打开HTML5表单时，相邻放置的字段的边框不正确对齐或子表单显示重叠。 在Forms Designer中预览同一HTML5表单时，字段和布局不会出现不对齐，子表单会出现在正确的位置。 如何解决此问题？

   当子表单设置为流内容且子表单具有隐藏的边框元素时，相邻放置的字段的边框将不正确对齐或子表单显示重叠。 要解决此问题，可以从相应的XDP中删除或注释隐藏的&lt;border>元素。 例如，以下&lt;border>元素被标记为注释：

   ```xml
               <!--<border>
                  <edge presence="hidden"/>
                  <corner thickness="0.175mm" presence="hidden"/>
               </border> -->
   ```

1. 为什么屏幕阅读器不能正确处理日期／时间字段对象？

   屏幕阅读器不支持日期／时间字段。 但是，您可以手动输入字段的日期／时间，以使屏幕阅读器阅读该日期／时间。 使用工具提示或屏幕阅读器文本指示用户手动选择字段的日期／时间。

1. HTML5表单是否支持浮动字段的显示模式？

   答案： HTML5表单不支持浮动字段的显示模式。

### 脚本 {#scripting}

1. HTML表单的JavaScript实现有任何限制吗？

   答案:

   * 对xfa.connectionSet脚本的支持有限。 对于connectionSet，仅支持对Web服务的服务器端调用。 有关详细信息，请参阅 [脚本支持](/help/forms/using/scripting-support.md)。
   * 客户端脚本中不支持$record和$data。 但是，如果脚本以formReady、layoutReady块编写，则脚本仍然有效，因为这些事件在服务器端运行。
   * 不支持XFA Draw元素特定的脚本，如更改Draw文本（或字段大小写时的Caption文本）。

1. 使用formCalc有任何限制吗？

   答案： 当前仅实现formCalc脚本的子集。 有关详细信息，请参阅 [脚本支持](/help/forms/using/scripting-support.md)。

1. 是否存在推荐的命名规范，是否存在保留的关键字？

   * 在AEM Forms Designer中，建议不要以下划线(_)开头的对象（如子表单或文本字段）的名称。 要在名称的开头使用下划线，请在下划线后面添加前缀_&lt;prefix>&lt;objectname>。
   * 所有HTML5表单API都是保留关键字。 对于自定义API/函数，请使用与HTML5表单API不 [同的名称](/help/forms/using/scripting-support.md)。

1. HTML5表单是否支持浮动字段？

   是，HTML5 Forms支持浮动字段。 要启用浮动字段，请向渲染用户档案添加以下属性：

   >[!NOTE]
   >
   >默认情况下，字段不启用浮动。 您可以使用表单设计器设置字段的浮动属性。

   1. 打开CRXde lite并导航到该 `/content/xfaforms/profiles/default` 节点。
   1. 添加String类 `mfDataDependentFloatingField`型的属性，并将该属性的值设置为 `true`。
   1. 单击“ **全部保存**”。 现在，使用更新的呈现用户档案为HTML表单启用浮动字段。

      >[!NOTE]
      >
      >要为特定表单启用浮动字段而不更新呈现用户档案，请将mfDataDependentFloatingField=true属性作为URL参数传递。

1. HTML5表单是否多次执行初始化脚本和表单就绪事件?

   是的，初始化脚本和表单就绪事件执行多次，至少在服务器上执行一次，在客户端执行一次。 建议根据某些业务逻辑(表单或字段事件)编写诸如初始化或表单：就绪型脚本的脚本，以便根据数据状态和幂等元（如果数据相同）执行操作。

### 设计XDP {#designing-xdp}

1. HTML5表单中是否有保留的关键字？

   答案： 所有HTML5表单API都是保留关键字。 对于自定义API/函数，请使用与HTML5表单API不 [同的名称](/help/forms/using/scripting-support.md)。 除保留关键字外，如果您使用以下划线(_)开头的对象名称，建议在下划线后添加唯一前缀。 添加前缀有助于避免与HTML5表单内部API的任何可能冲突。 例如，`_fpField1`
