---
title: 内容片段模板
seo-title: 内容片段模板
description: 在创建内容片段时选择模板，并为新片段提供基本结构、元素和变量
seo-description: 在创建内容片段时选择模板，并为新片段提供基本结构、元素和变量
uuid: d147bac8-b710-40ed-9664-decb5ffcf8e7
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: a975ea2e-5e24-4a96-bd62-63bb98836ff2
docset: aem65
translation-type: tm+mt
source-git-commit: a430c4de89bde3b907d342106465d3b5a7c75cc8
workflow-type: tm+mt
source-wordcount: '644'
ht-degree: 3%

---


# 内容片段模板{#content-fragment-templates}

>[!CAUTION]
>
>[现在建议使用](/help/assets/content-fragments/content-fragments-models.md) “内容片段模型”来创建您的所有片段。
>
>内容片段模型用于We.Retail中的所有示例。

创建内容片段时，将选择模板。 它们为新片段提供了基本结构、元素和变异。 用于内容片段的模板受Granite Configuration Manager约束。

现成的模板位于：

* `/libs/settings/dam/cfm/templates`

您可以在以下位置为内容片段创建站点特定模板：

* `/apps/settings/dam/cfm/templates`
用于覆盖现成模板或提供客户特定、应用程序范围的模板的位置，这些模板在运行时不打算扩展／更改。

* `/conf/global/settings/dam/cfm/templates`
需要在运行时更改的实例范围客户特定模板的位置。

优先顺序为（降序） `/conf`, `/apps`、 `/libs`。

>[!CAUTION]
>
>您 ***不得*** 更改路径中的任 `/libs` 何内容。
>
>这是因为下次升级实 `/libs` 例时，内容会被覆盖（而应用修补程序或功能包时，内容很可能会被覆盖）。
>
>建议的配置和其他更改方法是：
>
>1. 在下面重新创建所需的项(即，当它存在 `/libs`时) `/apps`
   >
   >
1. 在 `/apps`

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

有关节点及其属性的更多详细信息：

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
     <td>此节点是每个模板的根节点。 它是必填的，应具有唯一的名称。</td>
    </tr>
    <tr>
     <td><code>jcr:title</code></td>
     <td><p><code>String</code></p> <p>required<br /> </p> </td>
     <td>模板的标题(在创建片段向 <strong>导中显示</strong> )。</td>
    </tr>
    <tr>
     <td><code>jcr:description</code></td>
     <td><p><code>String</code></p> <p>可选</p> </td>
     <td>描述模板用途的文本(在创建片段向导 <strong>中显示</strong> )。</td>
    </tr>
    <tr>
     <td><code>initialAssociatedContent</code></td>
     <td><p><code>String[]</code></p> <p>可选</p> </td>
     <td>默认情况下，具有与新创建的内容片段关联的集合路径的数组。</td>
    </tr>
    <tr>
     <td><code>precreateElements</code></td>
     <td><p><code>Boolean</code></p> <p>必需</p> </td>
     <td><p><code>true</code>，如果应在创建内容片段时创建表示内容片段的元素（主元素除外）的子资产； <em>假</em> ，如果应“迅速”创建它们。</p> <p><strong>注意</strong>: 当前，此参数必须设置为 <code>true</code>。</p> </td>
    </tr>
    <tr>
     <td><code>version</code></td>
     <td><p><code>Long</code></p> <p>必需</p> </td>
     <td><p>内容结构的版本； 当前支持：</p> <p><strong>注意</strong>: 当前，此参数必须设置为 <code>2</code>。<br /> </p> </td>
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
     <td><p>包含内容片段元素定义的节点。 它是必需的，并且需要至少包含一个Main元素 <strong>的子节</strong> 点，但可以包含[1...n]子节点。</p> <p>当使用模板时，元素子分支被复制到片段的模型子分支。</p> <p>第一个元素（如CRXDE Lite中所述）自动被视为主 <i>要元</i> 素； 节点名称无关，节点本身除以主资产代表外，没有特殊意义； 其他元素将作为子资产处理。</p> </td>
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
     <td>此节点定义元素。 它是必填的，应具有唯一的名称。</td>
    </tr>
    <tr>
     <td><code>jcr:title</code></td>
     <td><p><code>String</code></p> <p>必需</p> </td>
     <td>元素的标题（显示在片段编辑器的元素选择器中）。</td>
    </tr>
    <tr>
     <td><code>defaultContent</code></td>
     <td><p><code>String</code></p> <p>可选</p> <p>默认: ""</p> </td>
     <td>元素的初始内容； 仅在=时 <code>precreateElements</code><i> 使用 </i><code>true</code></td>
    </tr>
    <tr>
     <td><code>initialContentType</code></td>
     <td><p><code>String</code></p> <p>可选</p> <p>默认: <code>text/html</code></p> </td>
     <td><p>元素的初始内容类型； 仅当= <code>precreateElements</code><i> 时使 </i><code>true</code>用； 当前支持：</p>
      <ul>
       <li><code>text/html</code></li>
       <li><code>text/plain</code></li>
       <li><code>text/x-markdown</code></li>
      </ul> </td>
    </tr>
    <tr>
     <td><code>name</code></td>
     <td><p><code>String</code></p> <p>必需</p> </td>
     <td>元素的内部名称； 必须为片段类型唯一。</td>
    </tr>
   </tbody>
  </table>

* **变量**

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
     <td><p><code>nt:unstructured</code></p> <p>变量节点存在时必需</p> </td>
     <td><p>定义初始变量。<br /> 默认情况下，变体会添加到内容片段的所有元素。</p> <p>变体的初始内容将与相应元素相同(请参阅 <code class="code">defaultContent/
       initialContentType</code>)</p> </td>
    </tr>
    <tr>
     <td><code>jcr:title</code></td>
     <td><p><code>String</code></p> <p>必需</p> </td>
     <td>变体的标题(在片段编辑器的“变体”选 <strong>项卡</strong> （左边栏）中显示。</td>
    </tr>
    <tr>
     <td><code>jcr:desciption</code></td>
     <td><p><code>String</code></p> <p>可选</p> <p>默认: ""</p> </td>
     <td>提供变体描述的文本(在片 <span>段编辑器的“变 <strong>体</strong> ”选项卡（左边栏）中显示。</code></td>
    </tr>
   </tbody>
  </table>
