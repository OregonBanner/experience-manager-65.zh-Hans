---
title: HTML5表单的架构
seo-title: HTML5表单的架构
description: HTML5表单部署为嵌入的AEM实例中的包，并使用REST风格的Apache Sling体系结构将功能显示为REST端点，而不是HTTP/S。
seo-description: HTML5表单部署为嵌入的AEM实例中的包，并使用REST风格的Apache Sling体系结构将功能显示为REST端点，而不是HTTP/S。
uuid: 7f515cea-1447-4fc7-82ba-17f2e3f9f80c
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: a644978e-5736-4771-918a-dfefe350a4a1
docset: aem65
translation-type: tm+mt
source-git-commit: 84dd0d551431169239f63cff62a015e15f998e7d
workflow-type: tm+mt
source-wordcount: '2043'
ht-degree: 0%

---


# HTML5表单的架构{#architecture-of-html-forms}

## 架构 {#architecture}

HTML5表单功能部署为嵌入的AEM实例中的包，并使用RESTful [Apache Sling Architecture](https://sling.apache.org/)在HTTP/S上显示为REST端点。

![02-aem-forms-architecture_large](assets/02-aem-forms-architecture_large.jpg)

### 使用Sling Framework {#using-sling-framework}

[Apache ](https://sling.apache.org/) Sling以资源为中心。它使用请求URL首先解析资源。 每个资源都有&#x200B;**sling:resourceType**（或&#x200B;**sling:resourceSuperType**）属性。 根据此属性、请求方法和请求URL的属性，选择sling脚本来处理请求。 此sling脚本可以是JSP或servlet。 对于HTML5表单，**用户档案**&#x200B;节点充当sling资源，**用户档案渲染器**&#x200B;充当sling脚本，处理用特定用户档案渲染移动表单的请求。 **用户档案渲染器**&#x200B;是从请求中读取参数并调用FormsOSGi服务的JSP。

有关REST端点和支持的请求参数的详细信息，请参阅[渲染表单模板](/help/forms/using/rendering-form-template.md)。

当用户从客户端设备（如iOS或Android浏览器）发出请求时，Sling首先会根据请求URL解析用户档案节点。 从此用户档案节点中，它读取&#x200B;**sling:resourceSuperType**&#x200B;和&#x200B;**sling:resourceType**，以确定可处理此表单渲染请求的所有可用脚本。 然后，它使用Sling请求选择器和请求方法来标识最适合处理此请求的脚本。 请求到达用户档案渲染器JSP后，JSP将调用FormsOSGi服务。

有关sling脚本解析的详细信息，请参阅[AEM Sling备忘单](https://docs.adobe.com/content/docs/en/cq/current/developing/sling_cheatsheet.html)或[Apache Sling Url分解](https://sling.apache.org/site/url-decomposition.html)。

#### 典型表单处理调用流{#typical-form-processing-call-flow}

HTML5表单缓存处理（再现或提交）表单时所需的所有中间对象。 它不会缓存依赖于数据的对象，因为此类对象可能会更改。

Mobile Form维护两个不同级别的缓存，PreRender缓存和Render Cache。 preRender缓存包含已解析模板的所有片段和图像，而Render缓存包含已渲染的内容（如HTML）。

![HTML5表单工作流程](assets/cacheworkflow.png)

HTML5表单工作流程

HTML5表单不缓存缺少片段和图像引用的模板。 如果HTML5表单所用时间超过正常时间，请检查服务器日志中是否缺少引用和警告。 另外，请确保未达到对象的最大大小。

FormsOSGi服务通过两个步骤处理请求：

* **布局和初始表单状态生成**:FormsOSGi渲染服务调用Forms缓存组件以确定表单是否已缓存且未失效。如果表单已缓存且有效，则它将从缓存中提供生成的HTML。 如果表单失效，FormsOSGi渲染服务将以XML格式生成初始表单布局和表单状态。 此XML由FormsOSGi服务转换为HTML布局和初始JSON表单状态，然后缓存以备后续请求。
* **预填充的Forms**:在呈现时，如果用户请求具有预填充数据的表单，FormsOSGi呈现服务将调用Forms服务容器，并生成具有合并数据的新表单状态。但是，由于布局已在上述步骤中生成，因此此调用比第一次调用更快。 此调用仅执行数据合并并对数据运行脚本。

如果表单中或表单中使用的任何资产存在任何更新，表单缓存组件会检测到它，并且该特定表单的缓存将失效。 FormsOSGi服务完成处理后，用户档案渲染器jsp将JavaScript库引用和样式添加到此表单并返回对客户端的响应。 此处可将[Apache](https://httpd.apache.org/)等典型Web服务器与HTML压缩结合使用。 Web服务器将显着减小响应大小、网络流量以及在服务器和客户端计算机之间传输数据所需的时间。

当用户提交表单时，浏览器将JSON格式的表单状态发送给[提交服务代理](../../forms/using/service-proxy.md);然后，提交服务代理使用JSON数据生成数据XML，并提交该数据XML以提交端点。

## 组件 {#components}

您需要AEM Forms加载项包来启用HTML5表单。 有关安装AEM Forms加载项包的信息，请参阅[安装和配置AEM Forms](../../forms/using/installing-configuring-aem-forms-osgi.md)。

### OSGi组件(adobe-lc-forms-core.jar){#osgi-components-adobe-lc-forms-core-jar}

**AdobeXFAForms渲染器(com.adobe.livecycle.adobe-lc-forms-core)** 是从Felix管理控制台的Bundle视图(https://[ host]:[port]/system/console/bundles)查看HTML5表单OSGi捆绑的显示名称。

此组件包含用于渲染、缓存管理和配置设置的OSGi组件。

#### FormsOSGi服务{#forms-osgi-service}

此OSGi服务包含将XDP渲染为HTML的逻辑，并处理表单的提交以生成数据XML。 此服务使用Forms服务容器。 Forms服务容器内部调用执行该处理的本机组件`XMLFormService.exe`。

如果收到渲染请求，此组件将调用Forms服务容器生成布局和状态信息，然后进一步处理这些信息以生成HTML和JSON表单DOM状态。

此组件还负责从提交的表单状态JSON生成数据XML。

#### 缓存组件{#cache-component}

HTML5表单使用缓存优化吞吐量和响应时间。 您可以配置缓存服务的级别，以微调性能和空间利用率之间的平衡。

<table>
 <tbody>
  <tr>
   <th>缓存策略</th>
   <th>描述</th>
  </tr>
  <tr>
   <td>无</td>
   <td>不缓存工件<br /> </td>
  </tr>
  <tr>
   <td>保守派</td>
   <td>仅缓存在表单呈现之前生成的中间伪像（如包含内联片段和图像的模板）</td>
  </tr>
  <tr>
   <td>攻击性</td>
   <td>缓存已呈现的HTML内容<br />缓存在“保守”级别中缓存的所有对象。<br /> <strong>注意</strong>:此策略可获得最佳性能，但会消耗更多内存来存储缓存的伪像。</td>
  </tr>
 </tbody>
</table>

HTML5表单使用LRU策略执行内存中缓存。 如果缓存策略设置为“无”缓存，则不会创建现有缓存数据（如果有），则清除现有缓存数据。 除缓存策略外，您还可以配置内存中缓存的总大小，这有助于达到缓存大小的最大限制，如果超出此限制，将使用LRU模式释放缓存资源。

>[!NOTE]
>
>内存中缓存未在群集节点之间共享。

#### 配置服务{#configuration-service}

Configuration Service支持调整HTML5表单的配置参数和缓存设置。

要更新这些设置，请转至CQ FelixAdmin Console卡(位于https://&lt;&#39;[server]:[port]&#39;/system/console/configMgr)，搜索并选择“移动Forms配置”。

您可以配置缓存大小或使用配置服务禁用缓存。 您还可以使用“调试选项”参数启用调试。 有关调试表单的详细信息，请访问[调试HTML5表单](/help/forms/using/debug.md)。

### 运行时组件(adobe-lc-forms-runtime-pkg.zip){#runtime-components-adobe-lc-forms-runtime-pkg-zip}

运行时包包含用于呈现HTML表单的客户端库。

**作为运行时包的一部分提供的重要组件：**

#### 脚本引擎{#scripting-engine}

AdobeXFA实现支持两种脚本语言，以支持表单中的用户定义逻辑执行：JavaScript和FormCalc。

HTMLForms的脚本引擎使用JavaScript编写，以支持这两种语言的XFA脚本API。

在渲染时，FormCalc脚本将转换（并缓存）为服务器上对用户或设计人员透明的JavaScript。

此脚本引擎使用ECMAScript5的一些功能，如Object.defineProperty。 引擎／库以类别名&#x200B;**xfaforms.用户档案**&#x200B;的CQ客户端库的形式提供。 它还提供&#x200B;**FormBridge API**&#x200B;以使外部门户或应用程序能够与表单交互。 使用FormBridge，外部应用程序可以有计划地隐藏某些元素、获取或设置其值或更改其属性。

有关详细信息，请参阅[表单桥接器](/help/forms/using/form-bridge-apis.md)文章。

#### 布局引擎{#layout-engine}

HTML5表单的布局和可视方面基于SVG 1.1、jQuery、BackBone和CSS3功能。 表单的初始外观将在服务器上生成并缓存。 在客户端上管理初始布局的调整以及表单布局的任何进一步增量更改。 为此，运行时包包含一个以JavaScript编写并基于jQuery/Backbone的布局引擎。 此引擎处理所有动态行为，如“添加／删除”可重复实例、“可增长对象”布局。 此布局引擎一次只渲染一个表单页面。 最初，用户仅视图一页，而水平滚动条仅占第一页。 但是，当用户向下滚动时，下一页开始呈现。 此逐页再现减少了在浏览器中呈现第一页所需的时间，并增强了表单的可感知性能。 此引擎／库是类别名&#x200B;**xfaforms.用户档案**&#x200B;的CQ客户端库的一部分。

布局引擎还包含一组用于从用户捕获表单字段值的构件。 这些构件建模为[jQuery UI构件](https://api.jqueryui.com/jQuery.widget/)，这些构件实施了特定的附加合同以与布局引擎无缝协作。

有关构件和相应合同的详细信息，请参阅[HTML5表单的自定义构件](/help/forms/using/introduction-widgets.md)。

#### 样式 {#styling}

与HTML元素关联的样式是内嵌的或基于嵌入的CSS块添加的。 某些不依赖表单的常见样式是CQ客户端库的一部分，其类别名为xfaforms.用户档案。

除了默认样式属性外，每个表单元素还包含基于元素类型、名称和其他属性的特定CSS类。 使用这些类，您可以通过指定元素自己的CSS来重新设置元素样式。

有关默认样式和类的详细信息，请参阅[样式简介](/help/forms/using/css-styles.md)。

#### 服务器端脚本和Web服务{#server-side-script-and-web-services}

任何标记为在服务器上运行或标记为调用Web服务的脚本（无论其标记为执行的位置）始终在服务器上执行。

客户端脚本引擎：

1. 以JSON形式对传递当前表单状态的服务器进行同步调用
1. 在服务器上执行脚本或Web服务
1. 生成新的JSON状态
1. 返回响应时合并客户端上的新JSON状态。

#### 本地化资源包{#localization-resource-bundles}

HTML5表单支持意大利语(it)、西班牙语(es)、巴西葡萄牙语(pt_BR)、简体中文(zh_CN)、繁体中文（仅限支持）(zh_TW)、朝鲜语(ko_KR)、英语(en_US)、法语(fr_FR)、德语(de_DE)和日语(ja)语言。 根据请求标头中收到的区域设置，相应的资源包会发送到客户端。 此资源包作为用户档案JSP添加为类别名&#x200B;**xfaforms.I18N**&#x200B;的CQ客户端库。 您可以覆盖在用户档案中拾取区域设置包的逻辑。

### Sling Components(adobe-lc-forms-content-pkg.zip){#sling-components-adobe-lc-forms-content-pkg-zip}

Sling包包含与用户档案和用户档案渲染器相关的内容。

#### 个人资料 {#profiles}

用户档案是sling中表示表单或Forms系列的资源节点。 在CQ级别，这些用户档案是JCR节点。 节点位于JCR存储库的&#x200B;**/content**&#x200B;文件夹下，可位于&#x200B;**/content**&#x200B;文件夹下的任意子文件夹内。

#### 用户档案呈示器{#profile-renderers}

用户档案节点具有属性&#x200B;**sling:resourceSuperType**，其值为&#x200B;**xfaforms/用户档案**。 此属性在内部向位于&#x200B;**/libs/xfaforms/用户档案**&#x200B;文件夹中的用户档案节点的sling脚本发送转发请求。 这些脚本是JSP页，它们是将HTML表单和所需的JS/CSS对象组合在一起的容器。 页面包括对以下内容的引用：

* **xfaforms.I18N。&lt;locale>**:此库包含本地化数据。
* **xfaforms.用户档案**:此库包含XFA脚本和布局引擎的实现。

这些库建模为CQ客户端库，它利用CQ框架JavaScript库的自动连接、缩小和压缩功能。
有关CQ客户端库的详细信息，请参阅[CQ Clientlib文档](https://docs.adobe.com/docs/en/cq/current/developing/components/clientlibs.html)。

如上所述，用户档案渲染器JSP通过sling include调用Forms服务。 此JSP还根据管理员配置或请求参数设置各种调试选项。

HTML5表单允许开发人员创建用户档案和用户档案渲染器以自定义表单的外观。 例如，HTML表单允许开发人员将表单集成到现有HTML门户的面板或&lt;div>部分。
有关创建自定义用户档案的详细信息，请参阅[创建自定义用户档案](/help/forms/using/custom-profile.md)。
