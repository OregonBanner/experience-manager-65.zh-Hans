---
title: 从AEM工作流启动文档服务API
seo-title: 从AEM工作流启动文档服务API
description: 了解如何在DDX或提供的输入中调用AEM文档服务。 另请参阅如何将PDF转换为PDF/A
seo-description: 了解如何在DDX或提供的输入中调用AEM文档服务。 另请参阅如何将PDF转换为PDF/A
uuid: aacec2df-1ad6-4ff2-a99d-ef206efcdc09
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: 8b85bdc7-3864-49c9-81b0-cf15b8e986d9
exl-id: 123087a2-9d09-4579-9185-2ccd7d25bf8d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1199'
ht-degree: 0%

---

# 从AEM工作流{#initiate-document-services-apis-from-aem-workflow}启动文档服务API

## 汇编程序 {#assembler}

AEM Forms提供了自定义工作流以调用以下汇编程序服务API:

* **调用**:调用在输入DDX中指定的对提供的输入的操作。
* **到PDFA**:将输入的PDF文档转换为PDF/A文档。

### 调用DDX工作流{#invoke-ddx-workflow}

**调用DDX**&#x200B;工作流会调用`Invoke`汇编程序服务API，您可以使用该API来汇编或拆解文档、向PDF添加水印等。

1. 将&#x200B;**[!UICONTROL 调用DDX]**&#x200B;工作流步骤拖到Sidekick中的Forms Workflow选项卡下。
1. 双击添加的工作流步骤以编辑组件。
1. 在编辑组件对话框中，配置输入文档、环境选项和输出文档，然后单击&#x200B;**[!UICONTROL 确定]**。

#### 输入文档{#input-documents}

调用DDX工作流需要以下输入文档：

* **DDX**:它是调用DDX工作流步骤的必备输入，可通过从DDX输入下拉列表中选择以下选项之一来指定。

   * *相对于有效负载*:DDX输入文件相对于工作流项目的有效负荷文件夹。
   * *使用负载*:工作流项目的有效负荷用作输入DDX文档。
   * *绝对路径*:CRX存储库中DDX文档的绝对路径。

* **通过PayLoad创建映射**:选择后，有效载荷文件夹下的所有文档都将添加到汇编程序中API的输入 `invoke` 文档映射中。每个文档的节点名称将用作映射中的键。

* **输入文档的映射**:指定输入文档的映射。您可以添加任意数量的条目，其中每个条目在映射中指定文档的键和文档的源。

#### 环境选项{#environment-options}

环境选项选项卡允许您为调用API设置各种处理选项。

* *作业日志级别*:指定处理日志的日志级别。
* *仅验证*:检查输入DDX的有效性。

* *出错时失败*:指定在出错时对汇编程序服务的调用是否应失败。默认值为False。

#### 输出文档{#output-documents}

根据输入DDX，调用API可以生成多个输出文档。 “输出文档”(Output Documents)选项卡允许您选择输出文档的保存位置。

1. *在负载中保存输出*:将输出文档保存在有效负载文件夹下，或覆盖有效负载（如果有效负载是文件）。
1. *输出文档的映射*:允许通过为每个输出文档添加一个条目来明确指定保存每个输出文档的位置。每个条目指定文档以及保存文档的位置。 输出文档可能会覆盖有效负载或保存在有效负载文件夹下。 当存在多个输出文档时，此插件非常有用。

1. *作业日志*:指定保存作业日志文档的位置，这有助于对失败进行故障诊断。

### 转换为PDF/A工作流{#convert-to-pdf-a-workflow}

转换为PDF/A工作流步骤将调用`toPDFA`汇编程序服务API。 它用于将PDF文档转换为PDF/A兼容文档。

1. 将&#x200B;**[!UICONTROL ConvertToPDFA]**&#x200B;工作流步骤拖到Sidekick中的Forms Workflow选项卡下。

1. 双击添加的工作流步骤以编辑组件。
1. 在编辑组件对话框中，配置输入文档、转换选项和输出文档，然后单击&#x200B;**[!UICONTROL 确定]**。

#### 输入文档{#input-documents-1}

通过以下方式之一指定要转换为PDF/A兼容文档的文档源。

* *相对于有效负载*:输入文档与工作流项目的有效负荷文件夹相关。
* *使用负载*:工作流项目的有效负荷用作输入文档。
* *绝对路径*:CRX存储库中输入文档的绝对路径。

#### 转换选项{#conversion-options}

“转换选项”允许您指定用于更改PDF/A转换过程的选项。

* *合规性* :指定输出PDF/A必须符合的PDF/A标准。
* *结果级别* :指定用于PDF/A转换日志的日志级别。
* *签名* :指定在转换过程中必须处理输入文档中的签名的方式。
* *色彩空间* :指定要用于输出PDF/A文档的预定义色彩空间。
* ** 验证转化：指定在转换后是否应验证已转换的PDF/A文档是否符合PDF/A规范。
* *作业日志级别* :指定要用于处理日志的日志级别。

* *元数据扩展架构* :指定要用于PDF文档元数据中XMP属性的元数据扩展架构的路径。

#### 输出文档{#output-documents-1}

“输出文档”选项卡允许您指定输出文档的目标

* *PDFA文档*:指定保存已转换的PDF/A文档的位置。它可以覆盖有效负载文档或保存在有效负载文件夹下。
* *转化日志*:指定保存转换日志的位置。它可以覆盖有效负载文档，也可以保存在有效负载文件夹下。

## 表单 {#forms}

“渲染PDF表单”工作流是`renderPDFForm` Forms服务API的包装器，用于使用XDP模板和数据xml创建PDF表单。

### 渲染PDF表单工作流{#render-pdf-form-workflow}

1. 将“渲染PDF表单”工作流步骤拖动到Sidekick中的Forms Workflow选项卡下方。
1. 双击添加的工作流步骤以编辑组件。
1. 在“编辑组件”对话框中，配置输入文档、输出文档和其他参数，然后单击&#x200B;**[!UICONTROL 确定]**。

#### 输入文档{#input-documents-2}

* *模板文件*:指定XDP模板的位置。它是必填字段。

* *数据文档*:指定需要与模板合并的数据xml的位置。

#### 输出文档{#output-documents-2}

* *输出文档*: — 指定生成的PDF表单的名称。

#### 其他参数{#additional-parameters}

* *内容根*:指定存储在输入XDP模板中使用的片段或图像的存储库中文件夹的路径。
* *提交Url*:为生成的PDF表单指定默认的提交URL。
* *区域设置*:指定生成的PDF表单的默认区域设置。
* *Acrobat版本*:为生成的PDF表单指定目标Acrobat版本。
* *加标签的PDF*:指定是否使生成的PDF可访问。
* *XCI文档*:指定XCI文件的路径。

## 输出 {#output}

生成非交互式PDF工作流是`generatePDFOutput`输出服务API的包装器。 它用于从XDP模板和数据xml生成非交互式PDF文档。

### 生成非交互式PDF输出工作流   {#generate-non-interactive-pdf-output-workflow-nbsp}

1. 将“生成非交互式PDF输出”工作流拖动到Sidekick中的“Forms Workflow”选项卡下。
1. 双击添加的工作流步骤以编辑组件。
1. 在“编辑组件”对话框中，配置输入文档、输出文档和其他参数，然后单击&#x200B;**[!UICONTROL 确定]**。

#### 输入文档{#input-documents-3}

* *模板文件*:指定XDP模板的位置。它是必填字段。

* *数据文档*:指定需要与模板合并的数据xml的位置。

#### 输出文档{#output-document}

*输出文档*:指定生成的PDF表单的名称。

#### 其他参数{#additional-parameters-1}

* *内容根*:指定存储在输入XDP模板中使用的片段或图像的存储库中文件夹的路径。
* *区域设置*:指定生成的PDF表单的默认区域设置。
* *Acrobat版本*:为生成的PDF表单指定目标Acrobat版本。
* 线性化PDF:指定是否优化生成的PDF以用于Web查看。
* *加标签的PDF*:指定是否使生成的PDF可访问。
* *XCI文档*:指定XCI文件的路径。
