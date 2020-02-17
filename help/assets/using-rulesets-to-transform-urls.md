---
title: 使用规则集转换URL
description: 您可以在Dynamic media中部署规则集以转换URL。 规则集是用脚本语言（如JavaScript）编写的指令集，这些指令可评估XML数据并在数据满足某些条件时采取某些操作。
uuid: 9fed0c83-67b7-4483-a9b4-322e6a483449
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: abcff903-204b-4ab6-87d8-6f0ce63d7b41
translation-type: tm+mt
source-git-commit: 0595d89409e0ca21f771be5c55c3ec9548a8449f

---


# 使用规则集转换URL {#using-rulesets-to-transform-urls}

您可以在Dynamic media中部署规则集以转换URL。 规则集是用脚本语言（如JavaScript）编写的指令集，这些指令可评估XML数据并在数据满足某些条件时采取某些操作。 每个规则包括至少一个条件和至少一个操作。 规则根据条件评估XML数据，如果满足条件，则执行相应的操作。 规则集的示例包括：

* 添加MIME类型后缀。 许多服务和网站都需要图像后缀，如添 `.jpg` 加到URL。
* 为SEO（搜索引擎优化）创建指向URL的文件夹路径。

   了 [解Adobe Scene7 Publishing system如何支持SEO](/help/assets/assets/s7_seo.pdf)。

* 为SEO（搜索引擎优化）将元数据添加到URL。

   了 [解Adobe Scene7 Publishing system如何支持SEO](/help/assets/assets/s7_seo.pdf)。

* 设置内容配置以触发下载。
* 简化图像服务模板URL以实现个性化。 例如，将 `rgb{XX,YY,ZZ}` RTF转换为 `\redXX\greenYY\blueZZ`

* 请求要编码的特定字符(如、 `$`和 `{`), `}`以及要向ImageServer解码的特定字符。 例如，Facebook在包含特殊字符的URL中不能正常使用。

   请参 [阅从URL中删除特殊字符](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/remove-special-characters-urls.html)。

在Dynamic media的上下文中，使用基于XML的系统管理资产信息的网站可以将XML文件上传到Dynamic Media。 您可以将其中一个文件指定为用于服务Dynamic media资产的预处理规则集文件。 该文件重新构建标准URL协议格式，以满足与Dynamic Media集成的系统的业务逻辑。 指定XML文件作为规则集定义文件路径。

>[!CAUTION]
>
>使用规则集时要小心；它们可以防止Dynamic media内容显示在您的网站上。

有一些可用的示例规则集可以帮助您创建自己的规则集。
请参阅 [规则集引用](https://marketing.adobe.com/resources/help/en_US/s7/is_ir_api/is_api/image_catalog/c_rule_set_reference.html)。

与创建所有规则集一样，在使用XML validator程序（如xmlvalid）上传XML文件之前，请确保该文件是有效的。
另请参阅 [规则集疑难解答](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/scene7-ruleset-troubleshooting.html)。

此外，请确保首先在不影响实时生产环境的分阶段环境中测试规则集。
生产环境和暂存环境通常需要不同的登录名。

* **NA暂存环境登录页** : [https://s7sps1-staging.scene7.com/IpsWeb/](https://s7sps1-staging.scene7.com/IpsWeb/)
* **EMEA分阶段环境** 登录页： [https://s7sps3-staging.scene7.com/IpsWeb/](https://s7sps3-staging.scene7.com/IpsWeb/)
* **JAPAC暂存环境** 登录页： [https://s7sps5-staging.scene7.com/IpsWeb/](https://s7sps5-staging.scene7.com/IpsWeb/)

另请参 [阅在规则集中使用“asset”而不是“is”图像](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/ruleset-asset-instead-image.html)。

**部署XML规则集：**

1. 登录Dynamic Media Classic帐户：

   [https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html](https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html)

   您的凭据和登录是在配置时由Adobe提供的。 如果您没有此信息，请与技术支持联系。

1. 通过执行以下操作，上传规则集文件：

   * 在全局导航栏上，单击“上 **[!UICONTROL 传”]**。
   * 在“上 **[!UICONTROL 传]** ”页面的左上角附近，单击“浏 **[!UICONTROL 览”]**。
   * 在“打 **[!UICONTROL 开]** ”对话框中，浏览到规则集文件(XML)。
   * 选择文件，然后单击“ **[!UICONTROL 打开]**”。
   * 在上传页面的右侧 **** ，为规则集文件选择一个目标文件夹。
   * 在页面底部附近，确保选中“ **[!UICONTROL 上传后发布]** ”。
   * 在页面的右下角，单击“提交 **[!UICONTROL 上传”]**。
   * 在全局导航栏上，单击 **[!UICONTROL 作业]** ，以检查上传作业的状态。 当“作 **[!UICONTROL 业]** ”页面上的“状态 **[!UICONTROL ”列显示“上传完成]** ”时，请继续执行下一步。

1. 在页面顶部附近的导航栏上，单击“设置”>“应 **[!UICONTROL 用程序设置”>“发布设置”>“图像服务器”]**。
1. 在“图 **[!UICONTROL 像服务器发布]** ”页的“目录管理”组下，找到“规则集定义文件路径” **[!UICONTROL ，然后单]**********&#x200B;击“选择”。
1. 在“选 **[!UICONTROL 择规则集定义文件(XML)]** ”页面上，浏览至您的规则集文件，然后在页面的右下角单击“选 **[!UICONTROL 择”]**。
1. 在设置页面的右下角，单击“关 **[!UICONTROL 闭”]**。
1. 运行图像服务器发布作业。

   规则集条件将应用于对实时Dynamic Media图像服务器的请求。

   如果对规则集文件进行了更改，则在您重新上传和重新发布更新的规则集文件时，会立即应用这些更改。

