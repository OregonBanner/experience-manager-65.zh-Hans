---
title: 内容片段模板
seo-title: Content Fragment Templates
description: 创建内容片段时会选择模板，并为新片段提供基本结构、元素和变量
seo-description: Templates are selected when creating a content fragmen and provide the new fragment with the basic structure, element, and variation
uuid: d147bac8-b710-40ed-9664-decb5ffcf8e7
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: a975ea2e-5e24-4a96-bd62-63bb98836ff2
docset: aem65
exl-id: 1b75721c-b223-41f0-88d9-bd855b529f31
source-git-commit: a2b1bd5462ae1837470e31cfeb87a95af1c69be5
workflow-type: tm+mt
source-wordcount: '674'
ht-degree: 3%

---

# 内容片段模板{#content-fragment-templates}

>[!CAUTION]
>
>[内容片段模型](/help/assets/content-fragments/content-fragments-models.md) 建议创建所有新内容片段。
>
>内容片段模型用于WKND中的所有示例。

>[!NOTE]
>
>在AEM 6.3之前，内容片段是基于模板而不是模型创建的。
>
>内容片段模板现已弃用。 它们仍可用于创建片段，但建议改用内容片段模型。 不会向片段模板添加任何新功能，它们将在将来版本中删除。

创建内容片段时会选择模板。 它们为新片段提供了基本结构、元素和变量。 用于内容片段的模板受Granite配置管理器的约束。

现成模板保留在以下位置：

* `/libs/settings/dam/cfm/templates`

您可以在下面为内容片段创建特定于站点的模板：

* `/apps/settings/dam/cfm/templates`
覆盖现成模板或提供客户特定的应用程序范围模板的位置，这些模板在运行时不会扩展/更改。

* `/conf/global/settings/dam/cfm/templates`
在运行时需要更改的实例范围特定于客户的模板的位置。

优先级顺序为（降序） `/conf`, `/apps`, `/libs`.

>[!CAUTION]
>
>您 ***必须*** 不会更改 `/libs` 路径。
>
>这是因为 `/libs` 在下次升级实例时被覆盖（当您应用修补程序或功能包时，可能会被覆盖）。
>
>配置和其他更改的推荐方法是：
>
>1. 重新创建所需项目(即， `/libs`)下 `/apps`
>
>1. 在 `/apps`

>


模板的基本结构如下：

```xml
conf
  global
    settings
      dam
        cfm
          templates
            <template-name>
              ...
```

具体结构为：

```xml
+ <template-name>
    - jcr:primaryType
    - jcr:title
    - jcr:description
    - initialAssociatedContent
    - precreateElements
    - version
    + elements
        - jcr:primaryType
        + <element-name>
            - jcr:primaryType
            - jcr:title
            - defaultContent
            - initialContentType
            - name
        ... + other element definitions
    + variations
        - jcr:primaryType
        + <variation-name>
            - jcr:primaryType
            - jcr:title
            - jcr:description
            - name
        ... + other variation definitions
```

有关节点及其属性的更多详细信息包括：

* **模板**

   <table>
   <tbody>
    <tr>
     <th>名称</th>
     <th>类型</th>
     <th>值</th>
    </tr>
    <tr>
     <td><code>&lt;<em>template-name</em>&gt;</code></td>
     <td><code>nt:unstructured</code></td>
     <td>此节点是每个模板的根。 它是必选项，应具有唯一的名称。</td>
    </tr>
    <tr>
     <td><code>jcr:title</code></td>
     <td><p><code>String</code></p> <p>必需<br /> </p> </td>
     <td>模板的标题(显示在 <strong>创建片段</strong> 向导)。</td>
    </tr>
    <tr>
     <td><code>jcr:description</code></td>
     <td><p><code>String</code></p> <p>可选</p> </td>
     <td>描述模板用途的文本(显示在 <strong>创建片段</strong> 向导)。</td>
    </tr>
    <tr>
     <td><code>initialAssociatedContent</code></td>
     <td><p><code>String[]</code></p> <p>可选</p> </td>
     <td>默认情况下，具有应与新创建的内容片段关联的集合路径的数组。</td>
    </tr>
    <tr>
     <td><code>precreateElements</code></td>
     <td><p><code>Boolean</code></p> <p>必需</p> </td>
     <td><p><code>true</code>，如果在创建内容片段时应创建表示内容片段元素(主控元素除外)的子资产； <em>false</em> 是否应“即时”创建它们。</p> <p><strong>注意</strong>:当前，此参数必须设置为 <code>true</code>.</p> </td>
    </tr>
    <tr>
     <td><code>version</code></td>
     <td><p><code>Long</code></p> <p>必需</p> </td>
     <td><p>内容结构的版本；当前支持：</p> <p><strong>注意</strong>:当前，此参数必须设置为 <code>2</code>.<br /> </p> </td>
    </tr>
   </tbody>
  </table>

* **元素**

   <table>
   <tbody>
    <tr>
     <th>名称</th>
     <th>类型</th>
     <th>值</th>
    </tr>
    <tr>
     <td><code>elements</code> </td>
     <td><p><code>nt:unstructured</code></p> <p>必需</p> </td>
     <td><p>包含内容片段元素定义的节点。 它是强制性的，并且需要包含 <strong>主要</strong> 元素，但可以包含[1..n]子节点。</p> <p>使用模板时，元素子分支将复制到片段的模型子分支。</p> <p>第一个元素(在CRXDE Lite中查看)会自动被视为 <i>main</i> 元素；节点名称无关，节点本身除以主资产表示外，没有特殊意义；其他元素则作为子资产处理。</p> </td>
    </tr>
   </tbody>
  </table>

* **元素名称**

   <table>
   <tbody>
    <tr>
     <th>名称</th>
     <th>类型</th>
     <th>值</th>
    </tr>
    <tr>
     <td><code>&lt;<i>element-name</i>&gt;</code></td>
     <td><code>nt:unstructured</code></td>
     <td>此节点定义一个元素。 它是必选项，应具有唯一的名称。</td>
    </tr>
    <tr>
     <td><code>jcr:title</code></td>
     <td><p><code>String</code></p> <p>必需</p> </td>
     <td>元素的标题（显示在片段编辑器的元素选择器中）。</td>
    </tr>
    <tr>
     <td><code>defaultContent</code></td>
     <td><p><code>String</code></p> <p>可选</p> <p>默认: ""</p> </td>
     <td>元素的初始内容；仅在 <code>precreateElements</code><i> = </i><code>true</code></td>
    </tr>
    <tr>
     <td><code>initialContentType</code></td>
     <td><p><code>String</code></p> <p>可选</p> <p>默认: <code>text/html</code></p> </td>
     <td><p>元素的初始内容类型；仅在 <code>precreateElements</code><i> = </i><code>true</code>;当前支持：</p>
      <ul>
       <li><code>text/html</code></li>
       <li><code>text/plain</code></li>
       <li><code>text/x-markdown</code></li>
      </ul> </td>
    </tr>
    <tr>
     <td><code>name</code></td>
     <td><p><code>String</code></p> <p>必需</p> </td>
     <td>元素的内部名称；对于片段类型，必须为唯一。</td>
    </tr>
   </tbody>
  </table>

* **变体**

   <table>
   <tbody>
    <tr>
     <th>名称</th>
     <th>类型</th>
     <th>值</th>
    </tr>
    <tr>
     <td><code>variations</code> </td>
     <td><p><code>nt:unstructured</code></p> <p>可选</p> </td>
     <td>此可选节点包含内容片段初始变量的定义。</td>
    </tr>
   </tbody>
  </table>

* **变体名称**

   <table>
   <tbody>
    <tr>
     <th>名称</th>
     <th>类型</th>
     <th>值</th>
    </tr>
    <tr>
     <td><code>&lt;<i>variation-name</i>&gt;</code> </td>
     <td><p><code>nt:unstructured</code></p> <p>如果存在变量节点，则需要使用</p> </td>
     <td><p>定义初始变量。<br /> 默认情况下，变量会添加到内容片段的所有元素中。</p> <p>变量的初始内容将与相应元素相同(请参阅 <code class="code">defaultContent/
       initialContentType</code>)</p> </td>
    </tr>
    <tr>
     <td><code>jcr:title</code></td>
     <td><p><code>String</code></p> <p>必需</p> </td>
     <td>变量的标题(在片段编辑器的 <strong>变量</strong> 选项卡（左边栏）。</td>
    </tr>
    <tr>
     <td><code>jcr:desciption</code></td>
     <td><p><code>String</code></p> <p>可选</p> <p>默认: ""</p> </td>
     <td>提供变体描述的文本 <span>(在片段编辑器的 <strong>变量</strong> 选项卡（左边栏）。</code></td>
    </tr>
   </tbody>
  </table>
