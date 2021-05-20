---
title: 配置Forms位置
seo-title: 配置Forms位置
description: 了解如何为Forms配置位置。
seo-description: 了解如何为Forms配置位置。
uuid: ba35888b-492c-4678-890b-160b53e7d659
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 3d2b7cfb-228c-4cc2-8fcd-d500f0010010
exl-id: 0d9eb7fe-28a6-444e-957d-023687158c61
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '815'
ht-degree: 1%

---

# 配置Forms的位置{#configuring-locations-for-forms}

您可以指定属性的URL、URI和文件位置，如Web根、要检索的表单的位置、PDFForm转换中使用的种子PDF文件以及缓存位置。

1. 在管理控制台中，单击服务> Forms。
1. 在位置下，指定相应的选项。 选项如下所述。
1. 单击保存。

## 位置设置{#locations-settings}

**基本URL:** 表单资源（如图像和脚本）所在的基本URL。对于包含对外部依赖项（如图像或脚本）的HREF引用的HTML转换，此值是必需的。 其中一个脚本是xfasubset.js，HTML表单执行XFA智能所需的脚本。 此值必须等同于内容根URI的HTTP。

>[!NOTE]
>
>基本URL仅支持HTTP或存储库协议。 它不支持file:///等协议。 如果您需要访问资源（如自定义CSS或数字签名URI），请使用相应的API参数值指定绝对位置。

当依赖关系路径为绝对路径时，将忽略基本URL值。 否则，依赖关系路径将与基本URL组合使用。

默认值是空字符串。

以下示例指向相同的内容（使用内容根URI和基本URL）：

`(ContentRootURI)/subdir/image1.jpg`

`(BaseURL)/subdir/image1.jpg`

**FS Web根URI:** Forms Web应用程序的URL。如果Forms Web应用程序和客户端应用程序部署在同一应用程序服务器上，则可以将此框留空；将使用Forms API Web根URL。

如果Forms Web应用程序和客户端应用程序未部署到同一应用程序服务器，请在此框中提供Forms Web应用程序的URL，如以下示例所示：

`https://<host name>:<port>/FormServer`

其中，`host name`和`port`是托管Forms Web应用程序的服务器的名称和端口号。

默认值是空字符串。

**Web根URI:** 应用程序的Web根。此值与通过AEM Forms SDK指定的sTargetURL参数（当sTargetURL以相对方式提供时）结合使用，可构建一个绝对URL以访问特定于应用程序的Web内容。

默认值是空字符串。

**内容根URI:** 从中检索表单的URI或绝对位置。此值与通过API指定的sFormQuery参数结合使用，以构建要检索的表单的绝对路径。 此值可引用可使用HTTP访问的目录或Web位置。

默认值是空字符串。

**XCI配置URI:** 找到用于渲染的XCI文件的相对或绝对位置。对于相对值，假定XCI文件位于可部署的AEM Forms EAR文件中。

默认值为 `com/adobe/formServer/PA/pa.xci`.

**字体映射URI:** 字体映射文件的相对或绝对位置。对于相对值，假定此文件位于可部署的AEM Forms EAR文件中。

字体映射文件用于为表单中的HTML转换创建自定义字体映射，因此允许您指定当客户端计算机上没有字体时将替换的字体。

默认值为 `com/adobe/formServer/client-font-map.properties`.

以下条目是font-mapping文件中的一个条目示例：

`Arial=Arial,Helvetica,sans-serif`

**种子PDF文件：** PDFForm转换中用于优化交付的初始PDF文件。种子PDF文件指定了一个自定义的PDF文件（仅包含XFA流、图像和字体资源），该文件将附加表单设计和数据。 表单由Acrobat 7或更高版本渲染，并适用于PDFForm转换。

默认值是空字符串。

**缓存位置：** 指定Forms磁盘缓存的位置。更改此设置时，将重置当前位置的所有现有缓存信息，并在新位置创建新缓存。 选择以下选项之一：

**默认位置：** 这是默认选择。选择此选项后，将在依赖于您所使用的应用程序服务器的位置创建缓存：

* **JBoss:** [JBoss主页]\server\[安装类型]\svcdata\FormServer\Cache
* **WebLogic:** [WebLogic主页]\user_projects\domains\[aem-forms域名]\adobe\[forms服务器名称]\FormServer\Cache
* **WebSphere:** [IBM主页]\WebSphere\AppServer\installedApps\adobe\server1\FormServer\Cache

**LC临时目录：** 缓存在AEM forms temp目录的子目录中创建，该目录在管理控制台中的“设置”>“核心系统设置”>“配置”>“临时目录的位置”下指定。子目录名为adobeform_[servername]。

>[!NOTE]
>
>如果您使用的是临时清理实用程序，请注意，删除这些目录不会影响功能，但在创建新缓存之前会在短时间内显着影响性能。 要避免出现此问题，请在清除AEM表单临时目录时不要删除这些目录。
