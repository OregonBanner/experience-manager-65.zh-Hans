---
title: 指定输出的文件位置
description: 了解如何为某些类型的文件（例如，内容根URI、XCI配置文件、缓存和默认值）的输出指定文件位置。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 620c69d6-4fe1-46d6-b5d4-3b562142e547
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 1%

---

# 指定输出的文件位置 {#specify-file-locations-for-output}

您可以指定Output查找所需特定类型文件的位置。

1. 在管理控制台中，单击“服务”>“输出”。
1. 在“位置”下，指定相应的选项。
1. 单击“保存”。

## 位置设置 {#locations-settings}

**内容根URI：** 从中检索表单的存储库的URI或绝对位置。 此值将与sForm参数（通过API指定）相结合，以构造所检索表单的绝对路径。 此值可引用可使用HTTP访问的目录或Web位置。

默认值为空字符串。

**XCI配置文件：** 输出服务用于渲染的XCI配置文件的相对或绝对位置。 对于相对值，假定XCI文件位于AEM Forms可部署EAR文件中。

默认值为 `com/adobe/formServer/PA/pa_output.xci`。

**缓存位置：** 指定输出磁盘缓存的位置。 更改此设置时，将重置当前位置的所有现有缓存信息，并在新位置创建一个新缓存。 选择以下选项之一：

**默认位置：** 这是默认选项。 如果选择该选项，则会在依赖于您正在使用的应用程序服务器的位置创建缓存：

* **JBoss：** `[JBoss Home]\server\[install type]\svcdata\Output\Cache`
* **WebLogic：** `[WebLogic Home]\user_projects\domains\[aem-forms domain Name]\adobe\[Forms Server name]\Output\Cache`
* **WebSphere：** `[IBM Home]\WebSphere\AppServer\installedApps\adobe\server1\Output\Cache`

**LC临时目录：** 缓存在AEM forms临时目录的子目录中创建，该目录在管理控制台中的“设置”>“核心系统设置”>“配置”>“临时目录的位置”下指定。 子目录名为 `adobeoutput_[servername]`.

>[!NOTE]
>
>如果您使用临时清理实用程序，虽然删除这些目录不会影响功能，但在创建新缓存之前，可能会在短时间内显着影响性能。 为避免出现此问题，在清除AEM forms临时目录时，请勿删除这些目录。
