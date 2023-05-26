---
title: 使用 Sling 适配器
seo-title: Using Sling Adapters
description: Sling提供了一个Adapter模式，可以方便地翻译实现Adaptable接口的对象
seo-description: Sling offers an Adapter pattern to conveniently translate objects that implement the Adaptable interface
uuid: 07f66a33-072d-49e1-8e67-8b80a6a9072a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: c081b242-67e4-4820-9bd3-7e4495df459e
exl-id: 6465e2c4-28e5-4fc8-8cca-7b632f10ba5a
source-git-commit: 2bae11eafb875f01602c39c0dba00a888e11391a
workflow-type: tm+mt
source-wordcount: '2318'
ht-degree: 13%

---

# 使用 Sling 适配器{#using-sling-adapters}

[Sling](https://sling.apache.org) 提供 [适配器模式](https://sling.apache.org/site/adapters.html) 方便地翻译实现 [可适应](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/Adaptable.html#adaptTo%28java.lang.Class%29) 界面。 此界面提供了一个通用的 [adaptTo()](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/Adaptable.html#adaptTo%28java.lang.Class%29) 将对象转换为作为参数传递的类类型的方法。

例如，要将Resource对象转换为对应的Node对象，您只需执行以下操作：

```java
Node node = resource.adaptTo(Node.class);
```

## 用例 {#use-cases}

有以下用例：

* 获取特定于实施的对象。

   例如，基于JCR的泛型实现 [`Resource`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/resource/Resource.html) 接口提供对底层JCR的访问 [`Node`](https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html).

* 创建需要传递内部上下文对象的对象的快捷方式。

   例如，基于JCR的 [`ResourceResolver`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/resource/ResourceResolver.html) 包含对请求的引用 [`JCR Session`](https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Session.html)，而基于此请求会话工作的许多对象又需要此参数，例如 [`PageManager`](https://helpx.adobe.com/cn/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageManager.html) 或 [`UserManager`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/security/UserManager.html).

* 服务的快捷方式。

   一个罕见的案例。 `sling.getService()` 也很简单。

### Null返回值 {#null-return-value}

`adaptTo()` 可以返回null。

原因有多种，包括：

* 实施不支持目标类型
* 处理此情况的适配器工厂未处于活动状态(例如， 由于缺少服务引用)
* 内部条件失败
* 服务不可用

正确处理空值大小写很重要。 对于jsp渲染，可以接受让jsp失败，如果这将导致空的内容。

### 缓存 {#caching}

为了提高性能，实施可以缓存从返回的对象 `obj.adaptTo()` 呼叫。 如果 `obj` 相同，则返回的对象是相同的。

对所有用户执行此缓存 `AdapterFactory` 基于案例。

但是，没有一般规则 — 对象可以是新实例，也可以是现有实例。 这意味着您无法依赖这两种行为。 因此，它很重要，尤其是在内部 `AdapterFactory`，在这种情况下，对象可重用。

### 工作原理 {#how-it-works}

有多种方式可以 `Adaptable.adaptTo()` 可以实施：

* 对象本身；实现方法本身并映射到特定对象。
* 按 [`AdapterFactory`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/AdapterFactory.html)，可以映射任意对象。

   对象仍必须实施 `Adaptable` 界面和必须扩展 [`SlingAdaptable`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/adapter/SlingAdaptable.html) (通过 `adaptTo` 调用中央适配器管理器)。

   这允许挂接到 `adaptTo` 现有类的机制，例如 `Resource`.

* 两者兼而有之。

对于第一种情况，javadocs可以声明 `adaptTo-targets` 是可能的。 但是，对于特定子类（如基于JCR的资源），通常无法执行此操作。 在后一种情况下，实施 `AdapterFactory` 通常是捆绑包的私有类的一部分，因此不会在客户端API中公开，也不会在javadoc中列出。 从理论上讲，可以访问所有 `AdapterFactory` 实施来自 [osgi](/help/sites-deploying/configuring-osgi.md) 服务运行时并查看其“可适应的”（源和目标）配置，但不会将它们相互映射。 最终，这取决于内部逻辑，必须记录下来。 因此才有了此参考资料。

## 引用 {#reference}

### Sling {#sling}

[**资源**](https://helpx.adobe.com/cn/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html) 可适应：

<table>
 <tbody>
  <tr>
   <td><a href="https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html">节点</a></td>
   <td>如果这是基于JCR节点的资源或引用节点的JCR属性。</td>
  </tr>
  <tr>
   <td><a href="https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Property.html">属性</a></td>
   <td>如果这是基于JCR属性的资源。</td>
  </tr>
  <tr>
   <td><a href="https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Item.html">项目</a></td>
   <td>如果这是基于JCR的资源（节点或属性）。</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api//java/util/Map.html">地图</a></td>
   <td>如果这是基于JCR节点的资源（或其他支持值的资源映射），则返回属性的映射。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/cn/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ValueMap.html">ValueMap</a></td>
   <td>如果这是基于JCR节点的资源（或其他支持值的资源映射），则返回便于使用的属性映射。 还可以（更简单地）通过使用<br /> <code><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ResourceUtil.html#getvaluemap%28org.apache.sling.api.resource.resource%29">ResourceUtil.getValueMap(Resource)</a></code> （处理null大小写等）。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/inherit/InheritanceValueMap.html">InheritanceValueMap</a></td>
   <td>扩展 <a href="https://helpx.adobe.com/cn/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ValueMap.html">值映射</a> 这允许在查找资产时考虑资源的层次结构。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ModifiableValueMap.html">ModifiableValueMap</a></td>
   <td>的扩展 <a href="https://helpx.adobe.com/cn/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ValueMap.html">值映射</a>，允许您修改该节点上的属性。</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api/java/io/InputStream.html">输入流</a></td>
   <td>返回文件资源的二进制内容(如果这是基于JCR节点的资源，并且节点类型为 <code>nt:file</code> 或 <code>nt:resource</code>；如果这是捆绑资源；如果这是文件系统资源，则为文件内容)或二进制JCR属性资源的数据。</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api/java/net/URL.html">URL</a></td>
   <td>返回资源的URL（如果这是基于JCR节点的资源，则返回此节点的存储库URL；如果这是捆绑资源，则返回jar捆绑资源URL；如果这是文件系统资源，则返回文件URL）。</td>
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
   <td>如果此资源是使用sling注册脚本引擎的脚本（例如jsp文件），或者如果这是servlet资源。</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/String.html">字符串</a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/Boolean.html">布尔型</a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/Long.html">长</a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/Double.html">双精度</a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/util/Calendar.html">日历</a><br /> <a href="https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Value.html">值</a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/String.html">String[]</a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/Boolean.html">Boolean[]</a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/Long.html">Long[]</a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/util/Calendar.html">日历[]</a><br /> <a href="https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Value.html">值[]</a></td>
   <td>如果这是基于JCR属性的资源（且值适合），则返回值。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/LabeledResource.html">LabeledResource</a></td>
   <td>如果这是基于JCR节点的资源。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/cn/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/Page.html">页面</a></td>
   <td>如果这是基于JCR节点的资源，并且节点是 <code>cq:Page</code> (或 <code>cq:PseudoPage</code>)。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/cn/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/components/Component.html">组件</a></td>
   <td>如果这是 <code>cq:Component</code> 节点资源。</td>
  </tr>  
  <tr>
   <td><a href="https://helpx.adobe.com/cn/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/designer/Design.html">设计</a></td>
   <td>如果这是设计节点(<code>cq:Page</code>)。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/Template.html">模板</a></td>
   <td>如果这是 <code>cq:Template</code> 节点资源。</td>
  </tr>  
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/msm/api/Blueprint.html">Blueprint</a></td>
   <td>如果这是 <code>cq:Template</code> 节点资源。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/dam/api/Asset.html">资产</a></td>
   <td>如果这是dam：Asset节点资源。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/dam/api/Rendition.html">演绎版</a></td>
   <td>如果这是dam：Asset演绎版（nt：file，在dam：Assert的演绎版文件夹下）</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/tagging/Tag.html">标记</a></td>
   <td>如果这是 <code>cq:Tag</code> 节点资源。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/security/UserManager.html">用户管理器</a></td>
   <td>基于JCR会话（如果这是基于JCR的资源，并且用户有权访问UserManager）。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/jackrabbit/api/security/user/Authorizable.html">可授权</a></td>
   <td>“可授权”是“用户”和“组”通用的基本界面。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/jackrabbit/api/security/user/User.html">用户</a></td>
   <td>用户是一种特殊的可授权对象，可以进行身份验证和模拟。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/SimpleSearch.html">简单搜索</a></td>
   <td>在资源下搜索(或使用setSearchIn())（如果这是基于JCR的资源）。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/workflow/status/WorkflowStatus.html">工作流状态</a></td>
   <td>给定页面/工作流有效负载节点的工作流状态。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/replication/ReplicationStatus.html">复制状态</a></td>
   <td>给定资源或其jcr：content子节点的复制状态（首先选中）。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/connector/ConnectorResource.html">连接器资源</a></td>
   <td>如果这是基于JCR节点的资源，则返回适用于某些类型的连接器资源。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/contentsync/config/package-summary.html">配置</a></td>
   <td>如果这是 <code>cq:ContentSyncConfig</code> 节点资源。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/contentsync/config/package-summary.html">ConfigEntry</a></td>
   <td>如果低于 <code>cq:ContentSyncConfig</code> 节点资源。</td>
  </tr>
 </tbody>
</table>

[**ResourceResolver**](https://helpx.adobe.com/cn/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ResourceResolver.html) 可适应：

<table>
 <tbody>
  <tr>
   <td><a href="https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Session.html">会话</a></td>
   <td>请求的JCR会话（如果这是基于JCR的资源解析程序）（默认）。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/cn/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageManager.html">PageManager</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/components/ComponentManager.html">组件管理器</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/cn/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/designer/Designer.html">Designer</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/dam/api/AssetManager.html">AssetManager</a></td>
   <td>基于JCR会话（如果这是基于JCR的资源解析程序）。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/tagging/TagManager.html">标记管理器</a></td>
   <td>基于JCR会话（如果这是基于JCR的资源解析程序）。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/jackrabbit/api/security/user/UserManager.html">用户管理器</a></td>
   <td>UserManager提供对可授权对象（即用户和组）的访问权限以及维护这些对象的方法。 UserManager绑定到特定会话。
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
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/QueryBuilder.html">Querybuilder</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/Externalizer.html">外部化器</a></td>
   <td>用于外部化绝对URL，即使没有请求对象也是如此。<br /> </td>
  </tr>
 </tbody>
</table>

[**SlingHttpServletRequest**](https://helpx.adobe.com/cn/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/SlingHttpServletRequest.html) 可适应：

还没有目标，但实施了Adaptable，并且可以在自定义AdapterFactory中用作源。

[**SlingHttpServletResponse**](https://helpx.adobe.com/cn/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/SlingHttpServletResponse.html) 可适应：

<table>
 <tbody>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api/org/xml/sax/ContentHandler.html">ContentHandler</a><br /> (XML)</td>
   <td>如果这是sling重写器响应。</td>
  </tr>
 </tbody>
</table>

#### WCM {#wcm}

**[页面](https://helpx.adobe.com/cn/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/Page.html)** 可适应：

<table>
 <tbody>
  <tr>
   <td><a href="https://helpx.adobe.com/cn/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html">Resource</a><br /> </td>
   <td>页面的资源。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/LabeledResource.html">LabeledResource</a></td>
   <td>已标记的资源(==此)。</td>
  </tr>
  <tr>
   <td><a href="https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html">节点</a></td>
   <td>页面的节点。</td>
  </tr>
  <tr>
   <td>...</td>
   <td>页面资源可适应的一切。</td>
  </tr>
 </tbody>
</table>

**[组件](https://helpx.adobe.com/cn/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/components/Component.html)** 可适应：

| [Resource](https://helpx.adobe.com/cn/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html) | 组件的资源。 |
|---|---|
| [LabeledResource](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/LabeledResource.html) | 已标记的资源(==此)。 |
| [节点](https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | 组件的节点。 |
| ... | 组件资源可以适应的一切。 |

**[模板](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/Template.html)** 可适应：

<table>
 <tbody>
  <tr>
   <td><a href="https://helpx.adobe.com/cn/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html">Resource</a><a href="https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html"><br /> </a></td>
   <td>模板的资源。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/LabeledResource.html">LabeledResource</a></td>
   <td>已标记的资源(==此)。</td>
  </tr>
  <tr>
   <td><a href="https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html">节点</a></td>
   <td>此模板的节点。</td>
  </tr>
  <tr>
   <td>...</td>
   <td>模板资源可以适应的一切。</td>
  </tr>
 </tbody>
</table>

#### 安全性 {#security}

**可授权**， **用户** 和 **组** 适应：

| [节点](https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | 返回用户/组主节点。 |
|---|---|
| [复制状态](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/replication/ReplicationStatus.html) | 返回用户/组主节点的复制状态。 |

#### DAM {#dam}

**资产** 可适应：

| [Resource](https://helpx.adobe.com/cn/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html) | 资源的资源。 |
|---|---|
| [节点](https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | 资源的节点。 |
| ... | 资产资源可适应的一切。 |

#### 标记 {#tagging}

**标记** 可适应：

| [Resource](https://helpx.adobe.com/cn/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html) | 标记的资源。 |
|---|---|
| [节点](https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | 标记的节点。 |
| ... | 标记资源可以适应的一切。 |

#### 其他 {#other}

此外，Sling/JCR/OCM还提供 ` [AdapterFactory](https://sling.apache.org/site/adapters.html#Adapters-AdapterFactory)` 用于自定义OCM ([对象内容映射](https://jackrabbit.apache.org/object-content-mapping.html))对象。
