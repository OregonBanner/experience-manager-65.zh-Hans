---
title: 使用汇编程序服务
seo-title: 使用汇编程序服务
description: 汇编程序服务允许您组合、重新排列和扩充PDF和XDP文档，并获取有关PDF文档的信息。
seo-description: 汇编程序服务允许您组合、重新排列和扩充PDF和XDP文档，并获取有关PDF文档的信息。
uuid: 1efce50b-2d98-408e-aa43-ac4999de41a8
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: 6a99042f-79c7-494b-bca0-73f2b5725b58
docset: aem65
exl-id: 2acd6b19-0fe8-4994-b0f4-c9d5b9f3fdf1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2143'
ht-degree: 0%

---

# 使用汇编程序服务{#using-assembler-service}

汇编程序服务允许您组合、重新排列和扩充PDF和XDP文档，并获取有关PDF文档的信息。 提交给汇编程序服务的每个作业都包括文档描述XML(DDX)文档、源文档和外部资源（字符串和图形）。 有关汇编程序服务的更多信息，请参阅[汇编程序服务概述](../../forms/using/overview-aem-document-services.md#p-assembler-service-p)。

您可以将装配服务用于以下操作：

## 汇编PDF文档{#assemble-pdf-documents}

您可以使用汇编程序服务将两个或多个PDF文档组合成一个PDF文档或PDFPortfolio。 您还可以将有助于导航或增强安全性的功能应用于PDF文档。 以下是可以组合PDF文档的一些方法：

### 组合简单的PDF文档{#assemble-a-simple-pdf-document}

下图显示了合并到单个生成文档中的三个源文档。

![从多个PDF文档组合简单的PDF文档](assets/as_document_assembly.png)

从多个PDF文档组合简单的PDF文档

以下示例是用于组合文档的简单DDX文档。 它指定用于生成生成文档的源文档的名称以及生成文档的名称：

```xml
<PDF result="Doc4">
<PDF source="Doc1"/>
<PDF source="Doc2"/>
<PDF source="Doc3"/>
</PDF>
```

文档集将生成包含以下内容和\
特征：

* 每个源文档的全部或部分
* 每个源文档的所有或部分书签，已针对装配的结果文档进行标准化
* 基本文档(Doc1)采用的其他特征，包括元数据、页面标签和页面大小
* 可选地，生成的文档包括从源文档中的书签构建的目录

### 创建PDFPortfolio{#create-a-pdf-portfolio}

汇编程序服务可以创建包含文档集合和自包含用户界面的PDFPortfolio。 该界面称为PDFPortfolio布局或PDFPortfolio导航器（导航器）。 PDFPortfolio通过添加导航器、文件夹和欢迎页面扩展了PDF包的功能。 该界面可利用本地化的文本字符串、自定义颜色方案和图形资源来增强用户体验。 PDFPortfolio还可以包含用于组织组合中文件的文件夹。

当汇编程序服务解释以下DDX文档时，它会组合一个PDFPortfolio，该文件包括一个PDFPortfolio导航器和一个包含两个文件的包。 服务从myNavigator源指定的位置获取导航器。 它会将导航器的默认颜色方案更改为pinkScheme颜色方案。

```xml
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<PDF result="Untitled 1">
<Portfolio>
<Navigator source="myNavigator"/>
<ColorScheme scheme="pinkScheme"/>
</Portfolio>
<PackageFiles>
<PDF source="sourcePDF1"/>
<PDF source="sourcePDF2"/>
</PackageFiles>
</PDF>
</DDX>
```

### 组合加密文档{#assemble-encrypted-documents}

在组合文档时，还可以使用密码加密PDF文档。 使用密码加密PDF文档后，用户必须指定密码才能在Adobe Reader或Acrobat中查看PDF文档。 要使用密码加密PDF文档，DDX文档必须包含加密PDF文档所需的加密元素值。

加密服务不必包含在LiveCycle安装中，即可使用密码加密PDF文档。

如果一个或多个输入文档被加密，则提供作为DDX的一部分来打开文档的密码。

### 使用Bates编号{#assemble-documents-using-bates-numbering}来组合文档

在组合文档时，可以使用Bates编号来对每个页面应用唯一的页面标识符。 使用Bates编号时，文档（或文档集）中的每个页面都会分配一个唯一标识该页面的编号。 例如，包含物料清单信息并与组件生产相关联的制造文档可以包含标识符。 Bates编号包含按顺序递增的数值以及可选前缀和后缀。 前缀+数值+后缀称为Bates模式。

下图显示了一个PDF文档，其中包含位于文档标题中的唯一标识符。

![包含唯一标识符的PDF文档，位于文档标题中](do-not-localize/as_batesnumber.png)

包含唯一标识符的PDF文档，位于文档标题中

### 拼合和组合文档{#flatten-and-assemble-documents}

您可以使用汇编程序服务将交互式PDF文档（例如，表单）转换为非交互式PDF文档。 交互式PDF文档允许用户输入或修改位于PDF文档字段中的数据。 将交互式PDF文档转换为非交互式PDF文档的过程称为拼合。 对PDF文档进行扁平化处理后，表单字段会保留其图形外观，但不再具有交互性。 扁平化PDF文档的一个原因是为了确保数据无法修改。 此外，与字段关联的脚本将无法再正常工作。

在创建从交互式PDF文档装配的PDF文档时，汇编程序服务会先拼合这些表单，然后再将它们装配到生成的文档中。

>[!NOTE]
>
>汇编程序服务使用输出服务来拼合动态XFA表单。 如果汇编程序服务处理的DDX要求它扁平化XFA动态表单且输出服务不可用，则会引发异常。 汇编程序服务可以扁平化Acrobat表单或静态XFA表单，而无需使用输出服务。

## 汇编XDP文档{#assemble-xdp-documents}

您可以使用汇编程序服务将多个XDP文档组合到单个XDP文档或PDF文档中。 对于包含插入点的源XDP文件，您可以指定要插入的片段。

以下是可以组合XDP文档的一些方法：

### 组合简单的XDP文档{#assemble-a-simple-xdp-document}

下图显示了将三个源XDP文档组合到一个生成的XDP文档中。 生成的XDP文档包含三个源XDP文档，包括其关联数据。 生成的文档从基础文档（即第一个源XDP文档）中获取基本属性。

![从多个XDP文档组合一个简单的XDP文档](assets/as_assembler_xdpassembly.png)

从多个XDP文档组合一个简单的XDP文档

下面是一个DDX文档，该文档将生成上图所示的结果。

```xml
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<XDP result="MyXDPResult">
<XDP source="sourceXDP1"/>
<XDP source="sourceXDP2"/>
<XDP source="sourceXDP3"/>
</XDP>
</DDX>
```

### 在程序集{#resolving-references-during-assembly}期间解析引用

通常，XDP文档可以包含通过绝对或相对引用引用的图像。 默认情况下，汇编程序服务会保留对生成的XDP文档中图像的引用。

您可以指定汇编程序服务在组装时如何通过XDP文件中的绝对或相对引用来处理源XDP文档中引用的图像。 您可以选择将所有图像嵌入到结果中，以使其不包含相对或绝对参照。 您可以通过设置resolveAssets标记的值来定义此标记，该标记可采用以下任意选项。 默认情况下，结果文档中不解析任何引用。

<table>
 <tbody> 
  <tr> 
   <th>值</th> 
   <th>描述</th> 
  </tr> 
  <tr> 
   <td>无</td> 
   <td>不解析任何引用。</td> 
  </tr> 
  <tr> 
   <td>全部</td> 
   <td>在源XDP文档中嵌入所有引用的图像。</td> 
  </tr> 
  <tr> 
   <td>相对</td> 
   <td>在源XDP<br />文档中嵌入通过相对引用引用引用的所有图像。</td> 
  </tr> 
  <tr> 
   <td>绝对</td> 
   <td>在源XDP<br />文档中嵌入通过绝对引用引用引用的所有图像。</td> 
  </tr> 
 </tbody> 
</table>

您可以在XDP源标记或父XDP结果标记中指定resolveAssets属性的值。 如果为XDP结果标记指定了属性，则该属性将由所有XDP源元素继承，这些元素是XDP结果的子元素。 但是，显式指定源元素的属性将覆盖仅该源文档的结果元素的设置。

#### 解析XDP文档{#resolve-all-source-references-in-an-xdp-document}中的所有源引用

要解析源XDP文档中的所有引用，请为\
生成文档到所有人，如以下示例中所示：

```xml
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<XDP result="result.xdp" resolveAssets="all">
<XDP source="input1.xdp" />
<XDP source="input2.xdp" />
<XDP source="input3.xdp" />
</XDP>
</DDX
```

您还可以为所有源XDP文档指定属性，以便获得相同的属性\
个结果.

```xml
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<XDP result="result.xdp">
<XDP source="input1.xdp" resolveAssets="all"/>
<XDP source="input2.xdp" resolveAssets="all"/>
<XDP source="input3.xdp" resolveAssets="all"/>
</XDP>
</DDX>
```

#### 解析XDP文档{#resolve-selected-source-references-in-an-xdp-document}中选定的源引用

您可以通过为要解析的源引用指定resolveAssets属性来有选择地指定它们。 单个源文档的属性将覆盖生成的XDP文档的设置。 在此示例中，还会解析包含的片段。

```xml
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<XDP result="result.xdp" resolveAssets="all">
<XDP source="input1.xdp" >
<XDPContent source="fragment.xdp" insertionPoint="MyInsertionPoint"
fragment="myFragment"/>
</XDP>
<XDP source="input2.xdp" />
</XDP>
</DDX>
```

#### 选择性地解析绝对或相对引用{#selectively-resolve-absolute-or-relative-references}

您可以选择性地解析所有或部分源文档中的绝对或相对引用，如以下示例所示：

```xml
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<XDP result="result.xdp" resolveAssets="absolute">
<XDP source="input1.xdp" />
<XDP source="input2.xdp" />
</XDP>
</DDX
```

### 将表单片段动态插入XFA表单{#dynamically-insert-form-fragments-into-an-xfa-form}

您可以使用汇编程序服务创建一个XFA表单，该表单是从插入片段的其他XFA表单创建的。 使用此功能，您可以使用片段创建多个表单。

支持动态插入表单片段，支持单源控件。 您可以维护一个常用组件的源。 例如，您可以为公司横幅创建片段。 如果横幅发生更改，您只需修改片段即可。 包含片段的其他表单将保持不变。

表单设计人员使用LiveCycle设计器创建表单片段。 这些片段是XFA表单中唯一命名的子表单。 表单设计人员还使用Designer创建具有唯一命名插入点的XFA表单。 您（程序员）编写DDX文档，以指定如何将片段插入XFA表单。

下图显示了两个XML表单（XFA模板）。 左侧的表单包含一个名为myInsertionPoint的插入点。 右侧的表单包含一个名为myFragment的片段。

![将表单片段插入XFA表单](assets/as_assembler_fragment_assy_assembled.png)

将表单片段插入XFA表单

当汇编程序服务解释以下DDX文档时，它将创建包含另一个XML表单的XML表单。 myFragmentSource文档中的myFragment子表单会插入到myFormSource文档的myInsertionPoint中。

```xml
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<XDP result="myFormResult">
<XDP source="myFormSource">
<XDPContent fragment="myFragment" insertionPoint="myInsertionPoint"
source="myFragmentSource"/>
</XDP>
</XDP>
</DDX
```

### 将XDP文档打包为PDF {#package-an-xdp-document-as-pdf}

您可以使用汇编程序服务将XDP文档打包为PDF文档，如此DDX文档所示。

```xml
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<PDF result="Untitled 1" encryption="passEncProfile1">
<XDP>
<XDP source="sourceXDP3"/>
<XDP source="sourceXDP4"/>
</XDP>
</PDF>
</DDX>
```

## 反汇编PDF文档{#disassemble-pdf-documents}

您可以使用汇编程序服务来拆解PDF文档。 该服务可以从源文档中提取页面或基于书签划分源文档。 通常，如果PDF文档最初是从许多单独的文档（如语句集合）创建，则此任务会很有用。

### 从源文档{#extract-pages-from-a-source-document}中提取页面

在下图中，从源文档中提取页面1-3，并将其放置在新的生成文档中。

![从源文档提取特定页面](assets/as_intro_page_extraction.png)

从源文档提取特定页面

以下示例是用于拆解文档的DDX文档。

```xml
<PDF result="Doc4">
<PDF source="Doc2" pages="1-3"/>
</PDF>
```

### 根据书签{#divide-a-source-document-based-on-bookmarks}划分源文档

在下图中，文档A分为多个生成文档。 页面上的第一级书签标识新生成文档的开始。

![将基于书签的源文档划分为多个文档](assets/as_intro_pdfsfrombookmarks.png)

将基于书签的源文档划分为多个文档

以下示例是使用书签拆解源文档的DDX文档。

```xml
<PDFsFromBookmarks prefix="A">
<PDF source="DocA"/>
</PDFsFromBookmarks>
```

## 确定文档是否符合PDF/A规范{#determine-whether-documents-are-pdf-a-compliant}

您可以使用汇编程序服务来确定PDF文档是否符合PDF/A规范。 PDF/A是一种存档格式，用于长期保存文档内容。 字体嵌入在文档中，且文件未压缩。 因此，PDF/A文档通常比标准PDF文档大。 此外，PDF/A文档不包含音频和视频内容。

## 获取有关PDF文档{#obtain-information-about-a-pdf-document}的信息

您可以使用汇编程序服务获取有关PDF文档的以下信息：

* 文本信息。

   * 文档每个页面上的词语
   * 每个单词在文档每个页面上的位置
   * 文档每页各段的句子

* 书签，包括页码、标题、目标和外观。 您可以导出此\
   从PDF文档中获取的数据并将其导入PDF文档。

* 文件附件，包括文件信息。 对于页面级别的附件，它还包含\
   文件附件注释的位置。 您可以从PDF文档导出此数据，\
   将其导入PDF文档。

* 包文件，包括文件信息、文件夹、包、架构和字段数据。 您可以从PDF文档导出此数据，并将其导入PDF文档。

## 验证DDX文档{#validate-ddx-documents}

您可以使用汇编程序服务来确定DDX文档是否有效。 例如，如果您从以前的LiveCycle版本升级，则验证会确保DDX文档有效。

## 调用其他服务{#call-other-services}

您可以使用DDX文档，该文档会导致汇编程序服务调用以下LiveCycle服务。 汇编程序服务只能调用那些随LiveCycle安装的服务。

**Reader扩展服务**:使Adobe Reader用户能够对生成的PDF文档进行数字签名。

**Forms服务**:合并XDP文件和XML数据文件，以生成包含已填写交互式表单的PDF文档。

**输出服务**:将动态XML表单转换为包含非交互式表单（拼合表单）的PDF文档。汇编程序服务可拼合静态XML表单和Acrobat表单，而无需调用输出服务。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<PDF result="outDoc">
<PDF source="doc1"/>
<PDF source="doc2"/>
<ReaderRights
credentialAlias="LCESCred"
digitalSignatures="true"/>
</PDF>
</DDX>
```

使用DDX和汇编程序服务调用其他LiveCycle服务可以简化流程图。 它甚至可以减少您在自定义工作流方面花费的工作量。 (另请参阅
