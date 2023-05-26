---
title: 配置用于呈现的组件的内容片段
seo-title: Content Fragments Configuring Components for Rendering
description: 配置用于呈现的组件的内容片段
seo-description: Content Fragments Configuring Components for Rendering
uuid: 3f5aaf36-e6a7-4a3c-b305-e35ebcc98d0d
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 2aef9048-9d6e-4f5d-b443-5e73f8066d76
docset: aem65
exl-id: 9ef9ae75-cd8c-4adb-9bcb-e951d200d492
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 7%

---

# 配置用于呈现的组件的内容片段{#content-fragments-configuring-components-for-rendering}

有好几个 [高级服务](/help/sites-developing/content-fragments-config-components-rendering.md#definition-of-advanced-services-that-need-configuration) 与内容片段的呈现相关。 要使用这些服务，内容片段框架必须了解此类组件的资源类型。

这是通过配置 [OSGi服务 — 内容片段组件配置](#osgi-service-content-fragment-component-configuration).

>[!CAUTION]
>
>如果您不需要 [高级服务](/help/sites-developing/content-fragments-config-components-rendering.md#definition-of-advanced-services-that-need-configuration) 如下所述，您可以忽略此配置。

>[!CAUTION]
>
>扩展或使用现成组件时，不建议更改配置。

>[!CAUTION]
>
>您可以从头开始编写仅使用内容片段API的组件，而无需高级服务。 但是，在这种情况下，您必须开发组件，以便它处理相应的处理。
>
>因此，建议使用核心组件。

## 需要配置的高级服务的定义 {#definition-of-advanced-services-that-need-configuration}

需要注册组件的服务包括：

* 在发布期间正确确定依赖关系（即，如果片段和模型在上次发布后发生了更改，请确保它们可以随页面自动发布）。
* 支持全文搜索中的内容片段。
* 管理/处理 *中间内容。*
* 管理/处理 *混合媒体资产。*
* 引用的片段的Dispatcher刷新（如果重新发布包含片段的页面）。
* 使用基于段落的渲染。

如果您需要这些功能中的一个或多个功能，则（通常）使用现成功能会更容易，而不是从头开始开发。

## OSGi服务 — 内容片段组件配置 {#osgi-service-content-fragment-component-configuration}

该配置需要绑定到OSGi服务 **内容片段组件配置**：

`com.adobe.cq.dam.cfm.impl.component.ComponentConfigImpl`

>[!NOTE]
>
>参见 [配置OSGi](/help/sites-deploying/configuring-osgi.md) 了解更多详细信息。

例如：

![cfm-01](assets/cfm-01.png)

OSGi配置为：

<table>
 <tbody>
  <tr>
   <td>标签</td>
   <td>OSGi 配置<br /> </td>
   <td>描述</td>
  </tr>
  <tr>
   <td><strong>资源类型</strong></td>
   <td><code>dam.cfm.component.resourceType</code></td>
   <td>要注册的资源类型；例如 <br /> <p><span class="cmp-examples-demo__property-value"><code>core/wcm/components/contentfragment/v1/contentfragment</code></code></p> </td>
  </tr>
  <tr>
   <td><strong>引用属性</strong></td>
   <td><code>dam.cfm.component.fileReferenceProp</code></td>
   <td>包含片段引用的属性的名称；例如， <code>fragmentPath</code> 或 <code>fileReference</code></td>
  </tr>
  <tr>
   <td><strong>元素属性</strong></td>
   <td><code>dam.cfm.component.elementsProp</code></td>
   <td>包含要呈现的元素名称的属性的名称；例如，<code>elementName</code></td>
  </tr>
  <tr>
   <td><strong>变量属性</strong><br /> </td>
   <td><code>dam.cfm.component.variationProp</code></td>
   <td>包含要呈现的变量的名称的属性的名称；例如，<code>variationName</code></td>
  </tr>
 </tbody>
</table>

对于某些功能（例如，仅呈现段落范围），您必须遵守某些惯例：

<table>
 <tbody>
  <tr>
   <td>属性名称</td>
   <td>描述</td>
  </tr>
  <tr>
   <td><code>paragraphRange</code></td>
   <td><p>一个字符串属性，定义要在以下情况下输出的段落范围： <em>单元素渲染模式</em>.</p> <p>格式:</p>
    <ul>
     <li><code>1</code> 或 <code>1-3</code> 或 <code>1-3;6;7-8</code> 或 <code>*-3;5-*</code></li>
     <li>仅在以下情况下评估 <code>paragraphScope</code> 设置为 <code>range</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>paragraphScope</code></td>
   <td><p>一个字符串属性，定义在中时如何输出段落 <em>单元素渲染模式</em>.</p> <p>值:</p>
    <ul>
     <li><code>all</code> ：渲染所有段落</li>
     <li><code>range</code> ：渲染提供的段落范围 <code>paragraphRange</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>paragraphHeadings</code></td>
   <td>一个布尔属性，定义标题(例如， <code>h1</code>， <code>h2</code>， <code>h3</code>)将被计算为段落(<code>true</code>)或不是(<code>false</code>)</td>
  </tr>
 </tbody>
</table>

>[!CAUTION]
>
>这可能在6.5后里程碑之后发生变化。

## 示例 {#example}

例如，请参阅以下内容(在现成的AEM实例上)：

```
/apps/core/wcm/config/com.adobe.cq.dam.cfm.impl.component.ComponentConfigImpl-core-comp-v1.config
```

这包含：

```
dam.cfm.component.resourceType="core/wcm/components/contentfragment/v1/contentfragment"
dam.cfm.component.fileReferenceProp="fragmentPath"
dam.cfm.component.elementsProp="elementName"
dam.cfm.component.variationProp="variationName"
```
