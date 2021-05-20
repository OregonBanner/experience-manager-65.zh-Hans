---
title: 创建交互式通信
seo-title: 创建交互式通信
description: 使用交互式通信编辑器创建交互式通信。 使用拖放功能构建交互式通信，并预览不同设备类型的打印和Web输出。
seo-description: 使用交互式通信编辑器创建交互式通信。 使用拖放功能构建交互式通信，并预览不同设备类型的打印和Web输出。
uuid: d524a3de-00b4-444f-b3c7-be443fa24ec8
topic-tags: interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: f4d98cb9-84d8-4735-91d2-b9ceec861e5e
docset: aem65
feature: 交互式通信
exl-id: 1f89c3bf-e67e-4d13-9285-3367be1ac8f8
source-git-commit: 92092e1c050c9264c19e3cd9da9b240607af7bab
workflow-type: tm+mt
source-wordcount: '6212'
ht-degree: 1%

---

# 创建交互式通信{#create-an-interactive-communication}

## 概述 {#overview}

交互式通信集中管理个性化的交互式信函的创建、汇编和传递。 利用打印作为Web的主控渠道，可最大程度地减少在创建交互式通信的Web输出时的工作重复。

### 前提条件 {#prerequisites}

以下是创建交互式通信的先决条件：

* 设置[表单数据模型](/help/forms/using/data-integration.md)，其中包含测试数据或使用实际数据源(如Microsoft® Dynamics的实例)。
* 确保您具有[文档片段](/help/forms/using/document-fragments.md)。
* 确保具有[用于打印和Web渠道的模板](/help/forms/using/web-channel-print-channel.md)。
* 确保Web渠道具有所需的[主题](/help/forms/using/themes.md)。

## 创建交互式通信 {#createic}

1. 登录到AEM创作实例，然后导航到&#x200B;**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms和文档]**。
1. 点按&#x200B;**[!UICONTROL 创建]**，然后选择&#x200B;**[!UICONTROL 交互式通信]**。 “创建交互式通信”页面。

   ![创建交互式通信](assets/create-interactive-communication.png)

1. 输入以下信息。 : 

   * **[!UICONTROL 标题]**:输入交互式通信的标题。
   * **[!UICONTROL 名称]**:交互式通信的名称是从您输入的标题派生的。根据需要编辑它。
   * **[!UICONTROL 描述]**:输入有关交互式通信的描述。
   * **[!UICONTROL 表单数据模型]**:浏览并选择表单数据模型。有关表单数据模型的更多信息，请参阅[AEM Forms数据集成](/help/forms/using/data-integration.md)。

   * **[!UICONTROL 预填充服务]**:选择预填充服务以检索数据并预填充交互式通信。
   * **[!UICONTROL 后处理类型]**:您可以选择在提交交互式通信时触发的AEM或Forms工作流。选择要触发的工作流的类型。

   * **[!UICONTROL 后处理]**:选择要触发的工作流的名称。选择AEM工作流时，提供“附件路径”、“布局路径”、“PDF路径”、“打印数据路径”和“Web数据路径”。
   * **[!UICONTROL 标记]**:选择要应用于交互式通信的标记。您还可以键入新/自定义标记名称，然后按Enter以创建该名称。
   * **[!UICONTROL 作者]**：作者姓名自动取自已登录用户的用户名。
   * **[!UICONTROL 发布日期：]** 输入发布交互式通信的日期。
   * **[!UICONTROL 取消发布日期]**:输入取消发布交互式通信的日期。

1. 点按&#x200B;**[!UICONTROL Next]**。 将显示用于指定打印和Web渠道详细信息的屏幕。
1. 输入以下内容：

   * **[!UICONTROL 打印]**:选择此选项可生成交互式通信的打印渠道。
   * **[!UICONTROL 打印模板]**:浏览并选择XDP作为打印模板。
   * **[!UICONTROL Web]**:选择此选项可生成交互式通信的Web渠道或响应式输出。
   * **[!UICONTROL 交互式通信Web模板]**:浏览并选择Web模板。
   * **** 选择 **[!UICONTROL 主题]**:浏览并选择主题以设置交互式通信的Web渠道的样式。有关更多信息，请参阅AEM Forms](/help/forms/using/themes.md)中的[主题。

   * **[!UICONTROL 将“打印为主控”用于Web渠道]**:选择此选项可创建与打印渠道同步的Web渠道。将打印渠道用作Web渠道的主控，可确保Web渠道的内容和数据绑定是从打印渠道派生的，并且在点按“同步”时，在打印渠道中所做的更改会反映在Web渠道中。 但是，作者可以根据需要中断Web渠道中特定组件的继承。 有关更多信息，请参阅[将Web通道与打印通道同步](../../forms/using/create-interactive-communication.md#synchronize)。
如果选择**[!UICONTROL Use Print As 主控 for Web Channel]**&#x200B;选项，则可以选择以下任何模式以生成Web渠道：

      * **[!UICONTROL 自动布局]**:选择此模式可自动从打印渠道为Web渠道生成占位符、内容和数据绑定。
      * **[!UICONTROL 手动组织]**:选择此模式，可使用数据源选项卡中提供的主控内容手动选择打印渠道元素并将其添加到 **[!UICONTROL Web]** 渠道。有关更多信息，请参阅[选择打印渠道元素以创建Web渠道内容](#selectprintchannelelements)。

   有关打印渠道和Web渠道的更多信息，请参阅[打印渠道和Web渠道](/help/forms/using/web-channel-print-channel.md)。

1. 点按&#x200B;**[!UICONTROL 创建]**。将创建交互式通信，并出现一个警报框。 点按&#x200B;**[!UICONTROL 编辑]**&#x200B;以开始构建交互式通信的内容，如[使用交互式通信创作用户界面](#step2)添加内容中所述。 或者，您也可以点按&#x200B;**[!UICONTROL Done]**，然后选择稍后编辑交互式通信。

## 向交互式通信添加内容 {#step2}

创建交互式通信后，可以使用交互式通信创作界面来构建其内容。

有关交互式通信创作界面的更多信息，请参阅[交互式通信创作简介](/help/forms/using/introduction-interactive-communication-authoring.md)。

1. 按照[创建交互式通信](#createic)中所述，点按编辑，即会启动交互式通信创作界面。 或者，您也可以导航到AEM上的现有交互式通信资产，将其选中，然后点按&#x200B;**[!UICONTROL 编辑]**&#x200B;以启动交互式通信创作界面。

   默认情况下，将显示交互式通信的打印渠道，除非交互式通信是仅限Web渠道。 交互式通信的打印渠道显示目标区域，如所选XDP/打印渠道模板中所示。 在这些目标区域和字段中，您可以添加组件或资产。

1. 选择打印渠道后，选择&#x200B;**[!UICONTROL 组件]**&#x200B;选项卡。 打印渠道中提供以下组件：

   | **组件** | **功能** |
   |---|---|
   | 图表 | 添加一个图表，可在交互式通信中使用该图表，以可视方式表示从表单数据模型集合中检索的二维数据。 有关更多信息，请参阅[在交互式通信中使用图表](/help/forms/using/chart-component-interactive-communications.md)。 |
   | 文档片段 | 允许您向交互式通信添加可重用的组件，如文本、列表或条件。 添加的组件可以是基于表单数据模型的组件，也可以是没有表单数据模型的组件。 |
   | 图像 | 允许插入图像。 |

   将组件拖放到交互式通信中，并根据需要对其进行配置。

   在为打印和Web渠道创作交互式通信时，您还可以使用撤消和重做操作。

   使用撤消操作可放弃上次执行的操作，使用重做操作可再次合并已放弃的操作。 例如，如果您在交互式通信中插入了图像或创建了数据绑定，并且需要放弃它，则使用撤消操作。

   ![撤消重做操作](assets/undo_redo_actions_new.png)

   撤消和重做选项显示在创作UI页面工具栏上。 只有在执行操作后，才会显示撤消选项。 只有在执行撤消操作后，重做选项才会显示在页面工具栏上。 刷新页面时会重置这些操作。

1. 选择打印渠道后，转到&#x200B;**[!UICONTROL Assets]**&#x200B;选项卡，然后应用过滤器以仅显示您想要查看的资产。

   使用资产浏览器，您还可以直接将资产拖放到交互式通信目标区域。

   ![assets-docfragments](assets/assets-docfragments.png)

1. 将文档片段拖放到交互式通信中。 以下是可在交互式通信的打印渠道中使用的文档片段类型。

<table>
 <tbody>
  <tr>
   <td><strong>文档片段类型</strong></td>
   <td><strong>示例用途</strong></td>
  </tr>
  <tr>
   <td><a href="/help/forms/using/texts-interactive-communications.md" target="_blank">文本</a></td>
   <td>用于添加地址、收件人电子邮件和信件正文文本的文本 </td>
  </tr>
  <tr>
   <td><a href="/help/forms/using/conditions-interactive-communications.md" target="_blank">条件</a></td>
   <td>根据策略类型向通信添加相应标头图像的条件：Standard或Premium。<br /> </td>
  </tr>
  <tr>
   <td>列表</td>
   <td>文档片段的组，包括文本、条件、其他列表和图像。<br /> </td>
  </tr>
 </tbody>
</table>

您还可以通过使用&#x200B;**[!UICONTROL Assets]**&#x200B;选项卡将新片段拖放到目标区域上，来替换目标区域和文档片段之间的绑定。 拖动片段时目标区域的蓝色底纹表示文档片段可以拖放到目标区域。

有关文档片段的更多信息，请参阅[文档片段](/help/forms/using/document-fragments.md)。

通过创作界面，您可以区分未绑定和绑定字段以及交互式通信中的变量。 界面使用橙色边框突出显示未绑定的字段和变量。

![unbind_fields_variables_hightles_dc](assets/unbound_fields_variables_highlights_dc.jpg)

此外，当将鼠标悬停在这些元素上时，将显示工具提示，其中包含字段（未绑定）或变量（未绑定）消息。

文档片段中使用的未绑定变量有时可能不会显示在创作界面上。 这可能是由于文档片段中的内嵌文本规则所致，或者是由于条件片段所致。 在这种情况下，以蓝色突出显示的工具提示会作为文档片段的一部分显示。 工具提示显示文档片段中使用的未绑定变量的数量。

![未绑定变量](assets/df_unbound_variable_new.png)

点按文档片段，点按![configure_icon](assets/configure_icon.png)（配置），然后点按交互式通信Sidekick中的&#x200B;**[!UICONTROL 属性]**。 **[!UICONTROL 变量和数据模型对象]**&#x200B;部分列出了变量，包括隐藏变量以及文档片段中使用的数据模型对象。 使用每个数据模型对象或变量旁边的![编辑](assets/edit.svg)（编辑）图标来编辑属性。

1. 要设置变量绑定，请点按变量并选择![configure_icon](assets/configure_icon.png)(Configure)，然后在侧栏的“属性”面板中设置绑定属性。

   * **无**:代理将填写变量的值。
   * **文本片段**:如果选中此选项，则可以浏览并选择其内容在字段中呈现的文本文档片段。只能将这些文本文档片段绑定到中没有变量的变量。
   * **数据模型对象**:选择在字段中填充其值的表单数据模型属性。
   * **默认值：** 您可以使用此字段为变量定义默认值。预览交互式通信时或在代理UI中时，将显示值。
   * **显示模式：** 您还可以为变量定义显示格式。从&#x200B;**类型**&#x200B;下拉列表中选择任何预定义选项，以将显示格式应用于变量。 选择&#x200B;**Custom**&#x200B;以定义列表中不可用的显示模式。 有关更多信息，请参阅[数据显示模式](../../forms/using/create-interactive-communication.md#datadisplaypatterns)。

   导航到[变量和数据模型对象](../../forms/using/create-interactive-communication.md#hiddenvariables)以设置文档片段中隐藏变量的绑定。

   您还可以拖放数据源元素或文本文档片段以设置变量绑定。  要使用任何数据源元素创建绑定，请选择&#x200B;**数据源**&#x200B;选项卡，然后将该元素拖放到变量名称中。 数据源元素和变量必须具有相同的类型，才能成功设置绑定。 如果将数据源元素拖放到已绑定的变量，则新元素会替换前一个元素，以使用该变量创建新绑定。 同样，选择&#x200B;**Assets**&#x200B;选项卡，并将文本文档片段拖放到变量名称中，以设置它们之间的绑定。 文本文档片段不得包含任何变量。

1. 要添加表格，并选择打印渠道，请在&#x200B;**[!UICONTROL Assets]**&#x200B;选项卡中应用过滤器以仅显示布局片段。 将所需的布局片段拖放到交互式通信中。 布局片段基于XDP，可用于在交互式通信中创建图形布局或使用动态数据填充的静态和动态表。

   示例：一个布局表，用于显示旧政策和新政策的毛额溢价、忠诚度折扣%以及紧急路边援助可用性。

   有关布局片段的更多信息，请参阅[文档片段](/help/forms/using/document-fragments.md)。

1. 选择打印渠道后，在&#x200B;**[!UICONTROL Assets]**&#x200B;选项卡中，应用过滤器来显示图像。 将所需的图像拖放到交互式通信中，如公司徽标。

   此外，在交互式通信中管理以下内容：

   * [添加和配置图表](/help/forms/using/chart-component-interactive-communications.md)
   * [将Web渠道与打印渠道同步](../../forms/using/create-interactive-communication.md#synchronize)

      * 自动同步
      * 取消继承
      * 重新启用继承
      * 同步
   * [附件和库访问](../../forms/using/create-interactive-communication.md#attachmentslibrary)
   * [XDP/布局字段属性](../../forms/using/create-interactive-communication.md#xdplayoutfieldproperties)
   * [将规则添加到组件](../../forms/using/create-interactive-communication.md#rules)


1. 切换到&#x200B;**[!UICONTROL Web渠道]**。 Web渠道显示在交互式通信编辑器中。 首次从“打印”渠道切换到Web渠道时，会进行自动同步。 有关更多信息，请参阅[从打印渠道同步Web渠道](../../forms/using/create-interactive-communication.md#synchronize)。

   由于在本例中，我们将“打印”用作Web的主控，因此“打印”渠道占位符、内容和数据绑定会同步到Web渠道。 但是，您可以更改和自定义Web渠道中的特定内容。 [取消](#cancelinheritance) 对使用打印渠道生成的目标区域和变量的继承，以便能够自定义内容。

   ![webchannelassets](assets/webchannelassets.png)

   点按文档片段，点按![configure_icon](assets/configure_icon.png)（配置），然后点按交互式通信Sidekick中的&#x200B;**[!UICONTROL 属性]**。 **[!UICONTROL 变量和数据模型对象]**&#x200B;部分列出了变量，包括隐藏变量以及文档片段中使用的数据模型对象。 使用每个数据模型对象或变量旁边的![编辑](assets/edit.svg)（编辑）图标来编辑属性。 此外，对于已在使用打印渠道的Web渠道中自动生成[的文档片段，请使用每个数据模型对象和变量旁边的![cancelerientation](assets/cancelinheritance.png)（取消继承）图标[取消继承](#cancelinheritance)并能够编辑它们。](#synchronize)

1. 要在Web渠道中添加其他组件，并选择Web渠道，请点按&#x200B;**[!UICONTROL 组件]**。 根据需要将组件拖放到交互式通信的Web渠道中，然后继续配置这些组件。

   | 组件 | 功能 |
   |---|---|
   | 图表 | 添加一个图表，可在交互式通信中使用该图表，以可视方式表示从表单数据模型集合中检索的二维数据。 有关更多信息，请参阅[使用图表组件](../../forms/using/chart-component-interactive-communications.md)。 |
   | 文档片段 | 允许向交互式通信添加可重用的组件、文本、列表或条件。 您添加到交互式通信的可重用组件可以是基于表单数据模型的组件，也可以是没有表单数据模型的组件。 |
   | 图像 | 允许插入图像。 |
   | 面板 | 用于向交互式通信添加[Panel](../../forms/using/create-interactive-communication.md#add-panel-component-to-the-web-channel)。 |
   | 表 | 添加表格以便按行和列整理数据。 |
   | 目标区域 | 在Web渠道中插入目标区域以组织特定于Web渠道的组件。 目标区域是一个纯容器，用于对特定于Web渠道的组件进行分组。 |
   | 文本 | 向交互式通信的Web渠道中添加富文本。 文本还可以利用表单数据模型对象来使内容动态。 |
   | 按钮 | 用于向交互式通信添加[Button](../../forms/using/create-interactive-communication.md#add-button-component-to-the-web-channel)。 您可以使用按钮组件导航到其他交互式通信、自适应表单、其他资产（如图像或文档片段）或外部URL。 |
   | 分隔符 | 用于在交互式通信中插入水平线。 使用此组件可区分通信中的各个部分。 例如，您可以使用“分隔符”组件在信用卡对帐单中区分“客户详细信息”和“信用卡详细信息”部分。 |

1. 根据需要，在您的Web渠道中插入资产。

   您可以[预览交互式通信](#previewic)以查看交互式通信的打印和Web输出，并根据需要继续进行更改。

## 预览交互式通信 {#previewic}

可以使用&#x200B;**预览选项**&#x200B;评估交互式通信的外观。 交互式通信的Web渠道还提供了用于模拟各种设备的交互式通信体验的选项。 例如，iPhone、iPad和Desktop。 您可以将&#x200B;**预览**&#x200B;和&#x200B;**模拟器** ![标尺](assets/ruler.png)选项结合使用，以预览不同屏幕大小设备的Web输出。 预览中的示例数据是从指定的表单数据模型填充的。

1. 选择（打印或Web）渠道以预览和点按预览。 出现“Interactive Communication（交互式通信）”。

   >[!NOTE]
   >
   >预览将使用指定表单数据模型的示例数据填充。 有关预览与其他某些数据交互式通信或使用预填充服务的更多信息，请参阅[使用表单数据模型](/help/forms/using/using-form-data-model.md)和[使用表单数据模型](/help/forms/using/work-with-form-data-model.md)。

1. 对于Web渠道，使用![标尺](assets/ruler.png)查看交互式通信在各种设备上的显示方式。

   ![webchannelpreview](assets/webchannelpreview.png)

此外，您还可以使用代理UI](/help/forms/using/prepare-send-interactive-communication.md)准备和发送交互式通信。[

## 在交互式通信中配置属性{#configure-properties-in-interactive-communication}

### 附件和库访问 {#attachmentslibrary}

在“打印”渠道中，您可以配置附件和库访问权限，以允许代理在代理UI中管理用于交互式通信的附件：

1. 在“打印”渠道中，突出显示文档容器，然后点按&#x200B;**属性**。

   ![documentcontainerproperties](assets/documentcontainerproperties.png)

   “属性”面板将显示在侧栏中。

   ![属性附件](assets/propertiesattachments.png)

1. 展开&#x200B;**附件**&#x200B;并指定以下属性：

   * **[!UICONTROL 允许库访问]**:选择以在代理UI中启用代理的库访问。如果启用，则代理可在准备交互式通信时从库添加文件。
   * **[!UICONTROL 允许重新排序附件]**:选择以使代理使用交互式通信重新排序附件。
   * **[!UICONTROL 允许的最大附件数]**:指定交互式通信允许的最大附件数。
   * **[!UICONTROL 要附加的文件]**:点按 **** 添加并浏览以选择要附加的文件，并指定以下内容：

      * **[!UICONTROL 默认情况下，将此文件附加到文档]**:如果仅附件不是“必填”，则可以更改此选项。
      * **[!UICONTROL 必需：]** 代理将无法在代理UI中删除附件。

   ![附件](assets/attachfiles.png)

1. 点按&#x200B;**[!UICONTROL 完成]**。

### XDP/布局字段属性 {#xdplayoutfieldproperties}

1. 在编辑交互式通信的打印渠道时，将鼠标悬停在打印渠道模板中构建的字段上，然后选择![configure_icon](assets/configure_icon.png)(Configure)。

   “属性”(Properties)对话框显示在侧栏中。

   ![data_display_patterns_fields](assets/data_display_patterns_fields.jpg)

1. 指定以下内容：

   * **[!UICONTROL 名称]**:JCR节点名称。
   * **[!UICONTROL 标题]**:在代理UI和文档容器树中输入代理可见的标题。
   * **[!UICONTROL 绑定类型]**:为字段选择以下绑定类型之一。

      * 无：代理将填写属性的值。
      * 文本片段：如果选中此选项，则可以浏览并选择其内容在字段中呈现的文本文档片段。 或者，将文本文档片段拖放到字段名称中，以设置它们之间的绑定。 文本文档片段不得包含任何变量。
      * 数据模型对象：选择在字段中填充其值的表单数据模型属性。 或者，选择&#x200B;**数据源**&#x200B;选项卡，并将属性拖放到字段中。
   * **[!UICONTROL 默认值]**:默认值可确保当指定的数据模型对象或文本片段没有提供任何值时，该字段不为空。如果数据绑定类型为“无”，则会在字段中预填充默认值。
   * **[!UICONTROL 显示模式]**:您还可以为字段定义显示格式。从&#x200B;**类型**&#x200B;下拉列表中选择任何预定义选项，以将显示格式应用于字段。 选择&#x200B;**Custom**&#x200B;以定义列表中不可用的显示模式。 有关更多信息，请参阅[数据显示模式](../../forms/using/create-interactive-communication.md#datadisplaypatterns)

   * **[!UICONTROL 可由代理编辑]**:选择以允许代理编辑代理UI中字段中的值。如果“绑定类型”为“文本片段”，则此设置不适用。
   * **[!UICONTROL 标签]**:在代理UI中为代理指定随字段一起显示的文本字符串。如果“绑定类型”为“文本片段”，则此设置不适用。
   * **[!UICONTROL 工具提示]**:在Agent UI中，输入一个文本字符串，该字符串将在鼠标悬停在Agent上时可见。如果“绑定类型”为“文本片段”，则此设置不适用。
   * **[!UICONTROL 必需]**:选择以使该字段对座席为必填字段。如果“绑定类型”为“文本片段”，则此设置不适用。
   * **[!UICONTROL 允许多行]**:选择此字段可允许在字段中输入多行文本。如果“绑定类型”为“文本片段”，则此设置不适用。


1. 点按![done_icon](assets/done_icon.png)。

### 数据显示模式 {#datadisplaypatterns}

通过创作界面，您可以为在为打印和Web渠道创建交互式通信时可用的字段、变量和表单数据模型元素定义数据显示模式。

要配置数据显示模式，请点按该元素，选择![configure_icon](assets/configure_icon.png)(Configure)，然后在侧栏的&#x200B;**[!UICONTROL Properties]**&#x200B;面板中设置显示模式。 从&#x200B;**[!UICONTROL 类型]**&#x200B;下拉列表中选择任何预定义选项，以查看与选定类型关联的模式。 从&#x200B;**[!UICONTROL 类型]**&#x200B;下拉列表中选择&#x200B;**[!UICONTROL Custom]**&#x200B;以定义列表中不可用的模式。 编辑&#x200B;**[!UICONTROL Pattern]**&#x200B;字段中的值会自动将类型修改为&#x200B;**[!UICONTROL Custom]**。

要应用显示模式，“模式”字段中定义的字符或位数必须匹配或超过字段、变量和表单数据模型元素值中定义的字符或位数。 有关更多信息，请参阅[example](../../forms/using/create-interactive-communication.md#greaternumberofdigits)。

![data_display_pattern_example](assets/data_display_patterns_ssn_new.png)

在从打印渠道生成Web内容后，可以为字段、变量或表单数据模型元素重新定义显示模式。 因此，元素可以为打印和Web渠道定义不同的显示模式。 如果没有为打印渠道中的元素定义显示模式，并且使用打印渠道自动生成Web内容，则为打印渠道中的元素定义的数据绑定定义了&#x200B;**[!UICONTROL Type]**&#x200B;下拉列表中可用的显示模式选项。 如果没有为元素定义绑定，则元素的数据类型将定义可用的显示模式选项。 例如，如果为打印渠道中的元素创建Number类型的数据绑定，则&#x200B;**[!UICONTROL Type]**&#x200B;下拉列表中可用的显示模式选项将以各种格式为Number类型。

切换到&#x200B;**预览**&#x200B;模式或打开代理UI以查看应用于这些元素的显示模式。

下表列出了在为变量设置数据显示模式时显示的值示例：

| 类型 | 默认值 | 显示图案 | 显示值 | 描述 |
|---|---|---|---|---|
| 社会安全号码 | 123456789 | text{999-99-9999} | 123-45-6789 | 默认值字段中的位数与“模式”字段中的位数匹配。 成功显示基于模式的值。 |
| 社会安全号码 | 1234567 | text{999-99-9999} | 1-23-4567 | 默认值字段中的位数少于“模式”字段中的位数。 该模式适用于7位可用数字。 |
| 社会安全号码 | 1234567890 | text{999-99-9999} | 1234567890 | 默认值字段中的位数大于“模式”字段中的位数。 因此，显示值没有变化。 |

如果未为变量或表单数据模型元素指定显示模式，则默认使用[全局文档片段配置](https://helpx.adobe.com//experience-manager/6-5/forms/using/interactive-communication-configuration-properties.html)。

如果未将显示模式应用于数字数据类型的变量，则“打印”预览会根据全局文档片段配置显示该模式。 如果对默认全局文档片段配置应用更改，代理UI仍会根据为区域设置定义的默认分隔符来显示模式。

同样，对于字段，如果未指定显示模式，则创建打印模板(XDP)时定义的模式将应用于该字段。 如果在创建打印模板时没有模式，则基于XFA规范的默认模式将应用于这些字段。

此外，如果指定的显示模式不正确或无法应用，则基于XFA规范的默认模式将应用于字段、变量或表单数据模型元素。

## 将规则应用于交互式通信组件 {#rules}

要在交互式通信中条件化组件或内容，请点按组件/内容段，然后选择![createleicon](assets/createruleicon.png)（创建规则）以启动规则编辑器。

有关更多信息，请参阅：

* [规则编辑器](/help/forms/using/rule-editor.md)
* [交互式通信创作简介](/help/forms/using/introduction-interactive-communication-authoring.md)

## 使用表 {#tables}

### 交互式通信中的动态表{#dynamic-tables-in-interactive-communication}

您可以在交互式通信中使用布局片段添加动态表。 以下步骤使用信用卡报表的示例来说明如何使用布局片段在交互式通信中创建动态表。

1. 确保创建表所需的布局片段在AEM中可用。
1. 在交互式通信的打印渠道中，从资产浏览器将布局片段（包含多列表）拖放到目标区域中。

   ![lf_dragdrop](assets/lf_dragdrop.png)

   “交互式通信”布局区域中会显示一个表。

   ![lf_dragdrop_table](assets/lf_dragdrop_table.png)

1. 为表的每个单元格指定数据绑定。 要创建可重复行，请在属于公共集合属性的行中插入表单数据模型属性。

   1. 点按表中的单元格，然后选择![configure_icon](assets/configure_icon.png)(Configure)。

      “属性”(Properties)对话框显示在侧栏中。

      ![lf_cell_properties](assets/lf_cell_properties.png)

   1. 配置属性：

      * **[!UICONTROL 名称]**:JCR节点名称。
      * **[!UICONTROL 标题]**:输入将在交互式通信编辑器中显示的标题。
      * **[!UICONTROL 绑定类型]**:为字段选择以下绑定类型之一。

         * **[!UICONTROL 无]**
         * **[!UICONTROL 数据模型对象]**:字段中会填充表单数据模型属性的值。或者，选择&#x200B;**数据源**&#x200B;选项卡，并将属性拖放到字段中。
      * **[!UICONTROL 数据模型对象]**:其值在字段中填充的表单数据模型属性。
      * **[!UICONTROL 默认值]**:默认值可确保当指定的数据模型对象没有提供值时，该字段不为空。默认值会预填充在字段中。

      * **[!UICONTROL 可由代理编辑]**:选择以允许代理编辑代理UI中字段中的值。
   1. 点按![done_icon](assets/done_icon.png)。



1. 预览交互式通信以查看使用数据呈现的表。

   ![lf_preview](assets/lf_preview.png)

### 仅Web渠道表 {#webchanneltables}

点按Web模板中的根面板，然后点按&#x200B;**+** ，以将&#x200B;**Table**&#x200B;组件添加到交互式通信。 在交互式通信中插入包含两行的表。 表的第一行表示表标题。

#### 向表中添加行和列 {#addrowscolumnstable}

**添加或删除列：**

1. 点按表标题行中的默认文本框以查看组件工具栏。
1. 选择&#x200B;**添加列**&#x200B;或&#x200B;**删除列**&#x200B;可分别添加或删除表列。

![component_toolbar_table1](assets/component_toolbar_table1.png)

**要添加或删除行，请执行以下操作：**

1. 点按任意表行以查看组件工具栏。 您还可以使用交互式通信Sidekick中的内容浏览器选择表行。
1. 选择&#x200B;**添加行**&#x200B;或&#x200B;**删除行**&#x200B;可分别添加或删除表行。 使用工具栏中提供的&#x200B;**向上移动**&#x200B;和&#x200B;**向下移动**&#x200B;选项来重新排列表中的行。

![组件工具栏](assets/component_toolbar_table_row_new.png)

**A.** 添加行 **B.** 删除行 **C.** 向上 **移动D.** 向下移动

#### 在表格单元格中添加或编辑文本 {#addedittexttable}

1. 选择表单元格中的默认文本框，然后点按![编辑](assets/edit.png)（编辑）。
1. 在表单元格中键入文本，然后点按![done_icon](assets/done_icon.png)以保存该文本。

#### 在表单元格和数据模型对象元素之间创建绑定 {#createbindingtablecells}

1. 选择表行中的默认文本框，然后点按![edit](assets/edit.png)（编辑）。
1. 点按数据模型对象下拉列表，然后选择属性。
1. 点按以在表单元格和数据模型对象属性之间保存和创建绑定。

![创建数据绑定](assets/create_data_binding_table_new.png)

#### 为表单元格中的文本创建超链接 {#createhyperlinktable}

1. 选择表单元格中的默认文本框，然后点按![编辑](assets/edit.svg)（编辑）。
1. 在表格单元格中选择文本，然后点按超链接图标。
1. 在&#x200B;**Path**&#x200B;字段中指定URL。
1. 点按![done_icon](assets/done_icon.png)以保存超链接属性。

![创建超链接](assets/create_hyperlink_table_new.png)

#### 创建动态表 {#createdynamictables}

您可以使用类型集合的数据模型属性在交互式通信中创建仅Web渠道动态表。 此类表是集合属性的子属性的表示形式。 您只能编辑表中各单元格的格式属性。

1. 切换到Web渠道，然后选择显示数据源浏览器。
1. 将收藏集属性拖放到子表单中。 将在子表单中创建表。
1. 在交互式通信的Web预览中预览表。

#### 对表中的列进行排序 {#sortcolumns}

您可以根据交互式通信中表格中的任意列对数据进行排序。 列中的值可以按升序或降序排序。

排序可应用于包含以下项的表列：

* 静态文本
* 数据模型对象属性
* 静态文本和数据模型对象属性的组合

要启用排序，请执行以下操作：

1. 选择表，然后点按![configure_icon](assets/configure_icon.png)(Configure)。 您还可以使用交互式通信Sidekick中的&#x200B;**Content**&#x200B;浏览器选择表。
1. 选择&#x200B;**启用排序。**
1. 点按![done_icon](assets/done_icon.png)以保存表属性。 列标题中的排序图标（上箭头和下箭头）表示排序已启用。

   ![启用排序](assets/enable_sorting_new-1.png)

1. 切换到&#x200B;**预览**&#x200B;模式以查看输出。 表格会根据表格的第一列自动排序。
1. 单击列标题可根据列对值进行排序。

   带有向上箭头的列标题表示：

   * 表会根据该列进行排序。
   * 列中的值以升序显示。

   ![升序排序](assets/sorting_ascending_new-1.png)

   同样，带有向下箭头的列标题表示列中的值以降序显示。

## 编辑交互式通信属性{#edit-interactive-communication-properties}

创建交互式通信后，您可以在以后的阶段编辑其属性。

使用&#x200B;**Properties**&#x200B;页可以：

* 编辑在创建交互式通信时指定的字段的值，如标题和描述。
* 添加或删除现有交互式通信的Web渠道。
* 预览、下载或删除交互式通信
* 打开[Agent UI](/help/forms/using/prepare-send-interactive-communication.md)。

要访问&#x200B;**Properties**&#x200B;页面，请执行以下操作：

1. 登录到AEM创作实例，然后导航到&#x200B;**Adobe Experience Manager** > **Forms** > **Forms和文档**。
1. 选择交互式通信，然后点按&#x200B;**属性**。
1. 选择&#x200B;**General**&#x200B;选项卡以编辑&#x200B;**Title**&#x200B;和&#x200B;**Description**&#x200B;字段。

### 添加或删除Web渠道{#add-or-delete-the-web-channel}

执行以下步骤为现有交互式通信添加Web渠道：

1. 在&#x200B;**属性**&#x200B;页面上，选择&#x200B;**渠道**&#x200B;选项卡。
1. 选中&#x200B;**Web**&#x200B;复选框并为Web渠道选择模板。
1. 选择&#x200B;**使用Web通道的主控打印**&#x200B;以启用Web通道与打印通道之间的同步。
1. 点按&#x200B;**保存并关闭**&#x200B;以保存更改。

   同样，您也可以点按&#x200B;**渠道**&#x200B;选项卡上的&#x200B;**Web**&#x200B;复选框，以从交互式通信中删除Web渠道。

## 将按钮组件添加到Web渠道{#add-button-component-to-the-web-channel}

您可以将按钮作为组件添加到交互式通信的Web渠道中。 使用[规则编辑器](../../forms/using/rule-editor.md)定义规则，以便能够导航到其他交互式通信、自适应表单、其他资产（如图像或文档片段），或点按按钮时的外部URL。

要添加按钮并在其上定义规则，请执行以下操作：

1. 点按Web模板中的根面板，然后点按&#x200B;**+** ，以将&#x200B;**Button**&#x200B;组件添加到交互式通信。
1. 点按按钮组件，然后点按![edit-rules](assets/edit-rules.png) ，以在点按按钮时定义规则。
1. 在&#x200B;**When**&#x200B;部分中，从按钮的状态下拉列表中选择&#x200B;**clicked**。
1. 在&#x200B;**Then**&#x200B;部分中：

   1. 从下拉列表中选择一个操作。 例如，选择&#x200B;**导航到**&#x200B;作为操作类型。

   1. 指定交互式通信、自适应表单、资产或网页的URL。 例如，以下格式指定URL以导航到另一个交互式通信：https://&lt;server-name>:&lt;port>/editor.html/content/forms/af/&lt;Interactive Communication name>/channels/&lt;channel name - print or web>.html
   1. 指定在同一选项卡、新选项卡或新窗口中打开资产的选项。
   1. 点按&#x200B;**完成**，然后点按&#x200B;**关闭**&#x200B;以保存规则。

   同样，您也可以从操作类型下拉列表中选择其他可用选项，例如调用服务和提交表单。 有关更多信息，请参阅[规则编辑器](../../forms/using/rule-editor.md)。

1. 预览交互式通信，然后点按按钮以查看在步骤4(b)中指定的交互式通信、自适应表单、资产或网页。

## 将面板组件添加到Web渠道{#add-panel-component-to-the-web-channel}

面板组件是用于将其他组件分组在一起的占位符，可控制在交互式通信中如何布局一组组件（如折叠面板和选项卡）。 面板组件还允许您使一组组件可重复用于最终用户，例如在填写教育凭据所需的多个条目中。

执行以下步骤以将面板组件添加到Web渠道：

1. 使用以下任一选项在Web渠道中插入&#x200B;**面板**&#x200B;组件：

   * 点按某个组件，点按&#x200B;**+**&#x200B;并选择&#x200B;**面板**&#x200B;组件。

   * 从&#x200B;**组件**&#x200B;浏览器面板中，将&#x200B;**面板**&#x200B;组件拖放到交互式通信中。

   * 点按&#x200B;**内容**&#x200B;浏览器面板中的&#x200B;**面板**，然后点按&#x200B;**添加子面板**。 选择&#x200B;**添加子面板**&#x200B;选项将显示&#x200B;**添加子面板**&#x200B;对话框。 输入面板组件的标题以及可选描述和名称。

1. 从&#x200B;**内容**&#x200B;浏览器中点按面板，以对面板执行其他操作，如配置、编辑规则、复制、删除和插入组件。

   您还可以在&#x200B;**Content**&#x200B;浏览器中拖放面板，以在右侧窗格中反映交互式通信结构的更改。

## 与打印渠道同步Web渠道 {#synchronize}

在创建交互式通信时，如果选择“打印为Web渠道的主控”，则会创建与“打印”渠道同步的Web渠道，并且Web渠道的内容和数据绑定从打印渠道派生，并且当您点按“同步”时，在打印渠道中所做的更改可能会反映在Web渠道中。

但是，作者可以根据需要中断Web渠道中组件的继承。

![创建打印](assets/create_ic_print_master_new-1.png) ![主打印主控Web](assets/create_ic_print_master_web_new-1.png)

### 自动同步 {#autosync}

如果选择&#x200B;**[!UICONTROL Use Print As 主控 for Web Channel]**&#x200B;选项，则可以选择以下任何模式以生成Web渠道：

* **[!UICONTROL 自动布局]**:选择此模式可自动从打印渠道为Web渠道生成占位符、内容和数据绑定。
* **[!UICONTROL 手动组织]**:选择此模式，可使用数据源选项卡中提供的主控内容手动选择打印渠道元素并将其添加到Web渠道。有关更多信息，请参阅[选择打印渠道元素以创建Web渠道内容](#selectprintchannelelements)。

![创建IC选项](assets/create_ic_options_updated_new.png)

>[!NOTE]
>
>同步渠道仅同步从打印渠道到Web渠道的文档片段、图像、条件、列表和布局片段。 不会同步包含此类元素的子表单或父节点。

### 选择打印渠道元素以创建Web渠道内容 {#selectprintchannelelements}

如果在创建交互式通信时选择打印为主控，并且没有选择自动同步选项，则还可以将打印渠道元素拖放到Web渠道创作界面。

导航到&#x200B;**数据源** > **主控内容**&#x200B;以查看打印渠道元素。 将目标区域、字段或表拖放到Web渠道创作界面中。 元素名称旁边的蓝色圆图标表示“打印”渠道元素已包含在Web渠道中。

![主控内容](assets/master_content.png)

### 取消继承 {#cancelinheritance}

在Web渠道中，组件嵌入到目标区域中。

将鼠标悬停在Web渠道中的相关目标区域或变量上，然后选择![canceleintance](assets/cancelinheritance.png)（取消继承），然后在“取消继承”对话框中，点按&#x200B;**[!UICONTROL Yes]**。

目标区域内组件的继承将被取消，现在您可以根据需要对其进行编辑。

### 重新启用继承 {#re-enable-inheritance}

在Web渠道中，如果已取消组件的继承，则可以重新启用该组件。 要重新启用继承，请将鼠标悬停在相关目标区域（包括该组件）的边界上，然后点按![reenableintance](assets/reenableinheritance.png)。

此时会出现“还原继承”对话框。

![反继承](assets/revertinheritance.png)

如果需要，请选择&#x200B;**[!UICONTROL 在还原继承后同步页面]**。 选择此选项可同步整个交互式通信。 如果不选择此选项，则只有在恢复继承时同步相关目标区域。

点按&#x200B;**[!UICONTROL Yes]**。

### 同步 {#synchronize-1}

如果您将“打印为Web渠道的主控”并对“打印”渠道进行更改，则可以同步内容以将新所做的更改引入Web渠道。

1. 要将Web渠道与打印渠道同步，请切换到Web渠道，然后点按更多选项图标。

   ![自动同步选项](assets/auto_sync_options_new.png)

1. 点按以下任一项：

   * **[!UICONTROL 与打印同步]**:仅同步未取消继承的目标区域的内容。
   * **[!UICONTROL 重置]**:将Web渠道内容与打印渠道同步，并放弃对Web渠道所做的所有更改。

### 使用组件工具栏对继承的组件执行操作 {#componenttoolbar}

使用同步选项在Web渠道中自动生成内容后，您可以对组件执行更多操作，而无需取消继承。

![组件工具栏](assets/component_toolbar_inherited_web_new.png)

点按组件可查看以下选项：

* **复制：** 复制组件并将其粘贴到交互式通信中的其他位置。
* **剪切：** 在交互式通信中将组件从一个位置移动到另一个位置。
* **插入组件：** 在选定组件上方插入组件。
* **粘贴：** 使用上述选项粘贴您剪切或复制的组件。
* **组：** 如果要剪切、复制或粘贴多个组件，请选择多个组件。
* **父项：** 选择组件的父项。
* **查看SOM表达式：** 查看组 [件](../../forms/using/using-som-expressions-adaptive-forms.md) 的SOM表达式。

* **在面板中对象分组：** 在面板中对组件分组，以便能够同时对这些组件执行操作。有关详细信息，请参阅面板](#groupobjectspanel)中的[组对象。

* **取消继承：** [取消目](#cancelinheritance) 标区域中组件的继承以对其进行编辑。

### 在面板中对象组 {#groupobjectspanel}

Web渠道创作界面便于将面板中的组件分组以便能够同时对这些组件执行操作。 **内容**&#x200B;选项卡将分组的组件列为内容树中面板的子元素。

1. 点按某个组件并选择“组”（![组](assets/group.jpg)）操作。
1. 选择多个组件，然后点按面板&#x200B;**中的**&#x200B;组对象。

   ![组对象](assets/component_toolbar_group_objects_new.png)

1. 在面板&#x200B;**中的**&#x200B;对象组对话框中，输入面板的名称。
1. 为面板输入可选标题和描述。
1. 单击![bullet_checkmark](assets/bullet_checkmark.png)。

   分组的组件在内容树中显示为面板的子元素。

   ![content_tree_grouping](assets/content_tree_grouping.png)

## 打印通道{#output-format-print-channel}的输出格式

使用PrintChannel API为交互式通信的打印渠道定义输出格式。 如果不定义输出格式，则AEM Forms将生成PDF格式的输出。

```javascript
//options for rendering print channel of a multi-channel document
PrintChannelRenderOptions renderOptions = new PrintChannelRenderOptions();
PrintDocument printDocument = printChannel.render(renderOptions);
```

要以任何其他格式生成输出，请指定输出格式类型。 有关支持的输出格式类型列表，请参阅[PrintChannel API](https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/PrintConfig.html)。

例如，您可以使用以下示例将PCL定义为交互式通信的输出格式：

```javascript
//options for rendering print channel of a multi-channel document
PrintChannelRenderOptions renderOptions = new PrintChannelRenderOptions();
renderOptions.setRenderFormat(PrintConfig.HP_PCL_5e);
PrintDocument printDocument = printChannel.render(renderOptions);
```
