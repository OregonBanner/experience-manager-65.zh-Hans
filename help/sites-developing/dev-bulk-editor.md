---
title: 开发批量编辑器
seo-title: 开发批量编辑器
description: 标记允许对内容进行分类和组织
seo-description: 标记允许对内容进行分类和组织
uuid: 3cd04c52-5bdb-47f6-9fa3-d7a4937e8e20
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: e9a1ff95-e88e-41f0-9731-9a59159b4653
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 开发批量编辑器{#developing-the-bulk-editor}

本节介绍如何开发批量编辑器工具以及如何扩展基于批量编辑器的产品列表组件。

## 批量编辑器查询参数 {#bulk-editor-query-parameters}

使用批量编辑器时，可以向URL添加多个查询参数，以调用具有特定配置的批量编辑器。 如果您希望批量编辑器始终与某个配置（例如，在“产品列表”组件中）一起使用，则需要修改bulkeditor.jsp（位于/libs/wcm/core/components/bulkeditor中）或使用特定配置创建组件。 使用查询参数所做的更改不是永久的。

例如，如果在浏览器的URL中键入以下内容：

`https://<servername><port_number>/etc/importers/bulkeditor.html?rootPath=/content/geometrixx/en&queryParams=geometrixx&initialSearch=true&hrp=true`

显示批量编辑器时， **不显示“根路径** ”字段，因为hrp=true将隐藏该字段。 当参数hrp=false时，将显示字段（默认值）。

以下是批量编辑器查询参数的列表：

>[!NOTE]
>
>每个参数都可以有长名和短名。 例如，搜索根路径的长名称是 `rootPath`，短名称是 `rp`。 如果未定义长名称，则从请求中读取短名称。

<table>
 <tbody>
  <tr>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td><p> 参数</p> <p>（长名／短名）<br /> </p> </td>
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
   <td> 布尔型</td>
   <td> 如果为true，则启用内容模式<br /> </td>
  </tr>
  <tr>
   <td> colsValue / cv<br /> </td>
   <td> String[]</td>
   <td> 搜索的属性（cols中的选定值显示为复选框的选定值）</td>
  </tr>
  <tr>
   <td> extraCols / ec<br /> </td>
   <td> String[]</td>
   <td> 搜索到的其他属性（显示在以逗号分隔的文本字段中）</td>
  </tr>
  <tr>
   <td> initialSearch / is<br /> </td>
   <td> 布尔型</td>
   <td> 如果为true，则在页面加载时执行查询<br /> </td>
  </tr>
  <tr>
   <td> colsSelection / cs<br /> </td>
   <td> String[]</td>
   <td> 搜索的属性选择（显示为复选框）</td>
  </tr>
  <tr>
   <td> showGridOnly / sgo<br /> </td>
   <td> 布尔型</td>
   <td> 如果为true，则仅显示网格，而不显示搜索面板 <br /> </td>
  </tr>
  <tr>
   <td> searchPanelCollapsed / spc</td>
   <td> 布尔型</td>
   <td> 如果为true，则加载时搜索面板将折叠</td>
  </tr>
  <tr>
   <td> hideRootPath / hrp</td>
   <td> 布尔型</td>
   <td> 当为true时，隐藏根路径字段</td>
  </tr>
  <tr>
   <td> hideQueryParams / hqp</td>
   <td> 布尔型</td>
   <td> 当为true时，隐藏查询字段</td>
  </tr>
  <tr>
   <td> hideContentMode / hcm</td>
   <td> 布尔型</td>
   <td> 当为true时，隐藏内容模式字段</td>
  </tr>
  <tr>
   <td> hideColsSelection / hcs</td>
   <td> 布尔型</td>
   <td> 当为true时，隐藏列选择字段</td>
  </tr>
  <tr>
   <td> hideExtraCols / hec</td>
   <td> 布尔型</td>
   <td> 当为true时，隐藏额外的列字段</td>
  </tr>
  <tr>
   <td> hideSearchButton</td>
   <td> 布尔型</td>
   <td> 当为true时，隐藏搜索按钮</td>
  </tr>
  <tr>
   <td> hideSaveButton / hsavep</td>
   <td> 布尔型</td>
   <td> 当为true时，隐藏保存按钮</td>
  </tr>
  <tr>
   <td> hideExportButton / hexpb</td>
   <td> 布尔型</td>
   <td> 当为true时，隐藏导出按钮</td>
  </tr>
  <tr>
   <td> hideImportButton / hib</td>
   <td> 布尔型</td>
   <td> 当为true时，隐藏导入按钮</td>
  </tr>
  <tr>
   <td> hideResultNumber / hrn</td>
   <td> 布尔型</td>
   <td> 当为true时，隐藏网格搜索结果编号文本</td>
  </tr>
  <tr>
   <td> hideInsertButton / hinsertb</td>
   <td> 布尔型</td>
   <td> 当为true时，隐藏网格插入按钮</td>
  </tr>
  <tr>
   <td> hideDeleteButton / hdelb</td>
   <td> 布尔型</td>
   <td> 当为true时，隐藏网格删除按钮</td>
  </tr>
  <tr>
   <td> hidePathCol / hpc</td>
   <td> 布尔型</td>
   <td> 当为true时，隐藏网格“路径”列</td>
  </tr>
 </tbody>
</table>

### 开发基于批量编辑器的组件：产品列表组件 {#developing-a-bulk-editor-based-component-the-product-list-component}

本节概述了如何使用批量编辑器，并基于批量编辑器介绍了现有的Geometrixx组件：产品列表组件。

产品列表组件允许用户显示和编辑数据表。 例如，您可以使用产品列表组件来表示目录中的产品。 该信息将显示在标准HTML表中，并且任何编辑操作都会在“编辑”对话框中执 **行** ，该对话框包含一个BulkEditor构件。 (此批量编辑器与/etc/importers/bulkeditor.html上可访问的编辑器或通过“工具”菜单访问的编辑器完全相同)。 产品列表组件已针对特定的有限批量编辑器功能进行配置。 可以配置批量编辑器的每个部分（或从批量编辑器派生的组件）。

使用批量编辑器，您可以添加、修改、删除、筛选和导出行，保存修改并导入一组行。 每行都作为节点存储在产品列表组件实例本身下。 每个单元格都是每个节点的属性。 这是一个设计选择，它可以轻松更改，例如，您可以将节点存储在存储库中的其他位置。 查询servlet的角色是返回要显示的节点列表；搜索路径定义为产品列表实例。

产品列表组件的源代码位于/apps/geometrixx/components/productlist存储库中，由多个部分组成，如所有AEM组件：

* HTML渲染：渲染在JSP文件(/apps/geometrixx/components/productlist/productlist.jsp)中完成。 JSP读取当前产品列表组件的子节点，并将每个子节点显示为HTML表的一行。
* “编辑”对话框，在该对话框中可定义批量编辑器配置。 配置对话框以匹配组件的需求：列以及对网格或搜索执行的可能操作。 有关 [所有配置属性的信息](#bulk-editor-configuration-properties) ，请参阅批量编辑器配置属性。

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
   <td>contentMode</td>
   <td>启用内容模式为true:属性在jcr:content节点上读取，而不在搜索结果节点上读取</td>
  </tr>
  <tr>
   <td>colsValue</td>
   <td>搜索的属性（cols中的选定值显示为复选框的选择）</td>
  </tr>
  <tr>
   <td>extraCols</td>
   <td>额外搜索的属性（以逗号分隔的文本字段显示）</td>
  </tr>
  <tr>
   <td>initialSearch</td>
   <td>如果为True，则在页面加载时执行查询</td>
  </tr>
  <tr>
   <td>colsSelection</td>
   <td>搜索到的属性选择（显示为复选框）</td>
  </tr>
  <tr>
   <td>showGridOnly</td>
   <td>如果为true，则仅显示网格而不显示搜索面板（请勿忘记将initialSearch设置为true）</td>
  </tr>
  <tr>
   <td>searchPanelCollapsed</td>
   <td>默认情况下，“true”可折叠搜索面板</td>
  </tr>
  <tr>
   <td>hideRootPath</td>
   <td>隐藏根路径字段</td>
  </tr>
  <tr>
   <td>hideQueryParams</td>
   <td>隐藏查询字段</td>
  </tr>
  <tr>
   <td>hideContentMode</td>
   <td>隐藏内容模式字段</td>
  </tr>
  <tr>
   <td>hideColsSelection</td>
   <td>隐藏列选择字段</td>
  </tr>
  <tr>
   <td>hideExtraCols</td>
   <td>隐藏额外的列字段</td>
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
   <td>hideInsertButton</td>
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
   <td>查询servlet的路径</td>
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
   <td>商店</td>
   <td>商店配置</td>
  </tr>
  <tr>
   <td>colModel</td>
   <td>网格列模型配置</td>
  </tr>
  <tr>
   <td>rootPathInput</td>
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
   <td>colsSelection构件配置</td>
  </tr>
  <tr>
   <td>extraColsInput</td>
   <td>extraCols构件配置</td>
  </tr>
  <tr>
   <td>colsMetadata</td>
   <td>列元数据配置。 可能的属性（应用于列的所有单元格）: <br />
    <ul>
     <li>cellStyle:html样式 </li>
     <li>cellCls:css类 </li>
     <li>readOnly:true to not cable change value </li>
     <li>复选框：true：将列的所有单元格定义为复选框（true/false值） </li>
     <li>forcedPosition:整数值，用于指定必须在网格中放置列的位置（在0和列数-1之间）<p><br /> </p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### 列元数据配置 {#columns-metadata-configuration}

可以为每列配置：

* 显示属性：html样式、CSS类和只读

* 复选框
* 强制性职位

CSS和只读列

批量编辑器有三列配置：

* 单元格CSS类名称(cellCls):添加到已配置列的每个单元格的CSS类名。
* 单元格样式(cellStyle):添加到已配置列的每个单元格的HTML样式。
* 只读（只读）:为配置列的每个单元格设置只读。

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

可以在产品列表组件（/apps/geometrixx/components/productlist/dialog/items/editor/cols元数据）中找到以下示例：

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

如果复选框配置属性设置为true，则列的所有单元格将呈现为复选框。 复选框将 **true** 发送到服务器保存Servlet，否 **则为false** 。 在标题菜单中，您还可以选择 **全部** 或 **选择无**。 如果选定的标题是复选框列的标题，则这些选项将处于启用状态。

在前一个示例中，选择列仅包含复选框=&quot;true&quot;。

**强迫位置**

通过强制位置元数据forcedPosition，可指定列在网格中的位置：0是第一个位置，&lt;列数>-1是最后一个位置。 将忽略任何其他值。

在前一个示例中，选择列是第一个列，作为forcedPosition=&quot;0&quot;。

### 查询Servlet {#query-servlet}

默认情况下，可在上找到查询servlet `/libs/wcm/core/components/bulkeditor/json.java`。 您可以配置其他路径以检索数据。

查询Servlet的工作方式如下：它接收GQL查询和要返回的列，计算结果，并将结果作为JSON流发送回批量编辑器。

在“产品列表”组件情况下，发送到Query servlet的两个参数如下：

* 查询：&quot;path:/content/geometrixx/cn/customers/jcr:content/par/productlist Cube&quot;
* cols:“选择，产品ID，产品名称，颜色，目录代码，销售SKU”

并且返回的JSON流如下所示：

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

每次点击都对应一个节点及其属性，并在网格中显示为一行。

您可以扩展Query servlet以返回复杂的继承模型或返回存储在特定逻辑位置的节点。 查询Servlet可用于进行任何类型的复杂计算。 然后，网格可显示作为存储库中多个节点的聚合的行。 在这种情况下，这些行的修改和保存必须由保存Servlet管理。

### 保存Servlet {#save-servlet}

在批量编辑器的默认配置中，每行都是一个节点，该节点的路径存储在行记录中。 批量编辑器通过jcr路径保留行与节点之间的链接。 当用户编辑网格时，将生成所有修改的列表。 当用户单击“ **保存**”时，POST查询将发送到具有更新的属性值的每个路径。 这是Sling概念的基础，如果每个单元是节点的属性，则其工作良好。 但是，如果实现Query servlet进行继承计算，则此模型不能作为Query servlet返回的属性从另一个节点继承。

保存servlet的概念是修改不会直接发布到每个节点，而是发布到执行保存作业的一个servlet。 这使此Servlet能够分析修改并在正确的节点上保存属性。

每个更新的属性都将以下列格式发送到servlet:

* 参数名称：&lt;jcr path>/&lt;property name>

   示例：/content/geometrixx/cn/products/jcr:content/par/productlist/1258674859000/SellingSku

* 值：&lt;value>

   示例: 12123

servlet需要知道catalogCode属性的存储位置。

默认的保存Servlet实现位于/libs/wcm/bulkeditor/save/POST.jsp，用于产品列表组件。 它从请求中获取所有参数（格式为&lt;jcr path>/&lt;property name>），并使用JCR API在节点上写入属性。 如果节点不存在（网格插入的行），它也会创建节点。

默认代码不应按原样使用，因为它重新实现了服务器本机操作（&lt;jcr path>/&lt;property name>上的POST），因此它只是构建将管理属性继承模型的Save servlet的一个好起点。
