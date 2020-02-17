---
title: 自定义错误处理程序显示的页面
seo-title: 自定义错误处理程序显示的页面
description: AEM附带一个用于处理HTTP错误的标准错误处理程序
seo-description: AEM附带一个用于处理HTTP错误的标准错误处理程序
uuid: aaf940fd-e428-4c7c-af7f-88b1d02c17c6
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 63c94c82-ed96-4d10-b645-227fa3c09f4b
translation-type: tm+mt
source-git-commit: c13eabdf4938a47ddf64d55b00f845199591b835

---


# 自定义错误处理程序显示的页面{#customizing-pages-shown-by-the-error-handler}

AEM附带一个用于处理HTTP错误的标准错误处理程序；例如，通过显示：

![chlimage_1-67](assets/chlimage_1-67a.png)

系统提供的脚本存在( `/libs/sling/servlet/errorhandler`在下)以响应错误代码，默认情况下，标准CQ实例提供以下脚本：

* 403.jsp
* 404.jsp

>[!NOTE]
>
>AEM基于Apache Sling，因此请参阅 [https://sling.apache.org/site/errorhandling.html](https://sling.apache.org/site/errorhandling.html) ，了解有关Sling错误处理的详细信息。

>[!NOTE]
>
>在创作实例上， [CQ WCM调试过滤器](/help/sites-deploying/osgi-configuration-settings.md) （默认情况下）处于启用状态。 这始终导致响应代码为200。 默认错误处理程序通过将整个堆栈跟踪写入响应来做出响应。
>
>在发布实例上，CQ WCM调试过滤器始终 *处于禁用状态* （即使配置为已启用）。

## 如何自定义错误处理程序显示的页面 {#how-to-customize-pages-shown-by-the-error-handler}

您可以开发自己的脚本以自定义遇到错误时由错误处理程序显示的页面。 您的自定义页面将创建在 `/apps` 下面，并覆盖默认页面(在下面 `/libs`)。

>[!NOTE]
>
>有关更 [多详细信息](/help/sites-developing/overlays.md) ，请参阅使用叠加。

1. 在存储库中，复制默认脚本：

   * 起始日期: `/libs/sling/servlet/errorhandler/`
   * 到 `/apps/sling/servlet/errorhandler/`
   由于目标路径默认不存在，因此您首次执行此操作时需要创建它。

1. 导航至 `/apps/sling/servlet/errorhandler`. 您可以在此处：

   * 编辑相应的现有脚本以提供所需的信息。
   * 创建和编辑所需代码的新脚本。

1. 保存更改并测试。

>[!CAUTION]
>
>404.jsp和403.jsp处理函数专门设计用于满足CQ5身份验证要求；特别是，在出现这些错误时允许系统登录。
>
>因此，更换这两个操纵者应当非常谨慎。

### 自定义对HTTP 500错误的响应 {#customizing-the-response-to-http-errors}

HTTP 500错误是由服务器端异常引起的。

* **[500内部服务器错](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html)**误服务器遇到意外情况，导致其无法完成请求。

当请求处理导致异常时，Apache Sling框架（AEM构建于上）:

* 记录异常
* 返回：

   * HTTP响应代码500
   * 异常堆栈跟踪
   在响应体中。

通过 [自定义错误处理程序显示的页面](#how-to-customize-pages-shown-by-the-error-handler) ，可 `500.jsp` 以创建脚本。 但是，只有在明确执行 `HttpServletResponse.sendError(500)` 时才使用；例如从例外捕手那里。

否则，响应代码设置为500，但不 `500.jsp` 执行脚本。

要处理500个错误，错误处理程序脚本的文件名必须与异常类（或超类）相同。 要处理所有此类例外，可创建脚 `/apps/sling/servlet/errorhandler/Throwable.js`本p或 `/apps/sling/servlet/errorhandler/Exception.jsp`。

>[!CAUTION]
>
>在创作实例上， [CQ WCM调试过滤器](/help/sites-deploying/osgi-configuration-settings.md) （默认情况下）处于启用状态。 这始终导致响应代码为200。 默认错误处理程序通过将整个堆栈跟踪写入响应来做出响应。
>
>对于自定义错误处理程序，需要代码为500的响应——因此需要禁用 [CQ WCM调试过滤器](/help/sites-deploying/osgi-configuration-settings.md)。 这确保返回响应代码500，这反过来又触发正确的Sling错误处理程序。
>
>在发布实例上，CQ WCM调试过滤器始终 *处于禁用状态* （即使配置为已启用）。

