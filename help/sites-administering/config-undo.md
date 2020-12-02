---
title: 为页面编辑配置撤消
seo-title: 为页面编辑配置撤消
description: 了解如何在AEM中配置对页面编辑的撤消支持。
seo-description: 了解如何在AEM中配置对页面编辑的撤消支持。
uuid: e5a49587-a2a6-41d5-b449-f7a8f7e4cee6
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 3cc7efc5-bcb2-41c9-b78b-308f6b7a298e
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 2%

---


# 为页面编辑配置撤消{#configuring-undo-for-page-editing}

[OSGi服务](/help/sites-deploying/configuring-osgi.md) **Day CQ WCM撤消配置**(`com.day.cq.wcm.undo.UndoConfigService`)显示若干属性，这些属性控制用于编辑页面的撤消和重做命令的行为。

## 默认配置 {#default-configuration}

在标准安装中，默认设置定义为`sling:OsgiConfig`节点上的属性：

`/libs/wcm/core/config.author/com.day.cq.wcm.undo.UndoConfig`

此节点包含`cq.wcm.undo.whitelist`和`cq.wcm.undo.blacklist`属性，对于其他属性，则采用默认值。

>[!CAUTION]
>
>您&#x200B;***必须***&#x200B;不要更改`/libs`路径中的任何内容。
>
>这是因为下次升级实例时，`/libs`的内容会被覆盖（当您应用修补程序或功能包时，很可能会被覆盖）。

## 配置撤消和重做{#configuring-undo-and-redo}

您可以为自己的实例配置这些OSGi服务属性。

>[!NOTE]
>
>与AEM合作时，有多种方法管理此类服务的配置设置；请参阅[配置OSGi](/help/sites-deploying/configuring-osgi.md)以了解更多详细信息和建议的做法。

以下列表Web控制台中显示的属性，后跟相应OSGi参数的名称，以及说明和默认值（如果适用）:

* **启用**
( 
`cq.wcm.undo.enabled`)

   * **描述**:确定页面作者是否可以撤消和重做更改。
   * **默认**:  `Selected`
   * **类型**: `Boolean`

* **路径**
( 
`cq.wcm.undo.path`)

   * **描述**:用于持久二进制撤消数据的存储库路径。当作者更改图像等二进制数据时，数据的原始版本将保留在此处。 当对二进制数据所做的更改被撤消时，此二进制撤消数据将恢复到页面。
   * **默认**:  `/var/undo`
   * **类型**: `String`

   >[!NOTE]
   >
   >默认情况下，只有管理员才能访问`/var/undo`节点。 只有在为作者授予访问二进制撤消数据的权限后，他们才能对二进制内容执行撤消和重做操作。

* **最小. validity**
( 
`cq.wcm.undo.validity`)

   * **描述**:二进制撤消数据的最小存储时间（以小时为单位）。在此时间段后，二进制数据可用于删除，以节省磁盘空间。
   * **默认**:  `10`
   * **类型**: `Integer`

* **步骤**
( 
`cq.wcm.undo.steps`)

   * **描述**:撤消历史记录中存储的最大页面操作数。
   * **默认**:  `20`
   * **类型**: `Integer`

* **持久性**
( 
`cq.wcm.undo.persistence`)

   * **描述**:继续使用的类可撤消历史记录。提供了两个持久性类：

      * `CQ.undo.persistence.WindowNamePersistence`:使用window.name属性保留历史记录。
      * `CQ.undo.persistence.CookiePersistance`:使用cookies保留历史记录。
   * **默认**:  `CQ.undo.persistence.WindowNamePersistence`
   * **类型**: `String`


* **持久性模式**
( 
`cq.wcm.undo.persistence.mode`)

   * **描述**:确定何时保留撤消历史记录。选择此选项可在每个页面编辑后保留撤消历史记录。 清除此选项后，仅在页面重新加载时（例如，用户导航到其他页面）才会保留。

      持久还原历史使用Web浏览器资源。 如果用户的浏览器对页面编辑反应缓慢，请尝试在重新加载页面时保留撤消历史记录。

   * **默认**:  `Selected`
   * **类型**: `Boolean`

* **标记模式**
( 
`cq.wcm.undo.markermode`)

   * **描述**:指定在执行撤消或重做时用于指示哪些段落受影响的可视提示。以下值有效：

      * flash:段落的选择指示符暂时闪烁。
      * 选择：将选择段落。
   * **默认**:  `flash`
   * **类型**: `String`


* **良好的组件**
( 
`cq.wcm.undo.whitelist`)

   * **描述**:要受撤消和重做命令影响的组件列表。当组件通过撤消／重做正常工作时，向此列表添加组件路径。 附加星号(&amp;ast;)以指定一组组件：

      * 以下值指定基础文本组件：

         `foundation/components/text`

      * 以下值指定所有基础组件：

         `foundation/components/*`
   * 当撤消或重做发出到未处于此列表的组件时，将显示一条消息，指示该命令可能不可靠。

   * **默认**:属性中填充了AEM提供的许多组件。
   * **类型**: `String[]`


* **组件错误**
( 
`cq.wcm.undo.blacklist`)

   * **描述**:不希望受撤消命令影响的组件和／或组件操作列表。使用撤消命令添加行为不正常的组件和组件操作：

      * 如果您不希望组件在撤消历史记录中执行任何操作，请添加组件路径，例如`collab/forum/components/post`
      * 如果希望撤消历史记录中忽略该特定操作（其他操作正确工作），请在路径后面附加冒号(:)和操作，例如`collab/forum/components/post:insertParagraph.`

   >[!NOTE]
   >
   >当操作在此列表上时，它仍会添加到撤消历史记录中。 用户无法撤消在撤消历史记录中存在的早于&#x200B;**错误组件**&#x200B;操作的操作。

   * 典型操作名称如下：

      * `insertParagraph`:组件将添加到页面。
      * `removeParagraph`:此时会删除该组件。
      * `moveParagraph`:段落将移至其他位置。
      * `updateParagraph`:段落属性会更改。
   * **默认**:属性会填充多个组件操作。
   * **类型**: `String[]`




