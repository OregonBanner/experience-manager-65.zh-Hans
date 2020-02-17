---
title: 登录AEM Forms工作流
seo-title: 登录AEM Forms工作流
description: 使用日志调试AEM Forms工作流程问题。
seo-description: 使用日志调试AEM Forms工作流程问题。
uuid: 869d0271-c7e3-4b6d-8e63-893dc6af8b8a
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 14bb521a-42ea-4fe2-90fb-202e7ddf917a
docset: aem65
translation-type: tm+mt
source-git-commit: 8e724af4d69cb859537dd088119aaca652ea3931

---


# 登录AEM Forms工作流{#logging-in-aem-forms-workflows}

表单工作流程步骤提供了详细的日志，可方便地调试与工作流程相关的问题。 为AEM Forms工作流启用调试日志记录以查看日志。

默认情况下， **error.log文件中的** /crx-repository/logs/directory中提供所有日志信息 ** 。

表单工作流的调试日志包括：

* 输入每个工作流步骤。 例如：\
   `[DEBUG] "Executing Invoke DDX Process step"`

* 退出每个工作流步骤。 例如：\
   `[DEBUG] "Successfully finished Invoke DDX Process step"`

* 服务调用消息。 例如：\
   `[DEBUG] Invoking Adobe Sign Service for creating agreement`

* 服务退出消息。 例如：\
   `[DEBUG] Agreement created successfully with agreement id <agreement id>`

* 从元数据映射读取的变量。 例如：\
   `[DEBUG] Successfully retrieved variable <variable name> from workflow meta data map`

* 写入JCR存储库的变量。 例如：

   ```
      [DEBUG] Successfully written variable <variable name> into meta data node at <JCR path where meta data is being written>
   ```

* 具有完整堆栈跟踪的异常消息。 例如：\
   `[DEBUG] Exception in Adobe Sign Service <complete stack trace>`

* 动态步骤元数据参数。 例如：

   ```
   [DEBUG] Document of Record to be generated for adaptive form <path of adaptive form>
    [DEBUG] Locale to be used for Document of Record is <locale>
   ```

以下示例说明了“签名文档”步骤的日志：

```xml
[DEBUG] Executing sign document step.
[DEBUG] Using adobe sign configuration: <path of adobe sign configuration>
[DEBUG] Invoking Adobe Sign Service for creating agreement
[DEBUG] Agreement created successfully with agreement id <agreement id>
[DEBUG] Exception in Adobe Sign Service <complete stack trace>
[ERROR] Exception in Adobe Sign Service
[DEBUG] Successfully finished sign document step
```

使用日志评估：

* 您使用的是正确的Adobe Sign配置。
* Adobe sign服务在成功创建协议后退出。
* “签名文档”步骤将退出并显示成功消息。

如果有异常，您可以查看完整的堆栈跟踪以评估错误的原因。

## 为AEM Forms工作流启用调试日志记录 {#enable-debug-logging-for-aem-forms-workflows}

执行以下步骤以启用AEM Forms工作流的调试日志记录：

1. 转至AEM web控制台配置管理器：

   https://[服务器]:[port]/system/console/configMgr

1. 选择“ **[!UICONTROL Sling]** ”>“ **[!UICONTROL 日志支持”]**。
1. 点按 **[!UICONTROL 添加新记录器。]**
1. 选择 **[!UICONTROL 调试]** ，作为日 **[!UICONTROL 志级别]**。
1. 指定日志文件的位置。 日志文件的默认位置为： *logs\error.log*
1. 在“记录器”列中 **将包的名称指定为com.adobe.granite.workflow** . **[!UICONTROL core]** 。

   执行这些步骤可存储 **com.adobe.granite.workflow.core包的调试日志** 。 点 **[!UICONTROL 按+]** ，并将以下包名称添加到列表中：

   * com.adobe.fd.workflow
   * com.adobe.fd.workspace

