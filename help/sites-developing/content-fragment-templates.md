---
title: 内容片段模板
seo-title: Content Fragment Templates
description: 在创建内容片段时选择模板，并为新片段提供基本结构、元素和变体
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
>[内容片段模型](/help/assets/content-fragments/content-fragments-models.md) 建议用于创建所有新的内容片段。
>
>内容片段模型用于WKND中的所有示例。

>[!NOTE]
>
>在AEM 6.3之前，内容片段是基于模板而不是模型创建的。
>
>内容片段模板现已弃用。 它们仍可用于创建片段，但建议改用内容片段模型。 片段模板中不会添加任何新功能，将来版本中将删除这些功能。

创建内容片段时选择模板。 它们为新片段提供基本结构、元素和变量。 用于内容片段的模板受Granite Configuration Manager约束。

现成的模板保存在下：

* `/libs/settings/dam/cfm/templates`

您可以在以下位置为内容片段创建特定于站点的模板：

* `/apps/settings/dam/cfm/templates`
用于覆盖现成模板或提供特定于客户的应用程序范围的模板的位置，这些模板在运行时不会进行扩展/更改。

* `/conf/global/settings/dam/cfm/templates`
运行时需要更改的全实例客户特定模板的位置。

优先顺序为（降序） `/conf`， `/apps`， `/libs`.

>[!CAUTION]
>
>您 ***必须*** 不更改 `/libs` 路径。
>
>这是因为 `/libs` 下次升级实例时将被覆盖（在应用修补程序或功能包时很可能会被覆盖）。
>
>配置和其他更改的推荐方法是：
>
>1. 重新创建所需项目（即该项目存在于中） `/libs`)下 `/apps`
>
>1. 在中进行任何更改 `/apps`

>


模板的基本结构位于下方：

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
     <th>价值</th>
    </tr>
    <tr>
     <td><code>&lt;<em>template-name</em>&gt;</code></td>
     <td><code>nt:unstructured</code></td>
     <td>此节点是每个模板的根。 它是必填项，应具有唯一名称。</td>
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
     <td>一个数组，其中包含集合的路径，默认情况下，这些路径应该关联到新创建的内容片段。</td>
    </tr>
    <tr>
     <td><code>precreateElements</code></td>
     <td><p><code>Boolean</code></p> <p>必需</p> </td>
     <td><p><code>true</code>，如果在创建内容片段时应创建表示内容片段的元素(主控元素除外)的子资产； <em>false</em> 如果它们应该“动态”创建的话。</p> <p><strong>注释</strong>：此参数当前必须设置为 <code>true</code>.</p> </td>
    </tr>
    <tr>
     <td><code>version</code></td>
     <td><p><code>Long</code></p> <p>必需</p> </td>
     <td><p>内容结构的版本；当前支持：</p> <p><strong>注释</strong>：此参数当前必须设置为 <code>2</code>.<br /> </p> </td>
    </tr>
   </tbody>
  </table>

* **元素**

   <table>
   <tbody>
    <tr>
     <th>名称</th>
     <th>类型</th>
     <th>价值</th>
    </tr>
    <tr>
     <td><code>elements</code> </td>
     <td><p><code>nt:unstructured</code></p> <p>必需</p> </td>
     <td><p>包含内容片段元素定义的节点。 它是强制性的，并且需要为至少包含一个子节点 <strong>主要</strong> 元素，但可以包含[1..n]个子节点。</p> <p>使用模板时，元素子分支复制到片段的模型子分支。</p> <p>第一个元素(在CRXDE Lite中查看)自动视为 <i>主要</i> 元素；节点名称是无关的，并且节点本身不具有特殊重要性，除了它由主资产表示这一事实；其他元素作为子资产处理。</p> </td>
    </tr>
   </tbody>
  </table>

* **元素名称**

   <table>
   <tbody>
    <tr>
     <th>名称</th>
     <th>类型</th>
     <th>价值</th>
    </tr>
    <tr>
     <td><code>&lt;<i>element-name</i>&gt;</code></td>
     <td><code>nt:unstructured</code></td>
     <td>此节点定义一个元素。 它是必填项，应具有唯一名称。</td>
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
     <td><p>元素的初始内容类型；仅在 <code>precreateElements</code><i> = </i><code>true</code>；当前支持：</p>
      <ul>
       <li><code>text/html</code></li>
       <li><code>text/plain</code></li>
       <li><code>text/x-markdown</code></li>
      </ul> </td>
    </tr>
    <tr>
     <td><code>name</code></td>
     <td><p><code>String</code></p> <p>必需</p> </td>
     <td>元素的内部名称；对于片段类型必须是唯一的。</td>
    </tr>
   </tbody>
  </table>

* **变体**

   <table>
   <tbody>
    <tr>
     <th>名称</th>
     <th>类型</th>
     <th>价值</th>
    </tr>
    <tr>
     <td><code>variations</code> </td>
     <td><p><code>nt:unstructured</code></p> <p>可选</p> </td>
     <td>此可选节点包含内容片段的初始变体的定义。</td>
    </tr>
   </tbody>
  </table>

* **变量名称**

   <table>
   <tbody>
    <tr>
     <th>名称</th>
     <th>类型</th>
     <th>价值</th>
    </tr>
    <tr>
     <td><code>&lt;<i>variation-name</i>&gt;</code> </td>
     <td><p><code>nt:unstructured</code></p> <p>如果存在变体节点，则此为必填项</p> </td>
     <td><p>定义初始变量。<br /> 默认情况下，该变量会添加到内容片段的所有元素中。</p> <p>变体将具有与相应元素相同的初始内容(请参阅 <code class="code">defaultContent/
       initialContentType</code>)</p> </td>
    </tr>
    <tr>
     <td><code>jcr:title</code></td>
     <td><p><code>String</code></p> <p>必需</p> </td>
     <td>变体的标题(显示在片段编辑器的 <strong>变量</strong> 选项卡（左边栏）。</td>
    </tr>
    <tr>
     <td><code>jcr:desciption</code></td>
     <td><p><code>String</code></p> <p>可选</p> <p>默认: ""</p> </td>
     <td>提供变体说明的文本 <span>(显示在片段编辑器的 <strong>变量</strong> 选项卡（左边栏）。</code></td>
    </tr>
   </tbody>
  </table>
