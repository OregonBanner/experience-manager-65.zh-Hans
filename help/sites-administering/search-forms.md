---
title: 配置搜索表单
description: 了解如何配置Search Forms。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
exl-id: f82391d7-e30d-48d2-8f66-88fcae3dfb5f
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '2067'
ht-degree: 10%

---


# 配置搜索表单{#configuring-search-forms}

使用 **搜索Forms** 自定义在创作环境的各种AEM控制台和/或面板中提供的搜索面板中使用的搜索谓词选择。 自定义这些面板可根据您的特定需求使搜索功能通用。

A [谓词范围](#predicates-and-their-settings)s现成可用。 您可以添加多个谓词，其中包括“属性”谓词以搜索与您指定的单个属性匹配的资产，或“选项”谓词以搜索与为特定属性指定的一个或多个值匹配的资产。

您可以 [配置搜索表单](#configuring-your-search-forms) 用于各种控制台和资产浏览器（编辑页面时）。 此 [用于配置这些表单的对话框](#configuring-your-search-forms) 可以通过以下方式访问：

* **工具**

   * **常规**

      * **搜索表单**

首次访问此控制台时，您可以看到所有配置都有一个挂锁符号。 这表示相应的配置是默认（现成）配置 — 无法删除。 自定义配置后，锁定将消失 — 除非您 [删除自定义配置](#deleting-a-configuration-to-reinstate-the-default)，在这种情况下，将恢复默认设置（以及挂锁指示器）。

![搜索表单窗口](assets/chlimage_1-374.png)

## 配置 {#configurations}

可用的默认配置包括：

* **页面编辑器（文档搜索）：**

  此配置定义在资产浏览器中搜索文档时（编辑页面时）可用的选项。

* **页面编辑器（图像搜索）：**

  此配置定义在资产浏览器中搜索图像时（编辑页面时）可用的选项。

* **页面编辑器（手稿搜索）：**

  此配置定义在资产浏览器中搜索手稿时（编辑页面时）可用的选项。

* **页面编辑器（页面搜索）：**

  此配置定义在资产浏览器中搜索页面时（编辑页面时）可用的选项。

* **页面编辑器（段落搜索）：**

  此配置定义在资产浏览器中搜索段落时（编辑页面时）可用的选项。

* **页面编辑器（产品搜索）：**

  此配置定义在资产浏览器中搜索产品时（编辑页面时）可用的选项。

* **页面编辑器(Dynamic Media Classic) [以前称为Scene7] search)**：

  此配置定义在资源浏览器中搜索Scene7资源（编辑页面时）时可用的选项。

* **站点管理员搜索边栏**:

  此配置定义用户在使用站点控制台的搜索边栏时可用的搜索选项。

* **页面编辑器（视频搜索）：**

  此配置定义在资产浏览器中搜索视频时（编辑页面时）可用的选项。

* **资产管理员搜索边栏:**

  此配置定义用户在使用Assets控制台时可用的搜索选项。

* **目录管理员搜索边栏:**

  此配置定义用户在搜索商务目录时可用的搜索选项。

* **订单管理员搜索边栏:**

  此配置定义用户在搜索商务订单时可用的搜索选项。

* **产品收藏集管理员搜索边栏:**

  此配置定义用户在搜索商务产品收藏集时可用的搜索选项。

* **产品管理员搜索边栏:**

  此配置定义用户在搜索商务产品时可用的搜索选项。

* **项目管理员搜索边栏:**

  此配置定义用户在搜索项目时可用的搜索选项。

## 谓词及其设置 {#predicates-and-their-settings}

### 谓词 {#predicates}

以下谓词可用，具体取决于配置：

<table>
 <tbody>
  <tr>
   <th>谓词</th>
   <th>用途</th>
   <th>设置</th>
  </tr>
  <tr>
   <td>分析 </td>
   <td>显示Analytics提供的数据时，站点浏览器中的搜索/过滤功能。 Analytics搜索筛选器将加载，以匹配映射的自定义分析列。</td>
   <td>
    <ul>
     <li>字段标签</li>
     <li>描述</li>
    </ul> </td>
  </tr>
  <tr>
   <td>上次修改的资源 </td>
   <td>上次修改资源的日期。<br /> </td>
   <td>自定义谓词，基于日期谓词。</td>
  </tr>
  <tr>
   <td>组件 </td>
   <td>允许作者搜索/筛选包含特定组件的页面。 例如，图像库。<br /> </td>
   <td>
    <ul>
     <li>字段标签</li>
     <li>占位符</li>
     <li>属性名称*</li>
     <li>属性深度</li>
     <li>描述</li>
    </ul> </td>
  </tr>
  <tr>
   <td>日期 </td>
   <td>基于日期属性的资产基于滑块搜索。</td>
   <td>
    <ul>
     <li>字段标签</li>
     <li>属性名称*</li>
     <li>描述</li>
    </ul> </td>
  </tr>
  <tr>
   <td>日期范围 </td>
   <td>搜索在指定范围内为日期属性创建的资源。 在“搜索”面板中，您可以指定开始日期和结束日期。</td>
   <td>
    <ul>
     <li>字段标签</li>
     <li>占位符</li>
     <li>属性名称*</li>
     <li>范围文本（自）*</li>
     <li>范围文本（至）*</li>
     <li>描述</li>
    </ul> </td>
  </tr>
  <tr>
   <td>到期状态 </td>
   <td>根据到期状态搜索资产。</td>
   <td>
    <ul>
     <li>字段标签</li>
     <li>属性名称*</li>
     <li>描述</li>
    </ul> </td>
  </tr>
  <tr>
   <td>文件大小 </td>
   <td>根据资源的大小搜索资源。</td>
   <td>
    <ul>
     <li>字段标签</li>
     <li>属性名称*</li>
     <li>选项路径</li>
     <li>描述</li>
    </ul> </td>
  </tr>
  <tr>
   <td>隐藏的筛选器</td>
   <td>属性和值的筛选器，用户不可见。</td>
   <td>
    <ul>
     <li>属性名称</li>
     <li>属性值</li>
     <li>描述</li>
    </ul> </td>
  </tr>
  <tr>
   <td>选项 </td>
   <td><p>选项是由用户创建的内容节点。</p> <p>请参阅 <a href="#addinganoptionspredicate">添加选项谓词</a> 以了解更多信息。</p> </td>
   <td>
    <ul>
     <li>字段标签</li>
     <li>JSON 路径</li>
     <li>属性名称*</li>
     <li>单选</li>
     <li>选项路径</li>
     <li>描述</li>
    </ul> </td>
  </tr>
  <tr>
   <td>选项 属性 </td>
   <td>搜索选项的属性。</td>
   <td>
    <ul>
     <li>字段标签</li>
     <li>属性名称*</li>
     <li>选项节点路径<br /> </li>
     <li>单选</li>
     <li>描述</li>
    </ul> </td>
  </tr>
  <tr>
   <td>页面状态 </td>
   <td>根据页面状态搜索页面。</td>
   <td>
    <ul>
     <li>字段标签</li>
     <li>发布属性名称</li>
     <li>LiveCopy 属性名称</li>
     <li>描述</li>
    </ul> </td>
  </tr>
  <tr>
   <td>路径 </td>
   <td>搜索位于特定路径下的资产。</td>
   <td>
    <ul>
     <li>字段标签</li>
     <li>添加搜索路径</li>
     <li>描述</li>
    </ul> </td>
  </tr>
  <tr>
   <td>属性 </td>
   <td>搜索指定的属性。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>发布状态 </td>
   <td>根据资产的发布状态搜索资产</td>
   <td>
    <ul>
     <li>字段标签</li>
     <li>属性名称*</li>
     <li>描述</li>
    </ul> </td>
  </tr>
  <tr>
   <td>范围 </td>
   <td>搜索指定范围内的资源。 在“搜索”面板中，可以指定范围的最小值和最大值。</td>
   <td>
    <ul>
     <li>字段标签</li>
     <li>属性名称</li>
     <li>描述</li>
    </ul> </td>
  </tr>
  <tr>
   <td>范围选项 </td>
   <td>资产的特定搜索谓词，与常见的滑块谓词相同。 由于向后兼容问题，仍然可用。</td>
   <td>
    <ul>
     <li>字段标签</li>
     <li>属性名称*</li>
     <li>选项路径</li>
     <li>描述</li>
    </ul> </td>
  </tr>
  <tr>
   <td>评分 </td>
   <td>根据资产的评级搜索资产。<br /> </td>
   <td>
    <ul>
     <li>字段标签</li>
     <li>属性名称*</li>
     <li>选项路径</li>
     <li>描述</li>
    </ul> </td>
  </tr>
  <tr>
   <td>相对日期 </td>
   <td>根据资产的相对创建日期搜索资产<br /> </td>
   <td>
    <ul>
     <li>字段标签</li>
     <li>属性名称*</li>
     <li>相对日期</li>
     <li>描述</li>
    </ul> </td>
  </tr>
  <tr>
   <td>滑块范围 </td>
   <td>使用滑块功能扩展范围谓词的常用搜索谓词。 搜索属性的值必须介于滑块限制之间。</td>
   <td>
    <ul>
     <li>字段标签</li>
     <li>属性名称*</li>
     <li>描述</li>
    </ul> </td>
  </tr>
  <tr>
   <td>标记 </td>
   <td>根据标记搜索资源。 您可以配置Path属性以填充“标记”列表中的各种标记。</td>
   <td>
    <ul>
     <li>字段标签</li>
     <li>属性名称*</li>
     <li>选项路径</li>
     <li>描述</li>
    </ul> </td>
  </tr>
  <tr>
   <td>标记 </td>
   <td>基于标记进行搜索。</td>
   <td>
    <ul>
     <li>占位符</li>
     <li>属性名称*</li>
     <li>描述</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>* 常见的搜索谓词定义于：
>  `/libs/cq/gui/components/common/admin/customsearch/searchpredicates`
>
>* 仅与站点管理员（经典UI）相关的搜索谓词位于以下位置：
>  `/libs/cq/gui/components/siteadmin/admin/searchpanel/searchpredicates`
>   * 这些功能已弃用，仅可用于向后兼容。
>
>此信息仅供参考，您不得对 `/libs`.

### 谓词设置 {#predicate-settings}

根据谓词，可以选择用于配置的设置：

* **字段标签**

  将显示为可折叠标题或谓词字段标签的标签。

* **描述**

  用户的描述性详细信息。

* **占位符**

  空文本或谓词的占位符（如果未输入过滤文本）。

* **属性名称**

  要搜索的属性。 它使用相对路径和通配符 `*/*/*` 指定相对于的属性深度 `jcr:content` 节点（每个星号代表一个节点级别）。

  如果只想在资源的第一级子节点上搜索，该资源具有 `x` 上的属性 `jcr:content` 节点使用 `*/jcr:content/x`

* **属性深度**

  在资源中搜索该属性的最大深度。 因此，可以对该属性进行资源搜索并递归子项，直到子项的级别等于指定的深度。

* **属性值**

  作为绝对字符串或表达式语言的属性值；例如， `cq:Page` 或

  `${empty requestPathInfo.suffix ? "/content" : requestPathInfo.suffix}`。

* **范围文本**

  中范围字段的标签 **日期范围** 谓词。

* **选项路径**

  用户可以使用谓词设置选项卡中的路径浏览器选择路径。 选择 **+** 图标用于将所选内容添加到有效选项列表中(然后 **-** 图标以删除（如果需要）。

  这些选项是由用户创建的内容节点，具有以下结构：

  `(jcr:primaryType = nt:unstructured, value (String), jcr:title (String))`

* **选项节点路径**
实际上与 **选项路径**，只有公用谓词字段中有此变量，其他变量专用于资产。

* **单选**
如果选中，这些选项将呈现为仅允许单个选择的复选框。 如果错误地选中此复选框，则可取消选中此复选框。

* **发布和Live Copy属性名称**
站点特定谓词的发布和Live Copy复选框的标签。

* 中的字段标签上的&amp;ast； **设置** 制表符表示必填字段，如果留空，将显示错误消息

## 配置搜索Forms {#configuring-your-search-forms}

### 创建/打开自定义配置 {#creating-opening-a-customized-configuration}

1. 导航到 **工具** >>  **常规** >> **搜索Forms**.

1. 选择要自定义的配置。
1. 使用 **编辑** 图标以打开配置以进行更新。
1. 如果进行了新的自定义，则您可能需要 [添加新谓词字段并定义设置](#add-edit-a-predicate-field-and-define-field-settings) 根据需要。 如果存在自定义项，您可以选择现有字段并 [更新设置](#add-edit-a-predicate-field-and-define-field-settings).
1. 选择 **完成** 以保存配置。

   >[!NOTE]
   >
   >自定义配置存储（根据需要）在下：
   >
   >* `/apps/cq/gui/content/facets/<option>`
   >* `/apps/commerce/gui/content/facets/<option>`

### 添加/编辑谓词字段并定义字段设置 {#add-edit-a-predicate-field-and-define-field-settings}

您可以添加或编辑字段并定义/更新其设置：

1. [打开自定义配置](#creating-opening-a-customized-configuration) 以进行更新。
1. 如果要添加新字段，请打开 **选择谓词** 制表符并将所需的谓词拖到所需的位置。 例如， **日期范围谓词**：

   ![编辑搜索表单](assets/chlimage_1-375.png)

1. 取决于是否：

   * 您正在添加新字段：

     添加谓词后 **设置** 选项卡将打开并显示可以定义的属性。

   * 要更新现有的谓词：

     选择谓词字段（位于右侧），然后打开 **设置** 选项卡。

   例如， **日期范围谓词**：

   ![日期范围谓词的属性](assets/chlimage_1-376.png)

1. 根据需要进行更改并通过进行确认 **完成**.

### 预览搜索配置 {#previewing-the-search-configuration}

1. 选择预览图标：

   ![预览搜索表单](do-not-localize/chlimage_1-31.png)

1. 这将显示搜索表单，它们在相应控制台的搜索列中显示（完全展开）。

   ![预览搜索表单](assets/chlimage_1-377.png)

1. **关闭** 预览以返回并完成配置。

### 删除谓词字段 {#deleting-a-predicate-field}

1. [打开自定义配置](#creating-opening-a-customized-configuration) 以进行更新。
1. 选择谓词字段（位于右侧），打开 **设置** 选项卡，然后选择 **删除** 图标（左下方）。

   ![“删除”图标](do-not-localize/chlimage_1-32.png)

1. 此时将显示一个对话框，要求确认删除操作。

1. 通过确认此更改和任何其他更改 **完成**.

### 删除配置（恢复默认设置） {#deleting-a-configuration-to-reinstate-the-default}

自定义配置后，这将覆盖默认值。 您可以通过删除自定义配置来重新声明默认配置。

>[!NOTE]
>
>不能删除任一默认配置。

从控制台中删除自定义配置已完成：

1. 选择所需的配置(例如， **页面编辑器（段落搜索）**)，然后 **删除** 工具栏中的图标：

   ![删除表单](assets/chlimage_1-378.png)

1. 自定义配置将被删除，默认配置将恢复（控制台中挂锁符号的重新出现表示这一点）。

### 添加选项谓词 {#adding-options-predicates}

选项谓词（选项、选项属性）允许您配置要搜索的项目。 属性通常用于直接在页面下搜索某些内容；例如，页面节点上的属性。

以下示例（根据用于创建页面的模板进行搜索）说明了所涉及的步骤：

1. 创建定义要搜索的属性的节点。

   您需要一个根节点，其中包含可供用户使用的各个选项的定义。

   单个选项的节点需要以下属性：

   * `jcr:title`  — 要在搜索边栏中显示的字段标签
   * `value`  — 要搜索的属性值

   ![在CRXDE中添加选项](assets/chlimage_1-379.png)

   >[!NOTE]
   >
   >您 ***必须*** 不会更改中的任何内容 `/libs` 路径。
   >
   >这是因为 `/libs` 下次升级实例时将被覆盖（在应用修补程序或功能包时很可能会被覆盖）。
   >
   >建议用于配置和其他更改的方法是：
   >
   >1. 重新创建所需的项目，因为它存在于中 `/libs`，下 `/apps`. 在本例中，来自：
   >1. `/libs/cq/gui/content/common/options/predicates`
   >1. 在中进行任何更改 `/apps.`

1. 打开 **搜索Forms** 控制台并选择要更新的配置。 例如， **站点管理员搜索边栏**.

   然后单击/点按 **编辑搜索表单** 图标。

1. 根据配置，添加 **选项** 或 **Options属性** 到配置。
1. 更新这些字段，特别是：

   * **属性名称**

     指定要在目标节点上搜索的节点属性。 例如：

     `jcr:content/cq:template`

   * **选项节点路径**

     选择保留选项的路径。 例如：

     `/apps/cq/gui/content/common/options/predicates/templatetype`

   ![添加属性路径](assets/chlimage_1-380.png)

1. 选择 **完成** 以保存您的配置。
1. 导航到相应的控制台(在本例中， **站点**)并打开 **Search** 边栏。 此时将显示新定义的搜索表单以及各种选项。 选择所需的选项以查看搜索结果：

   ![最终结果](assets/chlimage_1-381.png)

## 用户权限 {#user-permissions}

下表列出了对搜索表单执行编辑、删除和预览操作所需的权限。

<table>
 <tbody>
  <tr>
   <td><strong>操作</strong></td>
   <td><strong>权限</strong></td>
  </tr>
  <tr>
   <td>编辑 </td>
   <td>对的读、写权限 <code>/apps </code>节点。</td>
  </tr>
  <tr>
   <td>删除</td>
   <td>对的读、写、删除权限 <code>/apps</code> 节点</td>
  </tr>
  <tr>
   <td>预览</td>
   <td>对的读、写、删除权限 <code>/var/dam/content</code> 节点。<br /> 对的读、写权限 <code>/apps</code> 节点。</td>
  </tr>
 </tbody>
</table>
