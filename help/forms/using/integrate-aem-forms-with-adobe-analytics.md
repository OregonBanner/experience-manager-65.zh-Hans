---
title: 如何将AEM Forms与Adobe Analytics集成？
seo-title: Learn how to integrate AEM Forms with Adobe Analytics.
description: AEM Forms与Adobe Analytics集成，用于捕获和跟踪已发布表单的性能量度。
seo-description: To discover interaction patterns and problems users face while using adaptive forms.
uuid: e258805c-4da8-4c5d-ae91-7bea78a6a71b
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
discoiquuid: 8f776f30-ff93-4d19-94c6-c4bfe6f1fae2
docset: aem65
exl-id: be2444df-c772-4a8e-83f9-0f565c15a44e
source-git-commit: 9ee8e79777b89fbf4d6e5b5fd1dbb1ef3bc9ad5d
workflow-type: tm+mt
source-wordcount: '1720'
ht-degree: 0%

---

# 与[!DNL Adobe Analytics] 集成  {#integrate-aem-forms-with-adobe-analytics}

AEM Forms集成 [Adobe Analytics](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/overview.html?lang=en) 以捕获和跟踪已发布表单的性能量度。 分析这些量度的目的在于使业务用户能够深入了解最终用户的行为并优化数据捕获体验。 您可以通过Adobe Analytics for Adaptive Forms捕获和跟踪已登录和未登录（匿名）用户的行为。

执行本文中所述的操作后，您可以在 [!DNL Adobe Analytics]，如以下视频中所示：

>[!VIDEO](https://video.tv.adobe.com/v/337262)

您可以使用 [!DNL Adobe Analytics] 以发现用户在使用自适应表单时遇到的交互模式和问题。 开箱即用， [!DNL Adobe Analytics] 跟踪并存储有关以下事件的信息：

* **呈现**:打开表单的次数。

* **提交**:提交表单的次数。

* **放弃**:用户在未完成表单时离开的次数。

* **错误**:在面板和面板的字段中遇到的错误数。

* **帮助**:用户打开面板帮助和面板字段的次数。

* **现场访问**:用户访问表单中字段的次数。

* **保存**:用户将表单保存到Forms Portal的次数。

除了这些开箱即用事件之外，您还可以使用规则编辑器在自适应表单中定义自定义事件，并将这些事件映射到 [!DNL Adobe Analytics]

下图说明了在查看 [!DNL Adobe Analytics]:

![Analytics概述](/help/forms/using/assets/analytics-workflow.png)

## 1.配置 [!DNL Adobe Analytics] {#Configure-adobe-analytics}

配置之前 [!DNL Adobe Analytics]，创建：

* 要登录的Adobe ID [Adobe Experience Cloud](https://experience.adobe.com/#/home).
* A [报表包](https://experienceleague.adobe.com/docs/analytics/admin/manage-report-suites/new-report-suite/t-create-a-report-suite.html).


### 安装AEM Forms和 [!DNL Adobe Analytics] 扩展 {#install-extensions}

执行以下步骤以配置AEM Forms和 [Adobe Analytics](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/analytics/overview.html) 扩展：

1. 登录到Adobe Experience Cloud，然后为公司选择适当的名称。

1. 点按 **[!UICONTROL 启动/数据收集]** 点按 **[!UICONTROL 转到Launch/数据收集]**.

1. 点按 **[!UICONTROL 新资产]** 并指定配置的名称。

1. 指定域名并点按 **[!UICONTROL 保存]** 以保存资产。

1. 点按标记属性列表中可用的配置名称。

1. 在 **[!UICONTROL 创作]** 部分，点按 **[!UICONTROL 扩展]**.

1. 点按 **[!UICONTROL 目录]** 点按 **[!UICONTROL 安装]** 对于 **[!UICONTROL Adobe Experience Manager Forms]** 扩展。 **[!UICONTROL Adobe Experience Manager Forms]** 显示在 **已安装** 选项卡。

1. 点按 **[!UICONTROL 安装]** 对于 **[!UICONTROL Adobe Analytics]** 扩展。
1. 在 **[!UICONTROL 开发报表包]**, **[!UICONTROL 暂存报表包]**&#x200B;和 **[!UICONTROL 产品报表包]** 下拉列表和点按 **[!UICONTROL 保存]** 以保存扩展。

### 配置数据元素 {#configure-data-elements}

您可以在为事件创建的规则中选择任何已配置的数据元素。 当自适应表单上发生事件时，AEM Forms会将这些数据元素发送到 [!DNL Adobe Analytics].

安装 **[!UICONTROL Adobe Experience Manager Forms]** 扩展中，您可以创建以下数据元素：

<table>
 <tbody>
  <tr>
   <td>FieldName</th>
   <td>字段标题</th>
   <td>FormInstance</th>
  </tr>
  <tr>
   <td>表单名称<br /> </td>
   <td>表单标题<br /> </td>
   <td>PageName</td>
  </tr>
  <tr>
   <td>PageURL<br /> </td>
   <td>面板标题<br /> </td>
   <td>逗留时间</td>
  </tr>
 </tbody>
</table>

请执行以下步骤以配置数据元素：

1. 在 **[!UICONTROL 创作]** 部分，点按 **[!UICONTROL 数据元素]**.

1. 点按 **[!UICONTROL 创建新数据元素]**.

1. 指定数据元素的名称。 例如， FormTitle数据元素类型的表单标题。

1. 指定 **[!UICONTROL Adobe Experience Manager Forms]** 作为扩展名。

1. 选择 **[!UICONTROL 数据元素类型]**.

1. 点按 **[!UICONTROL 保存]** 以保存数据元素。

   >[!VIDEO](https://video.tv.adobe.com/v/337472)

### 配置规则 {#configure-rules}

执行以下步骤以根据 **[!UICONTROL Adobe Experience Manager Forms]** 扩展：

1. 在 **[!UICONTROL 创作]** 部分，点按 **[!UICONTROL 规则]**.

1. 点按 **[!UICONTROL 创建新规则]**.

1. 指定规则的名称。 例如，表单提交用于记录表单提交。

1. 在 **[!UICONTROL 事件]** 部分，点按 **[!UICONTROL 添加]**.

1. 指定 **[!UICONTROL Adobe Experience Manager Forms]** 作为扩展名。

1. 选择事件类型。 的输入 **[!UICONTROL 名称]** 字段会根据选定的事件类型自动填充。

1. 点按 **[!UICONTROL 保留更改]** 以保存事件。

1. 在 **[!UICONTROL 操作]** 部分，点按 **[!UICONTROL 添加]**.

1. 指定 **[!UICONTROL Adobe Analytics]** 作为扩展名。

1. 选择 **[!UICONTROL 设置变量]** 作为操作类型。 下拉列表中的可用选项包括：

   * **[!UICONTROL 设置变量]**:使用此操作类型可定义要将选定数据元素从AEM Forms发送到的事件类型 [!DNL Adobe Analytics].

   * **[!UICONTROL 发送信标]**:使用此操作类型将数据从AEM Forms发送到 [!DNL Adobe Analytics].

   * **[!UICONTROL 清除变量]**:使用此操作类型可清除数据跟踪，以便事件在 [!DNL Adobe Analytics].

      建议的方法是使用 **[!UICONTROL 设置变量]** 操作类型以配置事件和数据元素，然后使用 **[!UICONTROL 发送信标]** 发送数据，然后使用 **[!UICONTROL 清除变量]** 以清除数据跟踪。

1. 在 **[!UICONTROL Prop]** 部分，将下拉列表中可用的报表包选项映射到使用 [配置数据元素](#configure-data-elements).

   例如，发送 **表单标题** 数据元素从AEM Forms到 [!DNL Adobe Analytics] 提交表单时：
   1. 在 **[!UICONTROL Prop]** ，为报表包中可用的表单标题选择一个属性，然后点按 ![“数据库”图标](/help/forms/using/assets/database-icon.svg) 将其映射到在中创建的表单标题 [配置数据元素](#configure-data-elements).

      ![define-props](/help/forms/using/assets/define-props.png)

   1. 点按 **[!UICONTROL 添加其他]** 向列表添加更多数据元素。

1. 在 **[!UICONTROL 事件]** 部分，从报表包中可用的选项中选择事件，然后点按 **[!UICONTROL 保留更改]**.

1. 在 **[!UICONTROL 操作]** 部分，点按+并指定 **[!UICONTROL Adobe Analytics]** 作为扩展名。

1. 选择 **[!UICONTROL 发送信标]** 作为操作类型。 在右侧窗格中，选择 **[!UICONTROL s.t()]** 将数据发送到 [!DNL Adobe Analytics] 将其视为页面查看，或 **[!UICONTROL s.tl()]** 将数据发送到 [!DNL Adobe Analytics] 并且不要将其视为页面查看。 点按 **[!UICONTROL 保留更改]**.

1. 在 **[!UICONTROL 操作]** 部分，点按+并指定 **[!UICONTROL Adobe Analytics]** 作为扩展名。

1. 选择 **[!UICONTROL 清除变量]** 作为操作类型。 点按 **[!UICONTROL 保留更改]**. 执行这些步骤后， **[!UICONTROL 操作]** 部分显示为：
   ![操作配置](/help/forms/using/assets/actions-config.png)

   自定义 **[!UICONTROL 操作]** 部分。 例如，您可以定义两个 **发送信标** 操作流程中将数据发送到的步骤 [!DNL Adobe Analytics] 并在一个步骤中将其视为页面查看，然后将数据发送到 [!DNL Adobe Analytics] ，并且不要将其视为第二步中的页面查看。

   ![操作配置](/help/forms/using/assets/actions-config-2.png)

1. 点按 **[!UICONTROL 保存]** 来保存规则。

   您可以为所有事件类型创建规则，如放弃、错误、字段访问、帮助、渲染、保存和提交。

   >[!VIDEO](https://video.tv.adobe.com/v/337425)


### 发布流程 {#publish-flow}

在创建数据元素并在规则中使用它们后，发布配置以在中收集表单数据 [!DNL Adobe Analytics].

执行以下步骤以发布配置：

1. 在 **[!UICONTROL 发布]** 部分，点按 **[!UICONTROL 发布流程]**.

1. 点按 **[!UICONTROL 添加库]** ，然后指定名称并选择库的环境。

1. 点按 **[!UICONTROL Add All Changed Resources]** 然后点按 **[!UICONTROL 保存并构建到开发环境]**.

1. 在 **[!UICONTROL 开发]** 部分，点按 ![更多选项](/help/forms/using/assets/more-options-icon.svg) 然后点按 **[!UICONTROL 批准并发布到生产环境]**.

1. 确认更改后，发布流程即会显示在 **[!UICONTROL 已发布]** 中。

![发布流程](/help/forms/using/assets/publish-flow.png)

## 2.配置AEM Forms {#configure-aem-forms}

在创建AdobeLaunch配置之前，请先创建 [使用Launch作为云解决方案的Adobe IMS配置Adobe](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/connect-aem-launch-adobe-io.html).

### 创建 Adobe Launch 配置 {#create-adobe-launch-configuration}

执行以下步骤以创建Adobe启动配置：

1. 在AEM Forms创作实例中，导航到 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL AdobeLaunch配置]**.

1. 选择要创建配置的文件夹，然后点按 **[!UICONTROL 创建]**.

1. 在 **[!UICONTROL 标题]** 字段。

1. 选择 [关联的Adobe IMS配置](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/connect-aem-launch-adobe-io.html).

1. 选择使用的公司名称 [配置Adobe Analytics](#Configure-adobe-analytics).

1. 选择在 [配置Adobe Analytics](#install-extensions).

1. 点按 **[!UICONTROL 保存并关闭]**.

1. 发布配置。

### 启用 [!DNL Adobe Analytics] 自适应表单 {#enable-analytics-adaptive-form}

使用 [!DNL Adobe Launch] 现有自适应表单中的配置：

1. 在AEM Forms创作实例中，导航到 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms和文档]**.
1. 选择自适应表单并点按 **[!UICONTROL 属性]**.
1. 在 **[!UICONTROL 基本]** 选项卡，选择 [配置容器](#create-adobe-launch-configuration) 在创建Adobe启动配置时使用。
1. 点按 **[!UICONTROL 保存并关闭]**. 自适应表单已启用 [!DNL Adobe Analytics].
1. 发布表单。

启用后 [!DNL Adobe Analytics] 对于自适应表单，您可以 [验证](https://experienceleague.adobe.com/docs/launch-learn/implementing-in-websites-with-launch/implement-solutions/analytics.html?lang=en#validate-the-page-view-beacon) 如果AEM Forms与 [!DNL Adobe Analytics]. AEM Forms与Adobe Analytics的集成已完成。 您现在可以 [在Adobe Analytics中配置和查看报表](#view-reports-adobe-analytics).

>[!NOTE]
>在这两种情况下 [旧版Analytics](/help/forms/using/configure-analytics-forms-documents.md) 和Launch Analytics功能同时启用， **启动Analytics** 将优先使用。

### 创建规则以捕获自定义事件（可选） {#capture-custom-events}

使用规则编辑器在自适应表单的特定字段上创建规则，以将自适应表单中的Analytics数据发送到 [!DNL Adobe Analytics].

在两步流程中，您可以在自适应表单中为字段定义规则。 规则调度事件。 事件的名称会映射到Launch中的自定义捕获事件Adobe。

要在自适应表单中使用规则编辑器创建规则，请执行以下操作：

1. 点按字段并选择 ![规则编辑器](/help/forms/using/assets/edit-rules-icon.svg) 打开规则编辑器页面。
1. 在 [!UICONTROL When] 部分。
1. 在 [!UICONTROL 然后] ，请选择 **[!UICONTROL 调度事件]** 从 **[!UICONTROL 选择操作]** 下拉列表。
1. 在 **[!UICONTROL 类型事件名称]** 字段。

例如，如果出生日期在特定日期之前，AEM Forms会调度 **安全性** 事件。

![分派事件](/help/forms/using/assets/security-event.png)

将事件映射到 [!DNL Adobe Analytics]:

1. [创建规则](#configure-rules).

1. 在 **[!UICONTROL 事件]** 部分，点按 **[!UICONTROL 添加]**.

1. 指定 **[!UICONTROL Adobe Experience Manager Forms]** 作为扩展名。

1. 选择 **[!UICONTROL 捕获自定义事件]** 从 **[!UICONTROL 事件类型]** 下拉列表。

1. 使用规则编辑器创建规则时，指定您在步骤4中指定的事件名称。

1. 点按 **保留更改** 和执行 [配置规则](#configure-rules).

## 3.在中配置和查看报表 [!DNL Adobe Analytics] {#view-reports-adobe-analytics}

将自适应表单配置为将事件数据发送到 [!DNL Adobe Analytics]，您可以在 [!DNL Adobe Analytics]:

1. 点按 ![选择产品](/help/forms/using/assets/select-analytics.png) 选择 **[!UICONTROL Analytics]**.

1. 点按 **[!UICONTROL 创建项目]** 选择 **[!UICONTROL 空白项目]**.

1. 从自由格式右上角的下拉列表中选择报表包名称。

1. 指定 **表单标题** 在 **[!UICONTROL 搜索维度项目]** 文本，以查看所有表单标题。

1. 将自适应表单标题拖放到 **[!UICONTROL 将区段拖放到此处（或任何其他组件）]** 框中。

1. 从 **[!UICONTROL 量度]** 部分中，将事件拖放到要跟踪的事件 **[!UICONTROL 将量度拖放到此处（或任何其他组件）]** 框中。

1. 点按 ![可视化图表](/help/forms/using/assets/visualization-icon.svg) 并将图表类型拖放到自由格式部分。 同样，您也可以向自由格式部分添加多个图表类型。

1. 点按Ctrl + S键并指定用于保存项目的名称。