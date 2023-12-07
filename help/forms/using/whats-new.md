---
title: 新增功能摘要 | AEM 6.5 Forms
description: 世界上最高级的数字体验管理解决方案的表单和文档的最新功能和改进。
topic-tags: introduction
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
exl-id: 47b9de1f-b16a-424c-b8b4-e9d7b3dcca86
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '1241'
ht-degree: 1%

---

# 新增功能摘要 | AEM 6.5 Forms{#new-features-summary-aem-forms}

## 交易报告 {#transaction-reports}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/forms-overview/latest-innovations.html) |
| AEM 6.5 | 本文 |


通过事务报表，您可以捕获和跟踪已提交的表单、已处理的文档和已渲染文档的数量。 跟踪这些交易背后的目标是针对产品使用情况做出明智的决策，并重新平衡硬件和软件投资。 事务的一些示例包括：

* 提交自适应表单、HTML5表单或表单集
* 交互式通信的打印或Web版本的演绎版
* 文档从一种文件格式转换为另一种文件格式

有关配置和使用事务报表的信息，请参阅 [交易报表概述](../../forms/using/transaction-reports-overview.md).

![示例交易报告](assets/surface_transaction_reporting.png)

## 交互式通信 {#interactive-communications}

**定义数据显示模式**

交互式通信作者现在可以定义 [数据显示模式](create-interactive-communication.md#datadisplaypatterns) 用于字段、变量和表单数据模型元素。 例如，日期、货币或电话格式。

**使用新类型的图表**

您现在可以添加 [象限图表和带多个系列的图表](../../forms/using/chart-component-interactive-communications.md) 更改为交互式通信。

**对表中的列进行排序**

您现在可以 [对表的列进行排序](../../forms/using/create-interactive-communication.md#sortcolumns) 在交互式通信中。 您可以使用静态文本或数据模型对象来绑定和排序表列。

**在Web渠道中使用新组件**

您现在可以将按钮和分隔符组件添加到Web渠道。 有关更多信息，请参阅 [将按钮组件添加到Web渠道](../../forms/using/create-interactive-communication.md#add-button-component-to-the-web-channel) 和 [Web渠道中的分隔符组件](../../forms/using/create-interactive-communication.md#separatorcomponent).

**用于调整组件大小的布局模式**

您现在可以切换到 [布局模式](../../forms/using/resize-using-layout-mode.md) 使用WYSIWYG界面在Web渠道中调整组件大小。

**可用性改进**

交互式通信作者现在可以在创建通信项时利用各种易于使用的操作。 操作列表包括：

* [在打印和Web渠道中执行撤消 — 重做操作](../../forms/using/create-interactive-communication.md#undoredoactions)
* [使用@符号在文档片段中添加变量](../../forms/using/texts-interactive-communications.md#searchvariables)
* [使用@符号在文档片段中添加数据模型元素](../../forms/using/texts-interactive-communications.md#searchdatamodelproperties)
* [删除或向现有交互式通信添加Web渠道](../../forms/using/create-interactive-communication.md#edit-interactive-communication-properties)
* [使用拖放操作将数据源元素与字段和变量绑定](../../forms/using/create-interactive-communication.md#binddatasourceelements)
* [创作交互式通信时突出显示未绑定的字段和变量](../../forms/using/create-interactive-communication.md#distinguishunboundfields)
* [在Web渠道中对继承的组件执行其他操作，如复制、分组等](../../forms/using/create-interactive-communication.md#componenttoolbar)

**同步过程的改进**

在使用打印渠道自动生成的Web渠道布局中有几项改进。

![交互式通信图表](assets/interactive-communication-charts.png)

## 自适应表单 {#adaptive-forms}

### 在自适应Forms中使用Adobe Sign基于云的数字签名 {#use-adobe-sign-s-cloud-based-digital-signatures-in-adaptive-forms}

[基于云的数字签名](https://helpx.adobe.com/sign/kb/digital-certificate-providers.html) 或远程签名是新一代的数字签名，可在桌面、移动设备和Web上使用，并且满足签名者身份验证的最高合规性和保证级别。 您现在可以 [签署自适应表单](../../forms/using/working-with-adobe-sign.md) 使用基于云的数字签名。

#### 在AEM Sites单页应用程序中嵌入自适应表单或交互式通信 {#embed-an-adaptive-form-or-interactive-communcation-in-aem-sites-single-page-applications}

AEM Forms允许您 [无缝嵌入自适应表单](../../forms/using/embed-adaptive-form-aem-sites-spa.md) 或AEM Sites单页应用程序(SPA)中的交互式通信。 嵌入式自适应表单和交互式通信功能完善，用户无需离开页面即可填写并提交表单。 它有助于用户停留在网页上其他元素的上下文中，同时与自适应表单或交互式通信交互。

#### 对自适应表单表的列进行排序 {#sort-columns-of-adaptive-form-tables}

您可以 [对自适应表单表的任意列进行排序](../../forms/using/adaptive-forms-tables.md#sortcolumnstable) 按升序或降序排列。 您可以将排序应用于具有静态文本、数据模型对象属性或静态文本和数据模型对象属性组合的表列。

#### 限制自适应Forms模板仅对特定路径可用 {#restrict-the-availability-of-adaptive-forms-templates-to-specific-paths}

自适应表单添加了对cq：allowedPaths属性的支持。 属性 [限制自适应Forms模板在特定路径上的可用性](creating-adaptive-form.md#adaptive-form-templates).

#### 将复选框动态添加到自适应表单 {#add-check-boxes-to-the-adaptive-form-dynamically}

您现在可以将规则定义为 [将复选框动态添加到自适应表单](../../forms/using/rule-editor.md#setpropertyrule) 基于自定义函数、表单对象或对象属性。

## AEM 工作流 {#aem-workflows}

### 在AEM工作流中使用变量 {#use-variables-in-aem-workflows}

通过变量，工作流步骤可在运行时跨工作流步骤保留和传递元数据。 您可以创建不同类型的变量以存储不同类型的数据。 例如，整数、字符串、文档或表单数据模型实例。 通常，当您需要根据其持有的值做出决策时，或者需要存储稍后在流程中需要的信息时，可以使用变量或变量集合。

变量是的扩展 [元数据映射](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html) 之前版本中提供的界面。 它有助于节省开发用于检索和更新元数据值的自定义ECMAScript代码所花费的时间。 继续使用MetaDataMap接口和ECMAScript代码处理元数据。 与MetaDataMap和ECMAScript相比，使用变量具有以下优点：

* 在整个工作流中动态存储、更新和使用变量中存储的值，而无需依赖自定义代码
* 直接检索值并更新已提交表单的表单数据模型和数据文件(XML/JSON )
* 将完整的文档存储在变量中以执行文档处理

转到步骤、OR拆分步骤以及所有AEM Forms工作流步骤都支持变量。 您可以使用MetaDataMap界面访问工作流步骤中不支持变量的变量。 有关更多信息，请参阅 [AEM Workflow中的变量](../../forms/using/variable-in-aem-workflows.md).

![在工作流中设置变量](assets/variable.png)

#### 将工作流用于其他自适应Forms  {#use-a-workflow-with-different-adaptive-forms}

您可以 [为分配任务指定自适应表单](../../forms/using/aem-forms-workflow-step-reference.md#assign-task-step) 以及运行时以表单为中心的工作流的记录文档步骤。 它允许工作流使用其他自适应Forms。 您可以在设计工作流时决定选择自适应表单的方法。 自适应表单可以位于绝对路径下、作为有效负荷提交到工作流中，或者位于使用变量计算的路径下。

#### 使用以表单为中心的工作流步骤的增强日志记录功能 {#use-enhanced-logging-capabilities-of-forms-centric-workflow-steps}

以表单为中心的工作流步骤的日志记录功能实现了标准化。 现在，所有以表单为中心的工作流步骤都会生成类似的标准化日志。 这有助于提高调试速度。

## 数据集成 {#data-integration}

您现在可以：

* [验证输入数据](../../forms/using/work-with-form-data-model.md#automated-validation-of-input-data) 基于约束列表。 它有助于确保只向数据源提交有效数据。
* [覆盖默认端点](../../forms/using/configure-data-sources.md#configure-soap-web-services) 在WSDL（Web服务描述语言）文件中定义。

* [覆盖默认值](../../forms/using/configure-data-sources.md#configure-restful-web-services) [方案、主机和基本路径](../../forms/using/configure-data-sources.md#configure-restful-web-services) 在Swagger定义文件中定义。

## 平台和安全更新 {#platform-and-security-updates}

### 主要平台更新 {#major-platform-updates}

AEM Forms可以使用受支持的操作系统、应用程序服务器、数据库、数据库驱动程序、JDK、LDAP服务器和电子邮件服务器的任意组合进行设置。 以下为中的主要更改 [支持的平台](../../forms/using/aem-forms-jee-supported-platforms.md)：

<table>
 <tbody>
  <tr>
   <td>组件</td>
   <td>已移除支持</td>
  </tr>
  <tr>
   <td>操作系统</td>
   <td>
    <ul>
     <li>Microsoft Windows Server 2012 R2</li>
     <li>IBM AIX*</li>
     <li>Sun Solaris*</li>
    </ul> </td>
  </tr>
  <tr>
   <td>应用程序服务器<br /> </td>
   <td>
    <ul>
    <li>WebSphere Liberty配置文件</li>
    <li>oracleWebLogic</li>
    </ul> </td>
  </tr>
  <tr>
   <td>数据库</td>
   <td>
    <ul>
     <li>IBM DB2 <br /> </li>
     <li>ORACLERAC</li>
    </ul> </td>
  </tr>
  <tr>
   <td>LDAP服务器</td>
   <td>
    <ul>
     <li>Microsoft Active Directory 2012</li>
     <li>Novell eDirectory 8.8.7 </li>
     <li>IBM Lotus Domino 8.5.0 </li>
    </ul> </td>
  </tr>
  <tr>
   <td>电子邮件服务器</td>
   <td>
    <ul>
     <li>IBM Lotus Domino 8.5.0 </li>
    </ul> </td>
  </tr>
  <tr>
   <td>连接器</td>
   <td>
    <ul>
     <li>Microsoft Sharepoint 2013连接器</li>
     <li>EMC Documentum 7.0连接器</li>
    </ul> </td>
  </tr>
  <tr>
   <td>AEM Forms应用程序<br /> </td>
   <td>
    <ul>
     <li>Windows 8.1支持</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Java </td>
   <td>
    <ul>
     <li>Java 11</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

&#42; 有关迁移到其他平台的信息，请与Adobe支持部门联系

#### 新的基于HTML5的UI {#new-html-based-uis}

根据AdobeFlash Player的计划生命周期结束以及基于Flash的内容迁移到开放标准的总体方向，AEM 6.5 Forms已在JEE管理控制台上取代了AEM Forms的基于Flash的Health Monitor、Process Management、Reader扩展和类别管理UI，改为基于HTML5的UI。

#### 安全性改进 {#security-improvements}

* JEE管理控制台上的AEM 6.5 Forms UI现在基于Apache Struts 2.5。
* AEM 6.5 Forms现在使用jQuery到3.2.1和jQuery UI 1.12.1。看， [升级文档](/help/forms/home.md) 以了解更改的影响。

#### 辅助功能改进 {#accessibility-improvements}

AEM 6.5 Forms改进了AEM Forms Workspace的可访问性。
