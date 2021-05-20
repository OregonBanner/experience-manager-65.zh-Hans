---
title: 新增功能摘要 | AEM 6.5 Forms
seo-title: 新增功能摘要 | AEM 6.5 Forms
description: 世界上最先进的数字体验管理解决方案的最新功能和表单和文档改进。
seo-description: 世界上最先进的数字体验管理解决方案的最新功能和表单和文档改进。
uuid: 179d372d-b7f6-4771-8349-fc6b7854efac
topic-tags: introduction
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 0e949429-cd5f-4301-aa72-14803cdfab00
docset: aem65
exl-id: 47b9de1f-b16a-424c-b8b4-e9d7b3dcca86
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1245'
ht-degree: 0%

---

# 新增功能摘要 | AEM 6.5 Forms{#new-features-summary-aem-forms}

## 事务报表{#transaction-reports}

利用交易报表，可捕获和跟踪已提交的表单、已处理文档和已渲染文档的数量。 跟踪这些交易的目标是对产品使用情况做出明智决策，并重新平衡对硬件和软件的投资。 一些交易示例包括：

* 提交自适应表单、HTML5表单或表单集
* 交互式通信的打印版或Web版的再现
* 将文档从一种文件格式转换为另一种文件格式

有关配置和使用事务报表的信息，请参阅[事务报表概述](../../forms/using/transaction-reports-overview.md)。

![交易报表示例](assets/surface_transaction_reporting.png)

## 交互式通信 {#interactive-communications}

**定义数据显示模式**

交互式通信作者现在可以为字段、变量和表单数据模型元素定义[数据显示模式](create-interactive-communication.md#datadisplaypatterns)。 例如，日期、货币或电话格式。

**使用新类型的图表**

现在，您可以向交互式通信添加具有多个系列](../../forms/using/chart-component-interactive-communications.md)的[象限图表和图表。

**对表中的列进行排序**

现在，您可以在交互式通信中对表](../../forms/using/create-interactive-communication.md#sortcolumns)的列进行[排序。 可以使用静态文本或数据模型对象绑定表列并对其进行排序。

**在Web渠道中使用新组件**

您现在可以向Web渠道中添加按钮和分隔符组件。 有关更多信息，请参阅[将按钮组件添加到Web渠道](../../forms/using/create-interactive-communication.md#add-button-component-to-the-web-channel)和[Web渠道中的分隔符组件](../../forms/using/create-interactive-communication.md#separatorcomponent)。

**用于调整组件大小的布局模式**

您现在可以切换到[布局模式](../../forms/using/resize-using-layout-mode.md)，以使用WYSIWYG界面调整Web渠道中的组件大小。

**可用性改进**

交互式通信作者现在可以在创建通信时利用各种易于使用的操作。 操作列表包括：

* [在打印和Web渠道中执行撤消重做操作](../../forms/using/create-interactive-communication.md#undoredoactions)
* [使用@符号在文档片段中添加变量](../../forms/using/texts-interactive-communications.md#searchvariables)
* [使用@符号在文档片段中添加数据模型元素](../../forms/using/texts-interactive-communications.md#searchdatamodelproperties)
* [删除或添加Web渠道到现有交互式通信](../../forms/using/create-interactive-communication.md#edit-interactive-communication-properties)
* [使用拖放操作将数据源元素与字段和变量绑定](../../forms/using/create-interactive-communication.md#binddatasourceelements)
* [在创作交互式通信时突出显示未绑定的字段和变量](../../forms/using/create-interactive-communication.md#distinguishunboundfields)
* [对Web渠道中的继承组件执行其他操作，例如复制、分组等](../../forms/using/create-interactive-communication.md#componenttoolbar)

**同步过程的改进**

使用“打印”渠道自动生成的Web渠道布局有一些改进。

![交互式通信图表](assets/interactive-communication-charts.png)

## 自适应表单 {#adaptive-forms}

### 在自适应Forms {#use-adobe-sign-s-cloud-based-digital-signatures-in-adaptive-forms}中使用Adobe Sign基于云的数字签名

[基于云的数字签](https://helpx.adobe.com/sign/kb/digital-certificate-providers.html) 名或远程签名是新一代的数字签名，可跨桌面、移动设备和Web使用，并满足签名者身份验证的最高级别合规性和保证。您现在可以使用基于云的数字签名对自适应表单](../../forms/using/working-with-adobe-sign.md)进行签名。[

#### 在AEM Sites单页应用程序中嵌入自适应表单或交互式通信{#embed-an-adaptive-form-or-interactive-communcation-in-aem-sites-single-page-applications}

AEM Forms允许您在AEM Sites单页应用程序(SPA)中无缝嵌入自适应表单](../../forms/using/embed-adaptive-form-aem-sites-spa.md)或交互式通信。 [嵌入式自适应表单和交互式通信功能完全，用户无需离开页面即可填写和提交表单。 它有助于用户停留在网页上其他元素的上下文中，并同时与自适应表单或交互式通信进行交互。

#### 对自适应表单表格的列{#sort-columns-of-adaptive-form-tables}排序

您可以[按升序或降序对自适应表单表](../../forms/using/adaptive-forms-tables.md#sortcolumnstable)的任何列进行排序。 您可以对具有静态文本、数据模型对象属性或静态文本和数据模型对象属性的组合的表列应用排序。

#### 将自适应Forms模板的可用性限制为特定路径{#restrict-the-availability-of-adaptive-forms-templates-to-specific-paths}

自适应表单增加了对cq:allowedPaths属性的支持。 属性[将自适应Forms模板的可用性限制为特定路径](creating-adaptive-form.md#adaptive-form-templates)。

#### 向自适应表单中动态添加复选框{#add-check-boxes-to-the-adaptive-form-dynamically}

您现在可以根据自定义函数、表单对象或对象属性将规则定义为[动态](../../forms/using/rule-editor.md#setpropertyrule)将复选框添加到自适应表单。

## AEM 工作流 {#aem-workflows}

### 在AEM工作流{#use-variables-in-aem-workflows}中使用变量

变量允许工作流步骤在运行时跨工作流步骤保存和传递元数据。 您可以创建不同类型的变量以存储不同类型的数据。 例如，整数、字符串、文档或表单数据模型实例。 通常，当您需要根据变量所包含的值做出决策或存储流程中稍后需要的信息时，会使用变量或变量集合。

变量是[MetaDataMap](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html)界面的扩展，在以前的版本中可用。 它有助于节省开发用于检索和更新元数据值的自定义ECMAScript代码所花费的时间。 您可以继续使用MetaDataMap接口和ECMAScript代码来处理元数据。 与MetaDataMap和ECMAScript相比，使用变量的一些好处包括：

* 在整个工作流中动态存储、更新和使用存储在变量中的值，而无需依赖自定义代码
* 直接检索值并将其更新到已提交表单的表单数据模型和数据文件(XML/JSON)中
* 将完整文档存储在变量中以执行文档处理

“转到”步骤或“拆分”步骤以及所有AEM Forms工作流步骤都支持变量。 您可以使用MetaDataMap界面访问工作流步骤中对变量没有本机支持的变量。 有关更多信息，请参阅AEM Workflows](../../forms/using/variable-in-aem-workflows.md)中的[变量。

![在工作流中为设置变量](assets/variable.png)

#### 使用具有不同自适应Forms {#use-a-workflow-with-different-adaptive-forms}的工作流

您可以在运行时为分配任务](../../forms/using/aem-forms-workflow-step-reference.md#assign-task-step)指定自适应表单，并记录以表单为中心的工作流的记录步骤。 [它允许工作流使用不同的自适应Forms。 您可以在设计工作流时确定选择自适应表单的方法。 自适应表单可以位于绝对路径中，作为有效负载提交到工作流，或位于使用变量计算的路径中。

#### 使用以表单为中心的工作流步骤的增强日志记录功能{#use-enhanced-logging-capabilities-of-forms-centric-workflow-steps}

以表单为中心的工作流步骤的日志记录功能已进行标准化。 现在，所有以表单为中心的工作流步骤都会生成类似的标准化日志。 这有助于提高调试速度。

## 数据集成{#data-integration}

您现在可以：

* [验证基](../../forms/using/work-with-form-data-model.md#automated-validation-of-input-data) 于约束列表的输入数据库。这有助于确保仅将有效数据提交到数据源。
* [覆盖在](../../forms/using/configure-data-sources.md#configure-soap-web-services) WSDL（Web服务描述语言）文件中定义的默认端点。

* [覆盖](../../forms/using/configure-data-sources.md#configure-restful-web-services) [Swagger定义文件中定义的](../../forms/using/configure-data-sources.md#configure-restful-web-services) 默认方案、主机和基本路径。

## 平台和安全更新{#platform-and-security-updates}

### 主要平台更新{#major-platform-updates}

AEM Forms可以使用支持的操作系统、应用程序服务器、数据库、数据库驱动程序、 JDK、LDAP服务器和电子邮件服务器的任意组合进行设置。 以下是[受支持平台](../../forms/using/aem-forms-jee-supported-platforms.md)中的主要更改：

<table>
 <tbody>
  <tr>
   <td>组件</td>
   <td>已删除支持</td>
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
    <li>OracleWebLogic</li>
    </ul> </td>
  </tr>
  <tr>
   <td>数据库</td>
   <td>
    <ul>
     <li>IBM DB2 <br /> </li>
     <li>OracleRAC</li>
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
     <li>适用于Microsoft Sharepoint 2013的连接器</li>
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

*联系Adobe支持人员以获取有关迁移到其他平台的信息

#### 新的基于HTML5的UI {#new-html-based-uis}

与计划中的AdobeFlash Player生命周期终止以及将基于Flash的内容迁移到开放标准的总体方向一致，AEM 6.5 Forms已将JEE管理控制台上基于Flash的运行状况监视器、流程管理、Reader扩展和AEM Forms类别管理UI中的基于的UI替换为基于HTML5的UI。

#### 安全改进{#security-improvements}

* AEM 6.5 Forms on JEE管理控制台UI现在基于Apache Struts 2.5。
* AEM 6.5 Forms现在将jQuery用于3.2.1和jQuery UI 1.12.1。有关更改的影响，请参阅[升级文档](/help/forms/home.md)。

#### 辅助功能改进{#accessibility-improvements}

AEM 6.5 Forms改进了AEM Forms工作区的辅助功能。
