---
title: 使用 Sling 适配器
seo-title: 使用 Sling 适配器
description: Sling提供了适配器模式，可方便地转换实施可适应界面的对象
seo-description: Sling提供了适配器模式，可方便地转换实施可适应界面的对象
uuid: 07f66a33-072d-49e1-8e67-8b80a6a9072a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: c081b242-67e4-4820-9bd3-7e4495df459e
exl-id: 6465e2c4-28e5-4fc8-8cca-7b632f10ba5a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2350'
ht-degree: 1%

---

# 使用 Sling 适配器{#using-sling-adapters}

[](https://sling.apache.org) Slingoffers an Adapter [模](https://sling.apache.org/site/adapters.html) 式，以便于转换实现Adaptable接口 [](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/Adaptable.html#adaptTo%28java.lang.Class%29) 的对象。此接口提供通用的[adaptTo()](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/Adaptable.html#adaptTo%28java.lang.Class%29)方法，该方法会将对象转换为作为参数传递的类类型。

例如，要将资源对象转换为相应的Node对象，您只需执行以下操作：

```java
Node node = resource.adaptTo(Node.class);
```

## 用例{#use-cases}

有以下用例：

* 获取特定于实施的对象。

   例如，通用[`Resource`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/resource/Resource.html)接口的基于JCR的实现提供了对基础JCR [`Node`](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html)的访问。

* 要求传递内部上下文对象的对象的快捷方式创建。

   例如，基于JCR的[`ResourceResolver`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/resource/ResourceResolver.html)包含对请求的[`JCR Session`](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Session.html)的引用，这反过来又需要对基于该请求会话工作的许多对象的引用，如[`PageManager`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageManager.html)或[`UserManager`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/security/UserManager.html)。

* 服务的快捷方式。

   极少数情况 — `sling.getService()`也很简单。

### 返回值{#null-return-value}为空

`adaptTo()` 可返回null。

原因有多种，包括：

* 实施不支持目标类型
* 处理此案例的适配器工厂不活动(例如 由于缺少服务引用)
* 内部条件失败
* 服务不可用

请务必优雅地处理空值大小写。 对于jsp渲染，如果jsp失败将导致内容为空，则可能可以接受。

### 缓存 {#caching}

为了提高性能，实施可以免费缓存`obj.adaptTo()`调用返回的对象。 如果`obj`相同，则返回的对象相同。

此缓存适用于所有基于`AdapterFactory`的情况。

但是，没有一般规则 — 对象可以是新实例或现有实例。 这意味着您不能依赖任一行为。 因此，在此情景中，对象可重复使用这一点很重要，在`AdapterFactory`内尤其如此。

### 工作原理{#how-it-works}

可通过多种方式来实施`Adaptable.adaptTo()`:

* 对象本身；实现方法本身，并映射到特定对象。
* 通过[`AdapterFactory`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/AdapterFactory.html)，可映射任意对象。

   这些对象仍必须实现`Adaptable`接口，并且必须扩展[`SlingAdaptable`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/adapter/SlingAdaptable.html)（这会将`adaptTo`调用传递到中央适配器管理器）。

   这允许将挂接到现有类的`adaptTo`机制中，如`Resource`。

* 两者兼有。

对于第一种情况，javaoc可以声明`adaptTo-targets`的可能性。 但是，对于特定子类（如基于JCR的资源），通常不可能执行此操作。 在后一种情况下，`AdapterFactory`的实现通常是包的私有类的一部分，因此不会在客户端API中公开，也不会在javaoc中列出。 理论上，可以从[OSGi](/help/sites-deploying/configuring-osgi.md)服务运行时访问所有`AdapterFactory`实施，并查看其“adaptables”（源和目标）配置，但不能将它们相互映射。 最后，这取决于必须记录的内部逻辑。 因此，该参考。

## 针对开发人员的 Adobe AIR API 参考 {#reference}

### Sling {#sling}

[****](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html) Resourceataifated用于：

<table>
 <tbody>
  <tr>
   <td><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html">节点</a></td>
   <td>如果这是基于JCR的资源或引用节点的JCR属性。</td>
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
   <td>返回属性的映射(如果这是基于JCR节点的资源（或其他支持值的资源映射）。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ValueMap.html">ValueMap</a></td>
   <td>如果这是基于JCR节点的资源（或其他资源支持值映射），则返回属性的方便使用映射。 还可以使用<br /> <code><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ResourceUtil.html#getvaluemap%28org.apache.sling.api.resource.resource%29">ResourceUtil.getValueMap(Resource)</a></code>（句柄空小写等）实现（更简单）。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/inherit/InheritanceValueMap.html">继承值映射</a></td>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ValueMap.html">ValueMap</a>的扩展，在查找属性时，可考虑资源的层次结构。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ModifiableValueMap.html">ModiableValueMap</a></td>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ValueMap.html">ValueMap</a>的扩展，用于修改该节点上的属性。</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api/java/io/InputStream.html">InputStream</a></td>
   <td>返回文件资源的二进制内容(如果这是基于JCR的资源，且节点类型为<code>nt:file</code>或<code>nt:resource</code>;如果是包资源；文件内容（如果这是文件系统资源）或二进制JCR属性资源的数据。</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api/java/net/URL.html">URL</a></td>
   <td>返回指向资源的URL(如果这是基于JCR节点的资源，则返回此节点的存储库URL;jar包URL（如果这是包资源）；文件URL（如果这是文件系统资源）。</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api/java/io/File.html">文件</a></td>
   <td>如果这是文件系统资源。</td>
  </tr>
  <tr>
   <td><a href="https://sling.apache.org/apidocs/sling5/org/apache/sling/api/scripting/SlingScript.html">SlingScript</a></td>
   <td>如果此资源是使用sling注册脚本引擎的脚本（例如jsp文件）。</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/products/servlet/2.2/javadoc/javax/servlet/Servlet.html">Servlet</a></td>
   <td>如果此资源是脚本（例如jsp文件），其脚本引擎已使用sling进行注册，或者这是Servlet资源。</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/String.html"></a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/Boolean.html"></a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/Long.html"></a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/Double.html"></a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/util/Calendar.html"></a><br /> <a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Value.html"></a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/String.html">StringBooleanLongDoubleCalendarValueString[]</a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/Boolean.html">Boolean[]</a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/Long.html">Long[]</a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/util/Calendar.html">Calendar[]</a><br /> <a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Value.html">Value[]</a></td>
   <td>如果这是基于JCR属性的资源（值适合），则返回值。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/LabeledResource.html">LakedResource</a></td>
   <td>如果这是基于JCR节点的资源。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/Page.html">页面</a></td>
   <td>如果这是基于JCR的资源，并且该节点是<code>cq:Page</code>（或<code>cq:PseudoPage</code>）。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/components/Component.html">组件</a></td>
   <td>如果这是<code>cq:Component</code>节点资源。</td>
  </tr>  
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/designer/Design.html">设计</a></td>
   <td>如果这是设计节点(<code>cq:Page</code>)。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/Template.html">模板</a></td>
   <td>如果这是<code>cq:Template</code>节点资源。</td>
  </tr>  
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/msm/api/Blueprint.html">Blueprint</a></td>
   <td>如果这是<code>cq:Template</code>节点资源。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/dam/api/Asset.html">资产</a></td>
   <td>如果这是dam:Asset节点资源。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/dam/api/Rendition.html">演绎版</a></td>
   <td>如果这是dam:Asset演绎版（nt:file位于dam:Assert的演绎版文件夹下）</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/tagging/Tag.html">Tag</a></td>
   <td>如果这是<code>cq:Tag</code>节点资源。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/security/UserManager.html">UserManager</a></td>
   <td>基于JCR会话（如果这是基于JCR的资源，且用户有权访问UserManager）。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/jackrabbit/api/security/user/Authorizable.html">可授权</a></td>
   <td>“可授权”是“用户”和“组”的常用基本界面。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/jackrabbit/api/security/user/User.html">用户</a></td>
   <td>用户是可进行身份验证和模拟的特殊可授权。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/SimpleSearch.html">SimpleSearch</a></td>
   <td>在资源下方搜索(或使用setSearchIn())（如果这是基于JCR的资源）。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/workflow/status/WorkflowStatus.html">WorkflowStatus</a></td>
   <td>给定页面/工作流有效负载节点的工作流状态。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/replication/ReplicationStatus.html">复制状态</a></td>
   <td>给定资源或其jcr:content子节点的复制状态（首先选中）。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/connector/ConnectorResource.html">连接器资源</a></td>
   <td>如果某些类型是基于JCR节点的资源，则返回该类型的适配连接器资源。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/contentsync/config/package-summary.html">配置</a></td>
   <td>如果这是<code>cq:ContentSyncConfig</code>节点资源。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/contentsync/config/package-summary.html">ConfigEntry</a></td>
   <td>如果这位于<code>cq:ContentSyncConfig</code>节点资源下。</td>
  </tr>
 </tbody>
</table>

[****](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ResourceResolver.html) ResourceResolveratifate为：

<table>
 <tbody>
  <tr>
   <td><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Session.html">会话</a></td>
   <td>请求的JCR会话(如果这是基于JCR的资源解析程序（默认）)。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageManager.html">PageManager</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/components/ComponentManager.html">组件管理器</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/designer/Designer.html">Designer</a></td>
   <td> </td>
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
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/jackrabbit/api/security/user/UserManager.html">UserManager</a></td>
   <td>UserManager提供对可授权对象（即用户和组）的访问和维护方法。 UserManager绑定到特定会话。
   </td>
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
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/QueryBuilder.html">QueryBuilder</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/Externalizer.html">外部器</a></td>
   <td>用于外部化绝对URL，即使不包含请求对象。<br /> </td>
  </tr>
 </tbody>
</table>

[****](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/SlingHttpServletRequest.html) SlingHttpServletRequestable适用于：

尚无目标，但实施了“适应性”，可在自定义AdapterFactory中用作源。

[****](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/SlingHttpServletResponse.html) SlingHttpServletResponse适用于：

<table>
 <tbody>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api/org/xml/sax/ContentHandler.html">ContentHandler</a><br /> (XML)</td>
   <td>如果这是Sling重写器响应。</td>
  </tr>
 </tbody>
</table>

#### WCM {#wcm}

**[](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/Page.html)** 页面调整为：

<table>
 <tbody>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html">资源</a><br /> </td>
   <td>页面的资源。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/LabeledResource.html">LakedResource</a></td>
   <td>标记的资源(==此)。</td>
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

**[](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/components/Component.html)** 组件会适应以下情况：

| [资源](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html) | 组件的资源。 |
|---|---|
| [LakedResource](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/LabeledResource.html) | 标记的资源(==此)。 |
| [节点](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | 组件的节点。 |
| ... | 组件资源可以适应的所有内容。 |

**[](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/Template.html)** Template会自动适应：

<table>
 <tbody>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html">资源</a><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html"><br /> </a></td>
   <td>模板的资源。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/LabeledResource.html">LakedResource</a></td>
   <td>标记的资源(==此)。</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html">节点</a></td>
   <td>此模板的节点。</td>
  </tr>
  <tr>
   <td>...</td>
   <td>模板资源可以适应的所有内容。</td>
  </tr>
 </tbody>
</table>

#### 安全 {#security}

**可授权**、用 **** 户 **** 和组适应：

| [节点](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | 返回用户/组主节点。 |
|---|---|
| [复制状态](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/replication/ReplicationStatus.html) | 返回用户/组主节点的复制状态。 |

#### DAM {#dam}

**** 资产可适应：

| [资源](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html) | 资产的资源。 |
|---|---|
| [节点](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | 资产的节点。 |
| ... | 资产资源可以调整的所有内容。 |

#### 标记 {#tagging}

**** 标记适应于：

| [资源](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html) | 标记的资源。 |
|---|---|
| [节点](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | 标记的节点。 |
| ... | 标记资源可以调整的所有内容。 |

#### 其他 {#other}

此外，Sling / JCR / OCM还为自定义OCM（[对象内容映射](https://jackrabbit.apache.org/object-content-mapping.html)）对象提供了` [AdapterFactory](https://sling.apache.org/site/adapters.html#Adapters-AdapterFactory)`。
