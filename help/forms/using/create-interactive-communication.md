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
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# 创建交互式通信{#create-an-interactive-communication}

## 概述 {#overview}

Interactive Communications集中管理个性化的交互式通信的创建、汇编和投放。 利用打印作为Web的主渠道，您可以最大程度地减少创建交互式通信的Web输出时的工作重复。

### 前提条件 {#prerequisites}

以下是创建交互式通信的先决条件：

* 设置包含 [测试数据的表单数据模型](/help/forms/using/data-integration.md) ，或与实际数据源（如Microsoft® Dynamics的实例）一起设置。
* 确保您拥有 [文档片段](/help/forms/using/document-fragments.md)。
* 确保您拥有用于 [印刷和Web渠道的模板](/help/forms/using/web-channel-print-channel.md)。
* 确保您拥有Web渠道所 [需](/help/forms/using/themes.md) 的主题。

## 创建交互式通信 {#createic}

1. 登录到AEM作者实例，然后导航到 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms &amp;文档]**。
1. 点按 **[!UICONTROL 创建]** ，然后选择 **[!UICONTROL 交互式通信]**。 “创建交互式通信”页面。

   ![创建交互通信](assets/create-interactive-communication.png)

1. 输入以下信息。 : 

   * **[!UICONTROL 标题]**:输入交互通信的标题。
   * **[!UICONTROL 名称]**:交互通信的名称是从您输入的标题派生的。 根据需要编辑它。
   * **[!UICONTROL 说明]**:输入有关交互式通信的说明。
   * **[!UICONTROL 表单数据模型]**:浏览并选择表单数据模型。 有关表单数据模型的详细信息，请参阅 [AEM表单数据集成](/help/forms/using/data-integration.md)。

   * **[!UICONTROL 预填服务]**:选择预填服务以检索数据并预填交互通信。
   * **[!UICONTROL 后处理类型]**:您可以选择在提交交互式通信时触发的AEM或表单工作流。 选择要触发的工作流的类型。

   * **[!UICONTROL 后期处理]**:选择要触发的工作流的名称。 选择AEM工作流时，请提供附件路径、布局路径、PDF路径、打印数据路径和Web数据路径。
   * **[!UICONTROL 标记]**:选择要应用于交互通信的标记。 您还可以键入新的／自定义标记名称，然后按Enter创建它。
   * **[!UICONTROL 作者]**：作者姓名自动取自已登录用户的用户名。
   * **[!UICONTROL 发布日期：]** 输入发布交互式通信的日期。
   * **[!UICONTROL 取消发布日期]**:输入取消发布交互式通信的日期。

1. 点按下 **[!UICONTROL 一步]**。 将显示用于指定打印和Web渠道详细信息的屏幕。
1. 输入以下内容：

   * **[!UICONTROL 打印]**:选择此选项可生成交互式通信的打印渠道。
   * **[!UICONTROL 打印模板]**:浏览并选择XDP作为打印模板。
   * **[!UICONTROL Web]**:选择此选项可生成Web渠道或交互式通信的响应式输出。
   * **[!UICONTROL 交互通信Web模板]**:浏览并选择Web模板。
   * **[!UICONTROL 主题]** , **[!UICONTROL 选择主题]**:浏览并选择主题，以设计交互式通信的Web渠道的样式。 有关详细信息，请参阅 [AEM Forms中的主题](/help/forms/using/themes.md)。

   * **[!UICONTROL 使用“打印为主页”进行Web渠道]**:选择此选项可创建与打印渠道同步的Web渠道。 使用打印渠道作为Web渠道的主页，可确保Web渠道的内容和数据绑定从打印渠道派生，并且当您点按“同步”时，打印渠道中所做的更改会反映在Web渠道中。 但是，允许作者根据需要中断Web渠道中特定组件的继承。 有关详细信息，请参 [阅将Web渠道与打印渠道同步](../../forms/using/create-interactive-communication.md#synchronize)。
如果选择“将打 **[!UICONTROL 印为主渠道用于Web渠道”选项]** ，则可以选择以下任一模式以生成Web:

      * **[!UICONTROL 自动布局]**:选择此模式可自动从“打印渠道”中为Web渠道生成占位符、内容和数据绑定。
      * **[!UICONCONTROL手动组织**:选择此模式，可使用“数据源”选项卡中提供的主内容手动选择“打印渠道”元素并将其添加 **[!UICONTROL 到Web渠道]** 。 有关详细信息，请参 [阅选择打印渠道元素以创建Web渠道内容](#selectprintchannelelements)。
   有关印刷渠道和Web渠道的详细信息，请参 [阅印刷渠道和Web渠道](/help/forms/using/web-channel-print-channel.md)。

1. 点按&#x200B;**[!UICONTROL 创建]**。将创建交互式通信，并显示一个警告框。 点按 **[!UICONTROL 编辑]** ，以开始构建交互式通信的内容，如使用交互式通信创 [作用户界面添加内容中所述](#step2)。 或者，您也可以点按完 **[!UICONTROL 成]** ，然后选择稍后编辑交互式通信。

## 将内容添加到交互式通信 {#step2}

创建交互式通信后，可以使用交互式通信创作界面构建其内容。

有关交互式通信创作界面的详细信息，请参 [阅交互式通信创作介绍](/help/forms/using/introduction-interactive-communication-authoring.md)。

1. 按照创建交互式通信中所述，点按编辑时，将启动交互式 [通信创作界面](#createic)。 或者，您也可以导航到AEM上的现有交互式通信资产，将其选中，然后点按编 **[!UICONTROL 辑]** ，以启动交互式通信创作界面。

   默认情况下，将显示交互式通信的打印渠道，除非交互式通信仅限Web渠道。 交互通信的打印渠道显示目标区域，如所选XDP/打印渠道模板中所示。 在这些目标区域和字段中，您可以添加组件或资产。

1. 选择“打印渠道”后，选择“组 **[!UICONTROL 件]** ”选项卡。 打印渠道中提供以下组件：

   | **组件** | **功能** |
   |---|---|
   | 图表 | 添加一个图表，您可以在交互通信中使用它来直观地表示从表单数据模型集合检索的二维数据。 有关详细信息，请参 [阅在Interactive Communications中使用图表](/help/forms/using/chart-component-interactive-communications.md)。 |
   | 文档片段 | 允许您向交互式通信添加可重用的组件，如文本、列表或条件。 添加的组件可以是基于表单数据模型的组件，也可以是没有表单数据模型的组件。 |
   | 图像 | 允许插入图像。 |

   将组件拖放到您的交互式通信中，并根据需要配置它们。

   在为打印和Web渠道创作交互式通信时，您还可以使用撤消和重做操作。

   使用撤消操作可放弃上次执行的操作，而重做操作可再次合并放弃的操作。 例如，如果您已在交互式通信中插入图像或创建了数据绑定，并且需要放弃它，请使用撤消操作。

   ![撤消重做操作](assets/undo_redo_actions_new.png)

   撤消和重做选项显示在创作UI页面工具栏上。 撤消选项仅在执行操作后显示。 重做选项仅在执行撤消操作后才会显示在页面工具栏上。 刷新页面时将重置这些操作。

1. 选择打印渠道后，转到“资 **[!UICONTROL 产]** ”选项卡并应用筛选器以仅显示要查看的资产。

   使用“资产”浏览器，您还可以直接将资产拖放到“交互通信”目标区域。

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
   <td>根据策略类型将相应的标题图像添加到通信的条件：标准版或高级版。 <br /> </td>
  </tr>
  <tr>
   <td>列表</td>
   <td>文档片段组，包括文本、条件、其他列表和图像。 <br /> </td>
  </tr>
 </tbody>
</table>

您还可以使用“资产”选项卡将新片段拖放到目标区域，以替换目标区域与文档片段之间 **的绑定** 。 拖动片段时目标区域的蓝色底纹表示文档片段可以拖放到目标区域。

有关文档片段的详细信息，请参阅 [文档片段](/help/forms/using/document-fragments.md)。

创作界面使您能够区分未绑定和绑定字段以及交互式通信中的变量。 界面使用橙色边框高亮显示未绑定的字段和变量。

![unbind_fields_variables_highlights_dc](assets/unbound_fields_variables_highlights_dc.jpg)

此外，当您将鼠标悬停在这些元素上时，将显示一个工具提示，其中显示“字段”（未绑定）或“变量”（未绑定）消息。

在文档片段中使用的未绑定变量有时不能显示在创作界面上。 这可能是由于文档片段中的内联文本规则或条件片段的情况。 在这种情况下，以蓝色突出显示的工具提示会作为文档片段的一部分显示。 工具提示显示在文档片段中使用的未绑定变量的数量。

![未绑定变量](assets/df_unbound_variable_new.png)

点按文档片段，点 ![按configure_icon](assets/configure_icon.png) (Configure)，然后从交互式通信的Sidekick中点 **[!UICONTROL 按属性]** 。 “变 **[!UICONTROL 量”和“数据模型对象]** ”部分列表变量，包括隐藏变量和文档片段中使用的数据模型对象。 使用每 ![个数据模型对象](assets/edit.svg) 或变量旁边的编辑（编辑）图标编辑属性。

1. 要设置变量的绑定，请点按变量，选择 ![configure_icon](assets/configure_icon.png) (Configure)，然后在提要栏的“属性”面板中设置绑定属性。

   * **无**:代理将填写变量的值。
   * **文本片段**:如果选择此项，则可浏览并选择其内容呈现在字段中的文本文档片段。 只有这些文本文档片段可以绑定到内部没有变量的变量。
   * **数据模型对象**:选择在字段中填充其值的表单数据模型属性。
   * **默认值：** 您可以使用此字段为变量定义默认值。 当您预览交互式通信或在代理UI中时，将显示该值。
   * **显示图案：** 您还可以为变量定义显示格式。 从“类型”( **Type** )下拉列表中选择任意预定义选项，以将显示格式应用于变量。 选 **择“自定** ”以定义列表中不可用的显示图案。 有关详细信息，请参阅 [数据显示模式](../../forms/using/create-interactive-communication.md#datadisplaypatterns)。
   导航到 [变量和数据模型对象](../../forms/using/create-interactive-communication.md#hiddenvariables) ，以设置隐藏变量在文档片段中的绑定。

   您还可以拖放数据源元素或文本文档片段以设置变量绑定。  要创建与任意数据源元素的绑定，请选择“ **Data Sources** ”选项卡，然后将元素拖放到变量名。 数据源元素和变量的类型必须相同，才能成功设置绑定。 如果将数据源元素拖放到已绑定的变量，则新元素将替换前一个元素，以创建与该变量的新绑定。 同样，选择 **资产** (Assets)选项卡，将文本文档片段拖放到变量名以设置它们之间的绑定。 文本文档片段不得包含任何变量。

1. 要添加表，在选择打印渠道的情况下，在“资 **[!UICONTROL 产]** ”选项卡中应用筛选器以仅显示布局片段。 将所需的布局片段拖放到交互式通信中。 布局片段基于XDP，可用于在交互通信中创建图形布局或用动态数据填充的静态和动态表。

   示例：用于显示高保费、忠诚度折扣%以及旧政策和新政策的紧急路边援助可用性的布局表。

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


1. 切换到 **[!UICONTROL Web渠道]**。 Web渠道显示在交互通信编辑器中。 首次从打印渠道切换到Web渠道时，会进行自动同步。 有关详细信息，请参 [阅从打印渠道同步Web渠道](../../forms/using/create-interactive-communication.md#synchronize)。

   由于在本例中我们将“打印”用作Web的主页，因此“打印渠道”占位符、内容和数据绑定将同步到Web渠道。 但是，您可以在Web渠道中更改和自定义特定内容。 [取消继承](../../forms/using/create-interactive-communication.md#main-pars-header-103384010) ，对于使用打印渠道生成的目标区域和变量，这些区域和变量可以自定义内容。

   ![webchannelassets](assets/webchannelassets.png)

   点按文档片段，点 ![按configure_icon](assets/configure_icon.png) (Configure)，然后从交互式通信的Sidekick中点 **[!UICONTROL 按属性]** 。 “变 **[!UICONTROL 量”和“数据模型对象]** ”部分列表变量，包括隐藏变量和文档片段中使用的数据模型对象。 使用每 ![个数据模型对象](assets/edit.svg) 或变量旁边的编辑（编辑）图标编辑属性。 此外，对于在Web文档中使用“打印渠道 [”自动生成的渠道片段，请使用每个数据模型对象和变量旁的“](../../forms/using/create-interactive-communication.md#main-pars-header-1213963149) （取消继承）”图标来取消继承 ![](assets/cancelinheritance.png)[](../../forms/using/create-interactive-communication.md#main-pars-header-103384010) ，并能够编辑继承。

1. 要在Web渠道中添加其他组件，在选择Web渠道的情况下，点按组 **[!UICONTROL 件]**。 根据需要在交互通信的Web渠道中拖放组件，然后继续配置它们。

   | 组件 | 功能 |
   |---|---|
   | 图表 | 添加一个图表，您可以在交互通信中使用它来直观地表示从表单数据模型集合检索的二维数据。 有关详细信息，请参 [阅使用图表组件](../../forms/using/chart-component-interactive-communications.md)。 |
   | 文档片段 | 允许您向交互式通信添加可重用的组件、文本、列表或条件。 您添加到交互通信的可重用组件可以是基于表单数据模型的，也可以是没有表单数据模型的。 |
   | 图像 | 允许插入图像。 |
   | 面板 | 允许您向交互式 [通信](../../forms/using/create-interactive-communication.md#add-panel-component-to-the-web-channel) 添加面板。 |
   | 表 | 添加表格以便按行和列整理数据。 |
   | 目标区域 | 在Web渠道中插入目标区域以组织Web渠道特定的组件。 目标区域是一个简单容器，它允许您对Web渠道特定组件进行分组。 |
   | 文本 | 将富文本添加到交互式通信的Web渠道。 文本还可以利用表单数据模型对象来使内容动态化。 |
   | 按钮 | 允许您向交互式通 [信添](../../forms/using/create-interactive-communication.md#add-button-component-to-the-web-channel) 加按钮。 您可以使用“按钮”组件导航到其他交互通信、自适应表单、图像或文档片段等其他资产或外部URL。 |
   | 分隔符 | 允许您在交互式通信中插入一条水平线。 使用此组件可区分对应部分。 例如，您可以使用分隔符组件在信用卡对帐单中区分客户详细信息和信用卡详细信息部分。 |

1. 根据需要，在Web渠道中插入资源。

   您可以 [预览您的交互式通信](#previewic) ，以查看交互式通信的打印和Web输出的外观并根据需要继续进行更改。

## 预览交互式通信 {#previewic}

您可以使用 **预览选项** ，评估交互式通信的外观。 交互通信的Web渠道还提供了一个选项，用于模拟各种设备的交互通信体验。 例如，iPhone、iPad和Desktop。 您可以结合使用 **预览****和模拟**![](assets/ruler.png) 器标尺选项来为不同屏幕尺寸的设备预览Web输出。 预览中的样本数据从指定的表单数据模型填充。

1. 选择（打印或Web）渠道以预览并点按预览。 出现“交互式通信”。

   >[!NOTE]
   >
   >预览将填充指定表单数据模型的示例数据。 有关使用某些其他数据预览交互通信或使用预填服务的详细信息，请参阅 [使用表单数据模型](/help/forms/using/using-form-data-model.md)[和使用表单数据模型](/help/forms/using/work-with-form-data-model.md)。

1. 对于Web渠道，使用标 ![尺](assets/ruler.png) ,视图交互式通信在各种设备上的显示效果。

   ![Web频道预览](assets/webchannelpreview.png)

此外，您还可 [以使用代理UI准备和发送交互式通信](/help/forms/using/prepare-send-interactive-communication.md)。

## 在交互通信中配置属性 {#configure-properties-in-interactive-communication}

### 附件和库访问 {#attachmentslibrary}

在打印渠道中，您可以配置附件和库访问权限，以允许代理在交互通信的代理UI中管理附件：

1. 在打印渠道中，高亮显示文档容器并点按属 **性**。

   ![文档容器属性](assets/documentcontainerproperties.png)

   “属性”面板显示在提要栏中。

   ![属性附件](assets/propertiesattachments.png)

1. 展开 **“附件** ”并指定以下属性：

   * **[!UICONTROL 允许库访问]**:选择此选项可在代理UI中为代理启用库访问。 如果启用，代理可在准备交互式通信时从库添加文件。
   * **[!UICONTROL 允许对附件重新排序]**:选择此选项后，代理可以使用交互式通信重新排序附件。
   * **[!UICONTROL 允许的最大附件数]**:指定交互式通信允许的最大附件数。
   * **[!UICONTROL 要附加的文件]**:点按 **[!UICONTROL 添加]** ，然后浏览以选择要附加的文件，并指定以下内容：

      * **[!UICONTROL 默认情况下，将此文件附加到文档]**:如果仅附件不是“必填”，则可以更改此选项。
      * **[!UICONTROL 强制：]** 代理将无法在代理UI中删除附件。
   ![附件](assets/attachfiles.png)

1. 点按&#x200B;**[!UICONTROL 完成]**。

### XDP/布局字段属性 {#xdplayoutfieldproperties}

1. 编辑交互式通信的打印渠道时，将指针悬停在打印渠道模板中构建的字段上，然后选择 ![configure_icon](assets/configure_icon.png) (Configure)。

   提要栏中将显示“属性”对话框。

   ![data_display_patterns_fields](assets/data_display_patterns_fields.jpg)

1. 指定以下内容：

   * **[!UICONTROL 名称]**:JCR节点名称。
   * **[!UICONTROL 标题]**:在代理UI中和文档容器树中输入代理将可见的标题。
   * **[!UICONTROL 绑定类型]**:为字段选择以下绑定类型之一。

      * 无：代理将填写该属性的值。
      * 文本片段：如果选择此项，则可浏览并选择其内容呈现在字段中的文本文档片段。 或者，将文本文档片段拖放到字段名称中，以设置它们之间的绑定。 文本文档片段不得包含任何变量。
      * 数据模型对象：选择在字段中填充其值的表单数据模型属性。 或者，选择 **Data Sources** （数据源）选项卡，并将属性拖放到字段。
   * **[!UICONTROL 默认值]**:默认值确保当指定的数据模型对象或文本片段没有提供值时字段不为空。 如果数据绑定类型为none，则在字段中预填充默认值。
   * **[!UICONTROL 显示图案]**:您还可以为字段定义显示格式。 从“类型”( **Type** )下拉列表中选择任意预定义选项，以将显示格式应用于字段。 选 **择“自定** ”以定义列表中不可用的显示图案。 有关详细信息，请参阅 [数据显示模式](../../forms/using/create-interactive-communication.md#datadisplaypatterns)

   * **[!UICONTROL 由代理编辑]**:选择此选项可允许代理编辑代理UI中字段中的值。 如果“绑定类型”是“文本片段”，则此设置不适用。
   * **[!UICONTROL 标签]**:在代理UI中，指定与字段一起显示给代理的文本字符串。 如果“绑定类型”是“文本片段”，则此设置不适用。
   * **[!UICONTROL 工具提示]**:输入一个文本字符串，该字符串将在将鼠标悬停在代理UI中时可见。 如果“绑定类型”是“文本片段”，则此设置不适用。
   * **[!UICONTROL 必需]**:选择此项可使座席的字段成为必填字段。 如果“绑定类型”是“文本片段”，则此设置不适用。
   * **[!UICONTROL 允许多行]**:选择此字段可允许在字段中输入多行文本。 如果“绑定类型”是“文本片段”，则此设置不适用。


1. 点 ![按done_icon](assets/done_icon.png)。

### 数据显示模式 {#datadisplaypatterns}

创作界面使您能够为在创建用于印刷和Web渠道的交互式通信时可用的字段、变量和表单数据模型元素定义数据显示模式。

要配置数据显示模式，请点按元素，选择 ![configure_icon](assets/configure_icon.png) (Configure)，然后在提要栏的“属性”面板中设置 **[!UICONTROL 显示模式]** 。 从“类型”( **[!UICONTROL Type]** )下拉列表中选择任何预定义选项，以视图与选定类型关联的图案。 从“ **[!UICONTROL 类型]****[!UICONTROL ”(Type]** )下拉列表中选择“自定义”(Custom)，以定义列表中不可用的模式。 在“图案”( **[!UICONTROL Pattern]** )字段中编辑值会自动将类型修改为“自 **[!UICONTROL 定义”(Custom)]**。

要应用显示模式，“模式”字段中定义的字符或数字数必须与字段、变量和表单数据模型元素的值中定义的字符或数字匹配或超过这些字符或数字。 有关详细信息，请参阅 [示例](../../forms/using/create-interactive-communication.md#greaternumberofdigits)。

![data_display_pattern_example](assets/data_display_patterns_ssn_new.png)

在从打印渠道生成Web内容后，您可以为字段、变量或表单数据模型元素重新定义显示模式。 结果，元素可以具有为打印和网络渠道定义的不同显示模式。 如果未为打印渠道中的元素定义显示图案并使用打印渠道自动生成Web内容，则为打印渠道中的元素定义的数据绑定定义了“类型”( **[!UICONTROL Type]** )下拉列表中可用的显示图案选项。 如果没有为元素定义绑定，则元素的数据类型将定义可用的显示模式选项。 例如，如果为打印渠道中的元素创建Number类型的数据绑定，则“ **[!UICONTROL Type]** ”（类型）下拉列表中可用的显示模式选项将采用各种格式的Number类型。

切换到 **预览模式** ，或打开代理UI以视图应用于这些元素的显示模式。

下表列表了在为变量设置数据显示模式时显示的值示例：

| 类型 | 默认值 | 显示图案 | 显示值 | 描述 |
|---|---|---|---|---|
| 社会安全号码 | 123456789 | text{999-99-999} | 123-45-6789 | 默认值字段中的位数与“模式”字段中的位数相匹配。 基于图案的值将成功显示。 |
| 社会安全号码 | 1234567 | text{999-99-999} | 1-23-4567 | 默认值字段中的位数小于“模式”字段中的位数。 该模式适用于7个可用数字。 |
| 社会安全号码 | 1234567890 | text{999-99-999} | 1234567890 | 默认值字段中的位数大于“模式”字段中的位数。 因此，显示值没有变化。 |

如果未为变量或表单数据模型元素指定显示模式，则默认情 [况下将使用全局文档片段配置](https://helpx.adobe.com//experience-manager/6-5/forms/using/interactive-communication-configuration-properties.html) 。

如果不将显示模式应用于数字数据类型的变量，打印预览会根据全局文档片段配置显示该模式。 如果对默认的全局文档片段配置应用更改，代理UI仍会根据为区域设置定义的默认分隔符显示模式。

同样，对于字段，如果未指定显示模式，则创建打印模板(XDP)时定义的模式将应用于字段。 如果创建打印模板时没有模式，则基于XFA规范的默认模式将应用于字段。

此外，如果指定的显示模式不正确或无法应用，则基于XFA规范的默认模式将应用于字段、变量或表单数据模型元素。

## 将规则应用于交互式通信组件 {#rules}

要在交互式通信中对组件或内容进行条件化，请点按组件／内容片段，然后选择创 ![建规则图标](assets/createruleicon.png) （创建规则）以启动规则编辑器。

有关详细信息，请参阅：

* [规则编辑器](/help/forms/using/rule-editor.md)
* [交互通信创作简介](/help/forms/using/introduction-interactive-communication-authoring.md)

## 使用表 {#tables}

### 交互通信中的动态表 {#dynamic-tables-in-interactive-communication}

您可以在交互式通信中使用布局片段添加动态表。 以下步骤使用信用卡对帐单的示例来说明如何使用布局片段在交互式通信中创建动态表。

1. 确保创建表所需的布局片段在AEM中可用。
1. 在交互式通信的打印渠道中，从资产浏览器将布局片段（带有多列表）拖放到目标区。

   ![lf_dragdrop](assets/lf_dragdrop.png)

   “交互式通信”布局区域中显示一个表。

   ![lf_dragdrop_table](assets/lf_dragdrop_table.png)

1. 为表的每个单元格指定数据绑定。 要创建可重复的行，请在属于公用集合属性的行中插入表单数据模型属性。

   1. 点按表中的单元格，然后选择 ![configure_icon](assets/configure_icon.png) (Configure)。

      提要栏中将显示“属性”对话框。

      ![lf_cell_properties](assets/lf_cell_properties.png)

   1. 配置属性：

      * **[!UICONTROL 名称]**:JCR节点名称。
      * **[!UICONTROL 标题]**:输入将在交互式通信编辑器中显示的标题。
      * **[!UICONTROL 绑定类型]**:为字段选择以下绑定类型之一。

         * **[!UICONTROL 无]**
         * **[!UICONTROL 数据模型对象]**:表单数据模型属性的值将填充在字段中。 或者，选择 **Data Sources** （数据源）选项卡，并将属性拖放到字段。
      * **[!UICONTROL 数据模型对象]**:在字段中填充其值的表单数据模型属性。
      * **[!UICONTROL 默认值]**:默认值确保当指定的数据模型对象没有提供值时字段不为空。 默认值会预填充在字段中。

      * **[!UICONTROL 由代理编辑]**:选择此选项可允许代理编辑代理UI中字段中的值。
   1. 点 ![按done_icon](assets/done_icon.png)。



1. 预览交互式通信以查看使用数据呈现的表。

   ![lf_预览](assets/lf_preview.png)

### 仅Web渠道表 {#webchanneltables}

点按Web模板中的根面板，然后点 **按+** ，将表 **** 组件添加到交互式通信。 在交互通信中插入包含两行的表。 表的第一行表示表标题。

#### 向表中添加行和列 {#addrowscolumnstable}

**要添加或删除列，请执行以下操作：**

1. 点按表标题行中的默认文本框以视图组件工具栏。
1. 选 **择“添加列** ”或“ **删除列** ”分别添加或删除表列。

![component_toolbar_table1](assets/component_toolbar_table1.png)

**要添加或删除行，请执行以下操作：**

1. 点按任意表行以视图组件工具栏。 您还可以使用交互式通信Sidekick中的内容浏览器选择表行。
1. 选择 **添加行** 或 **删除行** ，分别添加或删除表行。 使用工 **具栏中的** “上 **移”和“下移** ”选项重新排列表中的行。

![组件工具栏](assets/component_toolbar_table_row_new.png)

**答：** 添加 **行B。** 删除 **行C.** 上 **移D。** 向下移动

#### 在表单元格中添加或编辑文本 {#addedittexttable}

1. 在表单元格中选择默认文本框，然后点按( ![](assets/edit.png) 编辑)。
1. 在表单元格中键入文本，然后点 ![](assets/done_icon.png) 按以保存它。

#### 在表单元格和数据模型对象元素之间创建绑定 {#createbindingtablecells}

1. 在表行中选择默认文本框，然后点按( ![](assets/edit.png) 编辑)。
1. 点按数据模型对象下拉列表，然后选择属性。
1. 点按可保存表单元格和数据模型对象属性之间的绑定。

![创建数据绑定](assets/create_data_binding_table_new.png)

#### 为表单元格中的文本创建超链接 {#createhyperlinktable}

1. 在表单元格中选择默认文本框，然后点按( ![](assets/edit.svg) 编辑)。
1. 在表单元格中选择文本，然后点按超链接图标。
1. 在路径字段中指 **定** URL。
1. 点按 ![](assets/done_icon.png) 以保存超链接属性。

![创建超链接](assets/create_hyperlink_table_new.png)

#### 创建动态表 {#createdynamictables}

您可以使用类型集合的数据模型属性在交互式通信中创建仅Web渠道的动态表。 此表是集合属性的子属性的表示形式。 您只能编辑表中各个单元格的格式属性。

1. 切换到Web渠道，然后选择显示数据源浏览器。
1. 将集合属性拖放到子表单中。 在子表单中创建表。
1. 预览交互通信的Web预览中的表。

#### 对表中的列进行排序 {#sortcolumns}

您可以根据交互式通信中表格中的任意列对数据进行排序。 列中的值可以按升序或降序排序。

可以将排序应用于包含以下内容的表列：

* 静态文本
* 数据模型对象属性
* 静态文本和数据模型对象属性的组合

要启用排序，请执行以下操作：

1. 选择表并点按( ![](assets/configure_icon.png) 配置)。 您还可以使用交互式通信Sidekick中 **的** “内容”浏览器选择表。
1. 选择“ **启用排序”。**
1. 点 ![](assets/done_icon.png) 按以保存表属性。 列标题中的排序图标（向上和向下箭头）表示已启用排序。

   ![启用排序](assets/enable_sorting_new-1.png)

1. 切换到 **预览** 模式以视图输出。 表会根据表的第一列自动排序。
1. 单击列标题可根据列对值进行排序。

   带有向上箭头的列标题表示：

   * 表将根据该列进行排序。
   * 列中的值以升序显示。
   ![升序排序](assets/sorting_ascending_new-1.png)

   同样，带有向下箭头的列标题表示列中的值以降序显示。

## 编辑交互式通信属性 {#edit-interactive-communication-properties}

创建交互式通信后，您可以在以后的阶段编辑其属性。

使用“属 **性** ”页可以：

* 编辑创建交互通信时指定字段的值，如标题和说明。
* 为现有交互式通信添加或删除Web渠道。
* 预览、下载或删除交互式通信
* 打开代 [理UI](/help/forms/using/prepare-send-interactive-communication.md)。

要访问“属 **性** ”页面：

1. 登录到AEM作者实例，然后导航到 **Adobe Experience Manager** > **Forms** > **Forms &amp;文档**。
1. 选择“交互式通信”并点按 **属性**。
1. 选择“ **常规** ”选项卡以编辑“标 **题** ”和“ **描述** ”字段。

### 添加或删除Web渠道 {#add-or-delete-the-web-channel}

执行以下步骤，为现有交互式通信添加Web渠道:

1. 在“属 **性** ”页面上，选择 **渠道** 选项卡。
1. 选中“ **Web** ”复选框，然后为“Web”渠道选择模板。
1. 选 **择“使用打印作为Web渠道的主渠道** ”，以启用Web与打印渠道之间的同步。
1. Tap **Save &amp; Close** to save the changes.

   同样，您也可以点按 **渠道** 选项卡上的Web **** 渠道，以从交互通信中删除Web。

## 将“按钮”组件添加到Web渠道 {#add-button-component-to-the-web-channel}

您可以将按钮作为组件添加到交互式通信的Web渠道。 使用规则编 [辑器定义规则](../../forms/using/rule-editor.md) ，以便能够在点击按钮时导航到其他交互通信、自适应表单、图像或文档片段等其他资产或外部URL。

要添加按钮并定义其上的规则，请执行以下操作：

1. 点按Web模板中的根面板，然后点 **按+** ，将“ **Button** ”组件添加到“交互式通信”。
1. 点按按钮组件，然 ![](assets/edit-rules.png) 后点按按钮以定义规则。
1. 在“ **When** ”( **When** )部分，从按钮下拉列表的状态中选择已单击。
1. 在“时 **间** ”部分中：

   1. 从下拉列表中选择操作。 例如，选择 **导航到** ，作为操作类型。

   1. 指定交互通信、自适应表单、资产或网页的URL。 例如，以下格式指定URL以导航到另一个交互通信：https://&lt;server-name>:&lt;port>/editor.html/content/forms/af/&lt;Interactive Communication name>/渠道/&lt;渠道名称——打印或web>.html
   1. 指定在同一选项卡、新选项卡或新窗口中打开资产的选项。
   1. 点按 **完成** ，然后点 **按关闭** ，以保存规则。
   同样，您也可以从操作类型下拉列表中选择其他可用选项，如调用服务和提交表单。 有关详细信息，请参阅规 [则编辑器](../../forms/using/rule-editor.md)。

1. 预览交互式通信，然后点按按钮以视图在步骤4(b)中指定的交互式通信、自适应表单、资产或网页。

## 将面板组件添加到Web渠道 {#add-panel-component-to-the-web-channel}

面板组件是用于将其他组件分组在一起的占位符，它控制在交互通信中布置一组组件（如折叠面板和选项卡）的方式。 面板组件还允许您使一组组件可为最终用户重复使用，例如填写教育凭据所需的多个条目。

执行以下步骤将面板组件添加到Web渠道:

1. 使用以 **下任意选项** ，将Panel组件插入Web渠道:

   * 点按组件，点 **按+** 并选择 **面板组件** 。

   * 从“组 **件** ”浏览器面板中，将“面板”组 **件拖放到“交互式通信** ”上。

   * 点按“内 **容** ”浏览器面板中的 **面板** ，然后点按“添 **加子面板”**。 选择“添 **加子面板** ”选项将显 **示“添加子面板** ”对话框。 输入Panel组件的标题和可选说明和名称。

1. 从内容浏览器中点 **击面板** ，以对面板执行其他操作，如配置、编辑规则、复制、删除和插入组件。

   您还可以在内容浏览器中拖放一个面板 **** ，以反映右侧窗格中交互式通信结构的更改。

## 使Web渠道与打印渠道同步 {#synchronize}

在创建交互式通信时选择“打印为Web渠道的主页”时，将创建与打印渠道同步的Web渠道，并且Web渠道的内容和数据绑定从打印渠道派生，并且点按“同步”时，打印渠道中所做的更改可能会反映在Web渠道中。

但是，作者可以根据需要中断Web渠道中组件的继承。

![创建Print Master](assets/create_ic_print_master_new-1.png) ![Print Master Web](assets/create_ic_print_master_web_new-1.png)

### 自动同步 {#autosync}

如果选择“将打 **[!UICONTROL 印为主渠道用于Web渠道”选项]** ，则可以选择以下任一模式以生成Web:

* **[!UICONTROL 自动布局]**:选择此模式可自动从“打印渠道”中为Web渠道生成占位符、内容和数据绑定。
* **[!UICONTROL 手动组织]**:选择此模式，可使用“数据源”选项卡中提供的主内容手动选择打印渠道元素并将其添加到Web渠道。 有关详细信息，请参 [阅选择打印渠道元素以创建Web渠道内容](#selectprintchannelelements)。

![创建IC选项](assets/create_ic_options_updated_new.png)

>[!NOTE]
>
>同步渠道仅同步从打印渠道到Web渠道的文档片段、图像、条件、列表和布局片段。 包含此类元素的子表单或父节点不会同步。

### 选择“打印渠道”元素以创建Web渠道内容 {#selectprintchannelelements}

如果在创建交互式通信时选择“打印为主页”，但不选择自动同步选项，则还可以将“打印渠道”元素拖放到Web渠道创作界面。

导航到“ **数据源** ”>“ **主内容** ”以视图“打印渠道”元素。 将目标区域、字段或表拖放到Web渠道创作界面。 元素名称旁边的蓝色圆圈图标表示“打印渠道”元素已包含在Web渠道中。

![主内容](assets/master_content.png)

### 取消继承 {#cancelinheritance}

在Web渠道中，组件嵌入到目标区域。

将指针悬停在Web渠道中的相关目标区域或变量上，选择取消继承 ![（取消继承），然后在取消继承对话框中，点按](assets/cancelinheritance.png) 是 ****。

组件在目标区域内的继承将被取消，现在您可以根据需要编辑它们。

### 重新启用继承 {#re-enable-inheritance}

在Web渠道中，如果已取消组件的继承，则可以重新启用它。 要重新启用继承，请将指针悬停在包括组件的相关目标区域的边界上，然后点按重新启用 ![继承](assets/reenableinheritance.png)。

此时会显示“还原继承”对话框。

![反遗产](assets/revertinheritance.png)

如果需要，请选 **[!UICONTROL 择还原继承后同步页面]**。 选择此选项可同步整个交互式通信。 如果不选择此选项，则只有在恢复继承时，相关目标区域才会同步。

点按 **[!UICONTROL 是]**。

### 同步 {#synchronize-1}

如果您使用“打印为Web渠道的主页”并对“打印”渠道进行更改，则可以同步内容以将新做的更改引入Web渠道。

1. 要将Web渠道与打印渠道同步，请切换到Web渠道，然后点按更多选项图标。

   ![自动同步选项](assets/auto_sync_options_new.png)

1. 点按以下任一选项：

   * **[!UICONTROL 与打印同步]**:仅同步未取消继承的目标区域的内容。
   * **[!UICONTROL 重置]**:将Web渠道内容与打印渠道同步，并放弃对Web渠道所做的所有更改。

### 使用组件工具栏对继承的组件执行操作 {#componenttoolbar}

使用“同步”选项在Web渠道中自动生成内容后，您可以对组件执行更多操作，而无需取消继承。

![组件工具栏](assets/component_toolbar_inherited_web_new.png)

点按组件以视图以下选项：

* **复制：** 复制组件并将其粘贴到交互通信中的其他位置。
* **剪辑：** 在交互式通信中，将组件从一个位置移到另一个位置。
* **插入组件：** 在选定组件上方插入组件。
* **粘贴：** 使用上述选项粘贴您剪切或复制的组件。
* **组：** 如果要剪切、复制或粘贴多个组件，请选择多个组件。
* **父项：** 选择组件的父项。
* **视图SOM表达式:** 视图 [组件的SOM表达式](../../forms/using/using-som-expressions-adaptive-forms.md) 。

* **在面板中对象分组：** 将组件组合到面板中，以便能够同时对这些组件执行操作。 有关详细信息，请参 **[阅在面板中分组对象](../../forms/using/create-interactive-communication.md#main-pars-header-1815149576)**。

* **取消继承：** 取 [消目标区](../../forms/using/create-interactive-communication.md#main-pars-header-103384010) 内组件的继承以对其进行编辑。

### Group objects in Panel {#groupobjectspanel}

Web渠道创作界面便于将面板中的组件分组以能够同时对这些组件执行操作。 “内 **容** ”选项卡将分组的组件列表为内容树中面板的子元素。

1. 点按组件，然后选择组( ![组](assets/group.jpg))操作。
1. 选择多个组件，然后点按 **面板中的组对象**。

   ![对象组](assets/component_toolbar_group_objects_new.png)

1. 在“面 **板”对话框的“组对象** ”中，输入面板的名称。
1. 输入面板的可选标题和说明。
1. 单击 ![bullet_checkmark](assets/bullet_checkmark.png)。

   分组的组件在内容树中显示为面板的子元素。

   ![content_tree_grouping](assets/content_tree_grouping.png)

