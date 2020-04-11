---
title: HTML5表单的架构
seo-title: HTML5表单的架构
description: HTML5表单部署为嵌入式AEM实例中的包，并使用RESTful Apache Sling体系结构将功能显示为REST端点，而不是HTTP/S。
seo-description: HTML5表单部署为嵌入式AEM实例中的包，并使用RESTful Apache Sling体系结构将功能显示为REST端点，而不是HTTP/S。
uuid: 7f515cea-1447-4fc7-82ba-17f2e3f9f80c
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: a644978e-5736-4771-918a-dfefe350a4a1
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# HTML5表单的架构{#architecture-of-html-forms}

## 架构 {#architecture}

HTML5表单功能作为嵌入式AEM实例中的包部署，并使用REST风格的 [Apache Sling Architecture作为REST端点通过HTTP/S展示](https://sling.apache.org/)。

`<style> .background{ display: none; position: absolute; top: 0%; left: 0%; width: 100%; height: 100%; background-color: black; z-index:1001; -moz-opacity: 0.8; opacity:.80; filter: alpha(opacity=80); } .content { display: none; position: fixed; top: 50%; left: 50%; width: 1200px; height: 756px; margin-left: -600px; margin-top: -378px; border:10px solid orange; background-color: white; z-index:1002; overflow: visible; } </style>` [![01-aem-forms-architecture](assets/01-aem-forms-architecture.jpg)*视图全尺寸&#x200B;*](javascript:void(0).md)

[ ![02-aem-forms-architecture_large](assets/02-aem-forms-architecture_large.jpg)](javascript:void(0).md)

### 使用Sling Framework {#using-sling-framework}

[Apache Sling](https://sling.apache.org/) 以资源为中心。 它使用请求URL首先解析资源。 每个资源都 **有sling:resourceType** (或 **sling:resourceSuperType**)属性。 根据该属性、请求方法和请求URL的属性，选择sling脚本来处理请求。 此sling脚本可以是JSP或servlet。 对于HTML5表单， **用户档案节点充当sling资源，** 用户档案渲染器充当sling脚本 **** ，该脚本处理用特定用户档案渲染移动表单的请求。 **用户档案呈示器** 是从请求中读取参数并调用Forms OSGi服务的JSP。

有关REST端点和支持的请求参数的详细信息，请参 [阅渲染表单模板](/help/forms/using/rendering-form-template.md)。

当用户从客户端设备（如iOS或Android浏览器）发出请求时，Sling首先基于请求URL解析用户档案节点。 从此用户档案节点中，它读取 **sling:resourceSuperType** 和 **sling:resourceType** ，以确定可处理此表单渲染请求的所有可用脚本。 然后，它使用Sling请求选择器和请求方法来标识最适合处理此请求的脚本。 请求到达用户档案渲染器JSP后，JSP将调用Forms OSGi服务。

有关sling脚本分辨率的更多详细信息，请参 [阅AEM Sling备忘单](https://docs.adobe.com/content/docs/en/cq/current/developing/sling_cheatsheet.html) 或 [Apache Sling Url分解](https://sling.apache.org/site/url-decomposition.html)。

#### 典型表单处理呼叫流 {#typical-form-processing-call-flow}

HTML5表单可缓存处理（再现或提交）第一个请求时所需的所有中间对象。 它不会缓存依赖于数据的对象，因为此类对象可能会更改。

Mobile Form维护两个不同级别的缓存，即PreRender缓存和Render Cache。 preRender缓存包含已解析模板的所有片段和图像，而Render缓存包含已渲染的内容（如HTML）。

![HTML5表单工作流程](assets/cacheworkflow.png)

HTML5表单工作流程

HTML5表单不缓存缺少片段和图像引用的模板。 如果HTML5表单的时间超过正常时间，请检查服务器日志中是否有缺少的引用和警告。 另外，请确保未达到对象的最大大小。

Forms OSGi服务通过两个步骤处理请求：

* **布局和初始表单状态生成**:Forms OSGi渲染服务调用表单缓存组件以确定表单是否已缓存且尚未失效。 如果表单已缓存且有效，则它将从缓存中提供生成的HTML。 如果表单无效，则表单OSGi渲染服务将生成XML格式的初始表单布局和表单状态。 此XML将由Forms OSGi服务转换为HTML布局和初始JSON表单状态，然后缓存以备后续请求。
* **预填充的表单**:在呈现时，如果用户使用预填充的数据请求表单，则Forms OSGi呈现服务将调用Forms服务容器，并生成具有合并数据的新Form状态。 但是，由于布局已在上述步骤中生成，因此此调用比第一次调用更快。 此调用仅执行数据合并并对数据运行脚本。

如果表单中或表单内部使用的任何资源存在任何更新，则表单缓存组件会检测到该更新，并且该特定表单的缓存将失效。 在Forms OSGi服务完成处理后，用户档案渲染器jsp将JavaScript库引用和样式添加到此表单并将响应返回给客户端。 Apache等典型Web服务 [器](https://httpd.apache.org/) ，可在此处与HTML压缩一起使用。 Web服务器将显着减小响应大小、网络流量以及在服务器和客户机之间传送数据所需的时间。

当用户提交表单时，浏览器向提交服务代理发送JSON格式的表 [单状态](../../forms/using/service-proxy.md);然后，提交服务代理使用JSON数据生成数据XML，并提交该数据XML以提交端点。

## 组件 {#components}

您需要AEM Forms加载项包才能启用HTML5表单。 有关安装AEM Forms加载项包的信息，请参阅安 [装和配置AEM Forms](../../forms/using/installing-configuring-aem-forms-osgi.md)。

### OSGi组件(adobe-lc-forms-core.jar) {#osgi-components-adobe-lc-forms-core-jar}

**Adobe XFA Forms Renderer(com.adobe.livecycle.adobe-lc-forms-core)** ，是从Felix管理控制台的Bundle视图(https://[host]:[port]/system/console/bundles)查看HTML5表单OSGi包的显示名称。

此组件包含用于渲染、缓存管理和配置设置的OSGi组件。

#### 表单OSGi服务 {#forms-osgi-service}

此OSGi服务包含将XDP渲染为HTML的逻辑，并处理表单的提交以生成数据XML。 此服务使用Forms服务容器。 Forms服务容器会在内部调用执行 `XMLFormService.exe` 处理的本机组件。

如果收到渲染请求，此组件将调用Forms服务容器以生成布局和状态信息，并进一步处理这些信息以生成HTML和JSON表单DOM状态。

此组件还负责从提交的表单状态JSON生成数据XML。

#### 缓存组件 {#cache-component}

HTML5表单使用缓存优化吞吐量和响应时间。 您可以配置缓存服务级别以微调性能和空间利用率之间的平衡。

<table>
 <tbody>
  <tr>
   <th>缓存策略</th>
   <th>描述</th>
  </tr>
  <tr>
   <td>无</td>
   <td>不缓存对象<br /> </td>
  </tr>
  <tr>
   <td>保守派</td>
   <td>仅缓存在表单（如包含内联片段和图像的模板）的呈现之前生成的中间伪像</td>
  </tr>
  <tr>
   <td>咄咄逼人</td>
   <td>缓存呈现的HTML内容<br /> 缓存在“保守”级别中缓存的所有对象。<br /> 注 <strong>意</strong>:此策略可获得最佳性能，但会消耗更多内存来存储缓存的伪像。</td>
  </tr>
 </tbody>
</table>

HTML5表单使用LRU策略执行内存中缓存。 如果缓存策略设置为“无”缓存，则不会创建缓存，并清除现有缓存数据（如果有）。 除了缓存策略之外，您还可以配置内存中缓存的总大小，这有助于使缓存大小达到最大限度，如果超出该限度，它将使用LRU模式释放缓存资源。

>[!NOTE]
>
>内存中缓存不在群集节点之间共享。

#### 配置服务 {#configuration-service}

Configuration Service支持调整HTML5表单的配置参数和缓存设置。

要更新这些设置，请转至CQ Felix Admin Console(位于https://&lt;&#39;[server]:[port]&#39;/system/console/configMgr)，搜索并选择“移动表单配置”。

您可以配置缓存大小或使用配置服务禁用缓存。 您还可以使用“调试选项”参数启用调试。 有关调试表单的更多信息，请参 [阅调试HTML5表单](/help/forms/using/debug.md)。

### 运行时组件(adobe-lc-forms-runtime-pkg.zip) {#runtime-components-adobe-lc-forms-runtime-pkg-zip}

运行时包中包含用于呈现HTML表单的客户端库。

**作为运行时包的一部分提供的重要组件：**

#### 脚本引擎 {#scripting-engine}

Adobe XFA实现支持两种脚本语言，以支持在表单中执行用户定义的逻辑：JavaScript和FormCalc。

HTML Forms的脚本引擎使用JavaScript编写，以支持这两种语言的XFA脚本API。

在渲染时，FormCalc脚本将转换（并缓存）为对用户或设计人员透明的服务器上的JavaScript。

此脚本引擎使用ECMAScript5的某些功能，如Object.defineProperty。 引擎／库以CQ客户端库的形式提供，其类别名 **为xfaforms.用户档案**。 它还提供 **FormBridge API** ，使外部门户或应用程序能够与表单交互。 使用FormBridge，外部应用程序可以通过编程方式隐藏某些元素、获取或设置其值或更改其属性。

有关详细信息，请参阅 [Form Bridge文章](/help/forms/using/form-bridge-apis.md) 。

#### 布局引擎 {#layout-engine}

HTML5表单的布局和可视方面基于SVG 1.1、jQuery、BackBone和CSS3功能。 表单的初始外观将在服务器上生成并缓存。 在客户端上管理对初始布局的调整以及对表单布局的任何进一步增量更改。 为此，运行时包包含一个以JavaScript编写的基于jQuery/Backbone的布局引擎。 此引擎处理所有动态行为，如“添加／删除”可重复实例、“可增长对象”布局。 此布局引擎一次只渲染一个表单页面。 最初，用户仅视图一页，而水平滚动条仅占第一页。 但是，当用户向下滚动时，下一页开始呈现。 此逐页再现减少了在浏览器中呈现第一页所需的时间，并增强了表单的可感知性能。 此引擎／库是CQ客户端库的一部分，其类别名 **为xfaforms.用户档案**。

布局引擎还包含一组构件，用于从用户处捕获表单字段的值。 这些构件建模为 [jQuery UI构件](https://api.jqueryui.com/jQuery.widget/) ，可实现某些附加合同以与布局引擎无缝协作。

有关构件和相应合同的更多详细信息，请参 [阅HTML5表单的自定义构件](/help/forms/using/introduction-widgets.md)。

#### 样式 {#styling}

与HTML元素关联的样式是内嵌的，也是基于嵌入的CSS块添加的。 某些不依赖表单的常见样式是CQ客户端库的一部分，其类别名为xfaforms.用户档案。

除了默认的样式属性外，每个表单元素还包含基于元素类型、名称和其他属性的某些CSS类。 使用这些类，您可以通过指定元素自己的CSS来重新设置元素样式。

有关默认样式和类的更多详细信息，请参 [阅样式简介](/help/forms/using/css-styles.md)。

#### 服务器端脚本和Web服务 {#server-side-script-and-web-services}

任何标记为在服务器上运行或标记为调用Web服务（无论在何处标记为执行）的脚本始终在服务器上执行。

客户端脚本引擎：

1. 以JSON形式向通过当前表单状态的服务器发出同步调用
1. 在服务器上执行脚本或Web服务
1. 生成新的JSON状态
1. 返回响应时合并客户端上的新JSON状态。

#### 本地化资源包 {#localization-resource-bundles}

HTML5表单支持意大利语(it)、西班牙语(es)、巴西葡萄牙语(pt_BR)、简体中文(zh_CN)、繁体中文（仅限支持）(zh_TW)、韩语(ko_KR)、英语(en_US)、法语(fr_FR)、德语(de_DE)和日语(ja)语言。 根据在请求标头中收到的区域设置，相应的资源包会发送到客户端。 此资源包将作为CQ客户端库添加到用户档案JSP中，该客户端库具有类别名 **xfaforms.I18N**。 您可以覆盖在用户档案中拾取区域设置包的逻辑。

### Sling组件(adobe-lc-forms-content-pkg.zip) {#sling-components-adobe-lc-forms-content-pkg-zip}

Sling包中包含与用户档案和用户档案渲染器相关的内容。

#### 个人资料 {#profiles}

用户档案是sling中表示表单或表单系列的资源节点。 在CQ级别，这些用户档案是JCR节点。 节点位于JCR存储库的 **/content** 文件夹下，并且可以位于 **** /content文件夹下的任何子文件夹内。

#### 用户档案渲染器 {#profile-renderers}

用户档案节点具有 **值xfaforms/用户档案的** 属性sling:resourceSuperType ****。 此属性在内部向位于 **/libs/xfaforms/用户档案文件夹中的用户档案节点的sling脚本发送转发请求** 。 这些脚本是JSP页，它们是将HTML表单和所需的JS/CSS对象组合在一起的容器。 这些页面包括对以下内容的引用：

* **xfaforms.I18N。&lt;locale>**:此库包含本地化数据。
* **xfaforms.用户档案**:此库包含XFA脚本和布局引擎的实现。

这些库建模为CQ客户端库，它利用CQ框架JavaScript库的自动连接、缩小和压缩功能。
有关CQ客户端库的详细信息，请参 [阅CQ Clientlib文档](https://docs.adobe.com/docs/en/cq/current/developing/components/clientlibs.html)。

如上所述，用户档案渲染器JSP通过sling include调用Forms Service。 此JSP还根据管理员配置或请求参数设置各种调试选项。

HTML5表单允许开发人员创建用户档案和用户档案渲染器以自定义表单的外观。 例如，HTML表单允许开发人员将表单集成到现有HTML门户的面板或&lt;div>部分。
有关创建自定义用户档案的更多详细信息，请 [参阅创建自定义用户档案](/help/forms/using/custom-profile.md)。
