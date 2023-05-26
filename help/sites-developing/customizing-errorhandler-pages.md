---
title: 自定义错误处理程序显示的页面
seo-title: Customizing Pages shown by the Error Handler
description: AEM附带了用于处理HTTP错误的标准错误处理程序
seo-description: AEM comes with a standard error handler for handling HTTP errors
uuid: aaf940fd-e428-4c7c-af7f-88b1d02c17c6
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 63c94c82-ed96-4d10-b645-227fa3c09f4b
exl-id: d6745baa-44da-45dd-b5d5-a9b218e7e8cf
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '518'
ht-degree: 2%

---

# 自定义错误处理程序显示的页面{#customizing-pages-shown-by-the-error-handler}

AEM附带了用于处理HTTP错误的标准错误处理程序；例如，通过显示：

![chlimage_1-67](assets/chlimage_1-67a.png)

系统提供的脚本存在(在 `/libs/sling/servlet/errorhandler`)以响应错误代码，默认情况下，标准CQ实例中提供了以下内容：

* 403.jsp
* 404.jsp

>[!NOTE]
>
>AEM基于Apache Sling，因此请参见 [https://sling.apache.org/site/errorhandling.html](https://sling.apache.org/site/errorhandling.html) 以了解有关Sling错误处理的详细信息。

>[!NOTE]
>
>在创作实例上， [CQ WCM调试过滤器](/help/sites-deploying/osgi-configuration-settings.md) 默认情况下处于启用状态。 这始终导致响应代码200。 默认错误处理程序通过向响应写入完整栈栈跟踪进行响应。
>
>在发布实例上，CQ WCM调试过滤器为 *始终* 已禁用（即使配置为已启用）。

## 如何自定义错误处理程序显示的页面 {#how-to-customize-pages-shown-by-the-error-handler}

您可以开发自己的脚本，以自定义遇到错误时错误处理程序显示的页面。 您的自定义页面将创建于 `/apps` 和覆盖默认页面（位于页面下方） `/libs`)。

>[!NOTE]
>
>参见 [使用叠加](/help/sites-developing/overlays.md) 了解更多详细信息。

1. 在存储库中，复制默认脚本：

   * 从 `/libs/sling/servlet/errorhandler/`
   * 到 `/apps/sling/servlet/errorhandler/`

   由于目标路径在默认情况下不存在，因此，在首次执行此操作时，您将需要创建该路径。

1. 导航到 `/apps/sling/servlet/errorhandler`。在此，您可以：

   * 编辑相应的现有脚本以提供所需的信息。
   * 为所需代码创建和编辑新脚本。

1. 保存更改并进行测试。

>[!CAUTION]
>
>404.jsp和403.jsp处理程序经过专门设计，以满足CQ5身份验证的要求；特别是允许在这些错误发生时进行系统登录。
>
>因此，应谨慎地更换这两个处理程序。

### 自定义对HTTP 500错误的响应 {#customizing-the-response-to-http-errors}

HTTP 500错误是由服务器端异常引起的。

* **[500内部服务器错误](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html)**
服务器遇到意外情况，无法完成请求。

当请求处理导致异常时，Apache Sling框架(AEM构建于之上)：

* 记录异常
* 返回：

   * HTTP响应代码500
   * 异常栈栈跟踪

   在响应正文中。

按 [自定义错误处理程序显示的页面](#how-to-customize-pages-shown-by-the-error-handler) a `500.jsp` 可创建脚本。 但是，它仅在以下情况下使用 `HttpServletResponse.sendError(500)` 显式执行；即从异常捕获器中执行。

否则，响应代码将设置为500，但 `500.jsp` 脚本未执行。

要处理500个错误，错误处理程序脚本的文件名必须与exception类（或超类）相同。 要处理所有此类例外，您可以创建一个脚本 `/apps/sling/servlet/errorhandler/Throwable.js`p或 `/apps/sling/servlet/errorhandler/Exception.jsp`.

>[!CAUTION]
>
>在创作实例上， [CQ WCM调试过滤器](/help/sites-deploying/osgi-configuration-settings.md) 默认情况下处于启用状态。 这始终导致响应代码200。 默认错误处理程序通过向响应写入完整栈栈跟踪进行响应。
>
>对于自定义错误处理程序，需要代码为500的响应，因此 [需要禁用CQ WCM调试过滤器](/help/sites-deploying/osgi-configuration-settings.md). 这样可确保返回响应代码500，这反过来会触发正确的Sling错误处理程序。
>
>在发布实例上，CQ WCM调试过滤器为 *始终* 已禁用（即使配置为已启用）。
