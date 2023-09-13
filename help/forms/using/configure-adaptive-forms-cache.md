---
title: 配置自适应表单缓存
description: 自适应表单缓存专为自适应表单和文档设计。 它会缓存自适应表单和自适应文档，以减少在客户端渲染自适应表单或文档所需的时间。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
docset: aem65
role: Admin
exl-id: 153986f0-b6ff-4278-8bb6-70c320a4e539
source-git-commit: 5af420c8e95fed88a8516cce27b8bbc7d3974e75
workflow-type: tm+mt
source-wordcount: '889'
ht-degree: 1%

---

# 配置自适应表单缓存 {#configure-adaptive-forms-cache}

高速缓存是一种缩短数据访问时间、减少延迟并提高输入/输出(I/O)速度的机制。 自适应表单缓存仅存储自适应表单的HTML内容和JSON结构，而不保存任何预填数据。 它有助于减少在客户端渲染自适应表单所需的时间。 它专为自适应表单而设计。

## 在创作实例和发布实例中配置自适应表单缓存 {#configure-adaptive-forms-caching-at-author-and-publish-instances}

1. 转到位于的AEM Web控制台配置管理器 `https://[server]:[port]/system/console/configMgr`.
1. 单击 **[!UICONTROL 自适应表单和交互式通信Web渠道配置]** 以编辑其配置值。
1. 在 [!UICONTROL 编辑配置值] 对话框，指定AEM实例的最大表单数或文档数 [!DNL Forms] 服务器可以在以下位置缓存： **[!UICONTROL 自适应Forms的数量]** 字段。 默认值为 100。

   >[!NOTE]
   >
   >要禁用缓存，请将自适应Forms数量字段中的值设置为 **0**. 禁用或更改缓存配置时，将重置缓存并从缓存中删除所有表单和文档。

   ![自适应表单HTML缓存的“配置”对话框](assets/cache-configuration-edit.png)

1. 单击 **[!UICONTROL 保存]** 以保存配置。

您的环境配置为使用缓存自适应表单和相关资源。


## （可选）在Dispatcher上配置自适应表单缓存 {#configure-the-cache}

您还可以在Dispatcher上配置自适应表单缓存，以获得额外的性能提升。

### 先决条件 {#pre-requisites}

* 启用 [在客户端合并或预填充数据](prepopulate-adaptive-form-fields.md#prefill-at-client) 选项。 它有助于合并预填充表单的每个实例的唯一数据。

### 在Dispatcher上缓存自适应表单的注意事项 {#considerations}

* 使用自适应表单缓存时，请使用AEM [!DNL Dispatcher] 缓存自适应表单的客户端库（CSS和JavaScript）。
* 在开发自定义组件时，在用于开发的服务器上，将禁用自适应表单缓存。
* 不缓存不带扩展名的URL。 例如，包含模式的URL `/content/forms/[folder-structure]/[form-name].html` 将被缓存，缓存会忽略具有模式的URL `/content/dam/formsanddocument/[folder-name]/<form-name>/jcr:content`. 因此，请使用带有扩展名的URL来获得缓存的好处。
* 本地化自适应表单的注意事项：
   * 使用URL格式 `http://host:port/content/forms/af/<afName>.<locale>.html` 要请求自适应表单的本地化版本，而不是 `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`
   * [禁用使用浏览器区域设置](supporting-new-language-localization.md#how-localization-of-adaptive-form-works) 格式为 `http://host:port/content/forms/af/<adaptivefName>.html`.
   * 当您使用URL格式时 `http://host:port/content/forms/af/<adaptivefName>.html`、和 **[!UICONTROL 使用浏览器区域设置]** 在configuration manager中处于禁用状态时，将提供自适应表单的非本地化版本。 非本地化语言是开发自适应表单时使用的语言。 不会考虑为您的浏览器配置的区域设置（浏览器区域设置），并且会提供自适应表单的非本地化版本。
   * 当您使用URL格式时 `http://host:port/content/forms/af/<adaptivefName>.html`、和 **[!UICONTROL 使用浏览器区域设置]** 在配置管理器中，会提供自适应表单的本地化版本（如果可用）。 本地化的自适应表单的语言基于为您的浏览器配置的区域设置（浏览器区域设置）。 它可能会导致 [仅缓存自适应表单的第一个实例]. 要防止问题在实例中发生，请参阅 [故障排除](#only-first-insatnce-of-adptive-forms-is-cached).

### 在调度程序上启用缓存

要在Dispatcher上启用和配置缓存自适应表单，请执行以下步骤：

1. 为环境的每个发布实例打开以下URL，并 [为环境的发布实例启用刷新代理](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/page-invalidate.html#invalidating-dispatcher-cache-from-a-publishing-instance)：
   `http://[server]:[port]]/etc/replication/agents.publish/flush.html`

1. [将以下内容添加到您的dispatcher.any文件中](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#automatically-invalidating-cached-files)：

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

   * 自适应表单会保留在缓存中，直到未发布表单的更新版本为止。

   * 发布自适应表单中引用的资源的较新版本时，受影响的自适应表单会自动失效。 引用的资源自动失效有一些例外。 有关例外的解决方法，请参见 [故障排除](#troubleshooting) 部分。
1. [添加以下规则dispatcher.any或自定义规则文件](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#specifying-the-documents-to-cache). 它不包括不支持缓存的URL。 例如，交互式通信。

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

1. [将以下参数添加到忽略URL参数列表](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#ignoring-url-parameters)：

   ```JSON
      /ignoreUrlParams {
      /0001 { /glob "*" /type "deny" }
      # added for AEM forms specific use cases.
      /0003 { /glob "dataRef" /type "allow" }
      }
   ```

您的AEM环境配置为缓存自适应表单。 它会缓存所有类型的自适应表单。 如果在交付缓存的页面之前需要检查页面的用户访问权限，请参阅 [缓存受保护内容](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/permissions-cache.html?lang=zh-Hans).

## 疑难解答 {#troubleshooting}

### 某些包含图像或视频的自适应表单不会从Dispatcher缓存中自动失效 {#videos-or-images-not-auto-invalidated}

#### 问题 {#issue1}

当您通过资产浏览器选择图像或视频并将其添加到自适应表单并在资产编辑器中编辑这些图像或视频时，包含此类图像的自适应表单不会自动从Dispatcher缓存中失效。

#### 解决方案 {#Solution1}

发布图像和视频后，明确取消发布并发布引用这些资产的自适应表单。

### 仅缓存自适应表单的第一个实例 {#only-first-instance-of-adaptive-forms-is-cached}

#### 问题 {#issue3}

当自适应表单URL没有任何本地化信息时，并且 **[!UICONTROL 使用浏览器区域设置]** 在配置管理器中，提供了自适应表单的本地化版本。 仅缓存自适应表单的第一个实例并将其交付给每个后续用户。

#### 解决方案 {#Solution3}

通过执行以下步骤来解决问题：

1. 打开conf.d/httpd-dispatcher.conf或配置为在运行时加载的任何其他配置文件。

1. 将以下代码添加到文件中并进行保存。 它是一个示例代码，可对其进行修改以适合您的环境。

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
