---
title: 自定义错误处理程序显示的页面
seo-title: Customizing Pages shown by the Error Handler
description: AEM附带用于处理HTTP错误的标准错误处理程序
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

AEM附带用于处理HTTP错误的标准错误处理程序；例如，通过显示：

![chlimage_1-67](assets/chlimage_1-67a.png)

系统提供的脚本存在(在 `/libs/sling/servlet/errorhandler`)来响应错误代码，默认情况下，标准CQ实例提供以下内容：

* 403.jsp
* 404.jsp

>[!NOTE]
>
>AEM基于Apache Sling，请参阅 [https://sling.apache.org/site/errorhandling.html](https://sling.apache.org/site/errorhandling.html) 有关Sling错误处理的详细信息。

>[!NOTE]
>
>在创作实例上， [CQ WCM调试过滤器](/help/sites-deploying/osgi-configuration-settings.md) 默认情况下处于启用状态。 这始终会导致响应代码为200。 默认错误处理程序通过将整个堆栈跟踪写入响应进行响应。
>
>在发布实例上，CQ WCM调试过滤器为 *always* 已禁用（即使配置为已启用）。

## 如何自定义错误处理程序显示的页面 {#how-to-customize-pages-shown-by-the-error-handler}

您可以开发自己的脚本，以在遇到错误时自定义错误处理程序显示的页面。 您的自定义页面将在 `/apps` 并覆盖默认页面(位于 `/libs`)。

>[!NOTE]
>
>请参阅 [使用叠加](/help/sites-developing/overlays.md) 以了解更多详细信息。

1. 在存储库中，复制默认脚本：

   * 从 `/libs/sling/servlet/errorhandler/`
   * 到 `/apps/sling/servlet/errorhandler/`

   由于目标路径默认不存在，因此在首次执行此操作时，将需要创建目标路径。

1. 导航到 `/apps/sling/servlet/errorhandler`。在此，您可以：

   * 编辑相应的现有脚本以提供所需的信息。
   * 创建和编辑所需代码的新脚本。

1. 保存更改并测试。

>[!CAUTION]
>
>404.jsp和403.jsp处理程序已专门设计为满足CQ5身份验证的要求；特别是，允许在出现这些错误时进行系统登录。
>
>因此，对这两个处理程序的更换应当非常谨慎。

### 自定义对HTTP 500错误的响应 {#customizing-the-response-to-http-errors}

HTTP 500错误是由服务器端异常导致的。

* **[500内部服务器错误](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html)**
服务器遇到意外情况，导致其无法执行请求。

当请求处理导致异常时，Apache Sling框架(基于AEM构建):

* 记录异常
* 返回：

   * HTTP响应代码500
   * 异常堆栈跟踪

   在响应主体中。

按 [自定义错误处理程序显示的页面](#how-to-customize-pages-shown-by-the-error-handler) a `500.jsp` 脚本。 但是，仅在 `HttpServletResponse.sendError(500)` 显式执行；例如从例外捕手那里。

否则，响应代码将设置为500，但是 `500.jsp` 脚本。

要处理500错误，错误处理程序脚本的文件名必须与异常类（或超类）相同。 要处理所有此类例外，您可以创建脚本 `/apps/sling/servlet/errorhandler/Throwable.js`p或 `/apps/sling/servlet/errorhandler/Exception.jsp`.

>[!CAUTION]
>
>在创作实例上， [CQ WCM调试过滤器](/help/sites-deploying/osgi-configuration-settings.md) 默认情况下处于启用状态。 这始终会导致响应代码为200。 默认错误处理程序通过将整个堆栈跟踪写入响应进行响应。
>
>对于自定义错误处理程序，需要代码为500的响应 — 因此 [需要禁用CQ WCM调试过滤器](/help/sites-deploying/osgi-configuration-settings.md). 这可确保返回响应代码500，这反过来又触发正确的Sling错误处理程序。
>
>在发布实例上，CQ WCM调试过滤器为 *always* 已禁用（即使配置为已启用）。
