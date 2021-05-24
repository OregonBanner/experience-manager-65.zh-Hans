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
feature: 升级
exl-id: 797bbdf9-917a-4537-a5f9-bf2682db968b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1710'
ht-degree: 3%

---

# 升级自定义搜索Forms{#upgrading-custom-search-forms}

在AEM 6.2中，自定义搜索Forms存储在存储库中的位置已发生更改。 升级后，这些用户将从6.1中的位置(:

* /apps/cq/gui/content/facets

到下方的新位置：

* /conf/global/settings/cq/search/facets

因此，升级后需要手动调整，以使表单继续正常运行。

这适用于新的搜索Forms以及已自定义的默认Forms。

有关更多信息，请参阅[搜索彩块化](/help/assets/search-facets.md)文档。

## 更改resourceType属性{#changing-the-resourcetype-property}

除非另有说明，否则在升级后需要完成的大多数调整都需要更改已配置的自定义搜索Forms的`sling:resourceType`属性。 这是必需的，以便属性指向渲染脚本的正确位置。

您可以通过执行以下操作来更改资产：

1. 通过转到`https://server:port/crx/de/index.jsp`打开CRXDE Lite
1. 按照下面[自定义搜索Forms](/help/sites-deploying/upgrading-custom-search-forms.md#list-of-custom-search-forms)列表中的指定，浏览到需要调整的节点的位置。
1. 单击节点。 在右侧的属性窗格中，单击并修改&#x200B;**sling:resourceType**&#x200B;属性。
1. 最后，按&#x200B;**Save All**&#x200B;按钮保存更改。

## 自定义搜索Forms {#list-of-custom-search-forms}列表

在下面，您将找到所有自定义搜索Forms以及升级后所需修改的列表。 它们引用`/conf/global/settings/cq/search/facets/sites/items`中的名称。

### 节点名为“fulltext” {#fulltext-predicate-with-node-name-fulltext}的全文谓词

<table>
 <tbody>
  <tr>
   <td>6.1中默认搜索表单中的节点</td>
   <td>全文</td>
  </tr>
  <tr>
   <td><p>6.1中的资源类型</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/searchpredicates/fulltextpredicates</p> </td>
  </tr>
  <tr>
   <td>6.2中的资源类型</td>
   <td>不适用</td>
  </tr>
 </tbody>
</table>

在AEM 6.1中，标准全文谓词是搜索表单的一部分。 在6.2中，全文字段已被OmniSearch替换。 此谓词以编程方式跳过，可以删除。

**操作：** 完全删除节点。

### 其他全文谓词{#other-fulltext-predicates}

<table>
 <tbody>
  <tr>
   <td>6.1中默认搜索范围中的节点</td>
   <td>不适用</td>
  </tr>
  <tr>
   <td><p>6.1中的资源类型</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/searchpredicates/fulltextpredicates</p> </td>
  </tr>
  <tr>
   <td>6.2中的资源类型</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/searchpredicates/fulltextpredicates</p> </td>
  </tr>
 </tbody>
</table>

**操作：** 调整 `resourceType` 属性(添加“**/coral**”，如上面所示的位置6.2中所示)。

### 路径浏览器谓词{#path-browser-predicates}

<table>
 <tbody>
  <tr>
   <td>6.1<br /> <br />中默认搜索表单中的节点 </td>
   <td>路径</td>
  </tr>
  <tr>
   <td><p>6.1中的资源类型</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/search谓词/pathpredicate</p> </td>
  </tr>
  <tr>
   <td>6.2中的资源类型</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/search谓词/pathpredicate</p> </td>
  </tr>
 </tbody>
</table>

**操作：** 调整 `resourceType` 属性(添加“**/coral**”，如上面所示的位置6.2中所示)。

### 标记谓词{#tags-predicates}

<table>
 <tbody>
  <tr>
   <td>6.1<br /> <br />中默认搜索表单中的节点 </td>
   <td>标记</td>
  </tr>
  <tr>
   <td><p>6.1中的资源类型</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/search谓词/tagspredicate</p> </td>
  </tr>
  <tr>
   <td>6.2中的资源类型</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/search谓词/tagspredicates</p> </td>
  </tr>
 </tbody>
</table>

**操作：** 调整 **** resourceTypeproperty(添加“**/coral**”，如上面所示的6.2位置中所示)。

### 页面状态谓词 {#page-status-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1<br /> <br />中默认搜索表单中的节点 </td>
   <td>pagestatus谓词</td>
  </tr>
  <tr>
   <td><p>6.1中的资源类型</p> </td>
   <td><p>cq/gui/components/siteadmin/searchpanel/search谓词/pagestatus谓词</p> </td>
  </tr>
  <tr>
   <td>6.2中的资源类型</td>
   <td>不适用</td>
  </tr>
 </tbody>
</table>

“页面状态”已被两个“选项属性”谓词替换，一个用于发布，一个用于LiveCopy状态。

**操作:**

* 删除`pagestatuspredicate`节点
* 复制节点

   * `/libs/settings/cq/search/facets/sites/jcr:content/items/publishstatuspredicate`
   * 到 `/conf/global/settings/cq/search/facets/sites/jcr:content/items`

* 复制节点

   * `/libs/settings/cq/search/facets/sites/jcr:content/items/livecopystatuspredicate`
   * 到 `/conf/global/settings/cq/search/facets/sites/jcr:content/items`

* 确保将`analyticspredicate`节点的`listOrder`属性设置为“**8**”。 为避免冲突，需要此功能。

### 日期范围谓词{#date-range-predicates}

<table>
 <tbody>
  <tr>
   <td>6.1<br /> <br />中默认搜索表单中的节点 </td>
   <td>daterange谓词</td>
  </tr>
  <tr>
   <td>6.1中的资源类型</td>
   <td>cq/gui/components/common/admin/customsearch/search谓词/daterangepredicate</td>
  </tr>
  <tr>
   <td>6.2中的资源类型</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/search谓词/daterange谓词</p> </td>
  </tr>
 </tbody>
</table>

**操作：** 调整 `resourceType` 属性(添加“**/coral**”，如上面所示的位置6.2中所示)。

### 隐藏的筛选器 {#hidden-filter}

<table>
 <tbody>
  <tr>
   <td>6.1<br /> <br />中默认搜索表单中的节点 </td>
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
   <td>6.1<br /> <br />中默认搜索表单中的节点 </td>
   <td>分析</td>
  </tr>
  <tr>
   <td><p>6.1中的资源类型</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/analyticspredicate</p> </td>
  </tr>
  <tr>
   <td>6.2中的资源类型</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/analyticspredicates</p> </td>
  </tr>
 </tbody>
</table>

**操作：** 调整 `resourceType` 属性(添加“**/coral**”，如上面所示的位置6.2中所示)。

### 范围谓词 {#range-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1<br /> <br />中默认搜索表单中的节点 </td>
   <td>不适用</td>
  </tr>
  <tr>
   <td><p>6.1中的资源类型</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/rangrepade</p> </td>
  </tr>
  <tr>
   <td>6.2中的资源类型</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/rangrepadice</p> </td>
  </tr>
 </tbody>
</table>

**操作：** 调整 `resourceType` 属性(添加“**/coral**”，如上面所示的位置6.2中所示)。

>[!NOTE]
>
>注意：与6.1相反，范围谓词不再在搜索栏中呈现标记。

### 选项属性谓词 {#options-property-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1<br /> <br />中默认搜索表单中的节点 </td>
   <td>不适用</td>
  </tr>
  <tr>
   <td><p>6.1中的资源类型</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/optionsspredication</p> </td>
  </tr>
  <tr>
   <td>6.2中的资源类型</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/optionsspredicates</p> </td>
  </tr>
 </tbody>
</table>

**操作：** 调整 `resourceType` 属性(添加“**/coral**”，如上面所示的位置6.2中所示)。

### 滑块范围谓词 {#slider-range-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1<br /> <br />中默认搜索表单中的节点 </td>
   <td>不适用</td>
  </tr>
  <tr>
   <td><p>6.1中的资源类型</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/sliderrangeprediate</p> </td>
  </tr>
  <tr>
   <td>6.2中的资源类型</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/sliderrangeprediate</p> </td>
  </tr>
 </tbody>
</table>

**操作：** 调整 `resourceType` 属性(添加“**/coral**”，如上面所示的位置6.2中所示)。

### 组件谓词 {#components-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1<br /> <br />中默认搜索表单中的节点 </td>
   <td>不适用</td>
  </tr>
  <tr>
   <td><p>6.1中的资源类型</p> </td>
   <td><p>cq/gui/components/siteadmin/searchpanel/searchpredicates/componentsspredicate</p> </td>
  </tr>
  <tr>
   <td>6.2中的资源类型</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/componentsspredicates</p> </td>
  </tr>
 </tbody>
</table>

**操作：** 调整 `resourceType` 属性(添加“**/coral**”，如上面所示的位置6.2中所示)。

### 作者谓词 {#author-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1<br /> <br />中默认搜索表单中的节点 </td>
   <td>不适用</td>
  </tr>
  <tr>
   <td><p>6.1中的资源类型</p> </td>
   <td><p>cq/gui/components/siteadmin/searchpanel/searchpredicates/userpredisate</p> </td>
  </tr>
  <tr>
   <td>6.2中的资源类型</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/userpredicates</p> </td>
  </tr>
 </tbody>
</table>

**操作：** 调整 `resourceType` 属性(添加“**/coral**”，如上面所示的位置6.2中所示)。

### 模板谓词 {#templates-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1<br /> <br />中默认搜索表单中的节点 </td>
   <td>不适用</td>
  </tr>
  <tr>
   <td><p>6.1中的资源类型</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/templatespredicate</p> </td>
  </tr>
  <tr>
   <td>6.2中的资源类型</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/templatespredicates</p> </td>
  </tr>
 </tbody>
</table>

**操作：** 调整 `resourceType` 属性(添加“**/coral**”，如上面所示的位置6.2中所示)。

## 资产管理员搜索边栏 {#assets-admin-search-rail}

以下节点引用`/conf/global/settings/dam/search/facets/assets/items`中的名称

### 节点名为“fulltext” {#fulltext-predicate-with-node-name-fulltext-1}的全文谓词

| 6.1中默认搜索表单中的节点 | 全文 |
|---|---|
| 6.1中的资源类型 | dam/gui/components/admin/customsearch/search谓词/fulltextpredicate |
| 6.2中的资源类型 | 不适用 |

在6.1中，标准全文谓词是搜索表单的一部分。 在6.2中，全文字段已被OmniSearch替换。 此谓词以编程方式跳过，可以删除。

**操作：** 删除上述节点。

### 路径浏览器谓词{#path-browser-predicates-1}

| 6.1中默认搜索表单中的节点 | 路径浏览器 |
|---|---|
| 6.1中的资源类型 | dam/gui/components/admin/customsearch/search谓词/pathbrowser谓词 |
| 6.2中的资源类型 | dam/gui/coral/components/admin/customsearch/search谓词/pathbrowser谓词 |

**操作：** 调整 `resourceType` 属性(添加“**/coral**”，如上面所示的位置6.2中所示)。

### Mime类型谓词{#mime-type-predicates}

| 6.1中默认搜索表单中的节点 | mimetype |
|---|---|
| 6.1中的资源类型 | dam/gui/components/admin/customsearch/search谓词/选项指定 |
| 6.2中的资源类型 | dam/gui/coral/components/admin/customsearch/search谓词/可选 |

**操作：** 调整 `resourceType` 属性(添加“**/coral**”，如上面所示的位置6.2中所示)。

### 文件大小谓词{#file-size-predicates}

| 6.1中默认搜索表单中的节点 | 文件大小 |
|---|---|
| 6.1中的资源类型 | dam/gui/components/admin/customsearch/search谓词/filesize谓词 |
| 6.2中的资源类型 | dam/gui/coral/components/admin/customsearch/search谓词/sliderangepredicate |

**操作：** 调 `resourceType` 整，如上面6.2位置所示。

### 资产上次修改时间谓词{#asset-last-modified-predicates}

| 6.1中默认搜索表单中的节点 | assetlastmodified谓词 |
|---|---|
| 6.1中的资源类型 | dam/gui/components/admin/customsearch/search谓词/assetlastmodified谓词 |
| 6.2中的资源类型 | dam/gui/coral/components/admin/customsearch/search谓词/assetlastmodified谓词 |

操作：调整resourceType属性（添加“/coral”，如上面显示的6.2位置所示）。

### 发布谓词{#publish-predicate}

| 6.1中默认搜索表单中的节点 | 发布 |
|---|---|
| 6.1中的资源类型 | dam/gui/components/admin/customsearch/search谓词/publishpredicate |
| 6.2中的资源类型 | dam/gui/coral/components/admin/customsearch/search谓词/publishpredicate |

**操作:**

* 调整`resourceType`属性（添加“**/coral**”，如上面所示的6.2位置所示）

* 添加`optionPaths`（类型为String）属性，其值为：`/libs/dam/options/predicates/publish`

* 添加`singleSelect`属性，其布尔值为`true`。

### 状态谓词{#status-predicates}

| 6.1中默认搜索表单中的节点 | 状态 |
|---|---|
| 6.1中的资源类型 | dam/gui/components/admin/customsearch/search谓词/选项指定 |
| 6.2中的资源类型 | dam/gui/coral/components/admin/customsearch/search谓词/可选 |

**操作：** 调整 `resourceType` 属性(添加“**/coral**”，如上面所示的位置6.2中所示)

### 到期状态谓词{#expiry-status-predicates}

| 6.1中默认搜索表单中的节点 | 过期状态 |
|---|---|
| 6.1中的资源类型 | dam/gui/components/admin/customsearch/search谓词/expiredassetprediate |
| 6.2中的资源类型 | dam/gui/coral/components/admin/customsearch/search谓词/expiredassetpredicate |

**操作：** 调整 `resourceType` 属性(添加“**/coral**”，如上面所示的位置6.2中所示)

### 元数据有效性谓词{#metadata-validity-predicates}

| 6.1中默认搜索表单中的节点 | 元数据有效性 |
|---|---|
| 6.1中的资源类型 | dam/gui/components/admin/customsearch/search谓词/选项指定 |
| 6.2中的资源类型 | dam/gui/coral/components/admin/customsearch/search谓词/可选 |

**操作：** 调整 `resourceType` 属性(添加“**/coral**”，如上面所示的位置6.2中所示)

### 评级谓词{#rating-predicates}

| 6.1中默认搜索表单中的节点 | 评级 |
|---|---|
| 6.1中的资源类型 | dam/gui/components/admin/customsearch/search谓词/rat谓词 |
| 6.2中的资源类型 | dam/gui/coral/components/admin/customsearch/search谓词/sliderangepredicate |

**操作：** 调整 `resourceType` 属性(添加“**/coral**”，如上面所示的位置6.2中所示)

### 方向谓词{#orientation-predicate}

| 6.1中默认搜索表单中的节点 | 方向 |
|---|---|
| 6.1中的资源类型 | dam/gui/components/admin/customsearch/search谓词/tagfilterpredicate |
| 6.2中的资源类型 | cq/gui/components/coral/common/admin/customsearch/search谓词/tagspredicates |

**操作:**

* 调整`resourceType`属性（添加“**/coral**”，如上面所示的6.2位置所示）

* 添加与同一节点上的`text`属性具有相同值的`fieldLabel`属性。

* 添加与同一节点上的`text`属性值相同的`emptyText`属性。

* 添加与同一节点上的`optionPaths`属性具有相同值的`rootPath`属性。

### 样式谓词{#style-predicate}

| 6.1中默认搜索表单中的节点 | 样式 |
|---|---|
| 6.1中的资源类型 | dam/gui/components/admin/customsearch/search谓词/tagfilterpredicate |
| 6.2中的资源类型 | cq/gui/components/coral/common/admin/customsearch/search谓词/tagspredicates |

**操作:**

* 调整`resourceType`属性（添加“**/coral**”，如上面所示的6.2位置所示）

* 添加与同一节点上的`text`属性具有相同值的`fieldLabel`属性。

* 添加与同一节点上的`text`属性值相同的`emptyText`属性。

* 添加与同一节点上的`optionPaths`属性具有相同值的`rootPath`属性。

### 视频格式谓词{#video-format-predicates}

| 6.1中默认搜索表单中的节点 | videoFormat |
|---|---|
| 6.1中的资源类型 | dam/gui/components/admin/customsearch/search谓词/选项指定 |
| 6.2中的资源类型 | dam/gui/coral/components/admin/customsearch/search谓词/可选 |

**操作：** 调整 `resourceType` 属性(添加“**/coral**”，如上面所示的位置6.2中所示)

### Mainasset谓词{#mainasset-predicate}

| 6.1中默认搜索表单中的节点 | 主资产 |
|---|---|
| 6.1中的资源类型 | granite/ui/components/foundation/form/hidden |
| 6.2中的资源类型 | granite/ui/components/coral/foundation/form/hidden |

**操作：** 调整 `resourceType` 属性(添加“**/coral**”，如上面所示的位置6.2中所示)
