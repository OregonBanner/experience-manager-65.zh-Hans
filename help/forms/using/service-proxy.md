---
title: HTML5表单服务代理
seo-title: HTML5表单服务代理
description: HTML5表单服务代理是用于注册提交服务代理的配置。 要配置服务代理，请通过请求参数submissionServiceProxy指定提交服务的URL。
seo-description: HTML5表单服务代理是用于注册提交服务代理的配置。 要配置服务代理，请通过请求参数submissionServiceProxy指定提交服务的URL。
uuid: 42d6c1da-3945-469d-b429-c33e563ed70c
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 081f7c17-4e5d-4c7e-a5c3-5541a29b9d55
docset: aem65
feature: 移动设备表单
exl-id: 8f9b10ae-1600-49c2-a061-153a2a89c67e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '732'
ht-degree: 1%

---

# HTML5表单服务代理{#html-forms-service-proxy}

HTML5表单服务代理是用于注册提交服务代理的配置。 要配置服务代理，请通过请求参数&#x200B;*submissionServiceProxy*&#x200B;指定提交服务的URL。

## 服务代理{#benefits-of-service-proxy-br}的好处

服务代理可消除以下情况：

* HTML5表单工作流要求为HTML5表单用户打开提交服务“/content/xfaforms/submission/default”。 它可向更广泛的意外受众公开AEM服务器。
* 服务URL将嵌入到表单的运行时模型中。 无法更改服务URL路径。
* 提交分为两步。 要提交表单数据，提交至少需要两个到服务器的历程。 因此，增加了服务器上的负载。
* HTML5表单在POST请求中发送数据，而不是PDF请求。 对于同时涉及PDF和HTML5表单的工作流，需要使用两种不同的处理提交的方法。

### 拓扑{#topologies-br}

HTML5表单可以使用以下拓扑连接到AEM服务器。

* AEM服务器或HTML5表单通过POST向服务器发送数据的拓扑。
* 代理服务器向服务器发送POST数据的拓扑。

![HTML5表单服务代理拓扑](assets/topology.png)

HTML5表单服务代理拓扑

HTML5表单连接到AEM服务器以运行服务器端脚本、Web服务和提交。 HTML5表单的XFA运行时在“/bin/xfaforms/submitaction”端点上使用Ajax调用以及各种参数来连接到AEM服务器。 HTML5表单可连接AEM服务器以执行以下操作：

#### 执行服务器端脚本和Web服务{#execute-server-sided-scripts-and-web-services}

标记为在服务器上运行的脚本称为服务器端脚本。 下表列出了服务器端脚本和Web服务中使用的所有参数。

<table>
 <tbody>
  <tr>
   <td><p><strong>参数</strong></p> </td>
   <td><p><strong>描述</strong></p> </td>
  </tr>
  <tr>
   <td><p>活动</p> </td>
   <td><p>活动包含触发请求的事件。 例如，单击、退出或更改</p> </td>
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
   <td><p>数据包含用于呈现表单的字节。</p> </td>
  </tr>
  <tr>
   <td><p>formDom</p> </td>
   <td><p>formDom包含JSON格式的HTML5表单的DOM。</p> </td>
  </tr>
  <tr>
   <td><p>数据包</p> </td>
   <td><p>数据包指定为表单。</p> </td>
  </tr>
  <tr>
   <td><p>debugDir</p> </td>
   <td><p>debugDir包含用于呈现表单的调试目录。</p> </td>
  </tr>
 </tbody>
</table>

#### 提交数据{#submit-data}

单击提交按钮时，HTML5表单会将数据发送到服务器。 下表列出了HTML5表单发送到服务器的所有参数。

<table>
 <tbody>
  <tr>
   <td><p><strong>参数</strong></p> </td>
   <td><p><strong>描述</strong></p> </td>
  </tr>
  <tr>
   <td><p>模板</p> </td>
   <td><p>用于呈现表单的模板。</p> </td>
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

#### 提交代理的工作方式？{#how-nbsp-the-nbsp-submit-proxy-works}

如果请求参数中不存在提交url，则提交服务代理将充当传递。 它充当了传递。 它会将请求发送到/bin/xfaforms/submitaction端点，并将响应发送到XFA运行时。

如果请求参数中存在提交url，则提交服务代理将选择拓扑。

* 如果AEM服务器发布数据，则代理服务将充当传递。 它会将请求发送到/bin/xfaforms/submitaction端点，并将响应发送到XFA运行时。
* 如果代理发布数据，则代理服务会将除submitUrl之外的所有参数传递到&#x200B;*/bin/xfaforms/submitaction*&#x200B;端点，并在响应流中接收xml字节。 然后，代理服务将数据xml字节发布到submitUrl以进行处理。

* 在向服务器发送数据(POST请求)之前，HTML5表单会验证服务器的连接性和可用性。 为验证连接性和可用性，HTML表单向服务器发送空头请求。 如果服务器可用，则HTML5表单会向服务器发送数据(POST请求)。 如果服务器不可用，则会显示一条错误消息&#x200B;*无法连接到服务器，*。 提前检测功能可防止用户重新填写表单的麻烦。 代理Servlet处理Head请求，并且不引发异常。
