---
title: HTML5表单服务代理
seo-title: HTML5表单服务代理
description: HTML5表单服务代理是为提交服务注册代理的配置。 要配置服务代理，请通过request参数submissionServiceProxy指定提交服务的URL。
seo-description: HTML5表单服务代理是为提交服务注册代理的配置。 要配置服务代理，请通过request参数submissionServiceProxy指定提交服务的URL。
uuid: 42d6c1da-3945-469d-b429-c33e563ed70c
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 081f7c17-4e5d-4c7e-a5c3-5541a29b9d55
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# HTML5表单服务代理{#html-forms-service-proxy}

HTML5表单服务代理是为提交服务注册代理的配置。 要配置服务代理，请通过request参数submissionServiceProxy指定提交服务 *的URL*。

## 服务代理的优势 {#benefits-of-service-proxy-br}

服务代理消除了以下问题：

* HTML5表单工作流程要求为HTML5表单用户打开提交服务“/content/xfaforms/submission/default”。 它使AEM服务器面临更广泛的意外受众。
* 服务URL嵌入到表单的运行时模型中。 无法更改服务URL路径。
* 提交过程分为两步。 要提交表单数据，提交至少需要两次到服务器的旅程。 因此，增加了服务器上的负载。
* HTML5表单以POST请求（而非PDF请求）发送数据。 对于同时包含PDF和HTML5表单的工作流程，需要两种不同的处理提交的方法。

### 拓扑 {#topologies-br}

HTML5表单可以使用以下拓扑连接到AEM服务器。

* AEM Server或HTML5表单通过POST将数据发送到服务器的拓扑。
* 代理服务器向服务器发送POST数据的拓扑。

![HTML5表单服务代理拓扑](assets/topology.png)

HTML5表单服务代理拓扑

HTML5表单连接到AEM服务器以运行服务器端脚本、Web服务和提交。 HTML5表单的XFA运行时使用“/bin/xfaforms/submitaction”端点上的Ajax调用与各种参数连接到AEM服务器。 HTML5表单连接AEM服务器以执行以下操作：

#### 执行服务器端脚本和Web服务 {#execute-server-sided-scripts-and-web-services}

标记为在服务器上运行的脚本称为服务器端脚本。 下表列表了服务器端脚本和Web服务中使用的所有参数。

<table>
 <tbody>
  <tr>
   <td><p><strong>参数</strong></p> </td>
   <td><p><strong>描述</strong></p> </td>
  </tr>
  <tr>
   <td><p>活动</p> </td>
   <td><p>活动包含触发请求的事件。 如单击、退出或更改</p> </td>
  </tr>
  <tr>
   <td><p>contextSom</p> </td>
   <td><p>contextSom包含执行事件的对象的SOM表达式。</p> </td>
  </tr>
  <tr>
   <td><p>模板</p> </td>
   <td><p>模板包含用于呈现表单的模板。</p> </td>
  </tr>
  <tr>
   <td><p>contentRoot</p> </td>
   <td><p>contentRoot包含用于呈现表单的模板根目录。</p> </td>
  </tr>
  <tr>
   <td><p>数据</p> </td>
   <td><p>数据包含用于呈现表单的bata字节。</p> </td>
  </tr>
  <tr>
   <td><p>formDom</p> </td>
   <td><p>formDom包含JSON格式的HTML5表单的DOM。</p> </td>
  </tr>
  <tr>
   <td><p>分组</p> </td>
   <td><p>包指定为表单。</p> </td>
  </tr>
  <tr>
   <td><p>debugDir</p> </td>
   <td><p>debugDir包含用于呈现表单的调试目录。</p> </td>
  </tr>
 </tbody>
</table>

#### 提交数据 {#submit-data}

单击“提交”按钮后，HTML5表单会向服务器发送数据。 下表列表了HTML5表单发送到服务器的所有参数。

<table>
 <tbody>
  <tr>
   <td><p><strong>参数</strong></p> </td>
   <td><p><strong>描述</strong></p> </td>
  </tr>
  <tr>
   <td><p>模板</p> </td>
   <td><p>用于渲染表单的模板。</p> </td>
  </tr>
  <tr>
   <td><p>contentRoot</p> </td>
   <td><p>用于呈现表单的模板根目录。</p> </td>
  </tr>
  <tr>
   <td><p>数据</p> </td>
   <td><p>用于呈现表单的bata字节。</p> </td>
  </tr>
  <tr>
   <td><p>formDom</p> </td>
   <td><p>JSON格式的HTML5表单的DOM。</p> </td>
  </tr>
  <tr>
   <td><p>提交url</p> </td>
   <td><p>发布数据XML的URL。</p> </td>
  </tr>
  <tr>
   <td><p>debugDir</p> </td>
   <td><p>用于呈现表单的调试目录。</p> </td>
  </tr>
 </tbody>
</table>

#### 提交代理的工作方式？ {#how-nbsp-the-nbsp-submit-proxy-works}

如果request参数中不存在submiturl，则提交服务代理将充当传递。 它充当传递。 它将请求发送到/bin/xfaforms/submitaction端点，并将响应发送到XFA运行时。

如果request参数中存在submiturl，则提交服务代理选择拓扑。

* 如果AEM服务器发布数据，则代理服务将充当传递。 它将请求发送到/bin/xfaforms/submitaction端点，并将响应发送到XFA运行时。
* 如果代理发布数据，则代理服务将submitUrl以外的所有参数传递给 */bin/xfaforms/submitaction* 端点，并在响应流中接收xml字节。 然后，代理服务将数据xml字节发布到submitUrl以进行处理。

* 在向服务器发送数据（POST请求）之前，HTML5表单会验证服务器的连接性和可用性。 为验证连接性和可用性，HTML表单向服务器发送空头请求。 如果服务器可用，HTML5表单会向服务器发送数据（POST请求）。 如果服务器不可用，则显示一条错 *误消息“无法连接到服务器* ”。 提前检测可以防止用户重新填写表单的麻烦。 代理servlet处理head请求且不引发异常。
