---
title: HTML5表单的渲染表单模板
seo-title: HTML5表单的渲染表单模板
description: HTML5表单配置文件与配置文件呈现相关联。 配置文件呈现是JSP页，负责通过调用Forms OSGi服务生成表单的HTML表示形式。
seo-description: HTML5表单配置文件与配置文件呈现相关联。 配置文件呈现是JSP页，负责通过调用Forms OSGi服务生成表单的HTML表示形式。
uuid: 34daed78-0611-4355-9698-0d7f758e6b61
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: cb75b826-d044-44be-b364-790c046513e0
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# HTML5表单的渲染表单模板 {#rendering-form-template-for-html-forms}

## 渲染端点 {#render-endpoint}

HTML5表单的概念是配置文件 **** ，这些配置文件作为REST端点公开，以支持表单模板的移动渲染。 这些配置文件具有关联的 **配置文件呈现器**。 它们是JSP页，负责通过调用Forms OSGi服务生成表单的HTML表示。 “配置文件”节点的JCR路径决定渲染端点的URL。 指向“默认”配置文件的表单的默认渲染端点如下所示：

https://&lt;*host*>:&lt;*port*>/content/xfaforms/profiles/default.html?contentRoot=&lt;xdp *&amp;template=&lt;xdpAgrop的名称***>的文件夹路径

For example, `http://localhost:4502/content/xfaforms/profiles/default.html?contentRoot=c:/xdps&template=sampleForm.xdp`

对于自定义配置文件，端点会相应地更改。 例如，名称为hrforms的自定义配置文件的终点是：

`http://localhost:4502/content/xfaforms/profiles/hrforms.html?contentRoot=c:/xdps&template=sampleForm.xdp`

如果您的模板位于名为FormSubmission的应用程序的AEM存储库中，则URI为：

```
http://localhost:4502/content/xfaforms/profiles/default.html?
 contentRoot=crx:///content/dam/formsanddocuments/FormSubmission/1.0
 &template=sampleForm.xdp
```

## 渲染参数 {#render-parameters}

以HTML形式呈现表单时支持的请求参数包括：

<table>
 <tbody>
  <tr>
   <th><strong>参数 </strong></th>
   <th><strong>描述</strong></th>
  </tr>
  <tr>
   <td>template<br /> </td>
   <td>此参数指定模板文件的名称。<br /> </td>
  </tr>
  <tr>
   <td>contentRoot<br /> </td>
   <td>此参数指定模板和关联资源所在的路径。 此路径可以是服务器文件系统路径或存储库路径或http或ftp路径。<br /> </td>
  </tr>
  <tr>
   <td>submitUrl<br /> </td>
   <td>此参数指定将表单数据xml发布到的url。<br /> </td>
  </tr>
 </tbody>
</table>

### 将数据与表单模板合并 {#merge-data-with-form-template}

| 参数 | 描述 |
|---|---|
| dataRef | 此参数指 **定与模板合并** 的数据文件的绝对路径。 此参数可以是以xml格式返回数据的其余服务的URL。 |
| 数据 | 此参数指定与模板合并的UTF-8编码数据字节。 如果指定此参数，HTML5表单将忽略dataRef参数。 |

### 传递渲染参数 {#passing-the-render-parameter}

HTML5表单支持三种传递渲染参数的方法。 您可以通过URL、键值对和配置文件节点传递参数。 在render参数中，键值对具有最高的优先级，后跟配置文件节点。 URL请求参数的优先级最低。

* **URL请求参数**:您可以在URL中指定渲染参数。 在URL请求参数中，最终用户可看到这些参数。 例如，以下提交URL在URL中包含模板参数： `http://localhost:4502/content/xfaforms/profiles/default.html?contentRoot=/Applications/FormSubmission/1.0&template=sampleForm.xdp`

* **SetAttribute请求参数**:可以将渲染参数指定为键值对。 在SetAttribute请求参数中，参数对最终用户不可见。 您可以将来自任何其他JSP的请求转发到HTML5表单配置文件渲染器JSP，并使用 *setAttribute* on request对象传递所有渲染参数。 此方法具有最高优先级。

* **** 配置文件节点请求参数：您可以将渲染参数指定为配置文件节点的节点属性。 在配置文件节点请求参数中，最终用户看不到这些参数。 配置文件节点是发送请求的节点。 要将参数指定为节点属性，请使用CRXDE lite。

### 提交参数 {#submit-parameters}

HTML5表单提交数据；在AEM服务器上执行服务器端脚本和Web服务。 有关用于在AEM服务器上执行服务器端脚本和Web服务的参数的详细信息，请参阅 [HTML5表单服务代理](/help/forms/using/service-proxy.md)。

**[联系支持](https://www.adobe.com/account/sign-in.supportportal.html)**
