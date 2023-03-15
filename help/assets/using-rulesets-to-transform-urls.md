---
title: 使用规则集转换 URL
description: 您可以在Dynamic Media中部署规则集以转换URL。 规则集是以脚本语言（如JavaScript）编写的指令集，用于评估XML数据并在该数据满足特定条件时执行特定操作。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
role: User, Admin,Developer
exl-id: b0ac587b-8592-4d37-9ce0-98a0859c367f
feature: Configuration,Rulesets
source-git-commit: 65af6e33ae3897519491952f4d3a6832700f77b2
workflow-type: tm+mt
source-wordcount: '760'
ht-degree: 0%

---

# 使用规则集转换URL {#using-rulesets-to-transform-urls}

您可以在Dynamic Media中部署规则集以转换URL。 规则集是以脚本语言（如JavaScript）编写的指令集，用于评估XML数据并在该数据满足特定条件时执行特定操作。 每个规则包括至少一个条件和至少一个操作。 规则根据条件评估XML数据，如果满足条件，则执行相应的操作。 规则集的示例包括：

* 添加MIME类型后缀。 许多服务和网站都需要图像后缀，例如，添加 `.jpg` 到URL。
* 创建指向URL的文件夹路径以用于SEO（搜索引擎优化）。

   参见 [Adobe Dynamic Media Classic如何支持SEO](/help/assets/assets/s7_seo.pdf).

* 向URL添加元数据以用于SEO（搜索引擎优化）。

   参见 [Adobe Dynamic Media Classic如何支持SEO](/help/assets/assets/s7_seo.pdf).

* 设置内容处置以触发下载。
* 简化用于个性化的图像服务模板URL。 例如，翻转 `rgb{XX,YY,ZZ}` 进入RTF-ready `\redXX\greenYY\blueZZ`

* 请求对某些字符进行编码，例如 `$`， `{`、和 `}`和某些要解码为ImageServer的字符。 例如，Facebook不能很好地处理包含特殊字符的URL。

   参见 [从URL中删除特殊字符](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/remove-special-characters-urls.html).

在Dynamic Media的上下文中，使用基于XML的系统管理资产信息的网站可以将XML文件上传到Dynamic Media。 您可以将其中一个文件指定为用于提供Dynamic Media资源的预处理规则集文件。 此文件将重新构建标准URL协议格式，以满足与Dynamic Media集成系统的业务逻辑。 指定一个XML文件作为规则集定义文件路径。

>[!CAUTION]
>
>使用规则集时请务必小心；规则集可能会阻止在您的网站上显示Dynamic Media内容。

提供了一些示例规则集，可帮助您创建自己的规则集。
参见 [规则集引用](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/rule-set-reference/c-rule-set-reference.html).

与创建所有规则集时一样，在使用xmlvalid等XML验证器程序上传XML文件之前，请确保该文件有效。
另请参阅 [规则集疑难解答](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/scene7-ruleset-troubleshooting.html).

此外，请确保首先在不影响实时生产环境的暂存环境中测试规则集。
生产环境和暂存环境通常需要不同的登录。

请参阅 [用于登录信息的Adobe Dynamic Media Classic桌面应用程序](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#sign-in-dmc-app).

<!-- OBSOLETE INFORMATION * **NA staging environment** login page: [https://s7sps1-staging.scene7.com/IpsWeb/](https://s7sps1-staging.scene7.com/IpsWeb/)
* **EMEA staging environment** login page: [https://s7sps3-staging.scene7.com/IpsWeb/](https://s7sps3-staging.scene7.com/IpsWeb/)
* **JAPAC staging environment** login page: [https://s7sps5-staging.scene7.com/IpsWeb/](https://s7sps5-staging.scene7.com/IpsWeb/) -->

另请参阅 [在规则集中使用“asset”而不是“is”图像](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/ruleset-asset-instead-image.html).

**要部署XML规则集，请执行以下操作：**

1. 登录到您的 [Dynamic Media Classic桌面应用程序](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#sign-in-dmc-app).

   Adobe在配置时提供了您的凭据和登录详细信息。 如果您没有此信息，请联系Adobe客户支持。

1. 通过执行以下操作上载规则集文件：

   * 在全局导航栏上，选择 **[!UICONTROL 上传]**.
   * 在 **[!UICONTROL 上传]** 页面，左上角附近，选择 **[!UICONTROL 浏览]**.
   * 在 **[!UICONTROL 打开]** 对话框，浏览到规则集文件(XML)。
   * 选择文件，然后选择 **[!UICONTROL 打开]**.
   * 在右侧 **[!UICONTROL 上传]** 页面，为规则集文件选择目标文件夹。
   * 在页面底部附近，确保 **[!UICONTROL 上传后发布]** 已选中。
   * 在页面的右下角，选择 **[!UICONTROL 提交上传]**.
   * 在全局导航栏上，选择 **[!UICONTROL 作业]** 以检查上载作业的状态。 当 **[!UICONTROL 状态]** 上的列 **[!UICONTROL 作业]** 页面显示上传完成，请继续后续步骤。

1. 在靠近页面顶部的导航栏上，选择 **[!UICONTROL 设置]** > **[!UICONTROL 应用程序设置]** > **[!UICONTROL 发布设置]** > **[!UICONTROL 图像服务器]**.
1. 在 **[!UICONTROL 图像服务器发布]** 页面，在 **[!UICONTROL 目录管理]** 组，查找 **[!UICONTROL 规则集定义文件路径]**，然后选择 **[!UICONTROL 选择]**.
1. 在 **[!UICONTROL 选择规则集定义文件(XML)]** 页面上，浏览到规则集文件，然后在页面的右下角选择 **[!UICONTROL 选择]**.
1. 在“设置”页面的右下角，选择 **[!UICONTROL 关闭]**.
1. 运行图像服务器发布作业。

   规则集条件将应用于对实时Dynamic Media图像服务器的请求。

   如果更改规则集文件，则在重新上传并重新发布更新的规则集文件时，将立即应用更改。
