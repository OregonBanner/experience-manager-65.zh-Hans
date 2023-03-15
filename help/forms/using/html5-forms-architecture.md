---
title: HTML5表单的架构
seo-title: Architecture of HTML5 forms
description: HTML5表单作为包部署在嵌入式AEM实例中，并使用RESTful Apache Sling架构将功能公开为HTTP/S上的REST端点。
seo-description: HTML5 forms is deployed as a package within the embedded AEM instance and exposes the functionality as REST end point over HTTP/S using RESTful Apache Sling architecture.
uuid: 7f515cea-1447-4fc7-82ba-17f2e3f9f80c
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: a644978e-5736-4771-918a-dfefe350a4a1
docset: aem65
feature: Mobile Forms
exl-id: ed8349a1-f761-483f-9186-bf435899df7d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2011'
ht-degree: 0%

---

# HTML5表单的架构{#architecture-of-html-forms}

## 架构 {#architecture}

HTML5表单功能作为包部署在嵌入式AEM实例中，并使用RESTful作为HTTP/S上的REST端点公开 [Apache Sling架构](https://sling.apache.org/).

![02-aem-forms-architecture_large](assets/02-aem-forms-architecture_large.jpg)

### 使用Sling框架 {#using-sling-framework}

[Apache Sling](https://sling.apache.org/) 以资源为中心。 它使用请求URL首先解析资源。 每个资源都有一个 **sling：resourceType** (或 **sling：resourceSuperType**)属性。 然后，根据此属性、请求方法和请求URL的属性，选择一个sling脚本来处理请求。 此sling脚本可以是JSP或servlet。 对于HTML5表单， **个人资料** 节点充当sling资源和 **配置文件渲染器** 用作sling脚本，处理使用特定配置文件呈现移动表单的请求。 A **配置文件渲染器** 是一个JSP，可从请求中读取参数并调用Forms OSGi服务。

有关REST端点和支持的请求参数的详细信息，请参阅 [渲染表单模板](/help/forms/using/rendering-form-template.md).

当用户从客户端设备(如iOS或Android浏览器)发出请求时，Sling首先根据请求URL解析配置文件节点。 从该配置文件节点中，它显示为 **sling：resourceSuperType** 和 **sling：resourceType** 以确定可处理此表单渲染请求的所有可用脚本。 然后，它使用Sling请求选择器以及请求方法来识别最适合处理此请求的脚本。 一旦请求到达配置文件渲染器JSP，JSP就会调用Forms OSGi服务。

有关sling脚本解析的更多详细信息，请参阅 [AEM Sling备忘单](https://docs.adobe.com/content/docs/en/cq/current/developing/sling_cheatsheet.html) 或 [Apache Sling Url分解](https://sling.apache.org/site/url-decomposition.html).

#### 典型的表单处理调用流程 {#typical-form-processing-call-flow}

HTML5表单缓存处理（呈现或提交）第一个请求中的表单所需的所有中间对象。 它不会缓存依赖于数据的对象，因为此类对象可能会发生更改。

Mobile Form维护两个不同的缓存级别：PreRender缓存和渲染缓存。 preRender缓存包含已解析模板的所有片段和图像，而渲染缓存包含HTML等渲染的内容。

![HTML5表单工作流](assets/cacheworkflow.png)

HTML5表单工作流

HTML5表单不会缓存缺少片段和图像引用的模板。 如果HTML5表单花费的时间超过正常时间，请检查服务器日志中是否有缺少的引用和警告。 还要确保未达到对象的最大大小。

Forms OSGi服务分两步处理请求：

* **布局和初始表单状态生成**：Forms OSGi渲染服务调用Forms缓存组件以确定表单是否已缓存且未失效。 如果表单已缓存且有效，则会从缓存中提供生成的HTML。 如果表单失效，Forms OSGi渲染服务会以XML格式生成初始表单布局和表单状态。 此XML由Forms OSGi服务转换为HTML布局和初始JSON表单状态，然后缓存以供后续请求使用。
* **预填充的Forms**：在渲染时，如果用户请求带有预填充数据的表单，Forms OSGi渲染服务将调用Forms服务容器，并使用合并的数据生成新的表单状态。 但是，由于布局已在上述步骤中生成，因此此调用比第一次调用更快。 此调用仅执行数据合并并对数据运行脚本。

如果表单中有任何更新，或者表单内使用了任何资产，则表单缓存组件会检测到该更新，并且特定表单的缓存将失效。 Forms OSGi服务完成处理后，配置文件渲染器jsp会将JavaScript库引用和样式添加到此表单，并将响应返回到客户端。 典型的Web服务器，如 [Apache](https://httpd.apache.org/) 可在此启用HTML压缩时使用。 Web服务器可以显着减小响应大小、网络流量以及在服务器和客户端计算机之间流式传输数据所需的时间。

当用户提交表单时，浏览器将表单状态以JSON格式发送到 [提交服务代理](../../forms/using/service-proxy.md)；然后，提交服务代理使用JSON数据生成数据XML并提交该数据XML以提交端点。

## 组件 {#components}

您需要AEM Forms附加组件包才能启用HTML5表单。 有关安装AEM Forms附加组件包的信息，请参阅 [安装和配置AEM Forms](../../forms/using/installing-configuring-aem-forms-osgi.md).

### OSGi组件(adobe-lc-forms-core.jar) {#osgi-components-adobe-lc-forms-core-jar}

**AdobeXFA Forms渲染器(com.adobe.livecycle.adobe-lc-forms-core)** 是从Felix Admin Console的包视图查看时HTML5表单OSGi包的显示名称(https://)[主机]：[端口]/system/console/bundles)。

此组件包含用于渲染、缓存管理和配置设置的OSGi组件。

#### Forms OSGi服务 {#forms-osgi-service}

此OSGi服务包含将XDP渲染为HTML的逻辑，并处理表单提交以生成数据XML。 此服务使用Forms服务容器。 Forms服务容器在内部调用本机组件 `XMLFormService.exe` 执行处理操作的用户。

如果收到渲染请求，此组件将调用Forms服务容器以生成布局和状态信息，这些信息将进行进一步处理以生成HTML和JSON表单DOM状态。

此组件还负责从提交的表单状态JSON生成数据XML。

#### 缓存组件 {#cache-component}

HTML5表单使用缓存优化吞吐量和响应时间。 您可以配置缓存服务的级别，以微调性能和空间利用率之间的平衡。

<table>
 <tbody>
  <tr>
   <th>缓存策略</th>
   <th>描述</th>
  </tr>
  <tr>
   <td>无</td>
   <td>不缓存项目<br /> </td>
  </tr>
  <tr>
   <td>保守</td>
   <td>仅缓存在表单渲染之前生成的中间构件，如包含内联片段和图像的模板</td>
  </tr>
  <tr>
   <td>激进</td>
   <td>缓存渲染的HTML内容<br /> 缓存在保守级别缓存的所有工件。<br /> <strong>注释</strong>：此策略可提供最佳性能，但会消耗更多内存来存储缓存的工件。</td>
  </tr>
 </tbody>
</table>

HTML5表单使用LRU策略执行内存缓存。 如果缓存策略设置为“无”，将不会创建缓存，并将清除现有缓存数据（如果有）。 除了缓存策略之外，您还可以配置内存中的总缓存大小，这有助于使缓存大小达到最大限制，如果超过该限制，它将使用LRU模式释放缓存资源。

>[!NOTE]
>
>内存缓存不会在群集节点之间共享。

#### 配置服务 {#configuration-service}

配置服务允许调整HTML5表单的配置参数和缓存设置。

要更新这些设置，请转到CQ FelixAdmin Console(位于https://&lt;&#39;[服务器]：[端口]&#39;/system/console/configMgr)，搜索并选择移动Forms配置。

可以使用配置服务配置缓存大小或禁用缓存。 您还可以使用Debug Options参数启用调试。 有关调试表单的更多信息，请访问 [调试HTML5表单](/help/forms/using/debug.md).

### 运行时组件(adobe-lc-forms-runtime-pkg.zip) {#runtime-components-adobe-lc-forms-runtime-pkg-zip}

运行时包包含用于渲染HTML表单的客户端库。

**作为运行时包的一部分提供的重要组件：**

#### 脚本引擎 {#scripting-engine}

AdobeXFA实施支持两种脚本语言，以便支持在表单中执行用户定义的逻辑：JavaScript和FormCalc。

HTMLForms的脚本引擎使用JavaScript编写，以支持使用这两种语言的XFA脚本API。

在渲染时，FormCalc脚本在服务器上转换（和缓存）为JavaScript，对用户或设计者透明。

此脚本引擎使用ECMAScript5的某些功能，如Object.defineProperty。 引擎/库作为具有类别名称的CQ客户端库提供 **xfaforms.profile**. 它还提供 **FormBridge API** 启用外部门户或应用程序与表单交互。 使用FormBridge，外部应用程序能够以编程方式隐藏某些元素、获取或设置其值或更改其属性。

欲知更多详情，请参见 [Form Bridge](/help/forms/using/form-bridge-apis.md) 文章。

#### 布局引擎 {#layout-engine}

HTML5表单的布局和可视化方面基于SVG1.1、jQuery、BackBone和CSS3功能。 生成表单的初始外观并将其缓存在服务器上。 在客户端上管理初始布局的调整以及对表单布局所做的任何进一步增量更改。 为实现此目的，运行时包包含使用JavaScript编写并基于jQuery/Backbone的布局引擎。 此引擎处理所有动态行为，如添加/删除可重复实例、可增长对象布局。 此布局引擎每次渲染一个表单页面。 最初，用户只查看一个页面，水平滚动条只考虑第一页。 但是，当用户向下滚动时，下一页开始渲染。 此逐页演绎版减少了在浏览器中呈现第一页所需的时间并增强了表单的可感知性能。 此引擎/库是具有类别名称的CQ客户端库的一部分 **xfaforms.profile**.

布局引擎还包含一组用于从用户处捕获表单字段值的小组件。 这些构件建模为 [jQuery UI小组件](https://api.jqueryui.com/jQuery.widget/) 实施特定附加合同以与布局引擎无缝配合工作。

有关构件和相应合同的更多详细信息，请参阅 [适用于HTML5表单的自定义构件](/help/forms/using/introduction-widgets.md).

#### 样式 {#styling}

与HTML元素关联的样式可以内联添加，也可以基于嵌入的CSS块添加。 一些不依赖于表单的常见样式属于类别名为xfaforms.profile的CQ客户端库。

除了默认样式属性外，每个表单元素还根据元素类型、名称和其他属性包含特定的CSS类。 使用这些类，可以通过指定元素自己的CSS来重新设置元素的样式。

有关默认样式和类的更多详细信息，请参阅 [样式简介](/help/forms/using/css-styles.md).

#### 服务器端脚本和Web服务 {#server-side-script-and-web-services}

任何标记为在服务器上运行或标记为调用Web服务的脚本（无论其标记为执行的位置如何）始终在服务器上执行。

客户端脚本引擎：

1. 以JSON形式同步调用传递当前表单状态的服务器
1. 在服务器上执行脚本或Web服务
1. 生成新的JSON状态
1. 在返回响应时合并客户端上的新JSON状态。

#### 本地化资源包 {#localization-resource-bundles}

HTML5表单支持意大利语(it)、西班牙语(es)、巴西葡萄牙语(pt_BR)、简体中文(zh_CN)、繁体中文（仅有限支持）(zh_TW)、朝鲜语(ko_KR)、英语(en_US)、法语(fr_FR)、德语(de_DE)和日语(ja)语言。 根据在请求标头中收到的区域设置，将相应的资源包发送到客户端。 此资源包将作为具有类别名称的CQ客户端库添加到配置文件JSP中 **xfaforms.I18N**. 您可以覆盖在配置文件中选取区域设置包的逻辑。

### Sling组件(adobe-lc-forms-content-pkg.zip) {#sling-components-adobe-lc-forms-content-pkg-zip}

Sling包包含与配置文件和配置文件渲染器相关的内容。

#### 配置文件 {#profiles}

配置文件是Sling中表示表单或Forms系列的资源节点。 在CQ级别，这些配置文件是JCR节点。 节点位于 **/content** 文件夹，并且可以位于 **/content** 文件夹。

#### 配置文件渲染器 {#profile-renderers}

Profile节点具有属性 **sling：resourceSuperType** 带值 **xfaforms/profile**. 此属性在内部将请求转发到位于中的配置文件节点的sling脚本 **/libs/xfaforms/profile** 文件夹。 这些脚本是JSP页，是用来组合HTML表单和所需JS/CSS工件的容器。 这些页面包含对以下项的引用：

* **xfaforms.I18N。&lt;locale>**：此库包含本地化数据。
* **xfaforms.profile**：此库包含适用于XFA脚本和布局引擎的实施。

这些库被建模为CQ客户端库，它利用CQ框架JavaScript库的自动连接、缩小和压缩功能。
有关CQ客户端库的详细信息，请参阅 [CQ Clientlib文档](https://docs.adobe.com/docs/en/cq/current/developing/components/clientlibs.html).

如上所述，配置文件渲染器JSP通过sling include调用Forms服务。 此JSP还根据管理员配置或请求参数设置各种调试选项。

HTML5表单允许开发人员创建配置文件和配置文件渲染器以自定义表单的外观。 例如，HTML表单允许开发人员集成面板中的表单或 &lt;div> 现有HTML门户的部分。
有关创建自定义配置文件的更多详细信息，请参阅 [创建自定义用户档案](/help/forms/using/custom-profile.md).
