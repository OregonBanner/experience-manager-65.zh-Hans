---
title: 从AEM Workflow启动Document Services API
seo-title: Initiate Document Services APIs from AEM Workflow
description: 了解如何在DDX或提供的输入上调用AEM文档服务。 另请参阅如何将PDF转换为PDF/A
seo-description: Learn how to invoke AEM Document services on DDX or supplied inputs. Also see hwo to convert PDF to PDF/A
uuid: aacec2df-1ad6-4ff2-a99d-ef206efcdc09
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: 8b85bdc7-3864-49c9-81b0-cf15b8e986d9
exl-id: 123087a2-9d09-4579-9185-2ccd7d25bf8d
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '1167'
ht-degree: 0%

---

# 从AEM Workflow启动Document Services API  {#initiate-document-services-apis-from-aem-workflow}

## 汇编程序 {#assembler}

AEM Forms提供自定义工作流以调用以下Assembler服务API：

* **调用**：对提供的输入调用输入DDX中指定的操作。
* **toPDFA**：将输入PDF文档转换为PDF/A文档。

### 调用DDX工作流 {#invoke-ddx-workflow}

此 **调用DDX** 工作流会调用 `Invoke` Assembler服务API，可用于组装或分解文档、向PDF添加水印等。

1. 拖动 **[!UICONTROL 调用DDX]** “工作流”步骤中的“Forms Workflow”选项卡下Sidekick。
1. 双击添加的工作流步骤以编辑组件。
1. 在“编辑组件”对话框中，配置输入文档、环境选项和输出文档，然后单击 **[!UICONTROL 确定]**.

#### 输入文档 {#input-documents}

调用DDX工作流需要以下输入文档：

* **DDX**：它是调用DDX工作流步骤的必需输入，可通过从DDX输入下拉列表中选择以下选项之一来指定。

   * *相对于有效负荷*： DDX输入文件相对于工作流项的有效负荷文件夹。
   * *使用有效负荷*：工作流项的有效负载用作输入DDX文档。
   * *绝对路径*：CRX存储库中DDX文档的绝对路径。

* **从付费加载创建映射**：在选中时，有效负荷文件夹下的所有文档都将添加到输入文档的映射中 `invoke` Assembler中的API。 每个文档的节点名称在映射中用作键。

* **输入文档的映射**：指定输入文档的映射。 您可以添加任意数量的条目，其中每个条目在映射中指定文档的键和文档的源。

#### 环境选项 {#environment-options}

环境选项选项卡允许您为调用API设置各种处理选项。

* *作业日志级别*：指定处理日志的日志级别。
* *仅验证*：检查输入DDX的有效性。

* *出错时失败*：指定在发生错误时，对Assembler服务的调用是否应失败。 默认值为False。

#### 输出文档 {#output-documents}

根据输入DDX，调用API可以生成多个输出文档。 “输出文档”选项卡允许您选择保存输出文档的位置。

1. *将输出保存在有效负荷中*：将输出文档保存在有效负荷文件夹中，如果有效负荷是文件则覆盖有效负荷。
1. *输出文档的映射*：允许通过为每个输出文档添加一个条目来明确指定保存每个输出文档的位置。 每个条目都指定文档及其保存位置。 输出文档可能会覆盖有效负载或保存在有效负载文件夹下。 当有多个输出文档时，此插件非常有用。

1. *作业日志*：指定保存作业日志文档的位置，这有助于排除故障。

### 转换为PDF/A工作流 {#convert-to-pdf-a-workflow}

转化为PDF/工作流步骤会调用 `toPDFA` 汇编程序服务API。 它用于将PDF文档转换为PDF/A兼容文档。

1. 拖动 **[!UICONTROL ConvertToPDFA]** “工作流”步骤中的“Forms Workflow”选项卡下Sidekick。

1. 双击添加的工作流步骤以编辑组件。
1. 在“编辑组件”对话框中，配置输入文档、转换选项和输出文档，然后单击 **[!UICONTROL 确定]**.

#### 输入文档 {#input-documents-1}

通过下列方式之一指定要转换为PDF/A兼容文档的文档源。

* *相对于有效负荷*：输入文档相对于工作流项目的有效负荷文件夹。
* *使用有效负荷*：工作流项的有效负荷用作输入文档。
* *绝对路径*：CRX存储库中输入文档的绝对路径。

#### 转换选项 {#conversion-options}

“转换选项”允许您指定更改PDF/A转换过程的选项。

* *合规性* ：指定输出PDF/A必须符合的PDF/A标准。
* *结果级别* ：指定用于PDF/A转换日志的日志级别。
* *签名* ：指定在转换期间必须如何处理输入文档中的签名。
* *色彩空间* ：指定用于输出PDF/A文档的预定义颜色空间。
* *验证* 转换：指定转换后的PDF/A文档在转换后是否应验证PDF/A符合性。
* *作业日志级别* ：指定用于处理日志的日志级别。

* *元数据扩展架构* ：指定用于PDF文档元数据中XMP属性的元数据扩展架构的路径。

#### 输出文档 {#output-documents-1}

“输出文档”选项卡允许您指定输出文档的目标

* *PDFA文档*：指定保存转换后的PDF/文档的位置。 它可以覆盖有效负载文档或保存在有效负载文件夹下。
* *转换日志*：指定保存转化日志的位置。 它可以覆盖有效负荷文档，也可以保存在有效负荷文件夹下。

## Forms {#forms}

渲染PDF表单工作流是周围的包装器 `renderPDFForm` Forms服务API可使用XDPPDF和数据xml创建模板表单。

### 呈现PDF表单工作流 {#render-pdf-form-workflow}

1. 在Sidekick中，将渲染PDF表单工作流步骤拖动到“Forms Workflow”选项卡下。
1. 双击添加的工作流步骤以编辑组件。
1. 在“编辑组件”对话框中，配置输入文档、输出文档和其他参数，然后单击 **[!UICONTROL 确定]**.

#### 输入文档 {#input-documents-2}

* *模板文件*：指定XDP模板的位置。 它是必填字段。

* *数据文档*：指定需要与模板合并的数据xml的位置。

#### 输出文档 {#output-documents-2}

* *输出文档*： — 指定生成的PDF表单的名称。

#### 其他参数 {#additional-parameters}

* *内容根*：指定存储库中用于存储输入XDP模板中使用的片段或图像的文件夹的路径。
* *提交Url*：指定所生成PDF表单的默认提交URL。
* *区域设置*：指定生成的PDF表单的默认区域设置。
* *Acrobat版本*：为生成的PDF表单指定目标Acrobat版本。
* *已标记PDF*：指定是否使生成的PDF可访问。
* *XCI文档*：指定XCI文件的路径。

## 输出 {#output}

生成非交互式PDF工作流是周围的包装器 `generatePDFOutput` 输出服务API。 用于从XDP模板和数据xml生成非交互式PDF文档。

### 生成非交互式PDF输出工作流   {#generate-non-interactive-pdf-output-workflow-nbsp}

1. 在“Sidekick”中，将“生成非交互式PDF输出”Forms Workflow拖动到“工作流”选项卡下。
1. 双击添加的工作流步骤以编辑组件。
1. 在“编辑组件”对话框中，配置输入文档、输出文档和其他参数，然后单击 **[!UICONTROL 确定]**.

#### 输入文档 {#input-documents-3}

* *模板文件*：指定XDP模板的位置。 它是必填字段。

* *数据文档*：指定需要与模板合并的数据xml的位置。

#### 输出文档 {#output-document}

*输出文档*：指定生成的PDF表单的名称。

#### 其他参数 {#additional-parameters-1}

* *内容根*：指定存储库中用于存储输入XDP模板中使用的片段或图像的文件夹的路径。
* *区域设置*：指定生成的PDF表单的默认区域设置。
* *Acrobat版本*：为生成的PDF表单指定目标Acrobat版本。
* 线性PDF：指定是否优化生成的PDF以进行Web查看。
* *已标记PDF*：指定是否使生成的PDF可访问。
* *XCI文档*：指定XCI文件的路径。
