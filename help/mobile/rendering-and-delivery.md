---
title: 渲染和投放
seo-title: 渲染和投放
description: 'null'
seo-description: 'null'
uuid: 1253b6a5-6bf3-42b1-be3a-efa23b6ddb51
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
discoiquuid: 672d5b1e-6b2f-4afe-ab04-c398e5ef45d5
translation-type: tm+mt
source-git-commit: 7eb3529de1c99d09eaa78c7589320a85e729400b
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 7%

---


# 渲染和投放{#rendering-and-delivery}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如，React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md).

AEM内容可以通过[Sling默认Servlet](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html)轻松呈现，以呈现[JSON](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html#default-json-rendering)和其他格式。

这些现成的呈现方式通常沿着存储库移动，并按原样返回内容。

AEM还通过Sling支持开发和部署自定义sling渲染器以完全控制渲染的模式和内容。

内容服务默认渲染器填补了现成Sling默认值和自定义开发之间的空白，允许自定义和控制呈现内容的许多方面而无需开发。

下图显示了内容服务的呈现。

![chlimage_1-15](assets/chlimage_1-15.png)

## 请求JSON {#requesting-json}

使用&#x200B;**&lt;RESOURCE.caas[。&lt;export-config>.][&lt;export-config>.] jsonto请求JSON。**

<table>
 <tbody>
  <tr>
   <td>资源</td>
   <td>/content/entities<br />或<br />下的实体资源位于/content下</td>
  </tr>
  <tr>
   <td>EXPORT-CONFIG</td>
   <td><p><strong>可选</strong><br /> </p> <p>在/apps/mobileapps/caas/exportConfigs/EXPORT-CONFIG<br /> <br />下找到的导出配置如果省略，将应用默认的导出配置 </p> </td>
  </tr>
  <tr>
   <td>深度——整型</td>
   <td><strong>可选</strong><br /> <br /> 深度递归，用于渲染Sling渲染中使用的子项</td>
  </tr>
 </tbody>
</table>

## 创建导出配置{#creating-export-configs}

可以创建导出配置以自定义JSON渲染。

您可以在&#x200B;*/apps/mobileapps/caas/exportConfigs下创建配置节点。*

| 节点名称 | 配置的名称（用于渲染选择器） |
|---|---|
| jcr:primaryType | nt:unstructured |

下表显示了导出配置的属性：

<table>
 <tbody>
  <tr>
   <td><strong>名称</strong></td>
   <td><strong>类型</strong></td>
   <td><strong>默认值(if, not set)</strong></td>
   <td><strong>值</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td>includeComponents</td>
   <td>String[]</td>
   <td>包含所有内容</td>
   <td>sling:resourceType</td>
   <td>从JSON导出中排除具有指定sling:resourceType的节点的详细信息</td>
  </tr>
  <tr>
   <td>excludeComponents</td>
   <td>String[]</td>
   <td>排除任何内容</td>
   <td>sling:resourceType</td>
   <td>仅包含具有指定sling:resourceType（从JSON导出）的节点的详细信息</td>
  </tr>
  <tr>
   <td>excludePropertyPrefixes</td>
   <td>String[]</td>
   <td>排除任何内容</td>
   <td>属性前缀</td>
   <td>从JSON导出中排除具有指定前缀的开始的属性</td>
  </tr>
  <tr>
   <td>excludeProperties</td>
   <td>String[]</td>
   <td>排除任何内容</td>
   <td>属性名称</td>
   <td>从JSON导出中排除指定属性</td>
  </tr>
  <tr>
   <td>includeProperties</td>
   <td>String[]</td>
   <td>包含所有内容</td>
   <td>属性名称</td>
   <td><p>如果excludePropertyPrefixes set<br />这包括指定属性，尽管与被排除的前缀匹配，</p> <p>else（忽略的排除属性）仅包括这些属性</p> </td>
  </tr>
  <tr>
   <td>includeChildren</td>
   <td>String[]</td>
   <td>包含所有内容</td>
   <td>子名称</td>
   <td>从JSON导出中排除指定的子项</td>
  </tr>
  <tr>
   <td>excludeChildren</td>
   <td>String[]<br /> <br /> </td>
   <td>排除任何内容</td>
   <td>子名称</td>
   <td>仅包含从JSON导出中指定的子项，排除其他</td>
  </tr>
  <tr>
   <td>renameProperties</td>
   <td>String[]<br /> <br /> </td>
   <td>重命名为</td>
   <td>&lt;actual_property_name&gt;,&lt;replacement_property_name&gt;</td>
   <td>使用替换项重命名属性</td>
  </tr>
 </tbody>
</table>

### 资源类型导出覆盖{#resource-type-export-overrides}

在&#x200B;*/apps/mobileapps/caas/exportConfigs下创建配置节点。*

| name | resourceTypeOverrides |
|---|---|
| jcr:primaryType | nt：非结构化 |

下表显示了属性：

<table>
 <tbody>
  <tr>
   <td><strong>名称</strong></td>
   <td><strong>类型</strong></td>
   <td><strong>默认值(if, not set)</strong></td>
   <td><strong>值</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td>&lt;selector_to_inc&gt;</td>
   <td>String[] </td>
   <td>-</td>
   <td>sling:resourceType</td>
   <td>对于以下sling资源类型，不要返回默认的CaaS json导出。<br /> 将资源渲染为；以返回客户json导出<br /> &lt;resource&gt;。&lt;selector_to_inc&gt;.json </td>
  </tr>
 </tbody>
</table>

### 现有Content Services导出配置{#existing-content-services-export-configs}

内容服务包括两种导出配置：

* 默认（未指定配置）
* 页面（要呈现站点页面）

#### 默认导出配置{#default-export-configuration}

如果在所请求的URI中指定了配置，则将应用Content Services默认导出配置。

&lt;resource>.caas[。&lt;depth-int>].json

<table>
 <tbody>
  <tr>
   <td><strong>名称</strong></td>
   <td><strong>值</strong></td>
  </tr>
  <tr>
   <td>excludeProperties</td>
   <td> </td>
  </tr>
  <tr>
   <td>excludePropertyPrefixes</td>
   <td>jcr:,sling:,cq:,oak:,pge-</td>
  </tr>
  <tr>
   <td>includeProperties</td>
   <td>jcr:text,text<br /> jcr:title,title<br /> jcr:description,description<br /> jcr:lastModified,lastModified<br /> cq:tags<br /> cq:lastModified,lastModified</td>
  </tr>
  <tr>
   <td>includeComponents</td>
   <td> </td>
  </tr>
  <tr>
   <td>excludeComponents</td>
   <td> </td>
  </tr>
  <tr>
   <td>includeChildren</td>
   <td> </td>
  </tr>
  <tr>
   <td>excludeChildren</td>
   <td> </td>
  </tr>
  <tr>
   <td>Sling JSON重写</td>
   <td>foundation/components/image<br /> wcm/foundation/components/image<br /> mobileapps/caas/components/data/contentReference<br /> mobileapps/caas/components/data/assetlist</td>
  </tr>
 </tbody>
</table>

#### 页面导出配置{#page-export-configuration}

此配置扩展了默认值，以包括子节点下的子节点分组。

&lt;site_page>.caas.page[。&lt;depth-int>].json

### 其他资源 {#additional-resources}

请参阅以下资源，了解内容服务中的其他主题：

* [开发模型](/help/mobile/administer-mobile-apps.md)
* [创作内容服务](/help/mobile/develop-content-as-a-service.md)
* [管理内容服务](/help/mobile/developing-content-services.md)

