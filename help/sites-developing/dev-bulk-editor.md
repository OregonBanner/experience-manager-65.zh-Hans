---
title: 开发批量编辑器
description: 标记允许对内容进行分类和组织
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: 8753aaab-959f-459b-bdb6-057cbe05d480
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1835'
ht-degree: 2%

---

# 开发批量编辑器{#developing-the-bulk-editor}

本节介绍如何开发批量编辑器工具以及如何扩展产品列表组件（基于批量编辑器）。

## 批量编辑器查询参数 {#bulk-editor-query-parameters}

使用批量编辑器时，可以将多个查询参数添加到URL中以使用特定配置调用批量编辑器。 如果您希望批量编辑器始终与特定配置一起使用（例如，与产品列表组件中一样），则必须编辑 `bulkeditor.jsp` （位于/libs/wcm/core/components/bulkeditor中）或创建具有特定配置的组件。 使用查询参数所做的更改不是永久性的。

例如，如果在浏览器的URL中键入以下内容：

`https://<servername><port_number>/etc/importers/bulkeditor.html?rootPath=/content/geometrixx/en&queryParams=geometrixx&initialSearch=true&hrp=true`

此时将显示批量编辑器，但不包含 **根路径** 字段，因为hrp=true会隐藏该字段。 使用参数hrp=false，将显示字段（默认值）。

以下是Bulk Editor查询参数的列表：

>[!NOTE]
>
>每个参数可以有一个长名称和短名称。 例如，搜索根路径的长名称为 `rootPath`，简称为 `rp`. 如果未定义长名称，则从请求中读取短名称。

<table>
 <tbody>
  <tr>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td><p> 参数</p> <p>（长名称/短名称）<br /> </p> </td>
   <td> 类型 <br /> </td>
   <td> 描述 <br /> </td>
  </tr>
  <tr>
   <td> rootPath / rp<br /> </td>
   <td> 字符串 </td>
   <td> 搜索根路径</td>
  </tr>
  <tr>
   <td> queryParams / qp<br /> </td>
   <td> 字符串</td>
   <td> 搜索查询</td>
  </tr>
  <tr>
   <td> contentMode / cm<br /> </td>
   <td> 布尔值</td>
   <td> 为true时，启用内容模式<br /> </td>
  </tr>
  <tr>
   <td> colsValue / cv<br /> </td>
   <td> 字符串[]</td>
   <td> 搜索的属性（colsSelection中的选中值显示为复选框）</td>
  </tr>
  <tr>
   <td> extraCols / ec<br /> </td>
   <td> 字符串[]</td>
   <td> 额外的搜索属性（显示在逗号分隔的文本字段中）</td>
  </tr>
  <tr>
   <td> initialSearch / is<br /> </td>
   <td> 布尔值</td>
   <td> 为true时，在页面加载时执行查询<br /> </td>
  </tr>
  <tr>
   <td> colsSelection / cs<br /> </td>
   <td> 字符串[]</td>
   <td> 搜索属性选择（显示为复选框）</td>
  </tr>
  <tr>
   <td> showGridOnly / sgo<br /> </td>
   <td> 布尔值</td>
   <td> 为true时，仅显示网格，而不显示搜索面板 <br /> </td>
  </tr>
  <tr>
   <td> searchPanelCollapsed / spc</td>
   <td> 布尔值</td>
   <td> 为true时，搜索面板在加载时折叠</td>
  </tr>
  <tr>
   <td> hideRootPath / hrp</td>
   <td> 布尔值</td>
   <td> 为true时，隐藏根路径字段</td>
  </tr>
  <tr>
   <td> hideQueryParams / hqp</td>
   <td> 布尔值</td>
   <td> 为true时，隐藏查询字段</td>
  </tr>
  <tr>
   <td> hideContentMode / hcm</td>
   <td> 布尔值</td>
   <td> 为true时，隐藏内容模式字段</td>
  </tr>
  <tr>
   <td> hideColsSelection / hcs</td>
   <td> 布尔值</td>
   <td> 为true时，隐藏列选择字段</td>
  </tr>
  <tr>
   <td> hideExtraCols /标题</td>
   <td> 布尔值</td>
   <td> 为true时，隐藏额外的列字段</td>
  </tr>
  <tr>
   <td> hideSearchButton</td>
   <td> 布尔值</td>
   <td> 为true时，隐藏搜索按钮</td>
  </tr>
  <tr>
   <td> hideSaveButton / hsavep</td>
   <td> 布尔值</td>
   <td> 为true时，隐藏保存按钮</td>
  </tr>
  <tr>
   <td> hideExportButton / hexpb</td>
   <td> 布尔值</td>
   <td> 为true时，隐藏导出按钮</td>
  </tr>
  <tr>
   <td> hideImportButton / hib</td>
   <td> 布尔值</td>
   <td> 为true时，隐藏导入按钮</td>
  </tr>
  <tr>
   <td> hideResultNumber / hrn</td>
   <td> 布尔值</td>
   <td> 如果为true，则隐藏网格搜索结果编号文本</td>
  </tr>
  <tr>
   <td> hideInsertButton / hinsertb</td>
   <td> 布尔值</td>
   <td> 为true时，隐藏网格插入按钮</td>
  </tr>
  <tr>
   <td> hideDeleteButton / hdelb</td>
   <td> 布尔值</td>
   <td> 为true时，隐藏网格删除按钮</td>
  </tr>
  <tr>
   <td> hidePathCol / hpc</td>
   <td> 布尔值</td>
   <td> 为true时，隐藏网格“路径”列</td>
  </tr>
 </tbody>
</table>

### 开发基于批量编辑器的组件：产品列表组件 {#developing-a-bulk-editor-based-component-the-product-list-component}

本节概述了如何使用批量编辑器，并介绍了基于批量编辑器的现有Geometrixx组件：产品列表组件。

利用产品列表组件，用户可显示和编辑数据表。 例如，您可以使用产品列表组件表示目录中的产品。 该信息会显示在标准HTML表格中，并且任何编辑都会在 **编辑** 对话框，其中包含BulkEditor小组件。 (此批量编辑器与在/etc/importers/bulkeditor.html上或通过“工具”菜单访问的编辑器相同)。 产品列表组件已针对特定的有限批量编辑器功能进行了配置。 可以配置批量编辑器的每个部分（或从批量编辑器派生的组件）。

使用批量编辑器，您可以添加、修改、删除、过滤和导出行，保存修改并导入一组行。 每一行都作为节点存储在Product List组件实例本身下。 每个单元格都是每个节点的属性。 这是一种设计选择，可以轻松进行更改，例如，您可以将节点存储在存储库中的其他位置。 查询servlet的角色是返回要显示的节点列表；搜索路径被定义为产品列表实例。

产品列表组件的源代码位于存储库/apps/geometrixx/components/productlist中，它由若干部分组成，如所有Adobe Experience Manager (AEM)组件：

* HTML渲染：渲染在JSP文件(/apps/geometrixx/components/productlist/productlist.jsp)中完成。 JSP读取当前Product List组件的子节点，并将每个子节点显示为HTML表的行。
* “编辑”对话框，可在其中定义批量编辑器配置。 配置对话框以符合组件的需要：可用列以及对网格或搜索可能执行的操作。 请参阅 [批量编辑器配置属性](#bulk-editor-configuration-properties) 有关所有配置属性的信息。

以下是对话框子节点的XML表示形式：

```xml
        <editor
            jcr:primaryType="cq:Widget"
            colsSelection="[ProductId,ProductName,Color,CatalogCode,SellingSku]"
            colsValue="[ProductId,ProductName,Color,CatalogCode,SellingSku]"
            contentMode="false"
            exportURL="/etc/importers/bulkeditor/export.tsv"
            extraCols="Selection"
            hideColsSelection="false"
            hideContentMode="true"
            hideDeleteButton="false"
            hideExportButton="false"
            hideExtraCols="true"
            hideImportButton="false"
            hideInsertButton="false"
            hideMoveButtons="false"
            hidePathCol="true"
            hideRootPath="true"
            hideSaveButton="false"
            hideSearchButton="false"
            importURL="/etc/importers/bulkeditor/import"
            initialSearch="true"
            insertedResourceType="geometrixx/components/productlist/sku"
            queryParams=""
            queryURL="/etc/importers/bulkeditor/query.json"
            saveURL="/etc/importers/bulkeditor/save"
            xtype="bulkeditor">
            <saveButton
                jcr:primaryType="nt:unstructured"
                text="Save modifications"/>
            <searchButton
                jcr:primaryType="nt:unstructured"
                text="Apply filter"/>
            <queryParamsInput
                jcr:primaryType="nt:unstructured"
                fieldDescription="Enter here your filters"
                fieldLabel="Filters"/>
            <searchPanel
                jcr:primaryType="nt:unstructured"
                height="200">
                <defaults
                    jcr:primaryType="nt:unstructured"
                    labelWidth="150"/>
            </searchPanel>
            <grid
                jcr:primaryType="nt:unstructured"
                height="275"/>
            <store jcr:primaryType="nt:unstructured">
                <sortInfo
                    jcr:primaryType="nt:unstructured"
                    direction="ASC"
                    field="CatalogCode"/>
            </store>
            <colModel
                jcr:primaryType="nt:unstructured"
                width="150"/>
            <colsMetadata jcr:primaryType="nt:unstructured">
                <Selection
                    jcr:primaryType="nt:unstructured"
                    checkbox="true"
                    forcedPosition="0"
                    headerText=""/>
                <ProductId
                    jcr:primaryType="nt:unstructured"
                    cellCls="productlist-cell-productid"
                    headerText="Product Id"/>
                <ProductName
                    jcr:primaryType="nt:unstructured"
                    cellStyle="background-color: #FFCC99;"
                    headerText="Product Name"/>
                <CatalogCode
                    jcr:primaryType="nt:unstructured"
                    cellStyle="background-color: #EDEDED;"
                    headerText="Catalog Code"/>
                <Color jcr:primaryType="nt:unstructured">
                    <editor
                        jcr:primaryType="nt:unstructured"
                        store="[Blue,Red,Yellow]"
                        triggerAction="all"
                        typeAhead="true"
                        xtype="combo"/>
                </Color>
                <SellingSku
                    jcr:primaryType="nt:unstructured"
                    headerText="Sku Id"/>
            </colsMetadata>
        </editor>
```

### 批量编辑器配置属性 {#bulk-editor-configuration-properties}

可以配置批量编辑器的每个部分。 下表列出了批量编辑器的所有配置属性。

<table>
 <tbody>
  <tr>
   <td>属性名称</td>
   <td>定义</td>
  </tr>
  <tr>
   <td>rootPath</td>
   <td>搜索根路径</td>
  </tr>
  <tr>
   <td>queryParams</td>
   <td>搜索查询</td>
  </tr>
  <tr>
   <td>内容模式</td>
   <td>如果为True，则启用内容模式：在jcr：content节点上读取属性，而在搜索结果节点上不读取属性</td>
  </tr>
  <tr>
   <td>colsvalue</td>
   <td>搜索的属性（colsSelection中的选中值显示为复选框）</td>
  </tr>
  <tr>
   <td>extractcols</td>
   <td>额外的搜索属性（以逗号分隔的文本字段显示）</td>
  </tr>
  <tr>
   <td>初始搜索</td>
   <td>如果为True，则在页面加载时执行查询</td>
  </tr>
  <tr>
   <td>colsSelection</td>
   <td>搜索属性选择（显示为复选框）</td>
  </tr>
  <tr>
   <td>showGridOnly</td>
   <td>True表示仅显示网格，而不显示搜索面板（不要忘记将initialSearch设置为true）</td>
  </tr>
  <tr>
   <td>searchPanelCollapsed</td>
   <td>如果为True，则默认情况下折叠搜索面板</td>
  </tr>
  <tr>
   <td>隐藏根路径</td>
   <td>隐藏根路径字段</td>
  </tr>
  <tr>
   <td>hideQueryparams</td>
   <td>隐藏查询字段</td>
  </tr>
  <tr>
   <td>隐藏内容模式</td>
   <td>隐藏内容模式字段</td>
  </tr>
  <tr>
   <td>hideColsSelection</td>
   <td>隐藏列选择字段</td>
  </tr>
  <tr>
   <td>hideExtraCols</td>
   <td>隐藏额外栏位</td>
  </tr>
  <tr>
   <td>hideSearchButton</td>
   <td>隐藏搜索按钮</td>
  </tr>
  <tr>
   <td>hideSaveButton</td>
   <td>隐藏保存按钮</td>
  </tr>
  <tr>
   <td>hideExportButton</td>
   <td>隐藏导出按钮</td>
  </tr>
  <tr>
   <td>hideImportButton</td>
   <td>隐藏导入按钮</td>
  </tr>
  <tr>
   <td>hideResultNumber</td>
   <td>隐藏网格搜索结果编号文本</td>
  </tr>
  <tr>
   <td>隐藏插入按钮</td>
   <td>隐藏网格插入按钮</td>
  </tr>
  <tr>
   <td>hideDeleteButton</td>
   <td>隐藏网格删除按钮</td>
  </tr>
  <tr>
   <td>hidePathCol</td>
   <td>隐藏网格“路径”列</td>
  </tr>
  <tr>
   <td>queryURL</td>
   <td>查询Servlet的路径</td>
  </tr>
  <tr>
   <td>exportURL</td>
   <td>导出servlet的路径</td>
  </tr>
  <tr>
   <td>importURL</td>
   <td>导入servlet的路径</td>
  </tr>
  <tr>
   <td>insertedResourceType</td>
   <td>插入行时添加到节点的资源类型</td>
  </tr>
  <tr>
   <td>saveButton</td>
   <td>保存按钮构件配置</td>
  </tr>
  <tr>
   <td>searchButton</td>
   <td>搜索按钮构件配置</td>
  </tr>
  <tr>
   <td>exportButton</td>
   <td>导出按钮构件配置</td>
  </tr>
  <tr>
   <td>importButton</td>
   <td>导入按钮构件配置</td>
  </tr>
  <tr>
   <td>searchPanel</td>
   <td>搜索面板构件配置</td>
  </tr>
  <tr>
   <td>网格</td>
   <td>网格构件配置</td>
  </tr>
  <tr>
   <td>存储</td>
   <td>存储配置</td>
  </tr>
  <tr>
   <td>colModel</td>
   <td>网格列模型配置</td>
  </tr>
  <tr>
   <td>根路径输入</td>
   <td>rootPath构件配置</td>
  </tr>
  <tr>
   <td>queryParamsInput</td>
   <td>queryParams构件配置</td>
  </tr>
  <tr>
   <td>contentModeInput</td>
   <td>contentMode构件配置</td>
  </tr>
  <tr>
   <td>colsSelectionInput</td>
   <td>colsSelection小组件配置</td>
  </tr>
  <tr>
   <td>extraColsInput</td>
   <td>extraCols构件配置</td>
  </tr>
  <tr>
   <td>colsMetadata</td>
   <td>列元数据配置。 可能的属性包括（应用于列的所有单元格）： <br />
    <ul>
     <li>cellStyle： html样式 </li>
     <li>cellCls： css类 </li>
     <li>readOnly：true表示不能更改值 </li>
     <li>复选框：true可将列的所有单元格定义为复选框（true/false值） </li>
     <li>forcedPosition：整数值，用于指定在网格中必须放置列的位置（介于0和列数–1之间）<p><br /> </p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### 列元数据配置 {#columns-metadata-configuration}

您可以为每个列配置：

* 显示属性：html样式、CSS类和只读

* 复选框
* 强制位置

CSS和只读列

批量编辑器具有三个列配置：

* 单元格CSS类名称(cellCls)：添加到已配置列的每个单元格的CSS类名称。
* 单元格样式(cellStyle)：添加到已配置列的每个单元格的HTML样式。
* 只读(readOnly)：为已配置列的每个单元格设置只读。

配置必须定义为以下配置：

```
"colsMetadata": {
"Column name": {
     "cellStyle": "html style",
     "cellCls": "CSS class",
     "readOnly": true/false
}
}
```

以下示例可以在productlist组件(/apps/geometrixx/components/productlist/dialog/items/editor/colsMetadata)中找到：

```xml
            <colsMetadata jcr:primaryType="nt:unstructured">
                <Selection
                    jcr:primaryType="nt:unstructured"
                    checkbox="true"
                    forcedPosition="0"
                    headerText=""/>
                <ProductId
                    jcr:primaryType="nt:unstructured"
                    cellCls="productlist-cell-productid"
                    headerText="Product Id"/>
                <ProductName
                    jcr:primaryType="nt:unstructured"
                    cellStyle="background-color: #FFCC99;"
                    headerText="Product Name"/>
                <CatalogCode
                    jcr:primaryType="nt:unstructured"
                    cellStyle="background-color: #EDEDED;"
                    headerText="Catalog Code"/>
                <Color jcr:primaryType="nt:unstructured">
                    <editor
                        jcr:primaryType="nt:unstructured"
                        store="[Blue,Red,Yellow]"
                        triggerAction="all"
                        typeAhead="true"
                        xtype="combo"/>
                </Color>
                <SellingSku
                    jcr:primaryType="nt:unstructured"
                    headerText="Sku Id"/>
            </colsMetadata>
```

**复选框**

如果复选框配置属性设置为true，则该列的所有单元格都会呈现为复选框。 选中框将发送 **true** 到服务器保存servlet， **false** 否则。 在标题菜单中，您还可以 **全选** 或 **全部不选**. 如果所选标题是复选框列的标题，则会启用这些选项。

在前面的示例中，selection列仅包含复选框，如checkbox=&quot;true&quot;。

**强制位置**

强制位置元数据forcedPosition允许您指定列在网格中的放置位置：0是第一个位置，而 &lt;number of=&quot;&quot; columns=&quot;&quot;>-1是最后一个位置。 任何其他值将被忽略。 

在前面的示例中，选择列是第一列，即forcedPosition=&quot;0&quot;。

### 查询Servlet {#query-servlet}

默认情况下，查询Servlet位于 `/libs/wcm/core/components/bulkeditor/json.java`. 您可以配置其他路径以检索数据。

查询servlet的工作方式如下：它接收GQL查询并接收要返回的列，计算结果，并将结果作为JSON流发送回批量编辑器。

在产品列表组件用例中，发送到查询servlet的两个参数如下：

* 查询： &quot;path：/content/geometrixx/en/customers/jcr：content/par/productlist Cube&quot;
* 列：“Selection、ProductId、ProductName、Color、CatalogCode、SellingSku”

并且JSON流返回如下：

```
{
  "hits": [{
      "jcr:path": "/content/geometrixx/en/products/jcr:content/par/productlist/1258674828905",
      "ProductId": "21",
      "ProductName": "Cube",
      "Color": "Blue",
      "CatalogCode": "43244",
      "SellingSku": "32131"
    }
  ],
  "results": 1
}
```

每次点击对应于一个节点及其属性，并在网格中显示为一行。

您可以扩展查询Servlet以返回复杂的继承模型或返回存储在特定逻辑位置的节点。 查询Servlet可用于任何类型的复杂计算。 然后，网格可以显示存储库中多个节点的聚合行。 在这种情况下，这些行的修改和保存必须由保存Servlet管理。

### 保存Servlet {#save-servlet}

在批量编辑器的默认配置中，每一行都是一个节点，此节点的路径存储在行记录中。 批量编辑器通过jcr路径保持行和节点之间的链接。 当用户编辑网格时，将生成所有修改的列表。 用户单击时 **保存**，则会向每个路径发送一个POST查询，其中包含更新的属性值。 这是Sling概念的基础，如果每个单元格是节点的属性，则它工作正常。 但是，如果实施查询Servlet来执行继承计算，则该模型无法工作，因为查询Servlet返回的属性可以从其他节点继承。

保存Servlet的概念是，修改不会直接发布到每个节点，而是发布到执行保存作业的一个Servlet。 这使此servlet能够分析修改并将属性保存在正确的节点上。

每个更新的属性都将以下列格式发送到servlet：

* 参数名称： &lt;jcr path=&quot;&quot;>/&lt;property name=&quot;&quot;>

  示例： /content/geometrixx/en/products/jcr：content/par/productlist/1258674859000/SellingSku

* 值： &lt;value>

  示例: 12123

servlet需要知道catalogCode属性的存储位置。

/libs/wcm/bulkeditor/save/POST.jsp上提供了默认的保存Servlet实施，该实施用在产品列表组件中。 它获取请求中的所有参数(使用 &lt;jcr path=&quot;&quot;>/&lt;property name=&quot;&quot;> 格式)并在节点上使用JCR API写入属性。 如果节点不存在，它还会创建节点（网格插入行）。

请勿按原样使用默认代码，因为它重新实施服务器本机执行的操作(POST &lt;jcr path=&quot;&quot;>/&lt;property name=&quot;&quot;>)，因此只是一个很好的起点，用于构建可管理属性继承模型的保存Servlet。
