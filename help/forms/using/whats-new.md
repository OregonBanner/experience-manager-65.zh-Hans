---
title: 新增功能摘要| AEM 6.5表单
seo-title: 新增功能摘要| AEM 6.5表单
description: 世界最先进的数字体验管理解决方案的最新功能和表单和文档改进。
seo-description: 世界最先进的数字体验管理解决方案的最新功能和表单和文档改进。
uuid: 179d372d-b7f6-4771-8349-fc6b7854efac
topic-tags: introduction
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 0e949429-cd5f-4301-aa72-14803cdfab00
docset: aem65
translation-type: tm+mt
source-git-commit: 726163106ddb80600eaa7cc09b1a2e9b035a223e

---


# 新增功能摘要| AEM 6.5表单{#new-features-summary-aem-forms}

## 事务报表 {#transaction-reports}

事务报表允许您捕获和跟踪提交的表单、已处理的文档和呈现的文档数。 跟踪这些交易的目标是对产品使用情况做出明智决策，并重新平衡硬件和软件投资。 一些交易示例包括：

* 提交自适应表单、HTML5表单或表单集
* 交互式通信的打印版或Web版的再现
* 将文档从一种文件格式转换为另一种文件格式

有关配置和使用事务报表的信息，请参阅事务 [报表概述](../../forms/using/transaction-reports-overview.md)。

![示例事务报表](assets/surface_transaction_reporting.png)

## 交互式通信 {#interactive-communications}

**定义数据显示模式**

交互通信作者现在可以为字 [段、变量和表单数据模型元素](create-interactive-communication.md#datadisplaypatterns) 定义数据显示模式。 例如，日期、货币或电话格式。

**使用新的图表类型**

您现在可以向 [Interactive Communications添加具有多个系列的象限图](../../forms/using/chart-component-interactive-communications.md) 和图表。

**对表中的列进行排序**

您现在可 [以对交互通信中的表列](../../forms/using/create-interactive-communication.md#sortcolumns) 进行排序。 可以用静态文本或数据模型对象绑定表列并对其进行排序。

**在Web渠道中使用新组件**

您现在可以将“按钮”和“分隔符”组件添加到Web渠道。 有关详细信息，请参 [阅将按钮组件添加到Web渠道中的Web](../../forms/using/create-interactive-communication.md#add-button-component-to-the-web-channel) , [以及Web渠道中的Separator组件](../../forms/using/create-interactive-communication.md#separatorcomponent)。

**用于调整组件大小的布局模式**

您现在可以切换到布 [局模式](../../forms/using/resize-using-layout-mode.md) ，以使用WYSIWYG界面调整Web渠道中的组件大小。

**可用性改进**

交互通信作者现在可以在创建通信时利用各种易于使用的操作。 运营列表包括：

* [在印刷和Web渠道中执行撤消——重做操作](../../forms/using/create-interactive-communication.md#undoredoactions)
* [使用@符号在文档片段中添加变量](../../forms/using/texts-interactive-communications.md#searchvariables)
* [使用@符号在文档片段中添加数据模型元素](../../forms/using/texts-interactive-communications.md#searchdatamodelproperties)
* [删除Web渠道或将其添加到现有交互通信](../../forms/using/create-interactive-communication.md#edit-interactive-communication-properties)
* [使用拖放操作将数据源元素与字段和变量绑定](../../forms/using/create-interactive-communication.md#binddatasourceelements)
* [在创作交互式通信时高亮显示未绑定的字段和变量](../../forms/using/create-interactive-communication.md#distinguishunboundfields)
* [对Web渠道中继承的组件执行其他操作，如复制、组或更多](../../forms/using/create-interactive-communication.md#componenttoolbar)

**同步过程的改进**

在使用“打印渠道”自动生成的Web渠道布局中，有几项改进。

![交互通信图表](assets/interactive-communication-charts.png)

## 自适应表单 {#adaptive-forms}

### 在自适应表单中使用Adobe Sign基于云的数字签名 {#use-adobe-sign-s-cloud-based-digital-signatures-in-adaptive-forms}

[基于云的数字签名](https://helpx.adobe.com/sign/kb/digital-certificate-providers.html) ，或远程签名，是跨桌面、移动设备和Web工作的新一代数字签名。 并达到签署方身份验证的最高级别的合规性和保证。 您现在可以 [使用基于云的数字签名](../../forms/using/working-with-adobe-sign.md) ，对自适应表单进行签名。

#### 在AEM Sites单页应用程序中嵌入自适应表单或交互式通信 {#embed-an-adaptive-form-or-interactive-communcation-in-aem-sites-single-page-applications}

AEM Forms允许您将自 [适应表单](../../forms/using/embed-adaptive-form-aem-sites-spa.md) 或交互式通信无缝嵌入AEM Sites单页应用程序(SPA)中。 嵌入式自适应表单和交互式通信功能齐全，用户无需离开页面即可填写和提交表单。 它帮助用户保持在网页上其他元素的上下文中，并同时与自适应表单或交互式通信交互。

#### 对自适应表单表列进行排序 {#sort-columns-of-adaptive-form-tables}

您可以 [按升序或降序对自适应表单表的任何列](../../forms/using/adaptive-forms-tables.md#sortcolumnstable) 进行排序。 可以对包含静态文本、数据模型对象属性或静态文本和数据模型对象属性的组合的表列应用排序。

#### 将自适应表单模板的可用性限制为特定路径 {#restrict-the-availability-of-adaptive-forms-templates-to-specific-paths}

自适应表单增加了对cq:allowedPaths属性的支持。 该属性将自 [适应表单模板的可用性限制为特定路径](../../forms/using/creating-adaptive-form.md#main-pars-text)。

#### 将复选框动态添加到自适应表单 {#add-check-boxes-to-the-adaptive-form-dynamically}

您现在可以定义规则， [以根据自定义函数、表单对象或对象属性](../../forms/using/rule-editor.md#setpropertyrule) ，动态地向自适应表单添加复选框。

## AEM 工作流 {#aem-workflows}

### 在AEM工作流中使用变量 {#use-variables-in-aem-workflows}

变量使工作流步骤能够在运行时跨工作流步骤保留和传递元数据。 您可以创建不同类型的变量来存储不同类型的数据。 例如，整数、字符串、文档或表单数据模型实例。 通常，当您需要根据变量所包含的值做出决策或存储以后在流程中需要的信息时，您会使用变量或变量集合。

变量是MetaDataMap界 [面的扩展](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html) ，该界面在早期版本中可用。 它有助于节省开发用于检索和更新元数据值的自定义ECMAScript代码所花费的时间。 您可以继续使用MetaDataMap界面和ECMAScript代码处理元数据。 与MetaDataMap和ECMAScript相比，使用变量的一些好处是：

* 在整个工作流中动态存储、更新和使用存储在变量中的值，无需依赖自定义代码
* 检索值并直接更新到已提交表单的表单数据模型和数据文件(XML/JSON)
* 将完整的文档存储在变量中以执行文档处理

“转到”步骤或“拆分”步骤以及所有AEM Forms工作流步骤都支持变量。 您可以使用MetaDataMap界面访问工作流步骤中不支持变量的变量。 有关详细信息，请参 [阅AEM工作流中的变量](../../forms/using/variable-in-aem-workflows.md)。

![在工作流中为设置变量](assets/variable.png)

#### 使用具有不同自适应表单的工作流 {#use-a-workflow-with-different-adaptive-forms}

您可以 [为运行时上以表单为中心的任务的分配工作流](../../forms/using/aem-forms-workflow-step-reference.md#assign-task-step) 、文档记录步骤指定自适应表单。 它允许工作流使用不同的自适应表单。 在设计工作流时，您可以决定选择自适应表单的方法。 自适应表单可以位于绝对路径中，作为有效负荷提交到工作流中，或者位于使用变量计算的路径中。

#### 使用以表单为中心的工作流程步骤的增强记录功能 {#use-enhanced-logging-capabilities-of-forms-centric-workflow-steps}

以表单为中心的工作流程步骤的记录功能已标准化。 现在，所有以表单为中心的工作流程步骤都可以生成类似的标准化日志。 它有助于提高调试速度。

## 数据集成 {#data-integration}

您现在可以：

* [根据约束列表](../../forms/using/work-with-form-data-model.md#automated-validation-of-input-data) ，验证输入数据。 它有助于确保仅向数据源提交有效数据。
* [覆盖在WSDL](../../forms/using/configure-data-sources.md#configure-soap-web-services) （Web服务描述语言）文件中定义的默认端点。

* [覆盖Swagger定](../../forms/using/configure-data-sources.md#configure-restful-web-services) 义文件中定义的默认方案 [](../../forms/using/configure-data-sources.md#configure-restful-web-services) 、主机和基本路径。

## 平台和安全更新 {#platform-and-security-updates}

### 主要平台更新 {#major-platform-updates}

可以使用支持的操作系统、应用程序服务器、数据库、数据库驱动程序、JDK、LDAP服务器和电子邮件服务器的任意组合来设置AEM Forms。 以下是受支持平台中的主 [要更改](../../forms/using/aem-forms-jee-supported-platforms.md):

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
     <li>Oracle Weblogic</li>
    </ul> </td>
  </tr>
  <tr>
   <td>数据库</td>
   <td>
    <ul>
     <li>IBM DB2 <br /> </li>
     <li>Oracle RAC</li>
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
     <li>Microsoft Sharepoint 2013的连接器</li>
     <li>EMC Documentum 7.0连接器</li>
    </ul> </td>
  </tr>
  <tr>
   <td>AEM Forms app<br /> </td>
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

*有关迁移到其他平台的信息，请与Adobe支持部门联系

#### 新的基于HTML5的UI {#new-html-based-uis}

根据Adobe Flash Player的计划EOL以及将基于Flash的内容迁移到开放标准的总体方向，AEM 6.5表单已使用基于HTML5的UI取代了JEE管理控制台上AEM表单的基于Flash的UI、进程管理、Reader扩展和类别管理UI。

#### 安全性改进 {#security-improvements}

* JEE管理控制台UI上的AEM 6.5表单现在基于Apache Struts 2.5。
* AEM 6.5 Forms现在将jQuery用于3.2.1和jQuery UI 1.12.1。请参 [阅升级文档](/help/forms/home.md) ，了解更改的影响。

#### 辅助功能改进 {#accessibility-improvements}

AEM 6.5 Forms改进了AEM Forms Workspace的辅助功能。
