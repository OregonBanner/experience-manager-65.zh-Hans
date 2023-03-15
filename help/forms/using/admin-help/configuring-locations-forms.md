---
title: 为Forms配置位置
seo-title: Configuring locations for Forms
description: 了解如何为Forms配置位置。
seo-description: Learn how to configure location for Forms.
uuid: ba35888b-492c-4678-890b-160b53e7d659
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 3d2b7cfb-228c-4cc2-8fcd-d500f0010010
exl-id: 0d9eb7fe-28a6-444e-957d-023687158c61
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '804'
ht-degree: 1%

---

# 为Forms配置位置 {#configuring-locations-for-forms}

您可以指定属性的URL、URI和文件位置，例如Web根目录、要检索的表单的位置、在PDFForm转换中使用的种子PDF文件以及缓存位置。

1. 在管理控制台中，单击服务> Forms。
1. 在“位置”下，指定相应的选项。 这些选项如下所述。
1. 单击“保存”。

## 位置设置 {#locations-settings}

**基本URL：** 表单资源（如图像和脚本）所在的基本URL。 HTML转换需要此值，这些转换包括对外部从属关系（如图像或脚本）的HREF引用。 其中一个脚本是xfasubset.js，它是HTML表单执行XFA智能所必需的。 此值必须是内容根URI的HTTP等效值。

>[!NOTE]
>
>基本URL仅支持HTTP或存储库协议。 它不支持file:///之类的协议。 如果您需要访问资源（如自定义CSS或数字签名URI），请使用相应的API参数值指定绝对位置。

当依赖关系路径为绝对路径时，将忽略基本URL值。 否则，依赖关系路径将与基本URL相结合。

默认值为空字符串。

以下示例指向相同的内容（使用内容根URI和基本URL）：

`(ContentRootURI)/subdir/image1.jpg`

`(BaseURL)/subdir/image1.jpg`

**FS Web根URI：** Forms Web应用程序的URL。 如果将Forms Web应用程序和客户端应用程序部署在同一应用程序服务器上，则可以将此框留空；将使用Forms API Web根URL。

如果Forms Web应用程序和客户端应用程序未部署到同一应用程序服务器，请在此框中提供Forms Web应用程序的URL，如以下示例所示：

`https://<host name>:<port>/FormServer`

位置 `host name`和 `port` 是托管Forms Web应用程序的服务器的服务器名称和端口号。

默认值为空字符串。

**Web根URI：** 应用程序的Web根目录。 此值会与通过AEM Forms SDK指定的sTargetURL参数（当sTargetURL以相对形式提供时）相结合，以构建访问特定于应用程序的Web内容的绝对URL。

默认值为空字符串。

**内容根URI：** 从中检索表单的URI或绝对位置。 此值与sFormQuery参数（通过API指定）相结合，可构造检索到的表单的绝对路径。 此值可以引用可使用HTTP访问的目录或Web位置。

默认值为空字符串。

**XCI配置URI：** 找到用于渲染的XCI文件的相对或绝对位置。 对于相对值，假定该XCI文件驻留在可部署的AEM表单EAR文件中。

默认值为 `com/adobe/formServer/PA/pa.xci`。

**字体映射URI：** 字体映射文件的相对或绝对位置。 对于相对值，假定此文件位于可部署的AEM forms EAR文件中。

font-mapping文件用于为表单中的HTML转换创建自定义字体映射，因此允许您指定在客户端计算机上无法使用字体时将替换的字体。

默认值为 `com/adobe/formServer/client-font-map.properties`。

以下条目是字体映射文件中一个条目的示例：

`Arial=Arial,Helvetica,sans-serif`

**种子PDF文件：** PDFForm转换中使用的初始PDF文件以优化投放。 种子PDF文件指定附加到表单设计和数据的自定义PDF文件（仅包含XFA流、图像和字体资源）。 表单由Acrobat 7或更高版本渲染，并适用于PDForm转换。

默认值为空字符串。

**缓存位置：** 指定Forms磁盘缓存的位置。 更改此设置时，将重置当前位置的所有现有缓存信息，并在新位置创建一个新缓存。 选择以下选项之一：

**默认位置：** 这是默认选项。 如果选择该选项，将在依赖于您正在使用的应用程序服务器的位置创建缓存：

* **JBoss：** [JBoss主页]\server\[install type]\svcdata\FormServer\Cache
* **WebLogic：** [WebLogic主页]\user_projects\domains\[aem-forms域名]\adobe\[表单服务器名称]\FormServer\Cache
* **WebSphere：** [IBM主页]\WebSphere\AppServer\installedApps\adobe\server1\FormServer\Cache

**LC临时目录：** 缓存在AEM forms临时目录的子目录中创建，该目录在管理控制台中的“设置”>“核心系统设置”>“配置”>“临时目录的位置”下指定。 该子目录名为adobeform_[服务器名称].

>[!NOTE]
>
>如果您使用临时清理实用程序，请注意，虽然删除这些目录不会影响功能，但在创建新缓存之前，它可能会在短时间内对性能产生重大影响。 为避免出现此问题，在清除AEM forms临时目录时，请勿删除这些目录。
