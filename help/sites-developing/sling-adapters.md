---
title: 使用Sling适配器
seo-title: 使用Sling适配器
description: Sling提供了一种适配器模式，可方便地翻译实现适配界面的对象
seo-description: Sling提供了一种适配器模式，可方便地翻译实现适配界面的对象
uuid: 07f66a33-072d-49e1-8e67-8b80a6a9072a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: c081b242-67e4-4820-9bd3-7e4495df459e
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# 使用Sling适配器{#using-sling-adapters}

[Sling](https://sling.apache.org) 提供Adapter [模式](https://sling.apache.org/site/adapters.html) ，可方便地翻译实现 [Adaptivable](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/Adaptable.html#adaptTo%28java.lang.Class%29) 接口的对象。 此接口提供一 [个通用adaptTo()方法](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/Adaptable.html#adaptTo%28java.lang.Class%29) ，该方法将对象转换为作为参数传递的类类型。

例如，要将Resource对象转换为相应的Node对象，您只需执行以下操作：

```java
Node node = resource.adaptTo(Node.class);
```

## Use Cases {#use-cases}

有以下用例：

* 获取特定于实施的对象。

   例如，基于JCR的通用接口实现提 [`Resource`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/resource/Resource.html) 供对基础JCR的访问 [`Node`](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html)。

* 需要传递内部上下文对象的对象的快捷创建方式。

   例如，基于JCR的 [`ResourceResolver`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/resource/ResourceResolver.html) 引用包含对请求的引用，而对于许多将基于该请求会话（如或）工作的对象，则需要该引用 [`JCR Session`](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Session.html)[`PageManager`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageManager.html)[`UserManager`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/security/UserManager.html)。

* 服务的快捷方式。

   一个罕见的例子— `sling.getService()` 也很简单。

### 空返回值 {#null-return-value}

`adaptTo()` 可以返回null。

原因有多种，包括：

* 实施不支持目标类型
* 处理此情况的适配器工厂不活动(例如 由于缺少服务引用)
* 内部条件失败
* 服务不可用

请务必优雅地处理空大小写。 对于jsp渲染，如果jsp失败将导致内容为空，则可能可以接受。

### 缓存 {#caching}

为了提高性能，实现可自由缓存从调用返回的对 `obj.adaptTo()` 象。 如果 `obj` 相同，则返回的对象也相同。

此缓存针对所有基于的情 `AdapterFactory` 况执行。

但是，没有一般规则——对象可以是新实例或现有实例。 这意味着您不能依赖任何一种行为。 因此，在此场景中，对象可 `AdapterFactory`以重复使用，这一点很重要，特别是在内部。

### 工作原理 {#how-it-works}

可以通过多种方 `Adaptable.adaptTo()` 式实现：

* 对象本身；实现方法本身并映射到某些对象。
* 按“” [`AdapterFactory`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/AdapterFactory.html)，可映射任意对象。

   这些对象必须仍实现接 `Adaptable` 口并且必须扩展 [`SlingAdaptable`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/adapter/SlingAdaptable.html) (这会将调用传递 `adaptTo` 给中央适配器管理器)。

   这允许钩入现 `adaptTo` 有类的机制，如 `Resource`。

* 两者兼有。

对于第一种情况，javadocs可以说明可 `adaptTo-targets` 能性。 但是，对于特定子类（如基于JCR的资源），这通常是不可能的。 在后一种情况下，实 `AdapterFactory` 现通常是包的专用类的一部分，因此不在客户端API中公开，也不在javadocs中列出。 理论上，可以从 `AdapterFactory` OSGi [](/help/sites-deploying/configuring-osgi.md) 服务运行时访问所有实现并查看其“适配器”（源和目标）配置，但不能将它们相互映射。 最后，这取决于必须记录的内部逻辑。 因此，该参考。

## 针对开发人员的 Adobe AIR API 参考 {#reference}

### Sling {#sling}

[**资源适应&#x200B;**](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html):

<table>
 <tbody>
  <tr>
   <td><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html">节点</a></td>
   <td>如果这是基于JCR节点的资源或引用节点的JCR属性。</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Property.html">属性</a></td>
   <td>如果这是基于JCR属性的资源。</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Item.html">项目</a></td>
   <td>如果这是基于JCR的资源（节点或属性）。</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api//java/util/Map.html">地图</a></td>
   <td>如果这是基于JCR节点的资源（或其他资源支持值映射），则返回属性的映射。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ValueMap.html">ValueMap</a></td>
   <td>如果这是基于JCR节点的资源（或其他资源支持值映射），则返回属性的方便使用映射。 还可以通过使用(处理空大小写等<br /> ) <code><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ResourceUtil.html#getvaluemap%28org.apache.sling.api.resource.resource%29">ResourceUtil.getValueMap(Resource)</a></code> （更简单）来实现。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/inherit/InheritanceValueMap.html">InheritanceValueMap</a></td>
   <td>ValueMap的 <a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ValueMap.html">扩展</a> ，它允许在查找属性时考虑资源的层次结构。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/PersistableValueMap.html">PersistableValueMap</a></td>
   <td>如果这是基于JCR节点的资源，且用户有权修改该节点上的属性。<br /> 注意：多个可持续地图不共享其值。</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api/java/io/InputStream.html">InputStream</a></td>
   <td>返回“文件”的二进制内容<code>nt:resource</code></td></tr><tr><td></td><td></td></tr><tr><td></td><td></td></tr><tr><td></td><td></td></tr><tr><td></td><td></td></tr><tr><td></td><td><code>AuthorizableResourceProvider</code><code>org.apache.sling.jackrabbit.usermanager</code><code>/system/userManager</code></td></tr><tr><td></td><td></td></tr><tr><td></td><td></td></tr><tr><td></td><td><code>cq:Page</code><code>cq:PseudoPage</code></td></tr><tr><td></td><td><code>cq:Component</code></td></tr><tr><td></td><td><code>cq:Page</code></td></tr><tr><td></td><td><code>cq:Template</code></td></tr><tr><td></td><td><code>cq:Page</code></td></tr><tr><td></td><td></td></tr><tr><td></td><td></td></tr><tr><td></td><td><code>cq:Tag</code></td></tr><tr><td></td><td><code>cq:Preferences</code></td></tr><tr><td></td><td></td></tr><tr><td></td><td></td></tr><tr><td></td><td></td></tr><tr><td></td><td></td></tr><tr><td></td><td></td></tr><tr><td></td><td></td></tr><tr><td></td><td></td></tr><tr><td></td><td></td></tr><tr><td></td><td></td></tr><tr><td></td><td><code>cq:ContentSyncConfig</code></td></tr><tr><td></td><td><code>cq:ContentSyncConfig</code></td></tr></tbody></table>

[**ResourceResolver **](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ResourceResolver.html)适应于：

<table>
 <tbody>
  <tr>
   <td><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Session.html">会话</a></td>
   <td>请求的JCR会话(如果这是基于JCR的资源解析程序（默认）)。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageManager.html">PageManager</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/components/ComponentManager.html">ComponentManager</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/designer/Designer.html">设计人员</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/dam/api/AssetManager.html">AssetManager</a></td>
   <td>基于JCR会话，如果这是基于JCR的资源解析程序。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/tagging/TagManager.html">TagManager</a></td>
   <td>基于JCR会话，如果这是基于JCR的资源解析程序。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/security/UserManager.html">UserManager</a></td>
   <td>基于JCR会话，如果这是基于JCR的资源解析程序，并且用户具有访问UserManager的权限。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/jackrabbit/api/security/user/Authorizable.html">可授权</a> </td>
   <td>当前用户。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/jackrabbit/api/security/user/User.html">用户</a><br /> </td>
   <td>当前用户。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/security/privileges/PrivilegeManager.html">PrivilegeManager</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/preferences/Preferences.html">首选项</a></td>
   <td>当前用户的首选项（如果这是基于JCR的资源解析程序，则基于JCR会话）。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/preferences/PreferencesService.html">首选项服务</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/auth/pin/PinManager.html">PinManager</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/QueryBuilder.html">QueryBuilder</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/Externalizer.html">外置器</a></td>
   <td>用于将绝对URL外置，即使没有请求对象。<br /> </td>
  </tr>
 </tbody>
</table>

[**SlingHttpServletRequest **](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/SlingHttpServletRequest.html)适应于：

目标尚未确定，但实施了“适应性”，可用作自定义AdapterFactory中的源。

[**SlingHttpServletResponse **](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/SlingHttpServletResponse.html)适应于：

<table>
 <tbody>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api/org/xml/sax/ContentHandler.html">ContentHandler</a><br /> (XML)</td>
   <td>如果这是笔记重写者的回应。</td>
  </tr>
 </tbody>
</table>

#### WCM {#wcm}

[**页面会&#x200B;**](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/Page.html)调整为：

<table>
 <tbody>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html">资源</a><br /> </td>
   <td>页面的资源。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/LabeledResource.html">LabeledResource</a></td>
   <td>标记的资源(== this)。</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html">节点</a></td>
   <td>页面的节点。</td>
  </tr>
  <tr>
   <td>...</td>
   <td>页面资源可以调整的所有内容。</td>
  </tr>
 </tbody>
</table>

[**组件适应&#x200B;**](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/components/Component.html):

| [资源](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html) | 组件的资源。 |
|---|---|
| [LabeledResource](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/LabeledResource.html) | 标记的资源(== this)。 |
| [节点](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | 组件的节点。 |
| ... | 组件的资源可以调整到的所有内容。 |

[**模板&#x200B;**](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/Template.html)适应于：

<table>
 <tbody>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html">资源</a><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html"><br /></a></td>
   <td>模板的资源。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/LabeledResource.html">LabeledResource</a></td>
   <td>标记的资源(== this)。</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html">节点</a></td>
   <td>此模板的节点。</td>
  </tr>
  <tr>
   <td>...</td>
   <td>模板资源可以调整的所有内容。</td>
  </tr>
 </tbody>
</table>

#### 安全 {#security}

[**可授权&#x200B;**](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/security/Authorizable.html)，用[**户**](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/security/User.html) 和 [**组&#x200B;**](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/security/Group.html)可适应：

| [节点](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | 返回用户／用户组主节点。 |
|---|---|
| [ReplicationStatus](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/replication/ReplicationStatus.html) | 返回用户／用户组主节点的复制状态。 |

#### DAM {#dam}

[**资产会&#x200B;**](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/dam/api/Asset.html)适应：

| [资源](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html) | 资产的资源。 |
|---|---|
| [节点](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | 资产的节点。 |
| ... | 资产资源可以适应的所有内容。 |

#### 标记 {#tagging}

[**标签适应&#x200B;**](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/tagging/Tag.html):

| [资源](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html) | 标记的资源。 |
|---|---|
| [节点](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | 标记的节点。 |
| ... | 标记资源可以适应的所有内容。 |

#### 其他 {#other}

此外，Sling / JCR / OCM还为自定义OCM(对 ` [AdapterFactory](https://sling.apache.org/site/adapters.html#Adapters-AdapterFactory)` 象内容映[射)对象提供了一个支持](https://jackrabbit.apache.org/object-content-mapping.html)。
