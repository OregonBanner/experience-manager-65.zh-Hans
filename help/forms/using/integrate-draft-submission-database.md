---
title: 将草稿和提交组件与数据库集成的示例
seo-title: 将草稿和提交组件与数据库集成的示例
description: 参考定制数据和元数据服务的实施，将草稿和提交组件与数据库集成。
seo-description: 参考定制数据和元数据服务的实施，将草稿和提交组件与数据库集成。
uuid: ccdb900e-2c2e-4ed3-8a88-5c97aa0092a1
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: da96d3d8-a338-470a-8d20-55ea39bd15bf
translation-type: tm+mt
source-git-commit: 2cf9dcf2e9cf71c54e19e2c6ee825c9a8f00a9b7

---


# 将草稿和提交组件与数据库集成的示例 {#sample-for-integrating-drafts-submissions-component-with-database}

## 示例概述 {#sample-overview}

AEM Forms门户草稿和提交组件允许用户将其表单另存为草稿，并稍后从任何设备提交。 此外，用户还可以在门户上视图其提交的表单。 要启用此功能，AEM Forms提供数据和元数据服务，以存储用户在表单中填写的数据以及与草稿和已提交表单关联的表单元数据。 默认情况下，此数据存储在CRX存储库中。 但是，当用户通过AEM发布实例与表单交互时（通常在企业防火墙之外），组织可能希望自定义数据存储，以使其更安全、更可靠。

本文档讨论的示例是自定义数据和元数据服务的参考实现，用于将草稿和提交组件与数据库集成在一起。 示例实现中使用的数据库 **是MySQL 5.6.24**。 但是，您可以将草稿和提交组件与您选择的任何数据库集成。

>[!NOTE]
>
>* 本文档中介绍的示例和配置符合MySQL 5.6.24的要求，您必须将它们相应地替换为数据库系统。
>* 确保您已安装最新版AEM Forms加载项包。 有关可用包的列表，请参阅 [AEM Forms发布文章](https://helpx.adobe.com/cn/aem-forms/kb/aem-forms-releases.html) 。
>



## 设置和配置示例 {#set-up-and-configure-the-sample}

对所有作者实例和发布实例执行以下步骤以安装和配置示例：

1. 将以下 **** aem-fp-db-integration-sample-pkg-6.1.2.zip包下载到文件系统。

   数据库集成的示例包

   [获取文件](assets/aem-fp-db-integration-sample-pkg-6.1.2.zip)

1. 转到位于https://[*host*]:[*port*]/crx/packmgr/的AEM包管理器。
1. 单击“ **[!UICONTROL 上传包”]**。

1. 浏览以选择 **aem-fp-db-integration-sample-pkg-6.1.2.zip包，然后单击“确** 定” ****。
1. 单击 **[!UICONTROL 包旁的]** “安装”以安装该包。
1. 转到 **[!UICONTROL AEM Web Console Configuration]**([*AEM Web Console*]&#x200B;配置)页&#x200B;[*面，网址为：https://host*]:port/system/console/configMgr。
1. 单击以在编辑 **[!UICONTROL 模式下打开Forms Portal草稿和提交配置]** 。

1. 如下表所述，指定属性的值：

   | **属性** | **描述** | **值** |
   |---|---|---|
   | Forms Portal Draft Data Service | 草稿数据服务的标识符 | formsportal.sampledataservice |
   | Forms Portal Draft Metadata Service | 草稿元数据服务的标识符 | formsportal.samplemetadataservice |
   | Forms Portal提交数据服务 | 提交数据服务的标识符 | formsportal.sampledataservice |
   | Forms Portal提交元数据服务 | 提交元数据服务的标识符 | formsportal.samplemetadataservice |
   | Forms Portal Pending Sign Data Service | 待定签名数据服务的标识符 | formsportal.sampledataservice |
   | Forms Portal待签名元数据服务 | 待定签名元数据服务的标识符 | formsportal.samplemetadataservice |

   >[!NOTE]
   >
   >服务通过其名称解析，这些名称作为键 `aem.formsportal.impl.prop` 的值如下：

   ```java
   @Service(value = {SubmitDataService.class, DraftDataService.class})
   @Property(name = "aem.formsportal.impl.prop", value = "formsportal.sampledataservice")
   @Service(value = { SubmitMetadataService.class, DraftMetadataService.class })
   @Property(name = "aem.formsportal.impl.prop", value = "formsportal.samplemetadataservice")
   ```

   您可以更改数据表和元数据表的名称。

   要为元数据表提供其他名称，请执行以下操作：

   * 在“Web控制台配置”中，查找并单击“表单门户元数据服务示例实施”。 您可以更改数据源、元数据／其他元数据表名称的值。
   要为数据表提供其他名称：

   * 在“Web控制台配置”中，查找并单击“Forms Portal Data Service示例实施”。 您可以更改数据源和数据表名称的值。
   >[!NOTE]
   >
   >如果更改表名，请在表单门户配置中提供这些名称。

1. 保留其他配置，然后单击“保 **[!UICONTROL 存”]**。

1. 可通过Apache Sling Connection Pooled Data Source进行数据库连接。
1. 对于Apache Sling连接，在Web控制台配置中查找并单击以在编辑模式下打开 **** Apache Sling Connection池化数据源。 如下表所述，指定属性的值：

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>值</strong></td>
  </tr>
  <tr>
   <td>数据源名称</td>
   <td><p>用于从数据源池过滤驱动程序的数据源名称</p> <p><strong>注意：示 </strong><em>例实现使用FormsPortal作为数据源名称。</em></p> </td>
  </tr>
  <tr>
   <td>JDBC驱动程序类</td>
   <td>com.mysql.jdbc.Driver</td>
  </tr>
  <tr>
   <td>JDBC连接URI<br /> </td>
   <td>jdbc:mysql://[<em>host</em>]:[<em>port</em>]/[<em>模式名称</em>]</td>
  </tr>
  <tr>
   <td>用户名</td>
   <td>对数据库表进行身份验证和执行操作的用户名</td>
  </tr>
  <tr>
   <td>密码</td>
   <td>与用户名关联的口令</td>
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
   <td>最小空闲连接数</td>
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
   <td>借阅测试</td>
   <td>已选中</td>
  </tr>
  <tr>
   <td>空闲时测试</td>
   <td>已选中</td>
  </tr>
  <tr>
   <td>验证查询</td>
   <td>示例值为SELECT 1(mysql)、从dual(oracle)中选择1、SELECT 1(MS Sql Server)(validationQuery)</td>
  </tr>
  <tr>
   <td>验证查询超时</td>
   <td>10000</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
> * MySQL的JDBC驱动程序不随示例提供。 确保已为其配置，并提供配置JDBC连接池所需的信息。
> * 将您的作者实例和发布实例指向使用同一数据库。 对于所有作者实例和发布实例，JDBC连接URI字段的值必须相同。
>



1. 保留其他配置，然后单击“保 **[!UICONTROL 存”]**。

1. 如果数据库模式中已有表，请跳到下一步。

   否则，如果数据库模式中还没有表，请执行以下SQL语句，为数据库模式中的数据、元数据和其他元数据创建单独的表：

   >[!NOTE]
   >
   >创作和发布实例不需要不同的数据库。 在所有创作和发布实例上使用相同的数据库。

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

   **SQL语句用于其他元数据表**

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

1. 如果数据库模式中已有表（数据、元数据和其他元数据表），请执行以下更改表查询:

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
   >如果您已经运行ALTER TABLE元数据添加查询，并且表中存在markedforDeletion列，则该元数据添加操作将失败。

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

现在配置了示例实施，您可以使用它列表草稿和提交，同时将所有数据和元数据存储在数据库中。 现在，我们来看一下示例中如何配置数据和元数据服务。

## 安装mysql-connector-java-5.1.39-bin.jar文件 {#install-mysql-connector-java-bin-jar-file}

对所有作者实例和发布实例执行以下步骤以安装mysql-connector-java-5.1.39-bin.jar文件：

1. 导航到 `https://'[server]:[port]'/system/console/depfinder` com.mysql.jdbc包并搜索。
1. 在“导出依据”列中，检查包是否由任何包导出。

   如果包未由任何包导出，请继续。

1. 导航到并 `https://'[server]:[port]'/system/console/bundles` 单击“ **[!UICONTROL 安装／更新”]**。
1. 单 **[!UICONTROL 击“选择文件]** ”并浏览以选择mysql-connector-java-5.1.39-bin.jar文件。 此外，选中“ **[!UICONTROL 开始包]** ”和“ **[!UICONTROL 刷新包]** ”复选框。
1. 单击“ **[!UICONTROL 安装”或“更新]**”。 完成后，重新启动服务器。
1. (仅&#x200B;*限Windows*)关闭操作系统的系统防火墙。

## 表单门户数据和元数据服务的示例代码 {#sample-code-for-forms-portal-data-and-metadata-service}

以下zip包含数 `FormsPortalSampleDataServiceImpl` 据和元 `FormsPortalSampleMetadataServiceImpl` 数据服务接口的和（实现类）。 此外，它还包含编译上述实现类所需的所有类。

[获取文件](assets/sample_package.zip)

## 验证文件名的长度 {#verify-length-of-the-file-name}

Forms Portal的数据库实现使用其他元数据表。 该表具有基于表的键列和id列的复合主键。 MySQL允许最长255个字符的主键。 您可以使用以下客户端验证脚本验证附加到文件构件的文件名的长度。 附加文件时将运行验证。 当文件名大于150（包括扩展名）时，下面过程中提供的脚本会显示一条消息。 您可以修改脚本以检查其中是否有不同数量的字符。

执行以下步骤以创建客 [户端库](/help/sites-developing/clientlibs.md) ，并使用脚本：

1. 登录到CRXDE并导航到/etc/clientlibs/
1. 创建cq:ClientLibraryFolder类 **型的节点** ，并提供该节点的名称。 For example, `validation`.

   单击“ **[!UICONTROL 全部保存]**”。

1. 右键单击节点，单击 **[!UICONTROL 创建新文件]**，然后创建扩展名为。txt的文件。 例如，将以 `js.txt`下代码添加到新创建的。txt文件，然后单击“全 **[!UICONTROL 部保存”]**。

   ```
   #base=util
    util.js
   ```

   在上述代码中， `util` 是文件夹的名称和文 `util.js` 件夹中的文件名 `util` 称。 文件 `util` 夹和文 `util.js` 件是按照以下步骤创建的。

1. 右键单击在步骤2 `cq:ClientLibraryFolder` 中创建的节点，选择创建>创建文件夹。 创建名为的文件夹 `util`。 单击“ **[!UICONTROL 全部保存]**”。 右键单击文件夹， `util` 选择创建>创建文件。 创建名为的文件 `util.js`。 单击“ **[!UICONTROL 全部保存]**”。

1. 将以下代码添加到util.js文件，然后单击“ **[!UICONTROL 全部保存”]**。 代码验证文件名的长度。

   ```
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
   >此脚本适用于开箱即用(OOTB)附件构件组件。 如果您已自定义OOTB附件构件，则更改上述脚本以合并相应的更改。

1. 将以下属性添加到在步骤2中创建的文件夹，然后单击“全 **[!UICONTROL 部保存”]**。

   * **[!UICONTROL 名称：]** 类别

   * **[!UICONTROL 类型：]** 字符串

   * **[!UICONTROL 值：]** fp.validation

   * **[!UICONTROL 多选项：]** 已启用

1. 导航到 `/libs/fd/af/runtime/clientlibs/guideRuntime`embed属性并 `fp.validation` 将值附加到该属性。

1. 导航到/libs/fd/af/runtime/clientlibs/guideRuntimeWithXFA并将值附 `fp.validation` 加到embed属性。

   >[!NOTE]
   >
   >如果您使用的是自定义客户端库，而不是guideRuntime和guideRuntimeWithXfa客户端库，请使用类别名将在此过程中创建的客户端库嵌入到运行时加载的自定义库中。

1. 单击“ **[!UICONTROL 全部保存”。]** 现在，当文件名大于150（包括扩展名）字符时，将显示一条消息。

