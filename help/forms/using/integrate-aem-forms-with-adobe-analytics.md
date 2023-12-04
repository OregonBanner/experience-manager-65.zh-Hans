---
title: 如何将AEM Forms与Adobe Analytics集成？
description: AEM Forms与Adobe Analytics集成，以捕获和跟踪已发布表单的性能指标。
docset: aem65
exl-id: 030fe9f2-cd41-4290-b8a6-2f9ade6b5789
source-git-commit: bd86d647fdc203015bc70a0f57d5b94b4c634bf9
workflow-type: tm+mt
source-wordcount: '1762'
ht-degree: 0%

---

# Analytics使用 [!DNL Adobe Launch] {#analyticsusingadobelaunch}

AEM Forms集成 [Adobe Analytics](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/overview.html?lang=en) 允许您捕获和跟踪已发布表单的性能指标。 分析这些量度背后的目标是使商业用户能够洞察最终用户行为并优化数据捕获体验。 您可以通过Adobe Analytics for Adaptive Forms捕获和跟踪已登录和未登录（匿名）用户的行为。

您还可以使用Cloud Service框架执行分析。 有关如何将AEM Forms与Cloud Service框架集成的详细信息，请参阅 [使用Cloud Service框架进行分析](/help/forms/using/configure-analytics-forms-documents.md). 与使用Adobe框架的Analytics相比，使用Cloud ServiceLaunch的主要优势在于，除了这些现成事件之外，您还可以定义自定义事件。 自定义事件使用规则编辑器或客户clientlibs定义，并映射到中的事件 [!DNL Adobe Analytics].

执行本文中提到的操作后，您可以在中配置和查看报表 [!DNL Adobe Analytics]，如以下视频中所示：

>[!VIDEO](https://video.tv.adobe.com/v/337262)

您可以使用 [!DNL Adobe Analytics] 发现用户在使用自适应表单时面临的交互模式和问题。 开箱即用， [!DNL Adobe Analytics] 跟踪并存储有关以下事件的信息：

* **渲染**：表单被打开的次数。

* **提交**：表单提交次数。

* **放弃**：用户未完成表单而离开的次数。

* **错误**：在面板和面板的字段中遇到的错误数。

* **帮助**：用户打开面板帮助和面板字段的次数。

* **实地访问**：用户访问表单中字段的次数。

* **保存**：用户将表单保存到Forms门户的次数。

除了这些开箱即用的事件之外，您还可以定义自定义事件。

下图说明了在中查看报告之前需要执行的操作 [!DNL Adobe Analytics]：

![Analytics概述](/help/forms/using/assets/analyticsworkflow.png)

## 1.配置 [!DNL Adobe Analytics] {#Configure-adobe-analytics}

配置之前 [!DNL Adobe Analytics]，创建：

* 要登录的Adobe ID [Adobe Experience Cloud](https://experience.adobe.com/#/home).
* A [报告包](https://experienceleague.adobe.com/docs/analytics/admin/manage-report-suites/new-report-suite/t-create-a-report-suite.html).


### 安装AEM Forms和 [!DNL Adobe Analytics] 扩展 {#install-extensions}

执行以下步骤以配置AEM Forms和 [Adobe Analytics](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/analytics/overview.html) 扩展：

1. 登录到Adobe Experience Cloud，然后为公司选择适当的名称。

1. 选择 **[!UICONTROL 启动/数据收集]** 并选择 **[!UICONTROL 转到Launch/数据收集]**.

1. 选择 **[!UICONTROL 新建属性]** 并指定配置的名称。

1. 指定域名并选择 **[!UICONTROL 保存]** 以保存资产。

1. 选择标记属性列表中可用的配置名称。

1. 在 **[!UICONTROL 创作]** 部分，选择 **[!UICONTROL 扩展]**.

1. 选择 **[!UICONTROL 目录]** 并选择 **[!UICONTROL 安装]** 对于 **[!UICONTROL Adobe Experience Manager Forms]** 扩展。 **[!UICONTROL Adobe Experience Manager Forms]** 会在中提供的已安装扩展列表中显示 **已安装** 选项卡。

1. 选择 **[!UICONTROL 安装]** 对于 **[!UICONTROL Adobe Analytics]** 扩展。
1. 在中选择报表包名称 **[!UICONTROL 开发报表包]**， **[!UICONTROL 暂存报表包]**、和 **[!UICONTROL 产品报表包]** 下拉列表并选择 **[!UICONTROL 保存]** 以保存该扩展。

### 配置数据元素 {#configure-data-elements}

您可以在为事件创建的规则中选择任何已配置的数据元素。 当自适应表单上发生事件时，AEM Forms将这些数据元素发送至 [!DNL Adobe Analytics].

安装之后 **[!UICONTROL Adobe Experience Manager Forms]** 扩展中，您可以创建以下数据元素：

<table>
 <tbody>
  <tr>
   <td>字段名称</th>
   <td>字段标题</th>
   <td>FormInstance</th>
  </tr>
  <tr>
   <td>表单名称<br /> </td>
   <td>表单标题<br /> </td>
   <td>页面名称</td>
  </tr>
  <tr>
   <td>PageURL<br /> </td>
   <td>面板标题<br /> </td>
   <td>逗留时间</td>
  </tr>
 </tbody>
</table>

执行以下步骤以配置数据元素：

1. 在 **[!UICONTROL 创作]** 部分，选择 **[!UICONTROL 数据元素]**.

1. 选择 **[!UICONTROL 创建新数据元素]**.

1. 指定数据元素的名称。 例如，FormTitle数据元素类型的表单标题。

1. 指定 **[!UICONTROL Adobe Experience Manager Forms]** 作为扩展名称。

1. 选择 **[!UICONTROL 数据元素类型]**.

1. 选择 **[!UICONTROL 保存]** 以保存数据元素。

   >[!VIDEO](https://video.tv.adobe.com/v/337472)

### 配置规则 {#configure-rules}

执行以下步骤以根据 **[!UICONTROL Adobe Experience Manager Forms]** 扩展名：

1. 在 **[!UICONTROL 创作]** 部分，选择 **[!UICONTROL 规则]**.

1. 选择 **[!UICONTROL 创建新规则]**.

1. 指定规则的名称。 例如，表单提交以记录表单提交。

1. 在 **[!UICONTROL 活动]** 部分，选择 **[!UICONTROL 添加]**.

1. 指定 **[!UICONTROL Adobe Experience Manager Forms]** 作为扩展名称。

1. 选择事件类型。 的输入 **[!UICONTROL 名称]** 字段会根据所选事件类型自动填充。

1. 选择 **[!UICONTROL 保留更改]** 以保存事件。

1. 在 **[!UICONTROL 操作]** 部分，选择 **[!UICONTROL 添加]**.

1. 指定 **[!UICONTROL Adobe Analytics]** 作为扩展名称。

1. 选择 **[!UICONTROL 设置变量]** 作为操作类型。 下拉列表中的可用选项包括：

   * **[!UICONTROL 设置变量]**：使用此操作类型定义从AEM Forms向其发送选定数据元素的事件类型 [!DNL Adobe Analytics].

   * **[!UICONTROL 发送信标]**：使用此操作类型将数据从AEM Forms发送到 [!DNL Adobe Analytics].

   * **[!UICONTROL 清除变量]**：使用此操作类型清除数据跟踪，以便事件在中仅注册一次 [!DNL Adobe Analytics].

     推荐的方法是使用 **[!UICONTROL 设置变量]** 操作类型以配置事件和数据元素，然后使用 **[!UICONTROL 发送信标]** 以发送数据，然后使用 **[!UICONTROL 清除变量]** 以清除数据跟踪。

1. 在 **[!UICONTROL Prop]** 部分，将下拉列表中可用的报表包选项映射到使用定义的数据元素 [配置数据元素](#configure-data-elements).

   例如，要发送 **表单标题** 从AEM Forms到的数据元素 [!DNL Adobe Analytics] 在提交表单时：
   1. 在 **[!UICONTROL Prop]** 部分，为报表包中可用的表单标题选择一个prop ，然后选择 ![“数据库”图标](/help/forms/using/assets/database-icon.svg) 以将其映射到在中创建的表单标题 [配置数据元素](#configure-data-elements).

      ![define-props](/help/forms/using/assets/define-props.png)

   1. 选择 **[!UICONTROL 添加其他]** 以向列表中添加更多数据元素。

1. 在 **[!UICONTROL 活动]** 部分，从报表包中可用的选项中选择一个事件，然后选择 **[!UICONTROL 保留更改]**.

1. 在 **[!UICONTROL 操作]** 部分，选择+并指定 **[!UICONTROL Adobe Analytics]** 作为扩展名称。

1. 选择 **[!UICONTROL 发送信标]** 作为操作类型。 在右窗格中，选择 **[!UICONTROL s.t()]** 以将数据发送到 [!DNL Adobe Analytics] 并将其视为页面查看或 **[!UICONTROL s.tl()]** 以将数据发送到 [!DNL Adobe Analytics] 并且不要将其视为页面查看。 选择 **[!UICONTROL 保留更改]**.

1. 在 **[!UICONTROL 操作]** 部分，选择+并指定 **[!UICONTROL Adobe Analytics]** 作为扩展名称。

1. 选择 **[!UICONTROL 清除变量]** 作为操作类型。 选择 **[!UICONTROL 保留更改]**. 执行这些步骤后， **[!UICONTROL 操作]** 部分显示为：
   ![操作配置](/help/forms/using/assets/actions-config.png)

   自定义 **[!UICONTROL 操作]** 部分。 例如，您可以定义两个 **发送信标** 操作流中用于将数据发送到的步骤 [!DNL Adobe Analytics] 并将其视为一个步骤中的页面查看，并将数据发送到 [!DNL Adobe Analytics] 并且不要将其视为第二步中的页面查看。

   ![操作配置](/help/forms/using/assets/actions-config-2.png)

1. 选择 **[!UICONTROL 保存]** 以保存规则。

   您可以为所有事件类型创建规则，例如“放弃”、“错误”、“字段访问”、“帮助”、“渲染”、“保存”和“提交”。

   >[!VIDEO](https://video.tv.adobe.com/v/337425)


### 发布流 {#publish-flow}

创建数据元素并在规则中使用它们后，发布配置以在中收集表单数据 [!DNL Adobe Analytics].

执行以下步骤以发布配置：

1. 在 **[!UICONTROL 发布]** 部分，选择 **[!UICONTROL 发布流]**.

1. 选择 **[!UICONTROL 添加库]** 并指定名称，然后选择库的环境。

1. 选择 **[!UICONTROL 添加所有已更改资源]** 然后选择 **[!UICONTROL 保存并生成到开发环境]**.

1. 在 **[!UICONTROL 开发]** 部分，选择 ![更多选项](/help/forms/using/assets/more-options-icon.svg) 然后选择 **[!UICONTROL 批准并发布到生产环境]**.

1. 确认更改，发布流将很快显示在中 **[!UICONTROL 已发布]** 部分。

![发布流程](/help/forms/using/assets/publish-flow.png)

## 2.配置AEM Forms {#configure-aem-forms}

在创建Adobe启动项配置之前，请创建 [将AdobeLaunch用作云解决方案的Adobe IMS配置](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/connect-aem-launch-adobe-io.html).

### 创建 Adobe Launch 配置 {#create-adobe-launch-configuration}

执行以下步骤以创建AdobeLaunch配置：

1. 在AEM Forms创作实例上，导航到 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL AdobeLaunch配置]**.

1. 选择一个文件夹以创建配置，然后选择 **[!UICONTROL 创建]**.

1. 在中指定配置的标题 **[!UICONTROL 标题]** 字段。

1. 选择 [关联的Adobe IMS配置](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/connect-aem-launch-adobe-io.html).

1. 选择期间使用的公司名称 [配置Adobe Analytics](#Configure-adobe-analytics).

1. 选择所创建属性的名称，同时 [配置Adobe Analytics](#install-extensions).

1. 选择&#x200B;**[!UICONTROL 保存并关闭]**。

1. 发布配置。

### 启用 [!DNL Adobe Analytics] 自适应表单 {#enable-analytics-adaptive-form}

使用 [!DNL Adobe Launch] 现有自适应表单中的配置：

1. 在AEM Forms创作实例上，导航到 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms和文档]**.
1. 选择自适应表单，然后选择 **[!UICONTROL 属性]**.
1. 在 **[!UICONTROL 基本]** 选项卡，选择 [配置容器](#create-adobe-launch-configuration) 在创建Adobe启动项配置时使用。
1. 选择 **[!UICONTROL 保存并关闭]**. 自适应表单已启用 [!DNL Adobe Analytics].
1. 发布表单。

启用后 [!DNL Adobe Analytics] 对于自适应表单，您可以 [验证](https://experienceleague.adobe.com/docs/launch-learn/implementing-in-websites-with-launch/implement-solutions/analytics.html?lang=en#validate-the-page-view-beacon) 如果AEM Forms与之间有适当的数据事件流 [!DNL Adobe Analytics]. AEM Forms与Adobe Analytics的集成已完成。 您现在可以 [在Adobe Analytics中配置和查看报表](#view-reports-adobe-analytics).

>[!NOTE]
>如果两者都有 [使用Cloud Service框架进行分析](/help/forms/using/configure-analytics-forms-documents.md) 和 **使用Adobe启动项的Analytics** 特征同时启用， **使用Adobe启动项的Analytics** 将优先。
> 

### 创建规则以捕获自定义事件（可选） {#capture-custom-events}

使用规则编辑器针对自适应表单的特定字段创建规则，以将Analytics数据从自适应表单发送到 [!DNL Adobe Analytics].

在两阶段流程中，您需要在自适应表单中的字段上定义规则。 规则调度事件。 事件名称将映射到Adobe启动项中的自定义捕获事件。

要在自适应表单中使用规则编辑器创建规则，请执行以下操作：

1. 选择字段并选择 ![规则编辑器](/help/forms/using/assets/rule-editor-icon.svg) 以打开规则编辑器页面。
1. 在中定义条件 [!UICONTROL 时间] 部分。
1. 在 [!UICONTROL 则] 部分，选择 **[!UICONTROL 分派事件]** 从 **[!UICONTROL 选择操作]** 下拉列表。
1. 在中指定事件的名称 **[!UICONTROL 键入事件名称]** 字段。

例如，如果出生日期在某个日期之前，AEM Forms会发送 **安全性** 事件。

![分派事件](/help/forms/using/assets/security-event.png)

将事件映射到中的自定义捕获事件 [!DNL Adobe Analytics]：

1. [创建规则](#configure-rules).

1. 在 **[!UICONTROL 活动]** 部分，选择 **[!UICONTROL 添加]**.

1. 指定 **[!UICONTROL Adobe Experience Manager Forms]** 作为扩展名称。

1. 选择 **[!UICONTROL 捕获自定义事件]** 从 **[!UICONTROL 事件类型]** 下拉列表。

1. 使用规则编辑器创建规则时，指定您在步骤4中指定的事件的名称。

1. 选择 **保留更改** 并执行中指定的其余操作 [配置规则](#configure-rules).

## 3.在中配置和查看报表 [!DNL Adobe Analytics] {#view-reports-adobe-analytics}

配置自适应表单以将事件数据发送到后 [!DNL Adobe Analytics]，您便可以开始在中查看报表 [!DNL Adobe Analytics]：

1. 选择 ![选择产品](/help/forms/using/assets/select-analytics.png) 并选择 **[!UICONTROL 分析]**.

1. 选择 **[!UICONTROL 创建项目]** 并选择 **[!UICONTROL 空白项目]**.

1. 从自由格式右上角的下拉列表中选择报表包名称。

1. 指定 **表单标题** 在 **[!UICONTROL 搜索维度项目]** 文本以查看所有表单标题。

1. 将自适应表单标题拖放到 **[!UICONTROL 将区段（或任何其他组件）拖放到此处]** 文本框。

1. 从 **[!UICONTROL 量度]** 部分，放置要跟踪的事件 **[!UICONTROL 将量度（或任何其他组件）拖放到此处]** 文本框。

1. 选择 ![可视化图表](/help/forms/using/assets/visualization-icon.svg) 并将图表类型拖放到“自由格式”部分。 同样，可以向自由格式部分添加多个图表类型。

1. 选择Ctrl + S键，并指定名称以保存项目。

有关查看表单分析报表的详细信息，请参阅 [查看和了解AEM Forms Analytics报表](../../forms/using/view-understand-aem-forms-analytics-reports.md).
