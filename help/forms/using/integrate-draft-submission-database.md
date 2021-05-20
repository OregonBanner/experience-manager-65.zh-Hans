---
title: 将草稿和提交组件与数据库集成的示例
seo-title: 将草稿和提交组件与数据库集成的示例
description: 引用自定义数据和元数据服务的实施，以将草稿和提交组件与数据库集成。
seo-description: 引用自定义数据和元数据服务的实施，以将草稿和提交组件与数据库集成。
uuid: ccdb900e-2c2e-4ed3-8a88-5c97aa0092a1
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: da96d3d8-a338-470a-8d20-55ea39bd15bf
exl-id: 2e4f8f51-df02-4bbb-99bb-30181facd1e0
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1493'
ht-degree: 1%

---

# 将草稿和提交组件与数据库{#sample-for-integrating-drafts-submissions-component-with-database}集成的示例

## 示例概述{#sample-overview}

AEM Forms Portal的草稿和提交组件允许用户将其表单另存为草稿，稍后从任何设备提交。 此外，用户还可以在门户上查看其提交的表单。 为启用此功能，AEM Forms提供了数据和元数据服务，用于存储用户在表单中填写的数据以及与草稿和提交的表单关联的表单元数据。 默认情况下，此数据存储在CRX存储库中。 但是，当用户通过AEM发布实例与表单进行交互时（通常位于企业防火墙之外），组织可能希望自定义数据存储以使其更加安全可靠。

本文档中讨论的示例是自定义数据和元数据服务的参考实现，用于将草稿和提交组件与数据库集成在一起。 示例实现中使用的数据库是&#x200B;**MySQL 5.6.24**。 但是，您可以将草稿和提交组件与您选择的任何数据库相集成。

>[!NOTE]
>
>* 本文档中介绍的示例和配置符合MySQL 5.6.24的要求，您必须将它们适当地替换为数据库系统。
>* 确保您已安装最新版本的AEM Forms附加组件包。 有关可用包的列表，请参阅[AEM Forms发行版](https://helpx.adobe.com/cn/aem-forms/kb/aem-forms-releases.html)文章。
>* 示例包仅适用于自适应Forms提交操作。


## 设置并配置示例{#set-up-and-configure-the-sample}

对所有创作实例和发布实例执行以下步骤以安装和配置示例：

1. 将以下&#x200B;**aem-fp-db-integration-sample-pkg-6.1.2.zip**&#x200B;包下载到您的文件系统。

   数据库集成的示例包

[获取文件](assets/aem-fp-db-integration-sample-pkg-6.1.2.zip)

1. 转到位于https://[*host*]&#x200B;的AEM包管理器：[*port*]/crx/packmgr/。
1. 单击&#x200B;**[!UICONTROL 上传包]**。

1. 浏览以选择&#x200B;**aem-fp-db-integration-sample-pkg-6.1.2.zip**&#x200B;包，然后单击&#x200B;**[!UICONTROL 确定]**。
1. 单击包旁边的&#x200B;**[!UICONTROL 安装]**&#x200B;以安装包。
1. 转到&#x200B;**[!UICONTROL AEM Web控制台配置]**
位于https://[*host*]&#x200B;的页面：[*port*]/system/console/configMgr。
1. 单击以在编辑模式下打开&#x200B;**[!UICONTROL Forms Portal草稿和提交配置]**。

1. 指定属性的值，如下表所述：

   | **属性** | **描述** | **值** |
   |---|---|---|
   | Forms门户草稿数据服务 | 草稿数据服务的标识符 | formsportal.sampledataservice |
   | Forms门户草稿元数据服务 | 草稿元数据服务的标识符 | formsportal.samplemetadataservice |
   | Forms门户提交数据服务 | 提交数据服务的标识符 | formsportal.sampledataservice |
   | Forms门户提交元数据服务 | 提交元数据服务的标识符 | formsportal.samplemetadataservice |
   | Forms门户待签署的Data Service | 挂起签名数据服务的标识符 | formsportal.sampledataservice |
   | Forms门户待签名元数据服务 | 挂起的签名元数据服务的标识符 | formsportal.samplemetadataservice |

   >[!NOTE]
   >
   >这些服务通过其名称解析，其名称被提及为`aem.formsportal.impl.prop`键值，如下所示：

   ```java
   @Service(value = {SubmitDataService.class, DraftDataService.class})
   @Property(name = "aem.formsportal.impl.prop", value = "formsportal.sampledataservice")
   @Service(value = { SubmitMetadataService.class, DraftMetadataService.class })
   @Property(name = "aem.formsportal.impl.prop", value = "formsportal.samplemetadataservice")
   ```

   您可以更改数据和元数据表的名称。

   要为元数据表提供其他名称，请执行以下操作：

   * 在Web控制台配置中，找到并单击Forms门户元数据服务实施示例。 您可以更改数据源、元数据/其他元数据表名称的值。

   要为数据表提供其他名称，请执行以下操作：

   * 在“Web控制台配置”中，找到并单击Forms Portal Data Service实施示例。 您可以更改数据源和数据表名称的值。
   >[!NOTE]
   >
   >如果更改表名称，请在表单门户配置中提供它们。

1. 保持其他配置原样，然后单击&#x200B;**[!UICONTROL Save]**。

1. 数据库连接可通过Apache Sling连接池化数据源完成。
1. 对于Apache Sling连接，在Web控制台配置的编辑模式下，找到并单击以打开&#x200B;**[!UICONTROL Apache Sling连接池化数据源]**。 指定属性的值，如下表所述：

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>值</strong></td>
  </tr>
  <tr>
   <td>数据源名称</td>
   <td><p>用于从数据源池筛选驱动程序的数据源名称</p> <p><strong>注意： </strong><em>实施示例使用FormsPortal作为数据源名称。</em></p> </td>
  </tr>
  <tr>
   <td>JDBC驱动程序类</td>
   <td>com.mysql.jdbc.Driver</td>
  </tr>
  <tr>
   <td>JDBC连接URI<br /> </td>
   <td>jdbc[<em>host</em>]:[<em>port</em>]/[<em>schema_name</em>]</td>
  </tr>
  <tr>
   <td>用户名</td>
   <td>对数据库表进行身份验证和执行操作的用户名</td>
  </tr>
  <tr>
   <td>密码</td>
   <td>与用户名关联的密码</td>
  </tr>
  <tr>
   <td>事务隔离</td>
   <td>READ_COMMITTED</td>
  </tr>
  <tr>
   <td>最大活动连接数</td>
   <td>1000</td>
  </tr>
  <tr>
   <td>最大空闲连接数</td>
   <td>100</td>
  </tr>
  <tr>
   <td>最小空闲连接</td>
   <td>10</td>
  </tr>
  <tr>
   <td>初始大小</td>
   <td>10</td>
  </tr>
  <tr>
   <td>最大等待</td>
   <td>100000</td>
  </tr>
  <tr>
   <td>借用测试</td>
   <td>已选中</td>
  </tr>
  <tr>
   <td>空闲时测试</td>
   <td>已选中</td>
  </tr>
  <tr>
   <td>验证查询</td>
   <td>示例值包括：SELECT 1(mysql)、从dual(oracle)中选择1、SELECT 1(MS Sql Server)(validationQuery)</td>
  </tr>
  <tr>
   <td>验证查询超时</td>
   <td>10000</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
> * MySQL的JDBC驱动程序未提供示例。 确保已为其进行配置，并提供配置JDBC连接池所需的信息。
> * 将创作实例和发布实例指向使用同一数据库。 对于所有创作实例和发布实例，JDBC连接URI字段的值必须相同。

>



1. 保持其他配置原样，然后单击&#x200B;**[!UICONTROL Save]**。

1. 如果数据库架构中已有表，请跳转到下一步。

   否则，如果数据库架构中没有表，请执行以下SQL语句，为数据库架构中的数据、元数据和其他元数据创建单独的表：

   >[!NOTE]
   >
   >创作实例和发布实例不需要不同的数据库。 在所有创作实例和发布实例上使用相同的数据库。

   **数据表的SQL语句**

   ```sql
   CREATE TABLE `data` (
   `owner` varchar(255) DEFAULT NULL,
   `data` longblob,
   `metadataId` varchar(45) DEFAULT NULL,
   `id` varchar(45) NOT NULL,
   PRIMARY KEY (`id`)
   ) ENGINE=InnoDB DEFAULT CHARSET=utf8;
   ```

   **元数据表的SQL语句**

   ```sql
   CREATE TABLE `metadata` (
   `formPath` varchar(1000) DEFAULT NULL,
   `formType` varchar(100) DEFAULT NULL,
   `description` text,
   `formName` varchar(255) DEFAULT NULL,
   `owner` varchar(255) DEFAULT NULL,
   `enableAnonymousSave` varchar(45) DEFAULT NULL,
   `renderPath` varchar(1000) DEFAULT NULL,
   `nodeType` varchar(45) DEFAULT NULL,
   `charset` varchar(45) DEFAULT NULL,
   `userdataID` varchar(45) DEFAULT NULL,
   `status` varchar(45) DEFAULT NULL,
   `formmodel` varchar(45) DEFAULT NULL,
   `markedForDeletion` varchar(45) DEFAULT NULL,
   `showDorClass` varchar(255) DEFAULT NULL,
   `sling:resourceType` varchar(1000) DEFAULT NULL,
   `attachmentList` longtext,
   `draftID` varchar(45) DEFAULT NULL,
   `submitID` varchar(45) DEFAULT NULL,
   `id` varchar(60) NOT NULL,
   `profile` varchar(255) DEFAULT NULL,
   `submitUrl` varchar(1000) DEFAULT NULL,
   `xdpRef` varchar(1000) DEFAULT NULL,
   `agreementId` varchar(255) DEFAULT NULL,
   `nextSigners` varchar(255) DEFAULT NULL,
   `eSignStatus` varchar(45) DEFAULT NULL,
   `pendingSignID` varchar(45) DEFAULT NULL,
   `agreementDataId` varchar(255) DEFAULT NULL,
   `enablePortalSubmit` varchar(45) DEFAULT NULL,
   `submitType` varchar(45) DEFAULT NULL,
   `dataType` varchar(45) DEFAULT NULL,
   `jcr:lastModified` varchar(45) DEFAULT NULL,
   PRIMARY KEY (`id`),
   UNIQUE KEY `ID_UNIQUE` (`id`)
   ) ENGINE=InnoDB DEFAULT CHARSET=utf8;
   ```

   **用于其他元数据的SQL语句**

   ```sql
   CREATE TABLE `additionalmetadatatable` (
   `value` text,
   `key` varchar(255) NOT NULL,
   `id` varchar(60) NOT NULL,
   PRIMARY KEY (`id`,`key`),
   CONSTRAINT ‘additionalmetadatatable_fk’ FOREIGN KEY (`id`) REFERENCES `metadata` (`id`) ON DELETE CASCADE
   ) ENGINE=InnoDB DEFAULT CHARSET=utf8;
   ```

   **注释表的SQL语句**

   ```sql
   CREATE TABLE `commenttable` (
   `commentId` varchar(255) DEFAULT NULL,
   `comment` text DEFAULT NULL,
   `ID` varchar(255) DEFAULT NULL,
   `commentowner` varchar(255) DEFAULT NULL,
   `time` varchar(255) DEFAULT NULL);
   ```

1. 如果数据库架构中已经有表（数据、元数据和其他元数据），请执行以下alter表查询：

   **用于更改数据表的SQL语句**

   ```sql
   ALTER TABLE `data` CHANGE `owner` `owner` VARCHAR(255) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL;
   ```

   **用于更改元数据表的SQL语句**

   ```sql
   ALTER TABLE metadata add markedForDeletion varchar(45) DEFAULT NULL
   ```

   >[!NOTE]
   >
   >如果您已经运行ALTER TABLE元数据添加查询，并且表中存在markedforDeletion列，则该查询将失败。

   ```sql
   ALTER TABLE metadata add agreementId varchar(255) DEFAULT NULL,
   add nextSigners varchar(255) DEFAULT NULL,
   add eSignStatus varchar(45) DEFAULT NULL,
   add pendingSignID varchar(45) DEFAULT NULL,
   add agreementDataId varchar(255) DEFAULT NULL,
   add enablePortalSubmit varchar(45) DEFAULT NULL,
   add submitType varchar(45) DEFAULT NULL,
   add dataType varchar(45) DEFAULT NULL;
   ```

   ```sql
   ALTER TABLE `metadata` CHANGE `formPath` `formPath` VARCHAR(1000) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `formType` `formType` VARCHAR(100) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `description` `description` TEXT CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `formName` `formName` VARCHAR(255) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `owner` `owner` VARCHAR(255) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `renderPath` `renderPath` VARCHAR(1000) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `showDorClass` `showDorClass` VARCHAR(255) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `sling:resourceType` `sling:resourceType` VARCHAR(1000) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `profile` `profile` VARCHAR(255) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `submitUrl` `submitUrl` VARCHAR(1000) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `xdpRef` `xdpRef` VARCHAR(1000) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL;
   ```

   **用于更改附加元数据表的SQL语句**

   ```sql
   ALTER TABLE `additionalmetadatatable` CHANGE `value` `value` TEXT CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL, CHANGE `key` `key` VARCHAR(255) CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL;
   ```

现在已配置示例实施，您可以在数据库中存储所有数据和元数据时，使用该实施列出草稿和提交。 现在，让我们看看如何在示例中配置数据和元数据服务。

## 安装mysql-connector-java-5.1.39-bin.jar文件{#install-mysql-connector-java-bin-jar-file}

对所有创作实例和发布实例执行以下步骤，以安装mysql-connector-java-5.1.39-bin.jar文件：

1. 导航到`https://'[server]:[port]'/system/console/depfinder`并搜索com.mysql.jdbc包。
1. 在“导出方式”列中，检查包是否由任何包导出。

   如果包未被任何包导出，则继续。

1. 导航到`https://'[server]:[port]'/system/console/bundles`并单击&#x200B;**[!UICONTROL Install/Update]**。
1. 单击&#x200B;**[!UICONTROL 选择文件]**&#x200B;并浏览以选择mysql-connector-java-5.1.39-bin.jar文件。 此外，选中&#x200B;**[!UICONTROL 启动包]**&#x200B;和&#x200B;**[!UICONTROL 刷新包]**&#x200B;复选框。
1. 单击&#x200B;**[!UICONTROL 安装或更新]**。 完成后，重新启动服务器。
1. （*仅Windows*）关闭操作系统的系统防火墙。

## 表单门户数据和元数据服务的示例代码{#sample-code-for-forms-portal-data-and-metadata-service}

以下zip包含用于数据和元数据服务接口的`FormsPortalSampleDataServiceImpl`和`FormsPortalSampleMetadataServiceImpl`（实施类）。 此外，它包含编译上述实现类所需的所有类。

[获取文件](assets/sample_package.zip)

## 验证文件名{#verify-length-of-the-file-name}的长度

Forms Portal的数据库实施使用其他元数据表。 表具有基于表的键和id列的复合主键。 MySQL允许主键的长度不超过255个字符。 您可以使用以下客户端验证脚本来验证附加到文件小组件的文件名长度。 附加文件后，将运行验证。 当文件名大于150（包括扩展名）时，以下过程中提供的脚本会显示一条消息。 您可以修改脚本，以检查其是否存在不同数量的字符。

执行以下步骤以创建[客户端库](/help/sites-developing/clientlibs.md)并使用脚本：

1. 登录到CRXDE并导航到/etc/clientlibs/
1. 创建类型为&#x200B;**cq:ClientLibraryFolder**&#x200B;的节点，并提供该节点的名称。 例如，`validation`。

   单击&#x200B;**[!UICONTROL Save All]**。

1. 右键单击节点，单击&#x200B;**[!UICONTROL 创建新文件]**，然后创建扩展名为.txt的文件。 例如， `js.txt`将以下代码添加到新创建的.txt文件中，然后单击&#x200B;**[!UICONTROL 保存全部]**。

   ```javascript
   #base=util
    util.js
   ```

   在上述代码中，`util`是文件夹的名称，`util.js`是`util`文件夹中文件的名称。 在以下步骤中创建`util`文件夹和`util.js`文件。

1. 右键单击在步骤2中创建的`cq:ClientLibraryFolder`节点，选择创建>创建文件夹。 创建名为`util`的文件夹。 单击&#x200B;**[!UICONTROL Save All]**。 右键单击`util`文件夹，选择创建>创建文件。 创建名为`util.js`的文件。 单击&#x200B;**[!UICONTROL Save All]**。

1. 将以下代码添加到util.js文件中，然后单击&#x200B;**[!UICONTROL 保存全部]**。 代码验证文件名的长度。

   ```javascript
   /*
    * ADOBE CONFIDENTIAL
    * ___________________
    *
    * Copyright 2016 Adobe Systems Incorporated
    * All Rights Reserved.
    *
    * NOTICE:  All information contained herein is, and remains
    * the property of Adobe Systems Incorporated and its suppliers,
    * if any.  The intellectual and technical concepts contained
    * herein are proprietary to Adobe Systems Incorporated and its
    * suppliers and may be covered by U.S. and Foreign Patents,
    * patents in process, and are protected by trade secret or copyright law.
    * Dissemination of this information or reproduction of this material
    * is strictly forbidden unless prior written permission is obtained
    * from Adobe Systems Incorporated.
    *
    */
   (function () {
       var connectWithGuideBridge = function (gb) {
           gb.connect(function () {
               //For first time load
               window.guideBridge.on("elementValueChanged" , function(event, payload) {
           var component = payload.target; // Field whose value has changed
                   if(component.name == 'fileAttachment' && component.parent) {
                       var fileItems = $('#'+payload.target.parent.id).find(".guide-fu-fileItem");
                       for (i = 0;i<fileItems.length;i++) {
                           var filename = $(fileItems[i]).find(".guide-fu-fileName").text();
                           //check whether it is previously attached file or a newly  attached one
                           if(filename.length > 150 && filename.indexOf("fp.attach.jsp") < 0) {
                               window.alert("filename is larger than 150 : "+filename);
                                $(fileItems[i]).find(".guide-fu-fileClose.close").click();
                           }
                       }
                   }
   
      });
           });
       };
   
       if (window.guideBridge) {
           connectWithGuideBridge(window.guideBridge);
       } else {
           window.addEventListener("bridgeInitializeStart", function (event) {
               connectWithGuideBridge(event.detail.guideBridge);
           });
       }
   })();
   ```

   >[!NOTE]
   >
   >此脚本适用于开箱即用(OOTB)附件小组件。 如果您已自定义OOTB附件小组件，请更改上述脚本以合并相应更改。

1. 将以下属性添加到步骤2中创建的文件夹中，然后单击&#x200B;**[!UICONTROL Save All]**。

   * **[!UICONTROL 名称：]** 类别

   * **[!UICONTROL 类型：]** 字符串

   * **[!UICONTROL 值：]** fp.validation

   * **[!UICONTROL 多选项：]** 已启用

1. 导航到`/libs/fd/af/runtime/clientlibs/guideRuntime`，并将`fp.validation`值附加到embed属性。

1. 导航到/libs/fd/af/runtime/clientlibs/guideRuntimeWithXFA并将`fp.validation`值附加到embed属性。

   >[!NOTE]
   >
   >如果您使用的是自定义客户端库，而不是guideRuntime和guideRuntimeWithXfa客户端库，请使用类别名称将此过程中创建的客户端库嵌入到运行时加载的自定义库中。

1. 单击&#x200B;**[!UICONTROL 全部保存。]** 现在，当文件名大于150（包括扩展名）字符时，会显示消息。
