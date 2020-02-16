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
source-git-commit: 0dc96f07e45ccbfea4edc87431677ada5b1bfa8c

---


# 内容片段模板{#content-fragment-templates}

>[!CAUTION]
>
>[现在建议使用内容片段模型](/help/assets/content-fragments-models.md) ，以创建您的所有片段。
>
>内容片段模型用于We.Retail中的所有示例。

在创建内容片段时，将选择模板。 它们为新片段提供了基本结构、元素和变量。 用于内容片段的模板受Granite Configuration manager约束。

现成模板位于以下位置：

* `/libs/settings/dam/cfm/templates`

您可以在以下位置为内容片段创建站点特定的模板：

* `/apps/settings/dam/cfm/templates`
覆盖现成模板或提供客户特定、应用程序范围的模板的位置，这些模板在运行时不会扩展／更改。

* `/conf/global/settings/dam/cfm/templates`
需要在运行时更改的实例范围客户特定模板的位置。

优先级顺序为（降序） `/conf`、 `/apps`、 `/libs`。

>[!CAUTION]
>
>您 ***不得*** 更改路径中的任 `/libs` 何内容。
>
>这是因为下次升级实 `/libs` 例时，将覆盖其内容（而应用修补程序或功能包时，很可能会覆盖该内容）。
>
>建议的配置和其他更改方法是：
>
>1. 在下面重新创建所需的项目(即，它存在于 `/libs`中) `/apps`
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
     <td>此节点是每个模板的根节点。 它是必填的，并且应具有唯一的名称。</td>
    </tr>
    <tr>
     <td><code>jcr:title</code></td>
     <td><p><code>String</code></p> <p>required<br /> </p> </td>
     <td>模板的标题(显示在创建片段 <strong>向导中</strong> )。</td>
    </tr>
    <tr>
     <td><code>jcr:description</code></td>
     <td><p><code>String</code></p> <p>可选</p> </td>
     <td>描述模板用途的文本(显示在创建片段 <strong>向导中</strong> )。</td>
    </tr>
    <tr>
     <td><code>initialAssociatedContent</code></td>
     <td><p><code>String[]</code></p> <p>可选</p> </td>
     <td>默认情况下，具有指向集合的路径的数组，该集合应该与新创建的内容片段相关联。</td>
    </tr>
    <tr>
     <td><code>precreateElements</code></td>
     <td><p><code>Boolean</code></p> <p>必需</p> </td>
     <td><p><code>true</code>, if the subassets sepresents the elements(master elements)of the content fragment is created when the content fragment;如 <em></em> 果应“即时”创建它们，则为false。</p> <p><strong>注意</strong>:当前，此参数必须设置为 <code>true</code>。</p> </td>
    </tr>
    <tr>
     <td><code>version</code></td>
     <td><p><code>Long</code></p> <p>必需</p> </td>
     <td><p>内容结构的版本；当前支持：</p> <p><strong>注意</strong>:当前，此参数必须设置为 <code>2</code>。<br /> </p> </td>
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
     <td><p>包含内容片段元素定义的节点。 它是必需的，并且对于 <strong>Main</strong> 元素至少需要包含一个子节点，但可以包含[1...n]子节点。</p> <p>当使用模板时，元素子分支被复制到片段的模型子分支。</p> <p>第一个元素（如CRXDE Lite中所述）自动被视为主 <i>要元</i> 素；节点名称不相关，节点本身除以主资产表示外，没有特殊意义；其他元素将作为子资产处理。</p> </td>
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
     <td>此节点定义元素。 它是必填的，并且应具有唯一的名称。</td>
    </tr>
    <tr>
     <td><code>jcr:title</code></td>
     <td><p><code>String</code></p> <p>必需</p> </td>
     <td>元素的标题（显示在片段编辑器的元素选择器中）。</td>
    </tr>
    <tr>
     <td><code>defaultContent</code></td>
     <td><p><code>String</code></p> <p>可选</p> <p>默认: ""</p> </td>
     <td>元素的初始内容；仅在 <code>precreateElements</code><i> =时使用 </i><code>true</code></td>
    </tr>
    <tr>
     <td><code>initialContentType</code></td>
     <td><p><code>String</code></p> <p>可选</p> <p>默认: <code>text/html</code></p> </td>
     <td><p>元素的初始内容类型；仅在 <code>precreateElements</code><i> =时使 </i><code>true</code>用；当前支持：</p>
      <ul>
       <li><code>text/html</code></li>
       <li><code>text/plain</code></li>
       <li><code>text/x-markdown</code></li>
      </ul> </td>
    </tr>
    <tr>
     <td><code>name</code></td>
     <td><p><code>String</code></p> <p>必需</p> </td>
     <td>元素的内部名称；对于片段类型，必须是唯一的。</td>
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
     <td>此可选节点包含内容片段的初始变体的定义。</td>
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
     <td><p>定义初始变量。<br /> 默认情况下，变量会添加到内容片段的所有元素。</p> <p>变体的初始内容将与相应元素具有相同的内容(请参阅 <code class="code">defaultContent/
       initialContentType</code>)</p> </td>
    </tr>
    <tr>
     <td><code>jcr:title</code></td>
     <td><p><code>String</code></p> <p>必需</p> </td>
     <td>变量的标题(显示在片段编辑器的“变 <strong>量</strong> ”选项卡（左边栏）中)。</td>
    </tr>
    <tr>
     <td><code>jcr:desciption</code></td>
     <td><p><code>String</code></p> <p>可选</p> <p>默认: ""</p> </td>
     <td>提供变量描述的文本(显 <span>示在片段编辑器的“变 <strong>量</strong> ”选项卡（左边栏）中)。</code></td>
    </tr>
   </tbody>
  </table>
