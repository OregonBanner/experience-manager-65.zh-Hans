---
title: 从AEM Workflow启动Document Services API
seo-title: 从AEM Workflow启动Document Services API
description: 了解如何在DDX或提供的输入中调用AEM文档服务。 另请参阅如何将PDF转换为PDF/A
seo-description: 了解如何在DDX或提供的输入中调用AEM文档服务。 另请参阅如何将PDF转换为PDF/A
uuid: aacec2df-1ad6-4ff2-a99d-ef206efcdc09
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: 8b85bdc7-3864-49c9-81b0-cf15b8e986d9
translation-type: tm+mt
source-git-commit: 7caf09f7020c066072eac04a349a19b144dfeb7b

---


# 从AEM Workflow启动Document Services API {#initiate-document-services-apis-from-aem-workflow}

## 汇编器 {#assembler}

AEM Forms提供自定义工作流以调用以下Assembler服务API:

* **invoke**:调用在输入DDX中指定的对提供的输入的操作。
* **toPDFA**:将输入的PDF文档转换为PDF/A文档。

### 调用DDX工作流 {#invoke-ddx-workflow}

调 **用DDX** 工作流调用 `Invoke` Assembler服务API，您可以使用它来组合或反汇编文档、向PDF添加水印等。

1. 将调用 **[!UICONTROL DDX工作流步骤拖到Sidekick中的“表单工作流]** ”选项卡下。
1. 双击添加的工作流步骤以编辑组件。
1. 在“编辑”组件对话框中，配置输入文档、环境选项和输出文档，然后单击“确 **[!UICONTROL 定”]**。

#### Input documents {#input-documents}

调用DDX工作流需要以下输入文档：

* **DDX**:它是调用DDX工作流步骤的必需输入，可以通过从DDX输入下拉列表中选择以下选项之一来指定它。

   * *相对于有效负荷*:DDX输入文件相对于工作流项目的有效负荷文件夹。
   * *使用有效负荷*:工作流项的有效负荷用作输入DDX文档。
   * *绝对路径*:CRX存储库中DDX文档的绝对路径。

* **从PayLoad创建地图**:选择此选项后，有效负荷文件夹下的所有文档将添加到Assembler中API的“输入文档 `invoke` 映射”中。 每个文档的节点名称将用作映射中的键。

* **输入文档的映射**:指定输入文档的映射。 您可以添加任意数量的条目，其中每个条目在地图中指定文档的键和文档的源。

#### Environment options {#environment-options}

“环境选项”选项卡允许您为调用API设置各种处理选项。

* *作业日志级别*:指定处理日志的日志级别。
* *仅验证*:检查输入DDX的有效性。

* *错误时失败*:指定在出错时对Assembler服务的调用是否应失败。 默认值为False。

#### Output documents {#output-documents}

根据输入DDX，调用API可以生成多个输出文档。 “输出文档”选项卡允许您选择输出文档的保存位置。

1. *在有效负荷中保存输出*:将输出文档保存在有效负荷文件夹下，或覆盖有效负荷（如果有效负荷是文件）。
1. *输出文档的映射*:允许通过为每个输出文档添加一个条目来显式指定保存每个输出文档的位置。 每个条目指定文档以及保存文档的位置。 输出文档可覆盖有效负荷或保存在有效负荷文件夹下。 当有多个输出文档时，此功能很有用。

1. *作业日志*:指定将作业日志文档保存到何处，这对于故障诊断很有帮助。

### Convert to PDF/A workflow {#convert-to-pdf-a-workflow}

“转换为PDF/A”工作流步骤将调用 `toPDFA` Assembler服务API。 它用于将PDF文档转换为符合PDF/A规范的文档。

1. 将“转 **[!UICONTROL 换为PDFA]** ”工作流步骤拖到Sidekick中的“表单工作流”选项卡下。

1. 双击添加的工作流步骤以编辑组件。
1. 在编辑组件对话框中，配置输入文档、转换选项和输出文档，然后单击确 **[!UICONTROL 定]**。

#### Input documents {#input-documents-1}

通过以下方式之一指定要转换为符合PDF/A规范的文档的源。

* *相对于有效负荷*:输入文档相对于工作流项目的有效负荷文件夹。
* *使用有效负荷*:工作流项的有效负荷用作输入文档。
* *绝对路径*:CRX存储库中输入文档的绝对路径。

#### Conversion options {#conversion-options}

“转换选项”允许您指定用于更改PDF/A转换过程的选项。

* *合规* :指定输出PDF/A必须符合的PDF/A标准。
* *结果级别* :指定用于PDF/A转换日志的日志级别。
* *签名* :指定在转换过程中必须如何处理输入文档中的签名。
* *色彩空间* :指定用于输出PDF/A文档的预定义色彩空间。
* *验证转换* :指定转换后是否应验证转换的PDF/A文档是否符合PDF/A规范。
* *作业日志级别* :指定用于处理日志的日志级别。

* *元数据扩展架构* :指定用于PDF文档元数据中XMP属性的元数据扩展架构的路径。

#### Output documents {#output-documents-1}

“输出文档”选项卡允许您指定输出文档的目标位置

* *PDFA文档*:指定保存转换的PDF/A文档的位置。 它可以覆盖有效负荷文档或保存在有效负荷文件夹下。
* *转换日志*:指定保存转换日志的位置。 它可以覆盖有效负荷文档，也可以保存在有效负荷文件夹下。

## Forms {#forms}

“渲染PDF表单”工作流程是围绕 `renderPDFForm` Forms服务API的包装器，用于使用XDP模板和data xml创建PDF表单。

### 渲染PDF表单工作流 {#render-pdf-form-workflow}

1. 将“渲染PDF表单”工作流步骤拖到Sidekick中的“表单工作流”选项卡下。
1. 双击添加的工作流步骤以编辑组件。
1. 在“编辑”组件对话框中，配置输入文档、输出文档和其他参数，然后单击“确 **[!UICONTROL 定”]**。

#### Input documents {#input-documents-2}

* *模板文件*:指定XDP模板的位置。 这是必填字段。

* *数据文档*:指定需要与模板合并的数据xml的位置。

#### Output documents {#output-documents-2}

* *输出文档*:-指定生成的PDF表单的名称。

#### 其他参数 {#additional-parameters}

* *内容根*:指定存储在输入XDP模板中使用的片段或图像的存储库中的文件夹路径。
* *提交Url*:为生成的PDF表单指定默认提交URL。
* *区域设置*:指定生成的PDF表单的默认区域设置。
* *Acrobat版本*:为生成的PDF表单指定目标Acrobat版本。
* *加标签的PDF*:指定是否使生成的PDF可访问。
* *XCI文档*:指定XCI文件的路径。

## 输出 {#output}

“生成非交互式PDF工作流”是包含 `generatePDFOutput` Output服务API的包装器。 它用于从XDP模板和数据xml生成非交互式PDF文档。

### 生成非交互式PDF输出工作流 {#generate-non-interactive-pdf-output-workflow-nbsp}

1. 将“生成非交互式PDF输出”工作流程拖到Sidekick中的“表单工作流”选项卡下。
1. 双击添加的工作流步骤以编辑组件。
1. 在“编辑”组件对话框中，配置输入文档、输出文档和其他参数，然后单击“确 **[!UICONTROL 定”]**。

#### Input documents {#input-documents-3}

* *模板文件*:指定XDP模板的位置。 这是必填字段。

* *数据文档*:指定需要与模板合并的数据xml的位置。

#### Output document {#output-document}

*输出文档*:指定生成的PDF表单的名称。

#### 其他参数 {#additional-parameters-1}

* *内容根*:指定存储在输入XDP模板中使用的片段或图像的存储库中的文件夹路径。
* *区域设置*:为生成的PDF表单指定默认区域设置。
* *Acrobat版本*:为生成的PDF表单指定目标Acrobat版本。
* 线性化PDF:指定是否为Web查看优化生成的PDF。
* *加标签的PDF*:指定是否使生成的PDF可访问。
* *XCI文档*:指定XCI文件的路径。

