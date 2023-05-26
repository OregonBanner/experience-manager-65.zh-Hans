---
title: 将Create Correspondence UI与自定义门户集成
seo-title: Integrating Create Correspondence UI with your custom portal
description: 了解如何将创建通信UI与您的自定义门户集成
seo-description: Learn how to integrate create correspondence UI with your custom portal
uuid: 68ef5bf2-b271-4c44-8840-6c495069164d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 0d3bb98e-7139-4d8e-b110-6ebd11debda1
docset: aem65
feature: Correspondence Management
exl-id: c3b6ee31-ccbb-4446-86c8-f618226fefc4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 4%

---

# 将Create Correspondence UI与自定义门户集成{#integrating-create-correspondence-ui-with-your-custom-portal}

## 概述 {#overview}

本文详细介绍了如何将创建通信解决方案与您的环境集成。

## 基于URL的调用 {#url-based-invocation}

从自定义门户调用“创建通信”应用程序的一种方法是使用以下请求参数准备URL：

* 书信模板的标识符（使用cmLetterId参数）。

* 从所需数据源获取的XML数据的URL（使用cmDataUrl参数）。

例如，自定义门户会将URL准备为\
`https://'[server]:[port]'/[contextPath]/aem/forms/createcorrespondence.html?random=[timestamp]&cmLetterId=[letter identifier]&cmDataUrl=[data URL]`，这可以是门户上链接的href。

>[!NOTE]
>
>以这种方式调用并不安全，因为必需的参数是作为GET请求传递的，方法是在URL中公开相同的（清晰可见）。

>[!NOTE]
>
>在调用创建通信应用程序之前，保存并上传数据以在给定dataURL处调用创建通信UI。 这可以从自定义门户本身完成，也可以通过其他后端流程完成。

## 基于内联数据的调用 {#inline-data-based-invocation}

调用“创建通信”应用程序的另一个（也是更安全的）方法可能是，只需点击位于https://&#39;的URL[服务器]：[端口]&#39;/[contextpath]/aem/forms/createcorrespondence.html中，在发送参数和数据，以作为POST请求调用创建通信应用程序时（对最终用户隐藏这些参数和数据）。 这也意味着您现在可以内联传递“创建通信”应用程序的XML数据（作为同一请求的一部分，使用cmData参数），这在之前的方法中是不可能的/理想的。

### 用于指定字母的参数 {#parameters-for-specifying-letter}

| **名称** | **类型** | **描述** |
|---|---|---|
| cmLetterInstanceId | 字符串 | 书信实例的标识符。 |
| cmLetterId | 字符串 | 书信模板的名称。 |

表中的参数顺序指定了用于加载书信的参数首选项。

### 用于指定XML数据源的参数 {#parameters-for-specifying-the-xml-data-source}

<table>
 <tbody>
  <tr>
   <td><strong>名称</strong></td> 
   <td><strong>类型</strong></td> 
   <td><strong>描述</strong></td> 
  </tr>
  <tr>
   <td>cmDataUrl<br /> </td> 
   <td>URL</td> 
   <td>使用基本协议（如cq、ftp、http或文件）从源文件中获取XML数据。<br /> </td> 
  </tr>
  <tr>
   <td>cmLetterInstanceId</td> 
   <td>字符串</td> 
   <td>使用信件实例中可用的xml数据。</td> 
  </tr>
  <tr>
   <td>cmUseTestData</td> 
   <td>布尔值</td> 
   <td>重用数据字典中附加的测试数据。</td> 
  </tr>
 </tbody>
</table>

表中的参数顺序指定了用于加载XML数据的参数的首选项。

### 其他参数 {#other-parameters}

<table>
 <tbody>
  <tr>
   <td><strong>名称</strong></td> 
   <td><strong>类型</strong></td> 
   <td><strong>描述</strong></td> 
  </tr>
  <tr>
   <td>cmPreview<br /> </td> 
   <td>布尔值</td> 
   <td>True表示在预览模式下打开书信<br /> </td> 
  </tr>
  <tr>
   <td>随机</td> 
   <td>时间戳</td> 
   <td>解决浏览器缓存问题。</td> 
  </tr>
 </tbody>
</table>

如果您对cmDataURL使用http或cq协议，则http/cq的URL应可匿名访问。
