---
title: 配置撤消以进行页面编辑
description: 了解如何为AEM中的页面编辑配置撤消支持。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
exl-id: 2cf3ac3f-ee17-480d-a32a-c57631502693
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '702'
ht-degree: 2%

---

# 配置撤消以进行页面编辑{#configuring-undo-for-page-editing}

此 [OSGi服务](/help/sites-deploying/configuring-osgi.md)  **Day CQ WCM撤消配置** ( `com.day.cq.wcm.undo.UndoConfigService`)公开了几个属性，这些属性控制用于编辑页面的撤消和重做命令的行为。

## 默认配置 {#default-configuration}

在标准安装中，默认设置被定义为 `sling:OsgiConfig`节点：

`/libs/wcm/core/config.author/com.day.cq.wcm.undo.UndoConfig`

此节点包含 `cq.wcm.undo.whitelist` 和 `cq.wcm.undo.blacklist` 属性，对于其他属性，将采用默认值。

>[!CAUTION]
>
>您 ***必须*** 不会更改中的任何内容 `/libs` 路径。
>
>这是因为 `/libs` 下次升级实例时将被覆盖（在应用修补程序或功能包时很可能会被覆盖）。

## 配置撤消和重做 {#configuring-undo-and-redo}

您可以为自己的实例配置这些OSGi服务属性。

>[!NOTE]
>
>使用AEM时，可通过多种方法管理此类服务的配置设置；请参阅 [配置OSGi](/help/sites-deploying/configuring-osgi.md) 以了解更多详细信息和建议的做法。

下面列出了Web控制台中显示的属性，其后是相应OSGi参数的名称，以及说明和默认值（如果适用）：

* **启用**
( `cq.wcm.undo.enabled`)

   * **描述**：确定页面作者是否可以撤消和重做更改。
   * **默认**： `Selected`
   * **类型**：`Boolean`

* **路径**
( `cq.wcm.undo.path`)

   * **描述**：用于保留二进制还原数据的存储库路径。 当作者更改二进制数据（如图像）时，数据的原始版本将保留在此处。 撤消对二进制数据的更改时，此二进制撤消数据将还原到页面。
   * **默认**： `/var/undo`
   * **类型**：`String`

  >[!NOTE]
  >
  >默认情况下，只有管理员才能访问 `/var/undo` 节点。 只有在授予作者访问二进制撤消数据的权限后，他们才能对二进制内容执行撤消和重做操作。

* **最低 有效性**
( `cq.wcm.undo.validity`)

   * **描述**：二进制还原数据存储的最小时间（以小时为单位）。 在此时间段之后，二进制数据可供删除，以节省磁盘空间。
   * **默认**： `10`
   * **类型**：`Integer`

* **步骤**
( `cq.wcm.undo.steps`)

   * **描述**：还原历史记录中存储的最大页面操作数。
   * **默认**： `20`
   * **类型**：`Integer`

* **持久性**
( `cq.wcm.undo.persistence`)

   * **描述**：保留撤消历史记录的类。 提供了两个持久性类：

      * `CQ.undo.persistence.WindowNamePersistence`：使用window.name属性保留历史记录。
      * `CQ.undo.persistence.CookiePersistance`：保留使用Cookie的历史记录。

   * **默认**： `CQ.undo.persistence.WindowNamePersistence`
   * **类型**：`String`

* **持久性模式**
( `cq.wcm.undo.persistence.mode`)

   * **描述**：确定何时保留撤消历史记录。 选择此选项可在每次编辑页面后保留还原历史记录。 清除此选项可仅在发生页面重新加载（例如，用户导航到其他页面）时保留。

     保留撤消历史记录会使用Web浏览器资源。 如果用户的浏览器对页面编辑的反应较慢，请尝试在页面重新加载时保留撤消历史记录。

   * **默认**： `Selected`
   * **类型**：`Boolean`

* **标记模式**
( `cq.wcm.undo.markermode`)

   * **描述**：指定用于指示发生撤消或重做时受影响的段落的可视提示。 以下值有效：

      * 闪烁：段落的选择指示器会暂时闪烁。
      * 选择：选定段落。

   * **默认**： `flash`
   * **类型**：`String`

* **组件良好**
( `cq.wcm.undo.whitelist`)

   * **描述**：您希望受撤消和重做命令影响的组件列表。 当组件路径在撤消/重做操作中正常运行时，将其添加到此列表。 附加星号(&amp;ast；)以指定一组组件：

      * 以下值指定基础文本组件：

        `foundation/components/text`

      * 以下值指定所有基础组件：

        `foundation/components/*`

   * 当向不在此列表中的组件发出撤消或重做命令时，将显示一条消息，指示该命令可能不可靠。

   * **默认**：属性由AEM提供的许多组件填充。
   * **类型**：`String[]`

* **组件损坏**
( `cq.wcm.undo.blacklist`)

   * **描述**：您不希望受撤消命令影响的组件和/或组件操作列表。 使用undo命令添加行为不正确的组件和组件操作：

      * 如果您希望在撤消历史记录中不包含组件的任何操作，请添加组件路径，例如， `collab/forum/components/post`
      * 例如，如果希望撤消历史记录中省略该特定操作（其他操作可正常工作），请在路径中附加一个冒号(：)和一个操作， `collab/forum/components/post:insertParagraph.`

  >[!NOTE]
  >
  >当操作在此列表上时，它仍会添加到撤消历史记录中。 用户无法撤消早于 **组件损坏** 撤消历史记录中的操作。

   * 典型操作名称如下：

      * `insertParagraph`：将组件添加到页面。
      * `removeParagraph`：删除组件。
      * `moveParagraph`：将段落移至其他位置。
      * `updateParagraph`：更改段落属性。

   * **默认**：属性由多个组件操作填充。
   * **类型**：`String[]`
