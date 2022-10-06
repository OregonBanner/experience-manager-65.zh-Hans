---
title: 在AEM Forms工作流中记录
seo-title: Logging in AEM Forms workflows
description: 使用日志调试AEM Forms工作流问题。
seo-description: Use logs to debug AEM Forms workflow issues.
uuid: 869d0271-c7e3-4b6d-8e63-893dc6af8b8a
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 14bb521a-42ea-4fe2-90fb-202e7ddf917a
docset: aem65
exl-id: 601c8d95-0d1a-4945-a522-e85d3e9fc4ae
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 5%

---

# 在AEM Forms工作流中记录{#logging-in-aem-forms-workflows}

Forms工作流步骤可方便地提供详细日志，以调试与工作流相关的问题。 为AEM Forms工作流启用调试日志记录以查看日志。

默认情况下， **error.log** 文件 */crx-repository-logs/* 目录访问Advertising Cloud的帮助。

表单工作流的调试日志包括：

* 每个工作流步骤的条目。 例如：\
   `[DEBUG] "Executing Invoke DDX Process step"`

* 退出每个工作流步骤。 例如：\
   `[DEBUG] "Successfully finished Invoke DDX Process step"`

* 服务调用消息。 例如：\
   `[DEBUG] Invoking Adobe Sign Service for creating agreement`

* 服务退出消息。 例如：\
   `[DEBUG] Agreement created successfully with agreement id <agreement id>`

* 从元数据映射中读取的变量。 例如：\
   `[DEBUG] Successfully retrieved variable <variable name> from workflow meta data map`

* 在JCR存储库中写入的变量。 例如：

   ```verilog
      [DEBUG] Successfully written variable <variable name> into meta data node at <JCR path where meta data is being written>
   ```

* 具有完整堆栈跟踪的异常消息。 例如：\
   `[DEBUG] Exception in Adobe Sign Service <complete stack trace>`

* 动态步骤元数据参数。 例如：

   ```verilog
   [DEBUG] Document of Record to be generated for adaptive form <path of adaptive form>
    [DEBUG] Locale to be used for Document of Record is <locale>
   ```

以下示例说明了“签名文档”步骤的日志：

```verilog
[DEBUG] Executing sign document step.
[DEBUG] Using adobe sign configuration: <path of adobe sign configuration>
[DEBUG] Invoking Adobe Sign Service for creating agreement
[DEBUG] Agreement created successfully with agreement id <agreement id>
[DEBUG] Exception in Adobe Sign Service <complete stack trace>
[ERROR] Exception in Adobe Sign Service
[DEBUG] Successfully finished sign document step
```

使用日志可评估以下情况：

* 您使用的是正确的adobe sign配置。
* 成功创建协议后，Adobe Sign服务将退出。
* “签名文档”步骤将退出，并显示一则成功消息。

如果出现异常，则可以查看完整的堆栈跟踪以评估错误的原因。

## 为AEM Forms工作流启用调试日志记录 {#enable-debug-logging-for-aem-forms-workflows}

执行以下步骤以为AEM Forms工作流启用调试日志记录：

1. 转到AEM Web控制台配置管理器：

   https://&#39;[服务器]:[端口]“/system/console/configMgr

1. 选择 **[!UICONTROL Sling]** > **[!UICONTROL 日志支持]**.
1. 点按 **[!UICONTROL 添加新的日志记录器。]**
1. 选择 **[!UICONTROL 调试]** 作为 **[!UICONTROL 日志级别]**.
1. 指定日志文件的位置。 日志文件的默认位置为： *logs\error.log*
1. 将包的名称指定为 **com.adobe.granite.workflow.core** 在 **[!UICONTROL 记录器]** 列。

   执行这些步骤后，可以存储 **com.adobe.granite.workflow.core** 包。 点按 **[!UICONTROL +]** 并将以下包名称添加到列表中：

   * com.adobe.fd.workflow
   * com.adobe.fd.workspace
