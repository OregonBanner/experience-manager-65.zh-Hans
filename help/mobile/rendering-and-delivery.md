---
title: 渲染和交付
seo-title: 渲染和交付
description: 'null'
seo-description: 'null'
uuid: 1253b6a5-6bf3-42b1-be3a-efa23b6ddb51
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
discoiquuid: 672d5b1e-6b2f-4afe-ab04-c398e5ef45d5
translation-type: tm+mt
source-git-commit: 7eb3529de1c99d09eaa78c7589320a85e729400b

---


# 渲染和交付{#rendering-and-delivery}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如，React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md).

AEM内容可以通过 [Sling默认Servlet轻松呈现](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html) ，以呈现 [JSON](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html#default-json-rendering) 和其他格式。

这些现成的呈现方式通常沿用存储库并按原样返回内容。

AEM通过Sling还支持开发和部署自定义sling渲染器以完全控制渲染的架构和内容。

内容服务默认渲染器填补了现成Sling默认值和自定义开发之间的空白，允许自定义和控制呈现内容的许多方面而无需开发。

下图显示了内容服务的呈现。

![chlimage_1-15](assets/chlimage_1-15.png)

## 请求JSON {#requesting-json}

使 **用&lt;RESOURCE.caas[.&lt;EXPORT-CONFIG][。&lt;EXPORT-CONFIG].json** ，用于请求JSON。

<table>
 <tbody>
  <tr>
   <td>资源</td>
   <td>/content/entities下的实体资源<br /> ，或 <br /> /content下的内容资源</td>
  </tr>
  <tr>
   <td>EXPORT-CONFIG</td>
   <td><p><strong>可选</strong><br /> </p> <p>在/apps/mobileapps/caas/exportConfigs/EXPORT-CONFIG下找到的导出配置如果忽略<br /><br /> ，将应用默认的导出配置 </p> </td>
  </tr>
  <tr>
   <td>DEPTH-INT</td>
   <td><strong>可选</strong><br /> SLING <br /> 渲染中用于渲染子项的深度递归</td>
  </tr>
 </tbody>
</table>

## 创建导出配置 {#creating-export-configs}

可以创建导出配置以自定义JSON呈现。

您可以在 */apps/mobileapps/caas/exportConfigs下创建配置节点。*

| 节点名称 | 配置的名称（用于渲染选择器） |
|---|---|
| jcr:primaryType | nt:unstructured |

下表显示了“导出配置”的属性：

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
   <td>从JSON导出中排除以指定前缀开头的属性</td>
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
   <td><p>如果excludePropertyPrefixs设置<br /> ，则这包括指定属性，尽管与被排除的前缀匹配，</p> <p>else（排除忽略的属性）仅包括这些属性</p> </td>
  </tr>
  <tr>
   <td>includeChildren</td>
   <td>String[]</td>
   <td>包含所有内容</td>
   <td>子名</td>
   <td>从JSON导出中排除指定的子项</td>
  </tr>
  <tr>
   <td>excludeChildren</td>
   <td>String[]<br /> <br /> </td>
   <td>排除任何内容</td>
   <td>子名</td>
   <td>从JSON导出仅包含指定的子项，排除其他子项</td>
  </tr>
  <tr>
   <td>renameProperties</td>
   <td>String[]<br /> <br /> </td>
   <td>重命名</td>
   <td>&lt;actual_property_name&gt;,&lt;replacement_property_name&gt;</td>
   <td>使用替换项重命名属性</td>
  </tr>
 </tbody>
</table>

### 资源类型导出优先选项 {#resource-type-export-overrides}

在 */apps/mobileapps/caas/exportConfigs下创建配置节点。*

| 名称 | resourceTypeOverrides |
|---|---|
| jcr:primaryType | nt:unstructured |

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
   <td>&lt;SELECTOR_TO_INC&gt;</td>
   <td>String[] </td>
   <td>-</td>
   <td>sling:resourceType</td>
   <td>对于以下sling资源类型，不要返回默认的CaaSjson导出。<br /> 通过将资源呈现为，返回客户json导出；<br /> &lt;RESOURCE&gt;。&lt;SELECTOR_TO_INC&gt;.json </td>
  </tr>
 </tbody>
</table>

### 现有Content Services导出配置 {#existing-content-services-export-configs}

内容服务包括两种导出配置：

* 默认（未指定配置）
* 页面（渲染站点页面）

#### 默认导出配置 {#default-export-configuration}

如果在所请求的URI中指定了配置，则将应用内容服务默认导出配置。

&lt;RESOURCE>.caas[。&lt;DEPTH-INT>].json

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
   <td>jcr:text,text<br /> jcr:title,title<br /> jcr:description,description<br /> jcr:lastModified,lastModified<br /> cq:tags,tags<br /> cq:lastModified,lastModified</td>
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
   <td>Sling JSON覆盖</td>
   <td>foundation/components/image<br /> wcm/foundation/components/image<br /> mobileapps/caas/components/data/contentReference<br /> mobileapps/caas/components/data/assetlist</td>
  </tr>
 </tbody>
</table>

#### 页面导出配置 {#page-export-configuration}

此配置扩展了默认值以包括子节点下的分组子项。

&lt;SITE_PAGE>.caas.page[。&lt;DEPTH-INT>].json

### 其他资源 {#additional-resources}

请参阅以下资源，了解内容服务中的其他主题：

* [开发模型](/help/mobile/administer-mobile-apps.md)
* [创作内容服务](/help/mobile/develop-content-as-a-service.md)
* [管理内容服务](/help/mobile/developing-content-services.md)

