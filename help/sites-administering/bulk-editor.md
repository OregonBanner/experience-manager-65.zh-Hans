---
title: 批量编辑器
seo-title: 批量编辑器
description: 了解如何使用批量编辑器。
seo-description: 了解如何使用批量编辑器。
uuid: 5f5e4190-d9b2-40a6-8cf4-4b7aebe35ad3
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 3649cffb-418a-4ad6-862f-56346a831b0b
docset: aem65
exl-id: c63e044c-4d2a-44d3-853b-8e7337e1ee03
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1154'
ht-degree: 1%

---

# 批量编辑器{#the-bulk-editor}

当不需要可视页面上下文时，使用批量编辑器可以非常高效地进行编辑，因为它允许您：

* 从多个页面中搜索（和显示）内容；可使用GQL（Google查询语言）完成此操作
* 直接在批量编辑器中编辑此内容
* 保存更改（到原始页面）
* 将此内容导出到制表符分隔(.tsv)的电子表格文件

>[!NOTE]
>
>您也可以将内容导入存储库，但默认情况下，对于批量编辑器，该功能会处于禁用状态，该功能在&#x200B;**工具**&#x200B;控制台中可用。

本节介绍如何在&#x200B;**工具**&#x200B;控制台中使用批量编辑器。 通常，管理员会使用批量编辑器来搜索和编辑多个项目。 为此，可使用GQL查询填充表，然后选择要处理的内容项。 作者通常使用批量编辑器作为可通过[产品列表](/help/sites-authoring/default-components.md#productlist)组件访问的自定义批量编辑器应用程序的一部分。

>[!CAUTION]
>
>AEM 6.4中的[弃用经典UI](/help/release-notes/deprecated-removed-features.md)后，批量编辑器也已弃用，因此Adobe不打算进一步增强批量编辑器。

## 批量编辑器{#example-use-case-for-the-bulk-editor}的用例示例

例如，如果您需要填写特定调查的用户的所有名称和电子邮件地址，批量编辑器可以提供该信息，并将其导出到电子表格中。

Geometrixx网站中包含说明此类用例的示例：

1. 导航到&#x200B;**支持**&#x200B;页面，然后导航到&#x200B;**客户服务满意度**&#x200B;调查。
1. **** 编辑表 **单段** 落开头。在对话框中，单击&#x200B;**Advanced**&#x200B;选项卡，展开&#x200B;**Action Configuration**，然后单击&#x200B;**View Data..**。

   ![](assets/custsatsurvey.png)

1. 批量编辑器是完全可自定义的。尽管在本例中，批量编辑器不允许用户编辑内容，但只允许用户将信息导出到电子表格。

   ![](assets/bulkeditor.png)

## 如何使用批量编辑器{#how-to-use-the-bulk-editor}

批量编辑器允许您：

* [根据查询参数搜索内容，在列中显示结果的指定属性，编辑此内容并保存更改](#searching-and-editing-content)
* [将此内容导出到制表符分隔的电子表格](#exporting-content)

* [从制表符分隔的电子表格导入内容](#importing-content)

### 搜索和编辑内容{#searching-and-editing-content}

要使用批量编辑器同时编辑多个项目，请执行以下操作：

1. 在&#x200B;**工具**&#x200B;控制台中，单击&#x200B;**导入器**&#x200B;文件夹以展开它。
1. 双击&#x200B;**批量编辑器**&#x200B;以将其打开。
1. 输入选择要求：

<table>
 <tbody>
  <tr>
   <td>字段</td>
   <td>属性</td>
  </tr>
  <tr>
   <td>根路径</td>
   <td>指示批量编辑器搜索的根路径。<br /> 例如，  <code>/content/geometrixx/en</code>。批量编辑器会搜索所有子节点。</td>
  </tr>
  <tr>
   <td>查询参数</td>
   <td>使用GQL参数，输入您希望批量编辑器在存储库中查找的搜索字符串；例如，<code>type:Page</code>会查找根路径中的所有页面，<code>text:professional</code>会查找其中包含“professional”字样的所有页面，而<code>"jcr:title":English</code>会查找所有将“English”作为标题的页面。 您只能搜索字符串。</td>
  </tr>
  <tr>
   <td>“内容模式”复选框</td>
   <td>选中此复选框可读取搜索结果<code>jcr:content</code>子节点中的属性（如果存在）。 仅用于页面。 属性名称的前缀为 <code>"jcr:content/"</code></td>
  </tr>
  <tr>
   <td>属性/列</td>
   <td>选中要批量编辑器返回的属性的复选框。 您选择的属性是结果窗格中的列标题。 默认情况下，节点路径会显示在结果中。</td>
  </tr>
  <tr>
   <td>自定义属性/列</td>
   <td>输入未在<strong>Properties/Columns</strong>字段中列出的任何其他属性。 这些自定义属性显示在结果窗格中。 您可以使用逗号添加多个属性以分隔属性。 <i>注意：</i> 如果添加的自定义属性尚不存在，则AEM WCM会显示一个空单元格。修改并保存空单元格时，该属性会添加到节点中。 新创建的属性必须遵循节点类型约束和属性命名空间。</td>
  </tr>
 </tbody>
</table>

例如：

![](assets/searchfilter.png)

1. 单击&#x200B;**搜索**。 批量编辑器会显示结果。
对于上述示例，将返回符合搜索标准的所有页面并显示请求的列。

   ![](assets/chlimage_1-39.png)

1. 在单元格中双击，可进行所需的任何更改。

   ![](assets/srchresultedit.png)

1. 单击&#x200B;**Save**&#x200B;以保存更改（编辑单元格后，将激活&#x200B;**Save**&#x200B;按钮）。

   >[!CAUTION]
   >
   >您在此处所做的更改将写入存储库内容；例如，在&#x200B;**Path**&#x200B;中引用的页面。

#### 其他GQL查询参数{#additional-gql-query-parameters}

* **路径：** 仅搜索此路径下的节点。如果指定多个具有路径前缀的术语，则只考虑最后一个术语。
* **类型：** 仅返回给定节点类型的节点。这包括主类型和混合类型。 您可以指定多个以逗号分隔的节点类型。 GQL将返回任何指定类型的节点。
* **order:** 按给定属性对结果进行排序。您可以指定多个以逗号分隔的属性名称。 要按降序顺序对结果进行排序，只需在属性名称前添加减号。 例如：order:-name。 使用加号将以升序返回结果，这也是默认值。
* **限制：** 使用间隔限制结果数。例如：限制：10..20请注意，间隔基于零，开始包含，结束为排除。 您还可以指定打开间隔：limit:10.. 或限制：..20如果忽略点，并且只指定了一个值，则GQL最多将返回此数量的结果。 例如，limit:10（将返回前10个结果）

### 导出内容{#exporting-content}

您可能需要导出内容，并在Excel电子表格中对其进行更改。 例如，您可能希望导出邮件列表，并直接在Excel中更改所有列出电话号码的区号，添加其他行，等等。

要导出内容，请执行以下操作：

1. 按照[搜索和编辑内容](#searching-and-editing-content)中所述搜索内容。
1. 单击&#x200B;**导出**，将更改导出到以制表符分隔的Excel电子表格中。 AEM WCM会询问您要将文件下载到的位置。

   >[!NOTE]
   >
   >默认情况下，更改以[Windows-1252](https://en.wikipedia.org/wiki/Windows-1252)（也称为CP-1252）进行编码。 您可以选中UTF-8以导出UTF-8中的更改。

   ![](assets/srchrsesultexport.png)

1. 选择位置并确认要下载文件。
1. 下载文件后，您可以从电子表格程序（例如Microsoft Excel）中打开该文件。 电子表格程序会导入文件并将其转换为电子表格格式。

   ![](assets/exportinexcel.png)

### 导入内容{#importing-content}

默认情况下，打开批量编辑器时，导入功能会隐藏。 只需将参数`hib=false`添加到URL中，即会在“批量编辑器”页面上显示&#x200B;**Import**&#x200B;按钮。 您可以从任何制表符分隔的(`.tsv`)文件中导入内容。 为了使导入正常工作，列标题（单元格的第一行）必须与要导入到的表的列标题相匹配。

>[!NOTE]
>
>重新导入内容时，会擦除这些节点之前的任何内容。 注意不要覆盖重要信息。

要导入内容，请执行以下操作：

1. 打开批量编辑器。
1. 将`?hib=false`添加到URL中，例如：
   `https://localhost:4502/etc/importers/bulkeditor.html?hib=false`
1. 单击&#x200B;**导入**。
1. 选择`.tsv`文件。 数据将导入到存储库中。
