---
title: 使用Assembler Service
seo-title: 使用Assembler Service
description: 通过Assembler服务，您可以合并、重新排列和增强PDF和XDP文档，并获取有关PDF文档的信息。
seo-description: 通过Assembler服务，您可以合并、重新排列和增强PDF和XDP文档，并获取有关PDF文档的信息。
uuid: 1efce50b-2d98-408e-aa43-ac4999de41a8
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: 6a99042f-79c7-494b-bca0-73f2b5725b58
docset: aem65
translation-type: tm+mt
source-git-commit: d9975c0dcc02ae71ac64aadb6b4f82f7c993f32c

---


# 使用Assembler Service{#using-assembler-service}

通过Assembler服务，您可以合并、重新排列和增强PDF和XDP文档，并获取有关PDF文档的信息。 提交到Assembler服务的每个作业都包括文档描述XML(DDX)文档、源文档和外部资源（字符串和图形）。 有关汇编器服务的详细信息，请参 [阅汇编器服务概述](../../forms/using/overview-aem-document-services.md#p-assembler-service-p)。

您可以将装配服务用于以下操作：

## 组合PDF文档 {#assemble-pdf-documents}

您可以使用Assembler服务将两个或多个PDF文档组合到一个PDF文档或PDF包中。 您还可以将有助于导航或增强安全性的功能应用到PDF文档。 以下是汇编PDF文档的一些方式：

### 组合简单的PDF文档 {#assemble-a-simple-pdf-document}

下图显示了将三个源文档合并到一个生成文档中的情况。

![从多个PDF文档组合一个简单的PDF文档](assets/as_document_assembly.png)

从多个PDF文档组合一个简单的PDF文档

以下示例是用于组合文档的简单DDX文档。 它指定用于生成生成文档的源文档的名称以及生成文档的名称：

```xml
<PDF result="Doc4">
<PDF source="Doc1"/>
<PDF source="Doc2"/>
<PDF source="Doc3"/>
</PDF>
```

文档组件会生成包含以下内容和\
特征：

* 每个源文档的全部或部分
* 每个源文档的所有或部分书签，为组合的生成文档进行标准化
* 基本文档(Doc1)采用的其他特征，包括元数据、页面标签和页面大小
* 可选地，生成的文档包括从源文档中的书签构建的目录

### 创建PDF包 {#create-a-pdf-portfolio}

Assembler服务可创建包含文档集合和自包含用户界面的PDF包。 该界面称为PDF包布局或PDF包导航器（导航器）。 PDF包通过添加导航器、文件夹和欢迎页面扩展了PDF包的功能。 该界面可以利用本地化的文本字符串、自定义颜色方案和图形资源来增强用户体验。 PDF包还可以包含用于组织包中文件的文件夹。

当Assembler服务解释以下DDX文档时，它会组装一个PDF包，其中包括一个PDF包导航器和一个包含两个文件的包。 服务从myNavigator源指定的位置获取导航器。 它将导航器的默认颜色方案更改为pinkScheme颜色方案。

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

### 组合加密文档 {#assemble-encrypted-documents}

在组合文档时，您还可以使用口令加密PDF文档。 在用密码加密PDF文档后，用户必须指定密码才能在Adobe reader或Acrobat中查看PDF文档。 要使用口令加密PDF文档，DDX文档必须包含加密PDF文档所需的加密元素值。

加密服务不必成为LiveCycle安装的一部分，即可使用口令加密PDF文档。

如果一个或多个输入文档被加密，请提供作为DDX的一部分打开文档的口令。

### 使用Bates编号组合文档 {#assemble-documents-using-bates-numbering}

在组合文档时，可以使用Bates编号将唯一的页面标识符应用于每个页面。 当您使用Bates编号时，文档（或文档集）中的每个页面都会分配一个唯一标识该页面的编号。 例如，包含物料清单信息并与组件生产相关联的制造文档可以包含标识符。 Bates编号包含按顺序递增的数字值和可选前缀和后缀。 前缀+数字值+后缀称为bates模式。

下图显示了一个PDF文档，其中包含位于文档标题中的唯一标识符。

![包含位于文档标题中的唯一标识符的PDF文档](do-not-localize/as_batesnumber.png)

包含位于文档标题中的唯一标识符的PDF文档

### 拼合和组合文档 {#flatten-and-assemble-documents}

您可以使用Assembler服务将交互式PDF文档（例如，表单）转换为非交互式PDF文档。 交互式PDF文档允许用户输入或修改位于PDF文档字段中的数据。 将交互式PDF文档转换为非交互式PDF文档的过程称为拼合。 拼合PDF文档时，表单域将保留其图形外观，但不再具有交互性。 拼合PDF文档的一个原因是要确保无法修改数据。 此外，与字段关联的脚本不再起作用。

当您创建从交互式PDF文档组合的PDF文档时，Assembler服务会在将这些表单组合到生成的文档中之前拼合这些表单。

>[!NOTE]
>
>Assembler服务使用Output服务拼合动态XFA表单。 如果Assembler服务处理一个DDX，它要求它拼合XFA动态表单且Output服务不可用，则会引发异常。 Assembler服务可以拼合Acrobat表单或静态XFA表单，而无需使用Output服务。

## 组合XDP文档 {#assemble-xdp-documents}

您可以使用Assembler服务将多个XDP文档组合到一个XDP文档或一个PDF文档中。 对于包含插入点的源XDP文件，可以指定要插入的片段。

以下是组合XDP文档的一些方式：

### 组合一个简单的XDP文档 {#assemble-a-simple-xdp-document}

下图显示了将三个源XDP文档组合到一个生成的XDP文档中。 生成的XDP文档包含三个源XDP文档，包括它们的关联数据。 生成的文档从基础文档（即第一个源XDP文档）获取基本属性。

![从多个XDP文档组合一个简单的XDP文档](assets/as_assembler_xdpassembly.png)

从多个XDP文档组合一个简单的XDP文档

此处是生成上述结果的DDX文档。

```xml
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<XDP result="MyXDPResult">
<XDP source="sourceXDP1"/>
<XDP source="sourceXDP2"/>
<XDP source="sourceXDP3"/>
</XDP>
</DDX>
```

### 在组件过程中解析参照 {#resolving-references-during-assembly}

通常，XDP文档可以包含通过绝对或相对引用引用引用的图像。 默认情况下，汇编器服务会保留对生成的XDP文档中图像的引用。

可以指定汇编程序服务在汇编时通过XDP文件中的绝对或相对引用处理源XDP文档中引用的图像的方式。 您可以选择将所有图像嵌入到生成中，以使其不包含相对或绝对引用。 可通过设置resolveAssets标记的值来定义此值，该标记可采用以下任意选项。 默认情况下，结果文档中不解析任何引用。

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
   <td>在源XDP文档中嵌入通过相对引用引用引用的所有图像<br /> 。</td> 
  </tr> 
  <tr> 
   <td>绝对</td> 
   <td>在源XDP文档中嵌入通过绝对引用引用引用的所有图像<br /> 。</td> 
  </tr> 
 </tbody> 
</table>

您可以在XDP源标签或父XDP结果标签中指定resolveAssets属性的值。 如果将属性指定给XDP结果标签，则属性将由XDP结果的子级所有XDP源元素继承。 但是，显式指定源元素的属性将覆盖仅该源文档的结果元素的设置。

#### 解析XDP文档中的所有源引用 {#resolve-all-source-references-in-an-xdp-document}

要解析源XDP文档中的所有引用，请为\
生成文档至所有对象，如下例所示：

```xml
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<XDP result="result.xdp" resolveAssets="all">
<XDP source="input1.xdp" />
<XDP source="input2.xdp" />
<XDP source="input3.xdp" />
</XDP>
</DDX
```

您还可以指定所有源XDP文档的属性，以获得相同的\
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

#### 解析XDP文档中的选定源引用 {#resolve-selected-source-references-in-an-xdp-document}

您可以通过为要解析的源引用指定resolveAssets属性来选择性地指定这些引用。 单个源文档的属性将覆盖生成的XDP文档的设置。 在此示例中，包含的片段也会被解析。

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

#### 选择性解析绝对或相对引用 {#selectively-resolve-absolute-or-relative-references}

您可以选择性地解析所有或部分源文档中的绝对或相对引用，如下例所示：

```xml
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<XDP result="result.xdp" resolveAssets="absolute">
<XDP source="input1.xdp" />
<XDP source="input2.xdp" />
</XDP>
</DDX
```

### 将表单片段动态插入XFA表单 {#dynamically-insert-form-fragments-into-an-xfa-form}

您可以使用汇编器服务创建一个XFA表单，该表单是从插入片段的其他XFA表单创建的。 使用此功能，您可以使用片段创建多个表单。

表单片段的动态插入支持单源控件。 您可以维护一个常用组件的源。 例如，您可以为公司横幅创建片段。 如果横幅发生更改，您只需修改片段。 包含片段的其他表单保持不变。

表单设计人员使用LiveCycle Designer创建表单片段。 这些片段在XFA表单中是唯一命名的子表单。 表单设计人员还使用设计人员创建具有唯一命名的插入点的XFA表单。 您（程序员）编写DDX文档，指定如何将片段插入XFA表单。

下图显示了两个XML表单（XFA模板）。 左侧的表单包含一个名为myInsertionPoint的插入点。 右侧的表单包含一个名为myFragment的片段。

![将表单片段插入XFA表单](assets/as_assembler_fragment_assy_assembled.png)

将表单片段插入XFA表单

当Assembler服务解释以下DDX文档时，它将创建一个包含另一个XML表单的XML表单。 myFragmentSource文档中的myFragment子表单插入在myFormSource文档的myInsertionPoint中。

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

您可以使用Assembler服务将XDP文档打包为PDF文档，如此DDX文档所示。

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

## 反汇编PDF文档 {#disassemble-pdf-documents}

您可以使用汇编器服务反汇编PDF文档。 该服务可以从源文档中提取页面或基于书签划分源文档。 通常，如果PDF文档最初是从许多单独的文档（如语句集合）创建的，则此任务很有用。

### 从源文档提取页面 {#extract-pages-from-a-source-document}

在下图中，从源文档中提取第1-3页并将其放置在新的生成文档中。

![从源文档提取特定页面](assets/as_intro_page_extraction.png)

从源文档提取特定页面

以下示例是用于反汇编文档的DDX文档。

```xml
<PDF result="Doc4">
<PDF source="Doc2" pages="1-3"/>
</PDF>
```

### 根据书签划分源文档 {#divide-a-source-document-based-on-bookmarks}

在下图中，文档A被分为多个生成文档。 页面上的第1级书签标识新生成文档的开始。

![将基于书签的源文档分为多个文档](assets/as_intro_pdfsfrombookmarks.png)

将基于书签的源文档分为多个文档

以下示例是使用书签拆解源文档的DDX文档。

```xml
<PDFsFromBookmarks prefix="A">
<PDF source="DocA"/>
</PDFsFromBookmarks>
```

## 确定文档是否符合PDF/A规范 {#determine-whether-documents-are-pdf-a-compliant}

您可以使用Assembler服务确定PDF文档是否符合PDF/A规范。 PDF/A是一种存档格式，用于长期保留文档的内容。 字体嵌入到文档中，且文件未压缩。 因此，PDF/A文档通常大于标准PDF文档。 此外，PDF/A文档不包含音频和视频内容。

## 获取有关PDF文档的信息 {#obtain-information-about-a-pdf-document}

您可以使用Assembler服务获取有关PDF文档的以下信息：

* 文本信息。

   * 文档每页上的单词
   * 文档每页上每个单词的位置
   * 文档每页各段的句子

* 书签，包括页码、标题、目标和外观。 您可以导出此\
   从PDF文档导入数据并导入到PDF文档中。

* 文件附件，包括文件信息。 对于页面级附件，它还包括\
   文件附件注释的位置。 您可以从PDF文档导出此数据，\
   将其导入PDF文档。

* 包文件，包括文件信息、文件夹、包、架构和字段数据。 您可以从PDF文档导出此数据，然后将其导入PDF文档。

## 验证DDX文档 {#validate-ddx-documents}

您可以使用Assembler服务确定DDX文档是否有效。 例如，如果您从先前的LiveCycle版本升级，则验证可确保DDX文档有效。

## 拨叫其他服务 {#call-other-services}

可以使用DDX文档，它们会导致Assembler服务调用以下LiveCycle服务。 Assembler服务只能调用与LiveCycle一起安装的那些服务。

**Reader Extensions服务**:使Adobe reader用户能够对生成的PDF文档进行数字签名。

**表单服务**:合并XDP文件和XML数据文件以生成包含已填写的交互式表单的PDF文档。

**输出服务**:将动态XML表单转换为包含非交互式表单的PDF文档（平展表单）。 Assembler服务无需调用Output服务即可拼合静态XML表单和Acrobat表单。

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

使用DDX和Assembler服务调用其他LiveCycle服务可以简化流程图。 它甚至可以减少您自定义工作流程所花费的精力。 (另请参阅
