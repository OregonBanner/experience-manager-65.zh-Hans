---
title: HTML5表单的渲染表单模板
seo-title: HTML5表单的渲染表单模板
description: HTML5表单配置文件与呈现的配置文件相关联。 “配置文件呈现”是JSP页面，负责通过调用Forms OSGi服务来生成表单的HTML表示形式。
seo-description: HTML5表单配置文件与呈现的配置文件相关联。 “配置文件呈现”是JSP页面，负责通过调用Forms OSGi服务来生成表单的HTML表示形式。
uuid: 34daed78-0611-4355-9698-0d7f758e6b61
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: cb75b826-d044-44be-b364-790c046513e0
feature: 移动设备表单
exl-id: 022b9953-2d64-473f-87b7-aac1602f6a7e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 1%

---

# HTML5表单的呈现表单模板{#rendering-form-template-for-html-forms}

## 呈现端点{#render-endpoint}

HTML5表单具有&#x200B;**Profiles**&#x200B;的概念，这些表单以REST端点的形式公开，以便能够移动渲染表单模板。 这些配置文件已关联&#x200B;**配置文件渲染器**。 它们是JSP页面，负责通过调用Forms OSGi服务来生成表单的HTML表示形式。 “配置文件”节点的JCR路径确定呈现端点的URL。 指向“default”配置文件的表单的默认渲染端点如下所示：

https://*host*>:&lt;*port*>/content/xfaforms/profiles/default.html?contentRoot=*包含xdp*>&amp;template=*xdp*&#x200B;名称的文件夹路径

例如，`http://localhost:4502/content/xfaforms/profiles/default.html?contentRoot=c:/xdps&template=sampleForm.xdp`

对于自定义配置文件，端点会相应地发生更改。 例如，名为hrforms的自定义用户档案的结束点是：

`http://localhost:4502/content/xfaforms/profiles/hrforms.html?contentRoot=c:/xdps&template=sampleForm.xdp`

如果您的模板位于名为FormSubmission的应用程序的AEM存储库中，则URI为：

```http
http://localhost:4502/content/xfaforms/profiles/default.html?
 contentRoot=crx:///content/dam/formsanddocuments/FormSubmission/1.0
 &template=sampleForm.xdp
```

## 呈现参数{#render-parameters}

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
   <td>此参数指定模板和关联资源所在的路径。 此路径可以是服务器文件系统路径或存储库路径、http或ftp路径。<br /> </td>
  </tr>
  <tr>
   <td>submitUrl<br /> </td>
   <td>此参数指定将表单数据xml发布到的URL。<br /> </td>
  </tr>
 </tbody>
</table>

### 使用表单模板{#merge-data-with-form-template}合并数据

| 参数 | 描述 |
|---|---|
| dataRef | 此参数指定与模板合并的数据文件的&#x200B;**绝对路径**。 此参数可以是指向rest服务的URL，该服务将以xml格式返回数据。 |
| 数据 | 此参数指定与模板合并的UTF-8编码数据字节。 如果指定此参数，则HTML5表单将忽略dataRef参数。 |

### 传递呈现参数{#passing-the-render-parameter}

HTML5表单支持三种传递呈现参数的方法。 您可以通过URL、键值对和配置文件节点传递参数。 在呈现参数中，键值对具有最高优先级，其后跟配置文件节点。 URL请求参数的优先级最低。

* **URL请求参数**:您可以在URL中指定渲染参数。在URL请求参数中，最终用户可以看到这些参数。 例如，以下提交URL在URL中包含模板参数：`http://localhost:4502/content/xfaforms/profiles/default.html?contentRoot=/Applications/FormSubmission/1.0&template=sampleForm.xdp`

* **SetAttribute请求参数**:您可以将渲染参数指定为键值对。在SetAttribute请求参数中，最终用户看不到这些参数。 您可以将来自任何其他JSP的请求转发到HTML5表单配置文件渲染器JSP，并在请求对象中使用&#x200B;*setAttribute*&#x200B;来传递所有渲染参数。 此方法具有最高的优先级。

* **配置文件节点请求参数：** 您可以将渲染参数指定为配置文件节点的节点属性。在配置文件节点请求参数中，最终用户看不到这些参数。 “配置文件”节点是发送请求的节点。 要将参数指定为节点属性，请使用CRXDE lite。

### 提交参数{#submit-parameters}

HTML5表单提交数据；在AEM服务器上执行服务器端脚本和web服务。 有关在AEM服务器上执行服务器端脚本和Web服务的参数的详细信息，请参阅[HTML5表单服务代理](/help/forms/using/service-proxy.md)。
