---
title: HTML5表单的渲染表单模板
description: HTML5表单配置文件与配置文件渲染相关联。 配置文件渲染器是JSP页，负责通过调用Forms OSGi服务来生成表单的HTML表示形式。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
feature: Mobile Forms
exl-id: 022b9953-2d64-473f-87b7-aac1602f6a7e
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '535'
ht-degree: 1%

---

# HTML5表单的渲染表单模板 {#rendering-form-template-for-html-forms}

## 渲染端点 {#render-endpoint}

HTML5表单的概念是 **配置文件** 这些组件将作为REST端点公开，以启用表单模板的移动渲染。 这些配置文件已关联 **配置文件渲染器**. 它们是JSP页，负责通过调用Forms OSGi服务来生成表单的HTML表示形式。 “配置文件”节点的JCR路径决定了渲染端点的URL。 表单的默认渲染端点指向“default”配置文件，如下所示：

https://&lt;*主机*>：&lt;*端口*>/content/xfaforms/profiles/default.html？contentRoot=&lt;*包含表单xdp的文件夹的路径*>&amp;template=&lt;*xdp的名称*>

例如，`http://localhost:4502/content/xfaforms/profiles/default.html?contentRoot=c:/xdps&template=sampleForm.xdp`

对于自定义配置文件，端点会相应地更改。 例如，名为hrforms的自定义用户档案的端点为：

`http://localhost:4502/content/xfaforms/profiles/hrforms.html?contentRoot=c:/xdps&template=sampleForm.xdp`

如果模板驻留在名为FormSubmission的应用程序的AEM存储库中，则URI为：

```http
http://localhost:4502/content/xfaforms/profiles/default.html?
 contentRoot=crx:///content/dam/formsanddocuments/FormSubmission/1.0
 &template=sampleForm.xdp
```

## 渲染参数 {#render-parameters}

将表单渲染为HTML时支持的请求参数包括：

<table>
 <tbody>
  <tr>
   <th><strong>参数 </strong></th>
   <th><strong>描述</strong></th>
  </tr>
  <tr>
   <td>模板<br /> </td>
   <td>此参数指定模板文件的名称。<br /> </td>
  </tr>
  <tr>
   <td>contentRoot<br /> </td>
   <td>此参数指定模板和相关资源所在的路径。 此路径可以是服务器文件系统路径或存储库路径、http或ftp路径。<br /> </td>
  </tr>
  <tr>
   <td>submitUrl<br /> </td>
   <td>此参数指定将表单数据xml发布到的URL。<br /> </td>
  </tr>
 </tbody>
</table>

### 将数据与表单模板合并 {#merge-data-with-form-template}

| 参数 | 描述 |
|---|---|
| dataRef | 此参数指定 **绝对路径** 与模板合并的数据文件的属性。 此参数可以是一个指向rest服务的URL，该服务以xml格式返回数据。 |
| 数据 | 此参数指定与模板合并的UTF-8编码数据字节。 如果指定此参数，HTML5表单将忽略dataRef参数。 |

### 传递渲染参数 {#passing-the-render-parameter}

HTML5表单支持三种传递渲染参数的方法。 您可以通过URL、键值对和配置文件节点传递参数。 在渲染参数中，键值对具有最高的优先级，其后是配置文件节点。 URL请求参数的优先级最低。

* **URL请求参数**：您可以在URL中指定渲染参数。 在URL请求参数中，这些参数对于最终用户可见。 例如，以下提交URL在URL中包含模板参数： `http://localhost:4502/content/xfaforms/profiles/default.html?contentRoot=/Applications/FormSubmission/1.0&template=sampleForm.xdp`

* **SetAttribute请求参数**：您可以将渲染参数指定为键值对。 在SetAttribute请求参数中，最终用户看不到这些参数。 您可以将来自任何其他JSP的请求转发到HTML5表单配置文件渲染器JSP并使用 *setAttribute* 用于传递所有渲染参数的请求对象。 此方法具有最高优先权。

* **配置文件节点请求参数：** 您可以将渲染参数指定为配置文件节点的节点属性。 在配置文件节点请求参数中，最终用户看不到这些参数。 配置文件节点是发送请求的节点。 要将参数指定为节点属性，请使用CRXDE lite。

### 提交参数 {#submit-parameters}

HTML5表单提交数据；在AEM服务器上执行服务器端脚本和Web服务。 有关用于在AEM服务器上执行服务器端脚本和Web服务的参数的详细信息，请参见 [HTML5表单服务代理](/help/forms/using/service-proxy.md).
