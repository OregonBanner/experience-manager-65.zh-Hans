---
title: 升级自定义搜索表单
seo-title: 升级自定义搜索表单
description: 本文详细介绍了升级后需要进行的调整，以便自定义搜索表单正常工作。
seo-description: 本文详细介绍了升级后需要进行的调整，以便自定义搜索表单正常工作。
uuid: 35b8fbb9-5951-4e1c-bf04-4471a55b9cb0
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
discoiquuid: a08cee9c-e981-4483-8bdc-e6353977f854
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 升级自定义搜索表单{#upgrading-custom-search-forms}

在AEM 6.2中，自定义搜索表单存储在存储库中的位置已更改。 升级后，它们会从6.1中的位置移至：

* /apps/cq/gui/content/facets

新位置：

* /conf/global/settings/cq/search/facets

因此，升级后需要手动调整，才能使表单继续运行。

这适用于新的搜索表单以及已自定义的默认表单。

有关详细信息，请参阅有关搜索彩块化 [的文档](/help/assets/search-facets.md)。

## 更改resourceType属性 {#changing-the-resourcetype-property}

除非另有说明，否则升级后需要完成的大多数调整都需要更改所配置的自 `sling:resourceType` 定义搜索表单的属性。 这是必需的，这样属性就会指向渲染脚本的正确位置。

您可以通过执行以下操作来更改属性：

1. 通过转到 `https://server:port/crx/de/index.jsp`
1. 按照以下自定义搜索表单列表中的指定，浏览到需要调整的节 [点的位置](/help/sites-deploying/upgrading-custom-search-forms.md#list-of-custom-search-forms) 。
1. 单击节点。 在右侧属性窗格中，单击并修改 **sling:resourceType属性** 。
1. 最后，按“全部保存”按钮保存 **更改** 。

## 自定义搜索表单列表 {#list-of-custom-search-forms}

在下面，您将找到所有自定义搜索表单的列表以及升级后需要进行的修改。 他们指的是中的名称 `/conf/global/settings/cq/search/facets/sites/items`。

### 带有节点名“fulltext”的全文谓词 {#fulltext-predicate-with-node-name-fulltext}

<table>
 <tbody>
  <tr>
   <td>6.1中默认搜索表单中的节点数</td>
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

**** 操作：完全删除节点。

### 其他全文谓词 {#other-fulltext-predicates}

<table>
 <tbody>
  <tr>
   <td>6.1中默认搜索自的节点数</td>
   <td>不适用</td>
  </tr>
  <tr>
   <td><p>6.1中的资源类型</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/search谓词/fulltextpredicates</p> </td>
  </tr>
  <tr>
   <td>6.2中的资源类型</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/search谓词/fulltextpredicate</p> </td>
  </tr>
 </tbody>
</table>

**** 操作：调整 `resourceType` 属性(添加“**/coral**”，如上面所示的6.2位置)。

### 路径浏览器谓词 {#path-browser-predicates}

<table>
 <tbody>
  <tr>
   <td>6.1中默认搜索表单中的节点／秒<br /><br /> </td>
   <td>路径</td>
  </tr>
  <tr>
   <td><p>6.1中的资源类型</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/search谓词／路径谓词</p> </td>
  </tr>
  <tr>
   <td>6.2中的资源类型</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/search谓词／路径谓词</p> </td>
  </tr>
 </tbody>
</table>

**** 操作：调整 `resourceType` 属性(添加“**/coral**”，如上面所示的6.2位置)。

### 标记谓词 {#tags-predicates}

<table>
 <tbody>
  <tr>
   <td>6.1中默认搜索表单中的节点／秒<br /><br /> </td>
   <td>标记</td>
  </tr>
  <tr>
   <td><p>6.1中的资源类型</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/search谓词/tagspredicate</p> </td>
  </tr>
  <tr>
   <td>6.2中的资源类型</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/search谓词/tagspredicate</p> </td>
  </tr>
 </tbody>
</table>

**** 操作：调整 **resourceType属性** (添加“**/coral**”，如上面所示的6.2位置)。

### 页面状态谓词 {#page-status-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1中默认搜索表单中的节点／秒<br /><br /> </td>
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

页面状态已被两个选项属性谓词替换，一个用于发布，另一个用于LiveCopy状态。

**操作:**

* 删除节 `pagestatuspredicate` 点
* 复制节点

   * `/libs/settings/cq/search/facets/sites/jcr:content/items/publishstatuspredicate`
   * 到 `/conf/global/settings/cq/search/facets/sites/jcr:content/items`

* 复制节点

   * `/libs/settings/cq/search/facets/sites/jcr:content/items/livecopystatuspredicate`
   * 到 `/conf/global/settings/cq/search/facets/sites/jcr:content/items`

* 确保将节 `listOrder` 点的属性 `analyticspredicate` 设置为“**8**”。 这是避免冲突所必需的。

### 日期范围谓词 {#date-range-predicates}

<table>
 <tbody>
  <tr>
   <td>6.1中默认搜索表单中的节点／秒<br /><br /> </td>
   <td>daterange谓词</td>
  </tr>
  <tr>
   <td>6.1中的资源类型</td>
   <td>cq/gui/components/common/admin/customsearch/search谓词/daterangepredicates</td>
  </tr>
  <tr>
   <td>6.2中的资源类型</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/search谓词/daterangepredicates</p> </td>
  </tr>
 </tbody>
</table>

**** 操作：调整 `resourceType` 属性(添加“**/coral**”，如上面所示的6.2位置)。

### 隐藏的筛选器 {#hidden-filter}

<table>
 <tbody>
  <tr>
   <td>6.1中默认搜索表单中的节点／秒<br /><br /> </td>
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

**** 操作：无需调整。

### 分析谓词 {#analytics-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1中默认搜索表单中的节点／秒<br /><br /> </td>
   <td>分析</td>
  </tr>
  <tr>
   <td><p>6.1中的资源类型</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchedates/analyticspredicates/analyticspredicate</p> </td>
  </tr>
  <tr>
   <td>6.2中的资源类型</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/search谓词/analyticspredicate</p> </td>
  </tr>
 </tbody>
</table>

**** 操作：调整 `resourceType` 属性(添加“**/coral**”，如上面所示的6.2位置)。

### 范围谓词 {#range-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1中默认搜索表单中的节点／秒<br /><br /> </td>
   <td>不适用</td>
  </tr>
  <tr>
   <td><p>6.1中的资源类型</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/search谓词/rangedredicate</p> </td>
  </tr>
  <tr>
   <td>6.2中的资源类型</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/search谓词/rangepredicate</p> </td>
  </tr>
 </tbody>
</table>

**** 操作：调整 `resourceType` 属性(添加“**/coral**”，如上面所示的6.2位置)。

>[!NOTE]
>
>注意：与6.1相反，“范围谓词”不再在搜索栏中呈现标记。

### 选项属性谓词 {#options-property-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1中默认搜索表单中的节点／秒<br /><br /> </td>
   <td>不适用</td>
  </tr>
  <tr>
   <td><p>6.1中的资源类型</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchredicates/optionspredicate</p> </td>
  </tr>
  <tr>
   <td>6.2中的资源类型</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/search谓词/optionspredicate</p> </td>
  </tr>
 </tbody>
</table>

**** 操作：调整 `resourceType` 属性(添加“**/coral**”，如上面所示的6.2位置)。

### 滑块范围谓词 {#slider-range-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1中默认搜索表单中的节点／秒<br /><br /> </td>
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

**** 操作：调整 `resourceType` 属性(添加“**/coral**”，如上面所示的6.2位置)。

### 组件谓词 {#components-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1中默认搜索表单中的节点／秒<br /><br /> </td>
   <td>不适用</td>
  </tr>
  <tr>
   <td><p>6.1中的资源类型</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/search谓词/componentspredicate</p> </td>
  </tr>
  <tr>
   <td>6.2中的资源类型</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/search谓词/componentspredicate</p> </td>
  </tr>
 </tbody>
</table>

**** 操作：调整 `resourceType` 属性(添加“**/coral**”，如上面所示的6.2位置)。

### 作者谓词 {#author-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1中默认搜索表单中的节点／秒<br /><br /> </td>
   <td>不适用</td>
  </tr>
  <tr>
   <td><p>6.1中的资源类型</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/userpredicates</p> </td>
  </tr>
  <tr>
   <td>6.2中的资源类型</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/userpredicate</p> </td>
  </tr>
 </tbody>
</table>

**** 操作：调整 `resourceType` 属性(添加“**/coral**”，如上面所示的6.2位置)。

### 模板谓词 {#templates-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1中默认搜索表单中的节点／秒<br /><br /> </td>
   <td>不适用</td>
  </tr>
  <tr>
   <td><p>6.1中的资源类型</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchredicates/templatespredicate</p> </td>
  </tr>
  <tr>
   <td>6.2中的资源类型</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/search谓词/templatespredicate</p> </td>
  </tr>
 </tbody>
</table>

**** 操作：调整 `resourceType` 属性(添加“**/coral**”，如上面所示的6.2位置)。

## 资产管理员搜索边栏 {#assets-admin-search-rail}

以下节点引用 `/conf/global/settings/dam/search/facets/assets/items`

### 带有节点名“fulltext”的全文谓词 {#fulltext-predicate-with-node-name-fulltext-1}

| 6.1中默认搜索表单中的节点数 | 全文 |
|---|---|
| 6.1中的资源类型 | dam/gui/components/admin/customsearch/searchedicates/fulltextpredicate |
| 6.2中的资源类型 | 不适用 |

在6.1中，标准全文谓词是搜索表单的一部分。 在6.2中，全文字段已替换为OmniSearch。 此谓词会以编程方式跳过，并且可以删除。

**** 操作：删除上述节点。

### 路径浏览器谓词 {#path-browser-predicates-1}

| 6.1中默认搜索表单中的节点数 | 路径浏览器 |
|---|---|
| 6.1中的资源类型 | dam/gui/components/admin/customsearch/search谓词/pathbrowser谓词 |
| 6.2中的资源类型 | dam/gui/coral/components/admin/customsearch/search谓词/pathbrowser谓词 |

**** 操作：调整 `resourceType` 属性(添加“**/coral**”，如上面所示的6.2位置)。

### MIME类型谓词 {#mime-type-predicates}

| 6.1中默认搜索表单中的节点数 | mimetype |
|---|---|
| 6.1中的资源类型 | dam/gui/components/admin/customsearch/search谓词／选项指定 |
| 6.2中的资源类型 | dam/gui/coral/components/admin/customsearch/search谓词／选项指定 |

**** 操作：调整 `resourceType` 属性(添加“**/coral**”，如上面所示的6.2位置)。

### 文件大小谓词 {#file-size-predicates}

| 6.1中默认搜索表单中的节点数 | 文件大小 |
|---|---|
| 6.1中的资源类型 | dam/gui/components/admin/customsearch/search谓词/filesizepredicate |
| 6.2中的资源类型 | dam/gui/coral/components/admin/customsearch/search谓词/sliderange谓词 |

**** 操作：如 `resourceType` 上面6.2位置所示调整。

### 资产上次修改时间谓词 {#asset-last-modified-predicates}

| 6.1中默认搜索表单中的节点数 | assetlastmodified谓词 |
|---|---|
| 6.1中的资源类型 | dam/gui/components/admin/customsearch/search谓词/assetlastmodifed谓词 |
| 6.2中的资源类型 | dam/gui/coral/components/admin/customsearch/search谓词/assetlastmodifed谓词 |

操作：调整resourceType属性（添加“/coral”，如上面所示的6.2位置）。

### 发布谓词 {#publish-predicate}

| 6.1中默认搜索表单中的节点数 | 发布 |
|---|---|
| 6.1中的资源类型 | dam/gui/components/admin/customsearch/search谓词/publishpredicate |
| 6.2中的资源类型 | dam/gui/coral/components/admin/customsearch/search谓词/publishpredicate |

**操作:**

* 调整 `resourceType` 属性(添加“**/coral**”，如上面所示的6.2位置)

* 添加 `optionPaths` 一个（类型为String）属性，其值为： `/libs/dam/options/predicates/publish`

* 添加 `singleSelect` 带布尔值的属性 `true`。

### 状态谓词 {#status-predicates}

| 6.1中默认搜索表单中的节点数 | 状态 |
|---|---|
| 6.1中的资源类型 | dam/gui/components/admin/customsearch/search谓词／选项指定 |
| 6.2中的资源类型 | dam/gui/coral/components/admin/customsearch/search谓词／选项指定 |

**** 操作：调整 `resourceType` 属性(添加“**/coral**”，如上面所示的6.2位置)

### 到期状态谓词 {#expiry-status-predicates}

| 6.1中默认搜索表单中的节点数 | 过期状态 |
|---|---|
| 6.1中的资源类型 | dam/gui/components/admin/customsearch/search谓词/expiredassetpredicate |
| 6.2中的资源类型 | dam/gui/coral/components/admin/customsearch/search谓词/expiredassetpredicate |

**** 操作：调整 `resourceType` 属性(添加“**/coral**”，如上面所示的6.2位置)

### 元数据有效性谓词 {#metadata-validity-predicates}

| 6.1中默认搜索表单中的节点数 | 元数据有效性 |
|---|---|
| 6.1中的资源类型 | dam/gui/components/admin/customsearch/search谓词／选项指定 |
| 6.2中的资源类型 | dam/gui/coral/components/admin/customsearch/search谓词／选项指定 |

**** 操作：调整 `resourceType` 属性(添加“**/coral**”，如上面所示的6.2位置)

### 评级谓词 {#rating-predicates}

| 6.1中默认搜索表单中的节点数 | 评级 |
|---|---|
| 6.1中的资源类型 | dam/gui/components/admin/customsearch/search谓词/rating谓词 |
| 6.2中的资源类型 | dam/gui/coral/components/admin/customsearch/search谓词/sliderange谓词 |

**** 操作：调整 `resourceType` 属性(添加“**/coral**”，如上面所示的6.2位置)

### 方向谓词 {#orientation-predicate}

| 6.1中默认搜索表单中的节点数 | 方向 |
|---|---|
| 6.1中的资源类型 | dam/gui/components/admin/customsearch/search谓词/tagfilter谓词 |
| 6.2中的资源类型 | cq/gui/components/coral/common/admin/customsearch/search谓词/tagspredicate |

**操作:**

* 调整 `resourceType` 属性(添加“**/coral**”，如上面所示的6.2位置)

* 添加 `fieldLabel` 与同一节点上的属性值 `text` 相同的属性。

* 添加 `emptyText` 与同一节点上的属性 `text` 值相同的属性。

* 添加 `rootPath` 与同一节点上的属性值相 `optionPaths` 同的属性。

### 样式谓词 {#style-predicate}

| 6.1中默认搜索表单中的节点数 | 样式 |
|---|---|
| 6.1中的资源类型 | dam/gui/components/admin/customsearch/search谓词/tagfilter谓词 |
| 6.2中的资源类型 | cq/gui/components/coral/common/admin/customsearch/search谓词/tagspredicate |

**操作:**

* 调整 `resourceType` 属性(添加“**/coral**”，如上面所示的6.2位置)

* 添加 `fieldLabel` 与同一节点上的属性值 `text` 相同的属性。

* 添加 `emptyText` 与同一节点上的属性 `text` 值相同的属性。

* 添加 `rootPath` 与同一节点上的属性值相 `optionPaths` 同的属性。

### 视频格式谓词 {#video-format-predicates}

| 6.1中默认搜索表单中的节点数 | videoFormat |
|---|---|
| 6.1中的资源类型 | dam/gui/components/admin/customsearch/search谓词／选项指定 |
| 6.2中的资源类型 | dam/gui/coral/components/admin/customsearch/search谓词／选项指定 |

**** 操作：调整 `resourceType` 属性(添加“**/coral**”，如上面所示的6.2位置)

### 主资产谓词 {#mainasset-predicate}

| 6.1中默认搜索表单中的节点数 | mainasset |
|---|---|
| 6.1中的资源类型 | granite/ui/components/foundation/form/hidden |
| 6.2中的资源类型 | granite/ui/components/coral/foundation/form/hidden |

**** 操作：调整 `resourceType` 属性(添加“**/coral**”，如上面所示的6.2位置)
