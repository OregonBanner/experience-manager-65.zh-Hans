---
title: 配置表单的位置
seo-title: 配置表单的位置
description: 了解如何为表单配置位置。
seo-description: 了解如何为表单配置位置。
uuid: ba35888b-492c-4678-890b-160b53e7d659
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 3d2b7cfb-228c-4cc2-8fcd-d500f0010010
translation-type: tm+mt
source-git-commit: 2cf9dcf2e9cf71c54e19e2c6ee825c9a8f00a9b7

---


# 配置表单的位置 {#configuring-locations-for-forms}

您可以指定属性的URL、URI和文件位置，如Web根目录、要检索的表单的位置、PDFForm转换中使用的种子PDF文件以及缓存位置。

1. 在管理控制台中，单击“服务”>“表单”。
1. 在“位置”下，指定相应的选项。 这些选项如下所述。
1. 单击保存。

## 位置设置 {#locations-settings}

**基本URL:** 表单资源（如图像和脚本）所在的基本URL。 此值是包含对外部依赖关系（如图像或脚本）的HREF引用的HTML转换所必需的。 xfasubset.js是执行XFA智能的HTML表单所必需的脚本之一。 此值必须是内容根URI的HTTP等效项。

>[!NOTE]
>
>基本URL仅支持HTTP或存储库协议。 它不支持file:///等协议。 如果您需要访问资源（如自定义CSS或数字签名URI），请使用相应的API参数值指定绝对位置。

当依赖关系路径为绝对路径时，将忽略基本URL值。 否则，依赖关系路径将与基本URL组合。

默认值为空字符串。

以下示例指向相同的内容（使用内容根URI和基本URL）:

`(ContentRootURI)/subdir/image1.jpg`

`(BaseURL)/subdir/image1.jpg`

**FS Web根URI:** Forms Web应用程序的URL。 如果Forms Web应用程序和客户端应用程序部署在同一应用程序服务器上，您可以将此框留空；将使用Forms API Web根URL。

如果Forms Web应用程序和客户端应用程序未部署到同一应用程序服务器，请在此框中提供Forms Web应用程序的URL，如本例所示：

`https://<host name>:<port>/FormServer`

其中 `host name`和 `port` 是承载Forms Web应用程序的服务器的名称和端口号。

默认值为空字符串。

**Web根URI:** 应用程序的Web根目录。 此值将与sTargetURL参数（当sTargetURL以相对形式提供时）结合使用（通过AEM表单SDK指定），以构建访问特定于应用程序的Web内容的绝对URL。

默认值为空字符串。

**内容根URI:** 从中检索表单的URI或绝对位置。 此值与通过API指定的sFormQuery参数组合，以构建检索到的表单的绝对路径。 此值可以引用可使用HTTP访问的目录或Web位置。

默认值为空字符串。

**XCI配置URI:** 找到用于渲染的XCI文件的相对或绝对位置。 对于相对值，假定XCI文件位于可部署的AEM forms EAR文件中。

默认值为 `com/adobe/formServer/PA/pa.xci`.

**字体映射URI:** 字体映射文件的相对或绝对位置。 对于相对值，假定此文件位于可部署的AEM表单EAR文件中。

字体映射文件用于为表单中的HTML转换创建自定义字体映射，因此允许您指定在客户端计算机上没有字体时将替换的字体。

默认值为 `com/adobe/formServer/client-font-map.properties`.

以下条目是font-mapping文件中某个条目的示例：

`Arial=Arial,Helvetica,sans-serif`

**种子PDF文件：** 用于PDFForm转换以优化投放的初始PDF文件。 种子PDF文件指定随表单设计和数据一起附加的自定义PDF文件（仅包含XFA流、图像和字体资源）。 表单由Acrobat 7或更高版本渲染，并适用于PDFForm转换。

默认值为空字符串。

**缓存位置：** 指定Forms磁盘缓存的位置。 更改此设置时，将重置当前位置的所有现有缓存信息，并在新位置创建新缓存。 选择以下选项之一：

**默认位置：** 这是默认选择。 选择此选项后，将在依赖于您所使用的应用程序服务器的位置创建缓存：

* **JBoss:**[JBoss主页]\server\[安装类型]\svcdata\FormServer\Cache
* **WebLogic:**[WebLogic主页]\user_projects\domains\[aem-forms域名]\adobe\[forms服务器名]\FormServer\Cache
* **WebSphere:**[IBM主页]\WebSphere\AppServer\installedApps\adobe\server1\FormServer\Cache

**LC临时目录：** 缓存创建在AEM表单临时目录的子目录中，该目录在管理控制台中的设置>核心系统设置>配置>临时目录位置下指定。 子目录名为adobeform_[servername]。

>[!NOTE]
>
>如果您使用的是临时清理实用程序，请注意，删除这些目录不会影响功能，但在创建新缓存之前，它可能会在短时间内显着影响性能。 要避免此问题，请勿在清除AEM表单临时目录时删除这些目录。

