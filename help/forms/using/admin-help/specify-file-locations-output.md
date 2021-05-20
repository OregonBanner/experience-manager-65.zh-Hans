---
title: 为输出指定文件位置
seo-title: 为输出指定文件位置
description: 了解如何为输出指定文件位置。
seo-description: 了解如何为输出指定文件位置。
uuid: 3287274f-85b5-4811-8abb-d347a9b80947
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 460bbb31-8187-469c-8102-b310093b6c03
exl-id: 620c69d6-4fe1-46d6-b5d4-3b562142e547
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 1%

---

# 指定输出{#specify-file-locations-for-output}的文件位置

您可以指定“输出”在何处查找它需要的特定类型的文件。

1. 在管理控制台中，单击服务>输出。
1. 在位置下，指定相应的选项。
1. 单击保存。

## 位置设置{#locations-settings}

**内容根URI:** 从中检索表单的存储库的URI或绝对位置。此值与通过API指定的sForm参数结合使用，以构建检索到的表单的绝对路径。 此值可引用可使用HTTP访问的目录或Web位置。

默认值是空字符串。

**XCI配置文件：** 输出服务用于渲染的XCI配置文件的相对或绝对位置。对于相对值，假定XCI文件位于AEM Forms可部署的EAR文件中。

默认值为 `com/adobe/formServer/PA/pa_output.xci`.

**缓存位置：** 指定输出磁盘缓存的位置。更改此设置时，将重置当前位置的所有现有缓存信息，并在新位置创建新缓存。 选择以下选项之一：

**默认位置：** 这是默认选择。选择此选项后，将在依赖于您所使用的应用程序服务器的位置创建缓存：

* **JBoss:** `[JBoss Home]\server\[install type]\svcdata\Output\Cache`
* **WebLogic:** `[WebLogic Home]\user_projects\domains\[aem-forms domain Name]\adobe\[forms server name]\Output\Cache`
* **WebSphere:** `[IBM Home]\WebSphere\AppServer\installedApps\adobe\server1\Output\Cache`

**LC临时目录：** 缓存在AEM forms temp目录的子目录中创建，该目录在管理控制台中的“设置”>“核心系统设置”>“配置”>“临时目录的位置”下指定。子目录名为`adobeoutput_[servername]`。

>[!NOTE]
>
>如果您使用的是临时清理实用程序，请注意，删除这些目录不会影响功能，但在创建新缓存之前，这会在短时间内对性能产生重大影响。 要避免出现此问题，请在清除AEM表单临时目录时不要删除这些目录。
