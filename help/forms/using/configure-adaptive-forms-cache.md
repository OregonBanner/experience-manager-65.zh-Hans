---
title: 配置自适应表单缓存
seo-title: 配置自适应表单缓存
description: '自适应表单缓存专门设计用于自适应表单和文档。 它缓存自适应表单和自适应文档，以减少在客户端上呈现自适应表单或文档所需的时间。 '
seo-description: '自适应表单缓存专门设计用于自适应表单和文档。 它缓存自适应表单和自适应文档，以减少在客户端上呈现自适应表单或文档所需的时间。 '
uuid: ba8f79fd-d8dc-4863-bc0d-7c642c45505c
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 9fa6f761-58ca-4cd0-8992-b9337dc1a279
docset: aem65
translation-type: tm+mt
source-git-commit: 2d54d115529126162c92e9943a188d05159535f9
workflow-type: tm+mt
source-wordcount: '934'
ht-degree: 0%

---


# 配置自适应表单缓存{#configure-adaptive-forms-cache}

缓存是一种缩短数据访问时间、减少延迟和提高输入／输出(I/O)速度的机制。 自适应表单缓存仅存储自适应表单的HTML内容和JSON结构，而不保存任何预填数据。 它有助于缩短在客户端上渲染自适应表单所需的时间。 它专门为自适应表单设计。

## 在作者和发布实例中配置自适应表单缓存{#configure-adaptive-forms-caching-at-author-and-publish-instances}

1. 转到位于`https://[server]:[port]/system/console/configMgr`的AEM Web控制台配置管理器。
1. 单击&#x200B;**[!UICONTROL 自适应表单和交互式通信Web渠道配置]**&#x200B;以编辑其配置值。
1. 在[!UICONTROL 编辑配置值]对话框中，在&#x200B;**[!UICONTROL 自适应Forms]**&#x200B;字段中指定AEM [!DNL Forms]服务器实例可缓存的表单或文档的最大数量。 默认值为 100。

   >[!NOTE]
   >
   >要禁用缓存，请将“Number of Adaptive Began”(自适应Forms)字段中的值设置为&#x200B;**0**。 在禁用或更改缓存配置时，将重置缓存并从缓存中删除所有表单和文档。

   ![自适应表单HTML缓存的配置对话框](assets/cache-configuration-edit.png)

1. 单击&#x200B;**[!UICONTROL 保存]**&#x200B;以保存配置。

您的环境配置为使用缓存自适应表单和相关资产。


## （可选）在调度程序{#configure-the-cache}处配置自适应表单缓存

您还可以在调度程序上配置自适应表单缓存以提高性能。

### 先决条件{#pre-requisites}

* 启用[在客户端](prepopulate-adaptive-form-fields.md#prefill-at-client)合并或预填数据选项。 它有助于合并预填表单的每个实例的唯一数据。

### 在调度程序{#considerations}上缓存自适应表单的注意事项

* 使用自适应表单缓存时，请使用AEM [!DNL Dispatcher]缓存自适应表单的客户端库（CSS和JavaScript）。
* 在开发自定义组件时，在用于开发的服务器上保持禁用自适应表单缓存。
* 未缓存扩展名的URL。 例如，对模式为`/content/forms/[folder-structure]/[form-name].html`的URL进行缓存，缓存会忽略模式为`/content/dam/formsanddocument/[folder-name]/<form-name>/jcr:content`的URL。 因此，将URL与扩展一起使用可以从缓存中受益。
* 本地化自适应表单的注意事项：
   * 使用URL格式`http://host:port/content/forms/af/<afName>.<locale>.html`请求自适应表单的本地化版本，而不是`http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`
   * [禁用对格](supporting-new-language-localization.md#how-localization-of-adaptive-form-works) 式URL使用浏览器 `http://host:port/content/forms/af/<adaptivefName>.html`锁定。
   * 当您使用URL格式`http://host:port/content/forms/af/<adaptivefName>.html`，并且禁用配置管理器中的&#x200B;**[!UICONTROL 使用浏览器区域设置]**&#x200B;时，将提供自适应表单的非本地化版本。 非本地化语言是开发自适应表单时使用的语言。 未考虑为浏览器配置的区域设置（浏览器区域设置），并提供自适应表单的非本地化版本。
   * 当您使用URL格式`http://host:port/content/forms/af/<adaptivefName>.html`，并在配置管理器中启用&#x200B;**[!UICONTROL 使用浏览器区域设置]**&#x200B;时，将提供自适应表单的本地化版本（如果有）。 本地化的自适应表单的语言基于为浏览器配置的区域设置（浏览器区域设置）。 它可能只导致[缓存自适应表单的第一个实例]。 要防止实例上出现问题，请参阅[疑难解答](#only-first-insatnce-of-adptive-forms-is-cached)。

### 在调度程序上启用缓存

执行以下列出的步骤，在调度程序上启用和配置缓存自适应表单：

1. 为环境的每个发布实例打开以下URL，并[为环境的发布实例启用刷新代理](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/page-invalidate.html#invalidating-dispatcher-cache-from-a-publishing-instance):
   `http://[server]:[port]]/etc/replication/agents.publish/flush.html`

1. [将以下内容添加到调度程序。any文件](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#automatically-invalidating-cached-files):

   ```JSON
      /invalidate
      {
      /0000
      {
      /glob "*"
      /type "deny"
      }
      /0001
      {
      # Consider all HTML files stale after an activation.
      /glob "*.html"
      /type "allow"
      }
      /0002
      {
      # Exclude htmls present in AF directories
      /glob "/content/forms/**/*.html"
      /type "deny"
      }
   ```

   添加以上内容时：

   * 自适应表单将保留在缓存中，直到未发布表单的更新版本。

   * 当自适应表单中引用的资源的较新版本发布时，受影响的自适应表单会自动失效。 引用资源的自动失效有一些例外。 有关异常的解决方法，请参阅[疑难解答](#troubleshooting)部分。
1. [添加以下规则dispatcher.any或自定义规则文件](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#specifying-the-documents-to-cache)。它不包括不支持缓存的URL。 例如，交互通信。

   ```JSON
      /0000 {
            /glob "*"
            /type "allow"
      }
      ## Don't cache csrf login tokens
      /0001 {
            /glob "/libs/granite/csrf/token.json"
            /type "deny"
      }
      ## Don't cache IC - print channel
      /0002 {
            /glob "/content/forms/**/channels/print.html"
            /type "deny"
      }
      ## Don't cache IC - web channel
      /0003 {
            /glob "/content/forms/**/channels/web.html"
            /type "deny"
      }
   ```

1. [将以下参数添加到忽略URL参数列表](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#ignoring-url-parameters):

   ```JSON
      /ignoreUrlParams {
      /0001 { /glob "*" /type "deny" }
      # added for AEM forms specific use cases.
      /0003 { /glob "dataRef" /type "allow" }
      }
   ```

您的AEM环境配置为缓存自适应表单。 它缓存所有类型的自适应表单。 如果在传送缓存的页面之前需要检查页面的用户访问权限，请参阅[缓存安全内容](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/permissions-cache.html)。

## 疑难解答 {#troubleshooting}

### 某些包含图像或视频的自适应表单不会从调度程序缓存{#videos-or-images-not-auto-invalidated}自动失效

#### 带有 OS 剪贴板 {#issue1}

当您通过资产浏览器选择图像或视频并将它们添加到自适应表单，并且这些图像和视频在资产编辑器中进行编辑时，包含这些图像的自适应表单不会自动从调度程序缓存中失效。

#### 解决方案{#Solution1}

发布图像和视频后，显式取消发布和发布引用这些资产的自适应表单。

### 只缓存自适应表单的第一个实例{#only-first-instance-of-adaptive-forms-is-cached}

#### 带有 OS 剪贴板 {#issue3}

当自适应表单URL没有任何本地化信息，并且启用配置管理器中的&#x200B;**[!UICONTROL 使用浏览器区域设置]**&#x200B;时，将提供自适应表单的本地化版本，并且只缓存自适应表单的第一实例并将其发送给每个后续用户。

#### 解决方案{#Solution3}

请执行以下步骤以解决问题：

1. 打开conf.d/httpd-dispatcher.conf或配置为在运行时加载的任何其他配置文件。

1. 将以下代码添加到文件并保存它。 它是修改它以适合您的环境的示例代码。

```XML
   <VirtualHost *:80>
        # Set log level high during development / debugging and then turn it down to whatever is appropriate
    LogLevel rewrite:trace6
        # Start Rewrite Engine
    RewriteEngine On
        # Handle actual URL convention (just pass through)
        RewriteRule "^/content/forms/af/(.*)[.](.*).html$" "/content/forms/af/$1.$2.html" [PT]
 
        # Handle selector based redirection basded on browser language
        # The Rewrite Cond(ition) is looking for the Accept-Lanague header and if found takes the first two character which most likely will be the desired language selector.
        RewriteCond %{HTTP:Accept-Language} ^(..).*$ [NC]
        RewriteRule "^/content/forms/af/(.*).html$" "/content/forms/af/$1.%1.html" [R]
   </VirtualHost>
```
