---
title: 使用 Sling 适配器
seo-title: 使用 Sling 适配器
description: Sling优惠适配器模式以方便地翻译实现适应性接口的对象
seo-description: Sling优惠适配器模式以方便地翻译实现适应性接口的对象
uuid: 07f66a33-072d-49e1-8e67-8b80a6a9072a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: c081b242-67e4-4820-9bd3-7e4495df459e
translation-type: tm+mt
source-git-commit: 36cc5ca0de9ae2933a0d7585a00f26cc984d24db
workflow-type: tm+mt
source-wordcount: '2350'
ht-degree: 1%

---


# 使用 Sling 适配器{#using-sling-adapters}

[Slingoffers](https://sling.apache.org)  an  [Adapter](https://sling.apache.org/site/adapters.html) 模式，以便于转换实现Adaptable接口的 [](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/Adaptable.html#adaptTo%28java.lang.Class%29) 对象。此接口提供通用[adaptTo()](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/Adaptable.html#adaptTo%28java.lang.Class%29)方法，它将对象转换为作为参数传递的类类型。

例如，要将资源对象转换为相应的节点对象，您只需执行以下操作：

```java
Node node = resource.adaptTo(Node.class);
```

## 用例{#use-cases}

有以下用例：

* 获取特定于实施的对象。

   例如，通用[`Resource`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/resource/Resource.html)接口的基于JCR的实现提供对基础JCR [`Node`](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html)的访问。

* 需要传递内部上下文对象的对象的快捷方式创建。

   例如，基于JCR的[`ResourceResolver`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/resource/ResourceResolver.html)包含对请求的[`JCR Session`](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Session.html)的引用，而对于许多将基于该请求会话工作的对象，如[`PageManager`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageManager.html)或[`UserManager`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/security/UserManager.html)，则需要该引用。

* 服务的快捷方式。

   极少的情况- `sling.getService()`也很简单。

### 空返回值{#null-return-value}

`adaptTo()` 可以返回null。

原因有多种，包括：

* 实现不支持目标类型
* 处理此情况的适配器工厂不活动(例如 由于缺少服务引用)
* 内部条件失败
* 服务不可用

请优雅地处理空大小写。 对于jsp渲染，如果jsp失败将导致内容为空，则可能可以接受。

### 缓存{#caching}

为了提高性能，实现可以免费缓存从`obj.adaptTo()`调用返回的对象。 如果`obj`相同，则返回的对象也相同。

此缓存针对所有基于`AdapterFactory`的情况执行。

但是，没有一般规则——对象可以是新实例或现有实例。 这意味着您不能依赖任何一种行为。 因此，在`AdapterFactory`中，对象在此场景中是可重用的，这一点很重要。

### 工作原理{#how-it-works}

`Adaptable.adaptTo()`有多种实现方式：

* 物体本身；实现方法本身并映射到某些对象。
* 通过[`AdapterFactory`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/AdapterFactory.html)，可映射任意对象。

   这些对象仍必须实现`Adaptable`接口，并且必须扩展[`SlingAdaptable`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/adapter/SlingAdaptable.html)（它将`adaptTo`调用传递给中央适配器管理器）。

   这允许将现有类（如`Resource`）的`adaptTo`机制挂接到其中。

* 两者兼有。

对于第一种情况，javadocs可以声明`adaptTo-targets`的可能性。 但是，对于特定子类（如基于JCR的资源），通常不可能这样做。 在后一种情况下，`AdapterFactory`的实现通常是捆绑包的私有类的一部分，因此不在客户端API中公开，也不在javadoc中列出。 理论上，可以从[OSGi](/help/sites-deploying/configuring-osgi.md)服务运行时访问所有`AdapterFactory`实现并查看其“adaptables”(源和目标)配置，但不能将它们相互映射。 最后，这取决于必须记录的内部逻辑。 因此，这一参考。

## 针对开发人员的 Adobe AIR API 参考 {#reference}

### Sling {#sling}

[**资**](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html) 源调整为：

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
   <td>如果这是基于JCR节点的资源（或其他资源支持值映射），则返回属性的易于使用的映射。 还可以使用<br /> <code><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ResourceUtil.html#getvaluemap%28org.apache.sling.api.resource.resource%29">ResourceUtil.getValueMap(Resource)</a></code>（处理空大小写等）来实现（更简单）。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/inherit/InheritanceValueMap.html">继承值映射</a></td>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ValueMap.html">ValueMap</a>的扩展，允许在查找属性时考虑资源层次。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ModifiableValueMap.html">ModifableValueMap</a></td>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ValueMap.html">ValueMap</a>的扩展，允许您修改该节点上的属性。</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api/java/io/InputStream.html">InputStream</a></td>
   <td>返回文件资源的二进制内容(如果这是基于JCR的节点资源，且节点类型为<code>nt:file</code>或<code>nt:resource</code>;如果这是捆绑资源；文件内容（如果这是文件系统资源）或二进制JCR属性资源的数据。</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api/java/net/URL.html">URL</a></td>
   <td>返回资源的URL(如果此节点是基于JCR节点的资源，则返回此节点的存储库URL;jar bundle URL（如果这是捆绑资源）;文件URL（如果这是文件系统资源）。</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api/java/io/File.html">文件</a></td>
   <td>如果这是文件系统资源。</td>
  </tr>
  <tr>
   <td><a href="https://sling.apache.org/apidocs/sling5/org/apache/sling/api/scripting/SlingScript.html">SlingScript</a></td>
   <td>如果此资源是脚本（例如jsp文件），则脚本引擎将注册为sling。</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/products/servlet/2.2/javadoc/javax/servlet/Servlet.html">Servlet</a></td>
   <td>如果此资源是脚本（例如jsp文件），其脚本引擎使用sling进行注册，或如果这是servlet资源。</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/String.html"></a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/Boolean.html"></a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/Long.html"></a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/Double.html"></a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/util/Calendar.html"></a><br /> <a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Value.html"></a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/String.html">StringBooleanLongDoubleCalendarValueString[]</a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/Boolean.html">Boolean[</a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/Long.html">]Long[</a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/util/Calendar.html">]Calendar[</a><br /> <a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Value.html">]Value[]</a></td>
   <td>如果这是基于JCR属性的资源（且值符合），则返回值。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/LabeledResource.html">LabeledResource</a></td>
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
   <td>如果这是dam：资产节点资源。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/dam/api/Rendition.html">呈现版本</a></td>
   <td>如果这是dam：资产演绎版（nt:file位于dam的演绎版文件夹下：Assert）</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/tagging/Tag.html">Tag</a></td>
   <td>如果这是<code>cq:Tag</code>节点资源。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/security/UserManager.html">UserManager</a></td>
   <td>如果这是基于JCR的资源，且用户具有访问UserManager的权限，则基于JCR会话。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/jackrabbit/api/security/user/Authorizable.html">可授权</a></td>
   <td>“可授权”是用户和组的通用基本界面。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/jackrabbit/api/security/user/User.html">用户</a></td>
   <td>用户是可验证和模拟的可授权的特殊用户。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/SimpleSearch.html">SimpleSearch</a></td>
   <td>在资源下搜索(如果这是基于JCR的资源，则使用setSearchIn())。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/workflow/status/WorkflowStatus.html">WorkflowStatus</a></td>
   <td>给定页面／工作流有效负荷节点的工作流状态。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/replication/ReplicationStatus.html">复制状态</a></td>
   <td>给定资源或其jcr:content子节点的复制状态（先选中）。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/connector/ConnectorResource.html">连接器资源</a></td>
   <td>如果这是基于JCR节点的资源，则返回特定类型的适配连接器资源。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/contentsync/config/package-summary.html">配置</a></td>
   <td>如果这是<code>cq:ContentSyncConfig</code>节点资源。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/contentsync/config/package-summary.html">ConfigEntry</a></td>
   <td>如果此资源位于<code>cq:ContentSyncConfig</code>节点资源下。</td>
  </tr>
 </tbody>
</table>

[**资源**](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ResourceResolver.html) 解析适应于：

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
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/components/ComponentManager.html">ComponentManager</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/designer/Designer.html">设计人员</a></td>
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
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/Externalizer.html">外置器</a></td>
   <td>用于外部化绝对URL，即使没有请求对象。<br /> </td>
  </tr>
 </tbody>
</table>

[**SlingHttpServletRequest**](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/SlingHttpServletRequest.html) 调整为：

尚未目标，但实现了Adaptible（适应性），可用作自定义AdapterFactory中的源。

[**SlingHttpServletResponse**](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/SlingHttpServletResponse.html) 适应于：

<table>
 <tbody>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api/org/xml/sax/ContentHandler.html">ContentHandler</a><br /> (XML)</td>
   <td>如果这是一个吊带重写者的回应。</td>
  </tr>
 </tbody>
</table>

#### WCM {#wcm}

**[页](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/Page.html)** 面调整为：

<table>
 <tbody>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html">资源</a><br /> </td>
   <td>页面的资源。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/LabeledResource.html">LabeledResource</a></td>
   <td>标记的资源（==此）。</td>
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

**[组件](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/components/Component.html)** 适应于：

| [资源](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html) | 组件的资源。 |
|---|---|
| [LabeledResource](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/LabeledResource.html) | 标记的资源（==此）。 |
| [节点](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | 组件的节点。 |
| ... | 组件的资源可以调整的所有内容。 |

**[模板](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/Template.html)** 适应于：

<table>
 <tbody>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html">资源</a><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html"><br /> </a></td>
   <td>模板的资源。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/LabeledResource.html">LabeledResource</a></td>
   <td>标记的资源（==此）。</td>
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

**可授权**、 **** 用户 **** 和组适应：

| [节点](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | 返回用户／组主节点。 |
|---|---|
| [复制状态](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/replication/ReplicationStatus.html) | 返回用户／组主节点的复制状态。 |

#### DAM {#dam}

**资** 产适应：

| [资源](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html) | 资产的资源。 |
|---|---|
| [节点](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | 资产的节点。 |
| ... | 资产资源可以调整的所有内容。 |

#### 标记 {#tagging}

**标** 语适应：

| [资源](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html) | 标记的资源。 |
|---|---|
| [节点](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | 标记的节点。 |
| ... | 标记资源可以调整的所有内容。 |

#### 其他 {#other}

此外，Sling/JCR/OCM还为自定义OCM（[对象内容映射](https://jackrabbit.apache.org/object-content-mapping.html)）对象提供` [AdapterFactory](https://sling.apache.org/site/adapters.html#Adapters-AdapterFactory)`。
