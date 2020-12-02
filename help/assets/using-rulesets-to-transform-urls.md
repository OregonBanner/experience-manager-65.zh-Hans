---
title: 使用规则集转换URL
description: 您可以在Dynamic Media中部署规则集以转换URL。 规则集是用脚本语言（如JavaScript）编写的指令集，用于评估XML数据，并在数据满足某些条件时采取某些操作。
uuid: 9fed0c83-67b7-4483-a9b4-322e6a483449
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: abcff903-204b-4ab6-87d8-6f0ce63d7b41
translation-type: tm+mt
source-git-commit: 7e9dcebc654e63e171e2baacfe53081f58676f8d
workflow-type: tm+mt
source-wordcount: '797'
ht-degree: 5%

---


# 使用规则集转换URL {#using-rulesets-to-transform-urls}

您可以在Dynamic Media中部署规则集以转换URL。 规则集是用脚本语言（如JavaScript）编写的指令集，用于评估XML数据，并在数据满足某些条件时采取某些操作。 每个规则包括至少一个条件和至少一个操作。 规则根据条件评估XML数据，如果满足条件，则执行相应的操作。 规则集的示例包括：

* 添加MIME类型后缀。 许多服务和网站需要图像后缀，如向URL添加`.jpg`。
* 为SEO（搜索引擎优化）创建URL的文件夹路径。

   请参阅[Adobe Scene7出版系统如何支持SEO](/help/assets/assets/s7_seo.pdf)。

* 为SEO（搜索引擎优化）向URL添加元数据。

   请参阅[Adobe Scene7出版系统如何支持SEO](/help/assets/assets/s7_seo.pdf)。

* 设置内容配置以触发下载。
* 简化图像服务模板URL以实现个性化。 例如，将`rgb{XX,YY,ZZ}`转换为RTF就绪型`\redXX\greenYY\blueZZ`

* 请求要编码的特定字符（如`$`、`{`和`}`）和要解码到ImageServer的某些字符。 例如，Facebook在包含特殊字符的URL中不能正常使用。

   请参阅[从URL中删除特殊字符](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/remove-special-characters-urls.html)。

在Dynamic Media的上下文中，使用基于XML的系统管理资产信息的网站可以将XML文件上传到Dynamic Media。 您可以将其中一个文件指定为用于提供Dynamic Media资产的预处理规则集文件。 此文件重新构建标准URL协议格式，以满足与Dynamic Media集成的系统的业务逻辑。 指定XML文件作为规则集定义文件路径。

>[!CAUTION]
>
>使用规则集时要小心；它们可以阻止Dynamic Media内容显示在您的网站上。

有一些可用的示例规则集可以帮助您创建自己的规则集。
请参阅[规则集引用](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-serving-api/image-serving-api/rule-set-reference/c-rule-set-reference.html)。

与创建所有规则集一样，在使用XML validator项目（如xmlvalid）上传XML文件之前，请确保XML文件有效。
另请参阅[规则集疑难解答](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/scene7-ruleset-troubleshooting.html)。

另外，请确保首先在不影响实时生产环境的分阶段环境中测试规则集。
生产环境和临时环境通常需要不同的登录名。

* **NA临时** 环境登录页： [https://s7sps1-staging.scene7.com/IpsWeb/](https://s7sps1-staging.scene7.com/IpsWeb/)
* **EMEA分阶段** 环境登录页： [https://s7sps3-staging.scene7.com/IpsWeb/](https://s7sps3-staging.scene7.com/IpsWeb/)
* **JAPAC登台** 环境登录页： [https://s7sps5-staging.scene7.com/IpsWeb/](https://s7sps5-staging.scene7.com/IpsWeb/)

另请参阅[在规则集](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/ruleset-asset-instead-image.html)中使用“asset”而不是“is”映像。

**部署XML规则集：**

1. 登录您的Dynamic Media Classic帐户：

   [https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html](https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html)

   您的凭据和登录是在设置时由Adobe提供的。 如果您没有此信息，请与技术支持联系。

1. 通过执行以下操作上传规则集文件：

   * 在全局导航栏上，单击&#x200B;**[!UICONTROL 上传]**。
   * 在&#x200B;**[!UICONTROL 上传]**&#x200B;页面左上角附近，单击&#x200B;**[!UICONTROL 浏览]**。
   * 在&#x200B;**[!UICONTROL 打开]**&#x200B;对话框中，浏览至规则集文件(XML)。
   * 选择文件，然后单击&#x200B;**[!UICONTROL 打开]**。
   * 在&#x200B;**[!UICONTROL 上传]**&#x200B;页面的右侧，为规则集文件选择目标文件夹。
   * 在页面底部附近，确保选中“上载后发布&#x200B;**[!UICONTROL ”。]**
   * 在页面的右下角，单击&#x200B;**[!UICONTROL 提交上传]**。
   * 在全局导航栏上，单击&#x200B;**[!UICONTROL 作业]**&#x200B;以检查上传作业的状态。 当&#x200B;**[!UICONTROL 作业]**&#x200B;页面上的&#x200B;**[!UICONTROL 状态]**&#x200B;列显示上载完成时，请继续执行后续步骤。

1. 在页面顶部附近的导航栏上，单击&#x200B;**[!UICONTROL 设置>应用程序设置>发布设置>图像服务器]**。
1. 在&#x200B;**[!UICONTROL 图像服务器发布]**&#x200B;页面的&#x200B;**[!UICONTROL 目录管理]**&#x200B;组下，找到&#x200B;**[!UICONTROL 规则集定义文件路径]**，然后单击&#x200B;**[!UICONTROL 选择]**。
1. 在&#x200B;**[!UICONTROL 择规则集定义文件 (XML)]** 页面上，浏览至您的规则集文件，然后在页面的右下角单击&#x200B;**[!UICONTROL 选择]**。
1. 在设置页面的右下角，单击&#x200B;**[!UICONTROL 关闭]**。
1. 运行图像服务器发布作业。

   规则集条件将应用于对实时Dynamic Media图像服务器的请求。

   如果对规则集文件进行了更改，则在重新上传和重新发布更新的规则集文件时，会立即应用这些更改。

