---
title: 创建交互式通信
seo-title: 创建交互式通信
description: 使用交互式通信编辑器创建交互式通信。 使用拖放功能构建交互式通信，并在不同设备类型上预览打印和Web输出。
seo-description: 使用交互式通信编辑器创建交互式通信。 使用拖放功能构建交互式通信，并在不同设备类型上预览打印和Web输出。
uuid: d524a3de-00b4-444f-b3c7-be443fa24ec8
topic-tags: interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: f4d98cb9-84d8-4735-91d2-b9ceec861e5e
docset: aem65
translation-type: tm+mt
source-git-commit: 3271ad3a7d0daac731803975e12d79b77905068a
workflow-type: tm+mt
source-wordcount: '6107'
ht-degree: 1%

---


# 创建交互式通信{#create-an-interactive-communication}

## 概述 {#overview}

交互通信集中管理个性化的交互式通信的创建、组合和投放。 将打印作为Web的主控渠道，您可以最大限度地减少在创建交互通信的Web输出时的重复工作。

### 前提条件 {#prerequisites}

以下是创建交互式通信的先决条件：

* 设置包含 [测试数据](/help/forms/using/data-integration.md) ，或与实际数据源（如Microsoft® Dynamics的实例）一起设置表单数据模型。
* 确保您拥有 [文档片段](/help/forms/using/document-fragments.md)。
* 确保您拥有 [用于印刷和Web渠道的模板](/help/forms/using/web-channel-print-channel.md)。
* 确保您拥有Web [渠道](/help/forms/using/themes.md) 所需的主题。

## 创建交互式通信 {#createic}

1. 登录到AEM作者实例，然后导航到 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL 表单]** > **[!UICONTROL 表单和文档]**。
1. 点按 **[!UICONTROL 创建]** ，然后选择 **[!UICONTROL 交互式通信]**。 “创建交互式通信”页面。

   ![创建交互通信](assets/create-interactive-communication.png)

1. 输入以下信息。 : 

   * **[!UICONTROL 标题]**: 输入交互通信的标题。
   * **[!UICONTROL 名称]**: 交互通信的名称是从您输入的标题派生的。 根据需要编辑它。
   * **[!UICONTROL 描述]**: 输入有关交互式通信的说明。
   * **[!UICONTROL 表单数据模型]**: 浏览并选择表单数据模型。 有关表单数据模型的详细信息，请参阅 [AEM Forms数据集成](/help/forms/using/data-integration.md)。

   * **[!UICONTROL 预填服务]**: 选择预填服务以检索数据并预填交互通信。
   * **[!UICONTROL 后处理类型]**: 您可以选择在提交交互式通信时触发的AEM或表单工作流。 选择要触发的工作流类型。

   * **[!UICONTROL 后期处理]**: 选择要触发的工作流的名称。 选择AEM工作流时，请提供附件路径、布局路径、PDF路径、打印数据路径和Web数据路径。
   * **[!UICONTROL 标记]**: 选择要应用于交互式通信的标记。 您还可以键入新／自定义标记名称，然后按Enter创建它。
   * **[!UICONTROL 作者]**：作者姓名自动取自已登录用户的用户名。
   * **[!UICONTROL 发布日期：]** 输入发布交互式通信的日期。
   * **[!UICONTROL 取消发布日期]**: 输入取消发布交互式通信的日期。

1. 点按 **[!UICONTROL 下一步]**。 将显示用于指定打印和Web渠道详细信息的屏幕。
1. 输入以下内容：

   * **[!UICONTROL 打印]**: 选择此选项可生成交互式通信的打印渠道。
   * **[!UICONTROL 打印模板]**: 浏览并选择XDP作为打印模板。
   * **[!UICONTROL Web]**: 选择此选项可生成Web渠道或交互式通信的响应式输出。
   * **[!UICONTROL 交互通信Web模板]**: 浏览并选择Web模板。
   * **[!UICONTROL 主题]** 和 **[!UICONTROL 选择主题]**: 浏览并选择主题，为交互式通信的Web渠道设置样式。 有关详细信息，请参阅 [AEM Forms主题](/help/forms/using/themes.md)。

   * **[!UICONTROL 将打印作为主控用于Web渠道]**: 选择此选项可创建与打印渠道同步的Web渠道。 将打印渠道用作Web渠道的主控，可确保Web渠道的内容和数据绑定是从打印渠道派生的，并且点按同步时，打印渠道中所做的更改会反映在Web渠道中。 但是，作者可以根据需要中断Web渠道中特定组件的继承。 有关详细信息，请参 [阅将Web渠道与打印渠道同步](../../forms/using/create-interactive-communication.md#synchronize)。
如果选择“ **[!UICONTROL 将打印为主控用于Web渠道]** ”选项，则可以选择以下任何模式以生成Web渠道:

      * **[!UICONTROL 自动布局]**: 选择此模式可自动为Web渠道从打印渠道生成占位符、内容和数据绑定。
      * **[!UICONTROL 手动组织]**: 选择此模式，可使用“数据源”选项卡中提供的主控内容手动选择“打印渠道”元素并将其 **[!UICONTROL 添加到Web]** 渠道。 有关详细信息，请参 [阅选择打印渠道元素以创建Web渠道内容](#selectprintchannelelements)。

   有关打印渠道和Web渠道的详细信息，请参 [阅打印渠道和Web渠道](/help/forms/using/web-channel-print-channel.md)。

1. 点按&#x200B;**[!UICONTROL 创建]**。此时会创建交互通信并显示警报框。 点按 **[!UICONTROL 编辑]** ，以开始构建交互式通信的内容，如使用交互式 [通信创作用户界面添加内容中所述](#step2)。 或者，您也可以点按 **[!UICONTROL 完成]** ，然后选择稍后编辑交互式通信。

## 将内容添加到交互式通信 {#step2}

创建交互式通信后，可以使用交互式通信创作界面来构建其内容。

有关交互式通信创作界面的详细信息，请参 [阅交互式通信创作介绍](/help/forms/using/introduction-interactive-communication-authoring.md)。

1. 按照创建交互式通信中所述的点按编辑，将启动交互式 [通信创作界面](#createic)。 或者，您也可以导航到AEM上的现有交互式通信资产，将其选中，然后点 **[!UICONTROL 按编辑]** ，以启动交互式通信创作界面。

   默认情况下，将显示交互通信的打印渠道，除非交互通信仅限Web渠道。 交互通信的打印渠道显示目标区域，如所选XDP/打印渠道模板中所示。 在这些目标区域和字段中，您可以添加组件或资产。

1. 选择“打印”渠道后，选择“组 **[!UICONTROL 件]** ”选项卡。 打印渠道中提供以下组件：

   | **组件** | **功能** |
   |---|---|
   | 图表 | 添加一个图表，您可以在交互通信中使用该图表来直观地表示从表单数据模型集合检索的二维数据。 有关详细信息，请参 [阅在Interactive Communications中使用图表](/help/forms/using/chart-component-interactive-communications.md)。 |
   | 文档片段 | 允许您向交互式通信中添加可重用的组件，如文本、列表或条件。 添加的组件可以是基于表单数据模型的组件，也可以是没有表单数据模型的组件。 |
   | 图像 | 允许插入图像。 |

   将组件拖放到您的交互式通信中，并根据需要进行配置。

   在为打印和Web渠道创作交互式通信时，您还可以使用撤消和重做操作。

   使用撤消操作可放弃上次执行的操作，而重做操作可再次合并放弃的操作。 例如，如果您已在交互式通信中插入图像或创建了数据绑定，并需要放弃它，请使用撤消操作。

   ![撤消重做操作](assets/undo_redo_actions_new.png)

   撤消和重做选项显示在创作UI页面工具栏上。 撤消选项仅在执行操作后显示。 只有在执行撤消操作后，重做选项才会显示在页面工具栏上。 刷新页面时将重置这些操作。

1. 选择打印渠道后，转到 **[!UICONTROL 资产]** 选项卡，并应用筛选器以仅显示要查看的资产。

   使用资产浏览器，您还可以直接将资产拖放到交互式通信目标区。

   ![assets-docfragments](assets/assets-docfragments.png)

1. 将文档片段拖放到交互通信中。 以下是可在交互通信的打印渠道中使用的文档片段类型。

<table>
 <tbody>
  <tr>
   <td><strong>文档片段类型</strong></td>
   <td><strong>示例用途</strong></td>
  </tr>
  <tr>
   <td><a href="/help/forms/using/texts-interactive-communications.md" target="_blank">文本</a></td>
   <td>用于添加地址、收件人电子邮件和信件正文的文本 </td>
  </tr>
  <tr>
   <td><a href="/help/forms/using/conditions-interactive-communications.md" target="_blank">条件</a></td>
   <td>根据策略类型向通信中添加适当的头图像的条件： 标准版或高级版。 <br /> </td>
  </tr>
  <tr>
   <td>列表</td>
   <td>文档片段组，包括文本、条件、其他列表和图像。 <br /> </td>
  </tr>
 </tbody>
</table>

您还可以使用“资产”选项卡将新片段拖放到目标区域，以替换目标区域和文档片段之 **[!UICONTROL 间的]** 绑定。 拖动片段时目标区域的蓝色底纹表示文档片段可以拖放到目标区域。

有关文档片段的详细信息，请参 [阅文档片段](/help/forms/using/document-fragments.md)。

创作界面使您能够区分未绑定字段和绑定字段以及交互式通信中的变量。 该接口使用橙色边框高亮显示未绑定字段和变量。

![unbind_fields_variables_highlights_dc](assets/unbound_fields_variables_highlights_dc.jpg)

此外，当您将鼠标悬停在这些元素上时，将显示一个工具提示，其中显示“字段”（未绑定）或“变量”（未绑定）消息。

在文档片段中使用的未绑定变量有时不能显示在创作界面上。 它可能是由于文档片段中的内联文本规则，或者是条件片段。 在这种情况下，以蓝色突出显示的工具提示将作为文档片段的一部分显示。 工具提示显示在文档片段中使用的未绑定变量数。

![未绑定变量](assets/df_unbound_variable_new.png)

点按文档片段，点 ![按configure_icon](assets/configure_icon.png) (Configure)，然后点 **[!UICONTROL 按交互式]** 通信Sidekick中的属性。 “变 **[!UICONTROL 量和数据模型对象]** ”部分列表变量，包括隐藏变量和文档片段中使用的数据模型对象。 使用每 ![个数据模型](assets/edit.svg) 对象或变量旁边的编辑（编辑）图标编辑属性。

1. 要设置变量的绑定，请点按变量， ![选择configure_icon](assets/configure_icon.png) (Configure)，然后在提要栏的“属性”面板中设置绑定属性。

   * **无**: 代理将填写变量的值。
   * **文本片段**: 如果选中，您可以浏览并选择其内容呈现在字段中的文本文档片段。 只有那些文本文档片段可以绑定到中没有变量的变量。
   * **数据模型对象**: 选择其值填充在字段中的表单数据模型属性。
   * **默认值：** 您可以使用此字段为变量定义默认值。 当您预览交互式通信或在代理UI中时，将显示该值。
   * **显示图案：** 您还可以为变量定义显示格式。 从“类型”(Type)下拉列表中 **选择** 任何预定义选项，将显示格式应用于变量。 选择 **“自定** 义”以定义列表中不可用的显示模式。 有关详细信息，请参阅 [数据显示模式](../../forms/using/create-interactive-communication.md#datadisplaypatterns)。

   导航到 [变量和文档模型对象](../../forms/using/create-interactive-communication.md#hiddenvariables) ，以设置隐藏变量在数据片段中的绑定。

   您还可以拖放数据源元素或文本文档片段以设置变量绑定。  要创建与任意数据源元素的绑定，请选 **择数据源** (Data Sources)选项卡，并将元素拖放到变量名称中。 数据源元素和变量的类型必须相同，才能成功设置绑定。 如果将数据源元素拖放到已绑定的变量，则新元素将替换前一个元素，以使用该变量创建新绑定。 同样，选择 **资产** 选项卡，将文本文档片段拖放到变量名以设置它们之间的绑定。 文本文档片段不能包含任何变量。

1. 要添加表格，在选择打印渠道的情况下，在“资 **[!UICONTROL 产]** ”选项卡中应用筛选器以仅显示布局片段。 将所需的布局片段拖放到交互通信中。 布局片段基于XDP，可用于在交互通信中创建图形布局或使用动态数据填充的静态和动态表。

   示例： 一个布局表，用于显示高保费、忠诚度折扣%，以及旧政策和新政策的紧急路边援助。

   有关布局片段的详细信息，请参阅 [文档片段](/help/forms/using/document-fragments.md)。

1. 选择打印渠道后，在“资产”选 **[!UICONTROL 项卡中]** ，将过滤器应用于显示图像。 将所需的图像拖放到交互式通信中，如公司徽标。

   此外，在交互通信中管理以下内容：

   * [添加和配置图表](/help/forms/using/chart-component-interactive-communications.md)
   * [使Web渠道与打印渠道同步](../../forms/using/create-interactive-communication.md#synchronize)

      * 自动同步
      * 取消继承
      * 重新启用继承
      * 同步
   * [附件和库访问](../../forms/using/create-interactive-communication.md#attachmentslibrary)
   * [XDP/布局字段属性](../../forms/using/create-interactive-communication.md#xdplayoutfieldproperties)
   * [向组件添加规则](../../forms/using/create-interactive-communication.md#rules)


1. 切换到 **[!UICONTROL Web渠道]**。 Web渠道显示在交互式通信编辑器中。 首次从“打印”渠道切换到“Web”渠道时，将进行自动同步。 有关详细信息，请参 [阅从打印渠道同步Web渠道](../../forms/using/create-interactive-communication.md#synchronize)。

   由于本例中我们将“打印”作为Web的主控，因此“打印”渠道占位符、内容和数据绑定将同步到Web渠道。 但是，您可以在Web渠道中更改和自定义特定内容。 [取消继承](#cancelinheritance) ，以使用打印目标生成渠道区域和变量，以便能够自定义内容。

   ![Web频道资源](assets/webchannelassets.png)

   点按文档片段，点 ![按configure_icon](assets/configure_icon.png) (Configure)，然后点 **[!UICONTROL 按交互式]** 通信Sidekick中的属性。 “变 **[!UICONTROL 量和数据模型对象]** ”部分列表变量，包括隐藏变量和文档片段中使用的数据模型对象。 使用每 ![个数据模型](assets/edit.svg) 对象或变量旁边的编辑（编辑）图标编辑属性。 此外，对于在Web文档中使 [用打印](#synchronize) 渠道自动生成的渠道片段 ![](assets/cancelinheritance.png) ，请使用每个数据模型对象和变量旁的（取消继承）图标 [来取消继承](#cancelinheritance) ，并可以编辑继承。

1. 要在Web渠道中添加其他组件，请在选择Web渠道后点按 **[!UICONTROL 组件]**。 根据需要在交互通信的Web渠道中拖放组件，然后继续配置它们。

   | 组件 | 功能 |
   |---|---|
   | 图表 | 添加一个图表，您可以在交互通信中使用该图表来直观地表示从表单数据模型集合检索的二维数据。 有关详细信息，请参 [阅使用图表组件](../../forms/using/chart-component-interactive-communications.md)。 |
   | 文档片段 | 允许您向交互式通信中添加可重用的组件、文本、列表或条件。 您添加到交互式通信的可重用组件可以是基于表单数据模型的组件，也可以是没有表单数据模型的组件。 |
   | 图像 | 允许插入图像。 |
   | 面板 | 允许您向交互 [式](../../forms/using/create-interactive-communication.md#add-panel-component-to-the-web-channel) 通信添加面板。 |
   | 表 | 添加表格以便按行和列整理数据。 |
   | 目标区域 | 在Web渠道中插入目标区域以组织Web渠道特定的组件。 目标区域是一个简单容器，它允许您对Web渠道特定组件进行分组。 |
   | 文本 | 将富文本添加到交互式通信的Web渠道。 文本还可以利用表单数据模型对象来使内容动态化。 |
   | 按钮 | 允许您向交互 [式](../../forms/using/create-interactive-communication.md#add-button-component-to-the-web-channel) 通信添加按钮。 您可以使用“按钮”组件导航到其他交互通信、自适应表单、其他资产(如图像或文档片段)或外部URL。 |
   | 分隔符 | 允许您在交互式通信中插入一条水平线。 使用此组件可区分通信中的各个部分。 例如，您可以使用分隔符组件在信用卡对帐单中区分“客户详细信息”和“信用卡详细信息”部分。 |

1. 根据需要，在您的Web渠道中插入资源。

   您可 [以预览您的交互式通信](#previewic) ，查看交互式通信的打印和Web输出的外观并根据需要继续进行更改。

## 预览交互式通信 {#previewic}

您可以使用 **预览选项** ，来评估交互式通信的外观。 交互通信的Web渠道还提供了一个选项，用于模拟各种设备的交互通信体验。 例如，iPhone、iPad和Desktop。 您可以将预览 **和** “器 **”** 、“模拟器 ![”标](assets/ruler.png) 尺选项结合使用，以预览屏幕大小不同的设备的Web输出。 预览中的示例数据从指定的表单数据模型填充。

1. 选择（打印或Web）渠道以预览并点按预览。 出现交互式通信。

   >[!NOTE]
   >
   >预览将填充指定表单数据模型的示例数据。 有关使用某些其他数据或使用预填服务预览交互式通信的详细信息，请 [参阅使用表单数据模型](/help/forms/using/using-form-data-model.md)[和使用表单数据模型](/help/forms/using/work-with-form-data-model.md)。

1. 对于Web渠道，使用 ![标尺](assets/ruler.png) ,视图交互式通信在各种设备上的外观。

   ![Web频道预览](assets/webchannelpreview.png)

此外，您还可 [以使用代理UI准备和发送交互式通信](/help/forms/using/prepare-send-interactive-communication.md)。

## 在交互通信中配置属性  {#configure-properties-in-interactive-communication}

### 附件和库访问 {#attachmentslibrary}

在打印渠道中，您可以配置附件和库访问权限以允许代理在交互通信的代理UI中管理附件：

1. 在打印渠道中，高亮显示文档容器并点 **按属性**。

   ![文档容器属性](assets/documentcontainerproperties.png)

   “属性”面板显示在提要栏中。

   ![属性附件](assets/propertiesattachments.png)

1. 展开 **附件** ，并指定以下属性：

   * **[!UICONTROL 允许库访问]**: 选择此选项可在代理UI中为代理启用库访问。 如果启用，代理可在准备交互通信时从库添加文件。
   * **[!UICONTROL 允许对附件重新排序]**: 选择此选项可使代理通过交互式通信重新排序附件。
   * **[!UICONTROL 允许的最大附件数]**: 指定交互式通信允许的最大附件数。
   * **[!UICONTROL 要附加的文件]**: 点按 **[!UICONTROL 添加]** ，然后浏览以选择要附加的文件，并指定以下内容：

      * **[!UICONTROL 默认情况下，将此文件附加到文档]**: 如果附件不是“必填”，则可以更改此选项。
      * **[!UICONTROL 强制：]** 代理将无法在代理UI中删除附件。

   ![附件](assets/attachfiles.png)

1. 点按&#x200B;**[!UICONTROL 完成]**。

### XDP/布局字段属性 {#xdplayoutfieldproperties}

1. 编辑交互式通信的打印渠道时，将指针悬停在打印渠道模板中构建的字段上，然后选择 ![configure_icon](assets/configure_icon.png) (Configure)。

   提要栏中将显示“属性”对话框。

   ![data_display_patterns_fields](assets/data_display_patterns_fields.jpg)

1. 指定以下内容：

   * **[!UICONTROL 名称]**: JCR节点名称。
   * **[!UICONTROL 标题]**: 在代理UI和文档容器树中输入代理将可见的标题。
   * **[!UICONTROL 绑定类型]**: 为字段选择以下绑定类型之一。

      * 无： 代理将填写属性的值。
      * 文本片段： 如果选中，您可以浏览并选择其内容呈现在字段中的文本文档片段。 或者，将文本文档片段拖放到字段名称以设置它们之间的绑定。 文本文档片段不能包含任何变量。
      * 数据模型对象： 选择其值填充在字段中的表单数据模型属性。 或者，选择 **数据源** 选项卡，并将属性拖放到字段。
   * **[!UICONTROL 默认值]**: 默认值确保在指定的数据模型对象或文本片段没有提供值时字段不为空。 如果数据绑定类型为无，则在字段中预填充默认值。
   * **[!UICONTROL 显示图案]**: 您还可以为字段定义显示格式。 从“类型”(Type)下拉列表中 **选择** 任何预定义选项，将显示格式应用于字段。 选择 **“自定** 义”以定义列表中不可用的显示模式。 有关详细信息，请参阅 [数据显示模式](../../forms/using/create-interactive-communication.md#datadisplaypatterns)

   * **[!UICONTROL 可由代理编辑]**: 选择此选项可允许代理编辑代理UI中字段中的值。 如果绑定类型为文本片段，则此设置不适用。
   * **[!UICONTROL 标签]**: 指定在代理UI中与字段一起显示给代理的文本字符串。 如果绑定类型为文本片段，则此设置不适用。
   * **[!UICONTROL 工具提示]**: 输入将在将鼠标悬停在代理程序UI中时可见的文本字符串。 如果绑定类型为文本片段，则此设置不适用。
   * **[!UICONTROL 必需]**: 选择此项可使座席的字段成为必填字段。 如果绑定类型为文本片段，则此设置不适用。
   * **[!UICONTROL 允许多行]**: 选择此字段可允许在字段中输入多行文本。 如果绑定类型为文本片段，则此设置不适用。


1. 点 ![按done_icon](assets/done_icon.png)。

### 数据显示模式 {#datadisplaypatterns}

创作界面允许您为字段、变量和表单数据模型元素定义数据显示模式，创建用于打印和Web渠道的交互式通信时可用。

要配置数据显示模式，请点按元素，选 ![择configure_icon](assets/configure_icon.png) (Configure)，然后在提要栏的“属性”面 **[!UICONTROL 板中设]** 置显示模式。 从“类型”(Type)下拉列表 **[!UICONTROL 中选择]** “任何预定义”(any pre-defined)选项，以视图与选定类型关联的模式。 从“ **[!UICONTROL 类型]** ”下 **[!UICONTROL 拉列表]** 中选择“自定义”(Custom)，以定义列表中不可用的模式。 在“模式”(Pattern)字 **[!UICONTROL 段中]** ，编辑值会自动将类型修改 **[!UICONTROL 为“自定]**&#x200B;义”。

要应用显示模式，“模式”字段中定义的字符或数字数必须与字段、变量和表单数据模型元素的值中定义的字符或数字匹配或超过。 有关详细信息，请参阅 [示例](../../forms/using/create-interactive-communication.md#greaternumberofdigits)。

![data_display_pattern_example](assets/data_display_patterns_ssn_new.png)

在从打印渠道生成Web内容后，您可以重新定义字段、变量或表单数据模型元素的显示模式。 因此，元素可以具有为打印和Web渠道定义的不同显示模式。 如果未为打印渠道中的元素定义显示模式，并使用打印渠道自动生成Web内容，则为打印渠道中的元素定义的数据绑定定义“类型”(Type)下拉列表中可用的显 **[!UICONTROL 示模式]** 选项。 如果没有为元素定义绑定，则元素的数据类型将定义可用的显示模式选项。 例如，如果为打印渠道中的元素创建“编号”类型的列表绑定，则“类型”下拉中可用的显示模式选项 **[!UICONTROL 为]** “编号”类型，其格式各异。

切换到 **预览** 模式或打开代理UI以视图应用于这些元素的显示模式。

下表列表了为变量设置数据显示模式后显示的值示例：

| 类型 | 默认值 | 显示图案 | 显示值 | 描述 |
|---|---|---|---|---|
| 社会安全号码 | 123456789 | text{999-99-999} | 123-45-6789 | 默认值字段中的位数与“模式”字段中的位数匹配。 成功显示基于图案的值。 |
| 社会安全号码 | 1234567 | text{999-99-999} | 1-23-4567 | 默认值字段中的位数小于“模式”字段中的位数。 该模式适用于7个可用数字。 |
| 社会安全号码 | 1234567890 | text{999-99-999} | 1234567890 | 默认值字段中的位数大于“模式”字段中的位数。 结果，显示值没有变化。 |

如果未为变量或表单数据模型元素指定显示模式，则默认 [情况下将使用全](https://helpx.adobe.com//experience-manager/6-5/forms/using/interactive-communication-configuration-properties.html) 局文档片段配置。

如果不将显示模式应用于数字预览类型的变量，“打印”文档会根据全局片段配置显示该模式。 如果对默认的全局文档片段配置应用更改，代理UI仍会根据为区域设置定义的默认分隔符显示模式。

同样，对于字段，如果未指定显示模式，则创建打印模板(XDP)时定义的模式将应用于字段。 如果创建打印模板时没有模式，则基于XFA规范的默认模式将应用于这些字段。

此外，如果指定的显示模式不正确或无法应用，则基于XFA规范的默认模式将应用于字段、变量或表单数据模型元素。

## 将规则应用于交互式通信组件 {#rules}

要在交互式通信中对组件或内容进行条件化，请点按组件／内容片段，然后选 ![择创建规则](assets/createruleicon.png) （创建规则）以启动规则编辑器。

有关详细信息，请参阅：

* [规则编辑器](/help/forms/using/rule-editor.md)
* [交互式通信创作简介](/help/forms/using/introduction-interactive-communication-authoring.md)

## 使用表 {#tables}

### 交互通信中的动态表 {#dynamic-tables-in-interactive-communication}

您可以在交互通信中使用布局片段添加动态表。 以下步骤使用信用卡对帐单的示例来说明如何使用布局片段在交互通信中创建动态表。

1. 确保在AEM中提供创建表所需的布局片段。
1. 在交互通信的打印渠道中，从资产浏览器将布局片段（带有多列表）拖放到目标区。

   ![lf_dragdrop](assets/lf_dragdrop.png)

   “交互式通信”布局区域中显示一个表。

   ![lf_dragdrop_table](assets/lf_dragdrop_table.png)

1. 为表的每个单元格指定数据绑定。 要创建可重复行，请在属于公用集合属性的行中插入表单数据模型属性。

   1. 点按表中的单元格，然后选 ![择configure_icon](assets/configure_icon.png) (Configure)。

      提要栏中将显示“属性”对话框。

      ![lf_cell_properties](assets/lf_cell_properties.png)

   1. 配置属性：

      * **[!UICONTROL 名称]**: JCR节点名称。
      * **[!UICONTROL 标题]**: 输入将在交互式通信编辑器中显示的标题。
      * **[!UICONTROL 绑定类型]**: 为字段选择以下绑定类型之一。

         * **[!UICONTROL 无]**
         * **[!UICONTROL 数据模型对象]**: 表单数据模型属性的值将填充在字段中。 或者，选择 **数据源** 选项卡，并将属性拖放到字段。
      * **[!UICONTROL 数据模型对象]**: 其值填充在字段中的表单数据模型属性。
      * **[!UICONTROL 默认值]**: 默认值确保在指定数据模型对象没有提供值时字段不为空。 默认值会预填充在字段中。

      * **[!UICONTROL 可由代理编辑]**: 选择此选项可允许代理编辑代理UI中字段中的值。
   1. 点 ![按done_icon](assets/done_icon.png)。



1. 预览交互式通信以查看用数据呈现的表。

   ![lf_预览](assets/lf_preview.png)

### 仅Web渠道表 {#webchanneltables}

点按Web模板中的根面板，然 **后点** 按+，将 **表组件** 添加到交互通信。 包含两行的表将插入交互通信中。 表的第一行表示表标题。

#### 向表中添加行和列 {#addrowscolumnstable}

**要添加或删除列，请执行以下操作：**

1. 点按表标题行中的默认文本框以视图组件工具栏。
1. 选择 **“添加列** ”或 **“删除列** ”，分别添加或删除表列。

![component_toolbar_table1](assets/component_toolbar_table1.png)

**要添加或删除行，请执行以下操作：**

1. 点按任何表行以视图组件工具栏。 您还可以使用交互式通信Sidekick中的内容浏览器选择表行。
1. 选择 **“添加行** ”或“ **删除行** ”，分别添加或删除表行。 使用工 **具栏中****的“上移** ”和“下移”选项重新排列表中的行。

![组件工具栏](assets/component_toolbar_table_row_new.png)

**A.添** 加行 **B.删** 除行 **C.上移** D.下 **移** 。

#### 添加或编辑表单元格中的文本 {#addedittexttable}

1. 在表单元格中选择默认文本框，然后点 ![](assets/edit.png) 按（编辑）。
1. 在表单元格中键入文本，然后点 ![](assets/done_icon.png) 按以保存它。

#### 在表单元格和数据模型对象元素之间创建绑定 {#createbindingtablecells}

1. 在表行中选择默认文本框，然后点 ![](assets/edit.png) 按（编辑）。
1. 点按数据模型对象下拉列表，然后选择属性。
1. 点按以保存表单元格和数据模型对象属性之间的绑定。

![创建数据绑定](assets/create_data_binding_table_new.png)

#### 为表单元格中的文本创建超链接 {#createhyperlinktable}

1. 在表单元格中选择默认文本框，然后点 ![](assets/edit.svg) 按（编辑）。
1. 选择表单元格中的文本，然后点按超链接图标。
1. 在路径字段中指 **定** URL。
1. 点按 ![](assets/done_icon.png) 以保存超链接属性。

![创建超链接](assets/create_hyperlink_table_new.png)

#### 创建动态表 {#createdynamictables}

在交互通信中，可以使用类型集合的渠道模型属性创建仅限Web的动态表。 此表是集合属性的子属性的表示。 只能编辑表中各个单元格的格式属性。

1. 切换到Web渠道，然后选择显示数据源浏览器。
1. 将集合属性拖放到子表单中。 在子表单中创建表。
1. 预览交互通信的Web预览中的表。

#### 对表中的列排序 {#sortcolumns}

您可以根据交互通信中表中的任意列对数据进行排序。 列中的值可以按升序或降序排序。

可以对包含以下内容的表列应用排序：

* 静态文本
* 数据模型对象属性
* 静态文本和数据模型对象属性的组合

要启用排序，请执行以下操作：

1. 选择表，然后点 ![](assets/configure_icon.png) 按（配置）。 您还可以使用交互式通信 **的Sidekick** 中的内容浏览器选择表。
1. 选择 **启用排序。**
1. 点 ![](assets/done_icon.png) 按以保存表属性。 列标题中的排序图标（向上和向下箭头）表示已启用排序。

   ![启用排序](assets/enable_sorting_new-1.png)

1. 切换到 **预览** 模式以视图输出。 根据表的第一列自动对表进行排序。
1. 单击列标题可根据列对值进行排序。

   带向上箭头的列标题表示：

   * 表会根据该列进行排序。
   * 列中的值以升序显示。

   ![升序排序](assets/sorting_ascending_new-1.png)

   同样，带有向下箭头的列标题表示以降序显示列中的值。

## 编辑交互式通信属性 {#edit-interactive-communication-properties}

创建交互式通信后，您可以在以后编辑其属性。

使用“属 **性** ”页可以：

* 编辑创建交互通信时指定字段的值，如标题和说明。
* 为现有交互式通信添加或删除Web渠道。
* 预览、下载或删除交互式通信
* 打开代 [理UI](/help/forms/using/prepare-send-interactive-communication.md)。

要访问“属 **性** ”页面：

1. 登录到AEM作者实例，然后导航到 **Adobe Experience Manager** > **表单** > **表单和文档**。
1. 选择交互式通信并点按 **属性**。
1. 选择“ **常规** ”选项卡以编 **辑“标题** ”和 **“** 说明”字段。

### 添加或删除Web渠道 {#add-or-delete-the-web-channel}

执行以下步骤，为现有交互通信添加Web渠道:

1. 在“属 **性** ”页面上，选择 **渠道** 选项卡。
1. 选中“ **Web** ”复选框，然后为Web渠道选择模板。
1. 选 **择“将打印用作Web渠道的主控** ”，以启用Web渠道与打印渠道之间的同步。
1. Tap **Save &amp; Close** to save the changes.

   同样，您也可以点 **击** “渠道”选 **项卡上** 的“Web”复选框，从“交互通信”中删除Web渠道。

## 将“按钮”组件添加到Web渠道 {#add-button-component-to-the-web-channel}

您可以将按钮作为组件添加到交互式通信的Web渠道。 使用规则编 [辑器](../../forms/using/rule-editor.md) 定义规则，以便能够在点击按钮时导航到其他交互通信、自适应表单、其他资产(如图像或文档片段)或外部URL。

要添加按钮并定义其规则，请执行以下操作：

1. 点按Web模板中的根面板，然 **后点** 按+，将 **Button组** 件添加到“交互通信”。
1. 点按按钮组件，然 ![](assets/edit-rules.png) 后点按按钮以定义规则。
1. 在“ **时间** ”部分，从 **按钮下** 拉列表的状态中选择已单击。
1. 在Then **部分** :

   1. 从下拉列表中选择操作。 例如，选择 **导航** 到作为操作类型。

   1. 指定交互通信、自适应表单、资产或网页的URL。 例如，以下格式指定URL以导航到另一个交互式通信： https://&lt;server-name>:&lt;port>/editor.html/content/forms/af/&lt;Interactive Communication name>/渠道/&lt;渠道名称——打印或web>.html
   1. 指定在同一选项卡、新选项卡或新窗口中打开资产的选项。
   1. 点按 **完成** ，然后点 **按关** 闭以保存规则。

   同样，您也可以从操作类型下拉列表中选择其他可用选项，如调用服务和提交表单。 有关详细信息，请参阅 [规则编辑器](../../forms/using/rule-editor.md)。

1. 预览交互通信，然后点击按钮以视图第4(b)步中指定的交互通信、自适应表单、资产或网页。

## 将面板组件添加到Web渠道 {#add-panel-component-to-the-web-channel}

面板组件是用于将其他组件分组在一起的占位符，它控制如何在交互通信中布置一组组件（如折叠面板和选项卡）。 面板组件还允许您使一组组件可以为最终用户重复使用，如填写教育凭据所需的多个条目。

执行以下步骤将面板组件添加到Web渠道:

1. 使用以 **下任意选** 项将面板组件插入Web渠道:

   * 点按组件，点 **按** 并选择 **面板组件** 。

   * 从“组 **件** ”浏览器面板中，将Panel **组件拖** 放到“交互式通信”上。

   * 点按“内 **容** ”浏览器 **面板** 中的面板，然后点 **按“添加子面板**”。 选择“添 **加子面板** ”选项将显 **示“添加子面板** ”对话框。 输入面板组件的标题和可选描述和名称。

1. 从内容浏览器 **点按面板** ，以对面板执行其他操作，如配置、编辑规则、复制、删除和插入组件。

   您还可以在内容浏览器中拖放一个面 **板** ，以反映右侧窗格中交互式通信结构的更改。

## 将Web渠道与打印渠道同步 {#synchronize}

在创建交互式通信时选择“打印为Web主控”时，将创建与打印渠道同步的Web渠道，并且Web渠道的内容和数据绑定从打印渠道派生，并且点按“同步”时，打印渠道中所做的更改可能会反映在Web渠道中。

但是，作者可以根据需要中断Web渠道中组件的继承。

![创建打印主控](assets/create_ic_print_master_new-1.png)![打印主控Web](assets/create_ic_print_master_web_new-1.png)

### 自动同步 {#autosync}

如果选择“ **[!UICONTROL 将打印为主控用于Web渠道]** ”选项，则可以选择以下任何模式以生成Web渠道:

* **[!UICONTROL 自动布局]**: 选择此模式可自动为Web渠道从打印渠道生成占位符、内容和数据绑定。
* **[!UICONTROL 手动组织]**: 选择此模式，以使用“渠道源”选项卡中提供的主控内容手动选择“打印渠道”元素并将其添加到Web。 有关详细信息，请参 [阅选择打印渠道元素以创建Web渠道内容](#selectprintchannelelements)。

![创建IC选项](assets/create_ic_options_updated_new.png)

>[!NOTE]
>
>同步渠道仅同步从打印渠道到Web渠道的文档片段、图像、条件、列表和布局片段。 包含此类元素的子表单或父节点不会同步。

### 选择“打印渠道元素”以创建Web渠道内容 {#selectprintchannelelements}

如果在创建交互式通信时选择“打印为主控”，但不选择自动同步选项，则还可以将“打印渠道”元素拖放到Web渠道创作界面。

导航到“ **数据源** ” > **“主控内容** ”以视图打印渠道元素。 将目标区域、字段或表拖放到Web渠道创作界面。 元素名称旁的蓝色圆圈图标表示“打印渠道”元素已包含在Web渠道中。

![主控内容](assets/master_content.png)

### 取消继承 {#cancelinheritance}

在Web渠道中，组件嵌入到目标区域。

将鼠标悬停在Web目标中的相关渠道区或变量上，选 ![择取消继承](assets/cancelinheritance.png) （取消继承），然后在取消继承对话框中，点 **[!UICONTROL 按是]**。

目标区域内组件的继承将被取消，现在您可以根据需要编辑它们。

### 重新启用继承 {#re-enable-inheritance}

在Web渠道中，如果已取消组件的继承，则可以重新启用它。 要重新启用继承，请将指针悬停在包括该组件的相关目标区域的边界上，然后点按重新启 ![用继承](assets/reenableinheritance.png)。

此时会出现“还原继承”对话框。

![反遗产](assets/revertinheritance.png)

如果需要，请选 **[!UICONTROL 择还原继承后同步页面]**。 选择此选项可同步整个交互通信。 如果不选择此选项，则恢复继承时只同步相关目标区域。

点按 **[!UICONTROL 是]**。

### 同步 {#synchronize-1}

如果对Web渠道使用“打印为主控”并对“打印”渠道进行更改，则可以同步内容以将新做的更改引入Web渠道。

1. 要将Web渠道与打印渠道同步，请切换到Web渠道，然后点按更多选项图标。

   ![自动同步选项](assets/auto_sync_options_new.png)

1. 点按以下任一选项：

   * **[!UICONTROL 与打印同步]**: 仅同步继承未取消的目标区域的内容。
   * **[!UICONTROL 重置]**: 将Web渠道内容与“打印”渠道同步，并放弃对Web渠道所做的所有更改。

### 使用组件工具栏对继承的组件执行操作 {#componenttoolbar}

在Web渠道中使用同步选项自动生成内容后，可以对组件执行更多操作，而不取消继承。

![组件工具栏](assets/component_toolbar_inherited_web_new.png)

点按组件以视图以下选项：

* **复制：** 复制组件并将其粘贴到交互通信中的其他位置。
* **剪切：** 在交互通信中将组件从一个位置移动到另一个位置。
* **插入组件：** 在选定组件上方插入组件。
* **粘贴：** 使用上述选项粘贴您剪切或复制的组件。
* **组：** 如果要剪切、复制或粘贴多个组件，请选择多个组件。
* **父项：** 选择组件的父项。
* **视图SOM表达式:** 视图 [组件的](../../forms/using/using-som-expressions-adaptive-forms.md) SOM表达式。

* **在面板中对象分组：** 将组件组合到面板中，以便能够同时对这些组件执行操作。 有关详细信息，请参 [阅在面板中对象进行分组](#groupobjectspanel)。

* **取消继承：** [取消目标](#cancelinheritance) 区域内组件的继承以对其进行编辑。

### Group objects in Panel {#groupobjectspanel}

Web渠道创作界面便于将面板中的组件分组，以便能够同时对这些组件执行操作。 “内 **容** ”选项卡将分组的组件列表为内容树中面板的子元素。

1. 点按组件，然后选择组( ![组](assets/group.jpg))操作。
1. 选择多个组件，然后点 **按面板中的组对象**。

   ![对象组](assets/component_toolbar_group_objects_new.png)

1. 在“面 **板”对话框的** “组对象”中，输入面板的名称。
1. 输入面板的可选标题和说明。
1. 单击 ![bullet_checkmark](assets/bullet_checkmark.png)。

   分组的组件在内容树中显示为面板的子元素。

   ![content_tree_grouping](assets/content_tree_grouping.png)

