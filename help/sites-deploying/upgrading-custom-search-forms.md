---
title: 升级自定义搜索Forms
seo-title: 升级自定义搜索Forms
description: 本文详细介绍了升级后需要进行的调整，以使自定义搜索表单正常工作。
seo-description: 本文详细介绍了升级后需要进行的调整，以使自定义搜索表单正常工作。
uuid: 35b8fbb9-5951-4e1c-bf04-4471a55b9cb0
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
discoiquuid: a08cee9c-e981-4483-8bdc-e6353977f854
feature: Upgrading
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1710'
ht-degree: 3%

---


# 升级自定义搜索Forms{#upgrading-custom-search-forms}

在AEM 6.2中，自定义搜索Forms存储在存储库中的位置已更改。 升级后，它们将从6.1中的位置移至：

* /apps/cq/gui/content/facets

到新位置：

* /conf/global/settings/cq/search/facets

因此，升级后需要手动调整，表单才能继续运行。

这适用于新的搜索Forms以及已自定义的默认Forms。

有关详细信息，请参阅[搜索彩块化](/help/assets/search-facets.md)的相关文档。

## 更改resourceType属性{#changing-the-resourcetype-property}

除非另有说明，否则在升级后需要完成的大多数调整都需要更改已配置的自定义搜索Forms的`sling:resourceType`属性。 这是必需的，以便属性指向渲染脚本的正确位置。

您可以通过执行以下操作来更改属性：

1. 转到`https://server:port/crx/de/index.jsp`打开CRXDE Lite
1. 浏览到需要调整的节点的位置，如下面[自定义搜索Forms](/help/sites-deploying/upgrading-custom-search-forms.md#list-of-custom-search-forms)列表中所指定。
1. 单击节点。 在右侧属性窗格中，单击并修改&#x200B;**sling:resourceType**&#x200B;属性。
1. 最后，按&#x200B;**全部保存**&#x200B;按钮保存更改。

## 列表自定义搜索Forms {#list-of-custom-search-forms}

在下面，您将找到所有自定义搜索Forms的列表，以及升级后需要进行的修改。 它们引用`/conf/global/settings/cq/search/facets/sites/items`中的名称。

### 全文谓词，节点名为&quot;fulltext&quot; {#fulltext-predicate-with-node-name-fulltext}

<table>
 <tbody>
  <tr>
   <td>6.1中默认搜索表单中的节点</td>
   <td>全文</td>
  </tr>
  <tr>
   <td><p>6.1中的资源类型</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/search谓词/fulltextpredicates</p> </td>
  </tr>
  <tr>
   <td>6.2中的资源类型</td>
   <td>不适用</td>
  </tr>
 </tbody>
</table>

在AEM 6.1中，标准全文谓词是搜索表单的一部分。 在6.2中，全文字段已替换为OmniSearch。 此谓词会以编程方式跳过，并且可以删除。

**操作：** 完全删除节点。

### 其他全文谓词{#other-fulltext-predicates}

<table>
 <tbody>
  <tr>
   <td>在6.1中默认搜索自中的节点</td>
   <td>不适用</td>
  </tr>
  <tr>
   <td><p>6.1中的资源类型</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/search谓词/fulltextpredicates</p> </td>
  </tr>
  <tr>
   <td>6.2中的资源类型</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/search谓词/fulltextpredicates</p> </td>
  </tr>
 </tbody>
</table>

**操作：** 调整 `resourceType` 属性(添加“**/coral**”，如上面指示的6.2位置)。

### 路径浏览器谓词{#path-browser-predicates}

<table>
 <tbody>
  <tr>
   <td>6.1<br /> <br />中默认搜索表单中的节点/秒 </td>
   <td>路径</td>
  </tr>
  <tr>
   <td><p>6.1中的资源类型</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/search谓词/path谓词</p> </td>
  </tr>
  <tr>
   <td>6.2中的资源类型</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/search谓词/pathpredicates</p> </td>
  </tr>
 </tbody>
</table>

**操作：** 调整 `resourceType` 属性(添加“**/coral**”，如上面指示的6.2位置)。

### 标记谓词{#tags-predicates}

<table>
 <tbody>
  <tr>
   <td>6.1<br /> <br />中默认搜索表单中的节点/秒 </td>
   <td>标记</td>
  </tr>
  <tr>
   <td><p>6.1中的资源类型</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/search谓词/tagspredicate</p> </td>
  </tr>
  <tr>
   <td>6.2中的资源类型</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/search谓词/tagspredicates/tagspredicate</p> </td>
  </tr>
 </tbody>
</table>

**操作：** 调整 **** resourceTypeproperty(添加“**/coral**”，如上面指示的6.2位置)。

### 页面状态谓词 {#page-status-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1<br /> <br />中默认搜索表单中的节点/秒 </td>
   <td>pagestatus谓词</td>
  </tr>
  <tr>
   <td><p>6.1中的资源类型</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/search谓词/pagestatus谓词</p> </td>
  </tr>
  <tr>
   <td>6.2中的资源类型</td>
   <td>不适用</td>
  </tr>
 </tbody>
</table>

页面状态已替换为两个选项属性谓词，一个用于发布，一个用于LiveCopy状态。

**操作:**

* 删除`pagestatuspredicate`节点
* 复制节点

   * `/libs/settings/cq/search/facets/sites/jcr:content/items/publishstatuspredicate`
   * 到 `/conf/global/settings/cq/search/facets/sites/jcr:content/items`

* 复制节点

   * `/libs/settings/cq/search/facets/sites/jcr:content/items/livecopystatuspredicate`
   * 到 `/conf/global/settings/cq/search/facets/sites/jcr:content/items`

* 确保将`analyticspredicate`节点的`listOrder`属性设置为“**8**”。 为避免冲突，必须这样做。

### 日期范围谓词{#date-range-predicates}

<table>
 <tbody>
  <tr>
   <td>6.1<br /> <br />中默认搜索表单中的节点/秒 </td>
   <td>达特兰治谓词</td>
  </tr>
  <tr>
   <td>6.1中的资源类型</td>
   <td>cq/gui/components/common/admin/customsearch/search谓词/daterangepredicate</td>
  </tr>
  <tr>
   <td>6.2中的资源类型</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/search谓词/daterangepredicates</p> </td>
  </tr>
 </tbody>
</table>

**操作：** 调整 `resourceType` 属性(添加“**/coral**”，如上面指示的6.2位置)。

### 隐藏的筛选器 {#hidden-filter}

<table>
 <tbody>
  <tr>
   <td>6.1<br /> <br />中默认搜索表单中的节点/秒 </td>
   <td>类型</td>
  </tr>
  <tr>
   <td><p>6.1中的资源类型</p> </td>
   <td><p>granite/ui/components/foundation/form/hidden</p> </td>
  </tr>
  <tr>
   <td>6.2中的资源类型</td>
   <td><p>granite/ui/components/foundation/form/hidden</p> </td>
  </tr>
 </tbody>
</table>

**操作：** 无需调整。

### 分析谓词 {#analytics-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1<br /> <br />中默认搜索表单中的节点/秒 </td>
   <td>分析</td>
  </tr>
  <tr>
   <td><p>6.1中的资源类型</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/search谓词/analyticsspecredicates</p> </td>
  </tr>
  <tr>
   <td>6.2中的资源类型</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/search谓词/analyticsspredicates</p> </td>
  </tr>
 </tbody>
</table>

**操作：** 调整 `resourceType` 属性(添加“**/coral**”，如上面指示的6.2位置)。

### 范围谓词 {#range-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1<br /> <br />中默认搜索表单中的节点/秒 </td>
   <td>不适用</td>
  </tr>
  <tr>
   <td><p>6.1中的资源类型</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/search谓词/rangepredicate</p> </td>
  </tr>
  <tr>
   <td>6.2中的资源类型</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/search谓词/rangepredicate</p> </td>
  </tr>
 </tbody>
</table>

**操作：** 调整 `resourceType` 属性(添加“**/coral**”，如上面指示的6.2位置)。

>[!NOTE]
>
>注意：与6.1相反，范围谓词不再在搜索栏中呈现标记。

### 选项属性谓词 {#options-property-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1<br /> <br />中默认搜索表单中的节点/秒 </td>
   <td>不适用</td>
  </tr>
  <tr>
   <td><p>6.1中的资源类型</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/search谓词/选项</p> </td>
  </tr>
  <tr>
   <td>6.2中的资源类型</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/search谓词/optionspredicates</p> </td>
  </tr>
 </tbody>
</table>

**操作：** 调整 `resourceType` 属性(添加“**/coral**”，如上面指示的6.2位置)。

### 滑块范围谓词 {#slider-range-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1<br /> <br />中默认搜索表单中的节点/秒 </td>
   <td>不适用</td>
  </tr>
  <tr>
   <td><p>6.1中的资源类型</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/search谓词/sliderrange谓词</p> </td>
  </tr>
  <tr>
   <td>6.2中的资源类型</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/search谓词/sliderrange谓词</p> </td>
  </tr>
 </tbody>
</table>

**操作：** 调整 `resourceType` 属性(添加“**/coral**”，如上面指示的6.2位置)。

### 组件谓词 {#components-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1<br /> <br />中默认搜索表单中的节点/秒 </td>
   <td>不适用</td>
  </tr>
  <tr>
   <td><p>6.1中的资源类型</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/search谓词/componentspredicate</p> </td>
  </tr>
  <tr>
   <td>6.2中的资源类型</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/search谓词/componentspredicates</p> </td>
  </tr>
 </tbody>
</table>

**操作：** 调整 `resourceType` 属性(添加“**/coral**”，如上面指示的6.2位置)。

### 作者谓词 {#author-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1<br /> <br />中默认搜索表单中的节点/秒 </td>
   <td>不适用</td>
  </tr>
  <tr>
   <td><p>6.1中的资源类型</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/search谓词/userpredicates</p> </td>
  </tr>
  <tr>
   <td>6.2中的资源类型</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/search谓词/userpredicates</p> </td>
  </tr>
 </tbody>
</table>

**操作：** 调整 `resourceType` 属性(添加“**/coral**”，如上面指示的6.2位置)。

### 模板谓词 {#templates-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1<br /> <br />中默认搜索表单中的节点/秒 </td>
   <td>不适用</td>
  </tr>
  <tr>
   <td><p>6.1中的资源类型</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/search谓词/templatespredicate</p> </td>
  </tr>
  <tr>
   <td>6.2中的资源类型</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/search谓词/templatespredicates</p> </td>
  </tr>
 </tbody>
</table>

**操作：** 调整 `resourceType` 属性(添加“**/coral**”，如上面指示的6.2位置)。

## 资产管理员搜索边栏 {#assets-admin-search-rail}

以下节点引用`/conf/global/settings/dam/search/facets/assets/items`中的名称

### 全文谓词，节点名为&quot;fulltext&quot; {#fulltext-predicate-with-node-name-fulltext-1}

| 6.1中默认搜索表单中的节点 | 全文 |
|---|---|
| 6.1中的资源类型 | dam/gui/components/admin/customsearch/search谓词/fulltextpredicate |
| 6.2中的资源类型 | 不适用 |

在6.1中，标准全文谓词是搜索表单的一部分。 在6.2中，全文字段已替换为OmniSearch。 此谓词会以编程方式跳过，并且可以删除。

**操作：** 删除上述节点。

### 路径浏览器谓词{#path-browser-predicates-1}

| 6.1中默认搜索表单中的节点 | 路径浏览器 |
|---|---|
| 6.1中的资源类型 | dam/gui/components/admin/customsearch/search谓词/pathbrowser谓词 |
| 6.2中的资源类型 | dam/gui/coral/components/admin/customsearch/search谓词/pathbrowser谓词 |

**操作：** 调整 `resourceType` 属性(添加“**/coral**”，如上面指示的6.2位置)。

### MIME类型谓词{#mime-type-predicates}

| 6.1中默认搜索表单中的节点 | mimetype |
|---|---|
| 6.1中的资源类型 | dam/gui/components/admin/customsearch/search谓词/选项 |
| 6.2中的资源类型 | dam/gui/coral/components/admin/customsearch/search谓词/选项 |

**操作：** 调整 `resourceType` 属性(添加“**/coral**”，如上面指示的6.2位置)。

### 文件大小谓词{#file-size-predicates}

| 6.1中默认搜索表单中的节点 | 文件大小 |
|---|---|
| 6.1中的资源类型 | dam/gui/components/admin/customsearch/search谓词/filesizepredicate |
| 6.2中的资源类型 | dam/gui/coral/components/admin/customsearch/search谓词/sliange谓词 |

**操作：** 按 `resourceType` 上面6.2位置中所示进行调整。

### 资产上次修改时间谓词{#asset-last-modified-predicates}

| 6.1中默认搜索表单中的节点 | assetlastmodified谓词 |
|---|---|
| 6.1中的资源类型 | dam/gui/components/admin/customsearch/search谓词/assetlastmodified谓词 |
| 6.2中的资源类型 | dam/gui/coral/components/admin/customsearch/search谓词/assetlastmodified谓词 |

操作：调整resourceType属性（添加“/coral”，如上面所示的6.2位置）。

### 发布谓词{#publish-predicate}

| 6.1中默认搜索表单中的节点 | 发布 |
|---|---|
| 6.1中的资源类型 | dam/gui/components/admin/customsearch/search谓词/publishpredicate |
| 6.2中的资源类型 | dam/gui/coral/components/admin/customsearch/search谓词/publishpredicate |

**操作:**

* 调整`resourceType`属性（添加&quot;**/coral**&quot;，如上面所示的6.2位置）

* 添加一个`optionPaths`（String类型）属性，其值为：`/libs/dam/options/predicates/publish`

* 添加具有布尔值`true`的`singleSelect`属性。

### 状态谓词{#status-predicates}

| 6.1中默认搜索表单中的节点 | 状态 |
|---|---|
| 6.1中的资源类型 | dam/gui/components/admin/customsearch/search谓词/选项 |
| 6.2中的资源类型 | dam/gui/coral/components/admin/customsearch/search谓词/选项 |

**操作：** 调整 `resourceType` 属性(添加“**/coral**”，如上面指示的6.2位置)

### 到期状态谓词{#expiry-status-predicates}

| 6.1中默认搜索表单中的节点 | 过期状态 |
|---|---|
| 6.1中的资源类型 | dam/gui/components/admin/customsearch/search谓词/expiredassetpredicate |
| 6.2中的资源类型 | dam/gui/coral/components/admin/customsearch/search谓词/expiredassetpredicate |

**操作：** 调整 `resourceType` 属性(添加“**/coral**”，如上面指示的6.2位置)

### 元数据有效性谓词{#metadata-validity-predicates}

| 6.1中默认搜索表单中的节点 | 元数据有效性 |
|---|---|
| 6.1中的资源类型 | dam/gui/components/admin/customsearch/search谓词/选项 |
| 6.2中的资源类型 | dam/gui/coral/components/admin/customsearch/search谓词/选项 |

**操作：** 调整 `resourceType` 属性(添加“**/coral**”，如上面指示的6.2位置)

### 评级谓词{#rating-predicates}

| 6.1中默认搜索表单中的节点 | 评级 |
|---|---|
| 6.1中的资源类型 | dam/gui/components/admin/customsearch/search谓词/rating谓词 |
| 6.2中的资源类型 | dam/gui/coral/components/admin/customsearch/search谓词/sliange谓词 |

**操作：** 调整 `resourceType` 属性(添加“**/coral**”，如上面指示的6.2位置)

### 方向谓词{#orientation-predicate}

| 6.1中默认搜索表单中的节点 | 方向 |
|---|---|
| 6.1中的资源类型 | dam/gui/components/admin/customsearch/search谓词/tagfilterpredicate |
| 6.2中的资源类型 | cq/gui/components/coral/common/admin/customsearch/search谓词/tagspredicates |

**操作:**

* 调整`resourceType`属性（添加&quot;**/coral**&quot;，如上面所示的6.2位置）

* 添加一个`fieldLabel`属性，该属性与同一节点上的`text`属性具有相同的值。

* 添加一个`emptyText`属性，其值与同一节点上的`text`属性相同。

* 添加与同一节点上的`optionPaths`属性具有相同值的`rootPath`属性。

### 样式谓词{#style-predicate}

| 6.1中默认搜索表单中的节点 | 样式 |
|---|---|
| 6.1中的资源类型 | dam/gui/components/admin/customsearch/search谓词/tagfilterpredicate |
| 6.2中的资源类型 | cq/gui/components/coral/common/admin/customsearch/search谓词/tagspredicates |

**操作:**

* 调整`resourceType`属性（添加&quot;**/coral**&quot;，如上面所示的6.2位置）

* 添加一个`fieldLabel`属性，该属性与同一节点上的`text`属性具有相同的值。

* 添加一个`emptyText`属性，其值与同一节点上的`text`属性相同。

* 添加与同一节点上的`optionPaths`属性具有相同值的`rootPath`属性。

### 视频格式谓词{#video-format-predicates}

| 6.1中默认搜索表单中的节点 | videoFormat |
|---|---|
| 6.1中的资源类型 | dam/gui/components/admin/customsearch/search谓词/选项 |
| 6.2中的资源类型 | dam/gui/coral/components/admin/customsearch/search谓词/选项 |

**操作：** 调整 `resourceType` 属性(添加“**/coral**”，如上面指示的6.2位置)

### 主资产谓词{#mainasset-predicate}

| 6.1中默认搜索表单中的节点 | mainasset |
|---|---|
| 6.1中的资源类型 | granite/ui/components/foundation/form/hidden |
| 6.2中的资源类型 | granite/ui/components/coral/foundation/form/hidden |

**操作：** 调整 `resourceType` 属性(添加“**/coral**”，如上面指示的6.2位置)
