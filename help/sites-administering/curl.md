---
title: 在AEM中使用cURL
seo-title: Using cURL with AEM
description: 了解如何将cURL用于常见的Adobe Experience Manager任务。
seo-description: Learn how to use cURL with AEM.
uuid: 771b9acc-ff3a-41c9-9fee-7e5d2183f311
contentOwner: Silviu Raiman
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: d4ceb82e-2889-4507-af22-b051af83be38
exl-id: e3f018e6-563e-456f-99d5-d232f1a4aa55
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '883'
ht-degree: 2%

---

# 在AEM中使用cURL{#using-curl-with-aem}

管理员通常需要自动执行或简化任何系统中的常见任务。 例如，在AEM中，管理用户、安装包和管理OSGi捆绑包是通常必须完成的任务。

由于构建AEM所基于的Sling框架具有RESTful特性，因此大多数任务可以通过URL调用来完成。 cURL可用于执行此类URL调用，可以是AEM管理员的有用工具。

## 什么是cURL {#what-is-curl}

cURL是用于执行URL操作的开源命令行工具。 它支持各种Internet协议，包括HTTP、HTTPS、FTP、FTPS、SCP、SFTP、TFTP、LDAP、DAP、DICT、TELNET、FILE、IMAP、POP3、SMTP和RTSP。

cURL是一个成熟且广泛使用的工具，最初于1997年发布，用于使用URL语法获取或发送数据。 名称cURL最初的意思是“查看URL”。

由于构建AEM所基于的Sling框架具有RESTful性质，因此大多数任务可以简化为URL调用，而该URL调用可以使用cURL执行。 [内容操作任务](/help/sites-administering/curl.md#common-content-manipulation-aem-curl-commands) 例如激活页面，以及启动工作流和 [运行任务](/help/sites-administering/curl.md#common-operational-aem-curl-commands) 例如包管理以及使用cURL管理用户等。 此外，您还可以 [创建您自己的cURL](/help/sites-administering/curl.md#building-a-curl-ready-aem-command) 命令用于AEM中的大多数任务。

>[!NOTE]
>
>通过cURL执行的任何AEM命令都必须像任何用户一样获得AEM授权。 使用cURL执行AEM命令时，会尊重所有ACL和访问权限。

## 正在下载cURL {#downloading-curl}

cURL是macOS和一些Linux调试程序的标准部分。 但是，它适用于大多数操作系统。 有关最新下载信息，请访问 [https://curl.haxx.se/download.html](https://curl.haxx.se/download.html).

cURL的源存储库也可以在GitHub上找到。

## 构建cURL就绪的AEM命令 {#building-a-curl-ready-aem-command}

cURL命令可以为AEM中的大多数操作构建，例如触发工作流、检查OSGi配置、触发JMX命令、创建复制代理等等。

要找到特定操作所需的确切命令，您需要在执行AEM命令时使用浏览器中的开发人员工具来捕获对服务器的POST调用。

以下步骤描述了如何使用Chrome浏览器中创建新页面作为示例来完成此操作。

1. 准备要在AEM中调用的操作。 在本例中，我们继续到 **创建页面** 向导，但尚未单击 **创建**.

   ![chlimage_1-66](assets/chlimage_1-66a.png)

1. 启动开发人员工具并选择 **网络** 选项卡。 单击 **保留日志** 选项。

   ![chlimage_1-67](assets/chlimage_1-67a.png)

1. 单击 **创建** 在 **创建页面** 向导以实际创建工作流。
1. 右键单击生成的POST操作并选择 **复制** -> **复制为cURL**.

   ![chlimage_1-68](assets/chlimage_1-68a.png)

1. 将cURL命令复制到文本编辑器并从命令中删除所有标头，这些标头以 `-H` （下图以蓝色突出显示）并添加适当的身份验证参数，例如 `-u <user>:<password>`.

   ![chlimage_1-69](assets/chlimage_1-69a.png)

1. 通过命令行执行cURL命令并查看响应。

   ![chlimage_1-70](assets/chlimage_1-70a.png)

## 常见操作AEM cURL命令 {#common-operational-aem-curl-commands}

以下是常见管理和操作任务的AEM cURL命令列表。

>[!NOTE]
>
>以下示例假定AEM运行于 `localhost` 在端口 `4502` 并使用用户 `admin` 包含密码 `admin`. 其他命令占位符设置在尖括号中。

### 包管理 {#package-management}

#### 列出所有已安装的包

```shell
curl -u <user>:<password> http://<host>:<port>/crx/packmgr/service.jsp?cmd=ls
```

#### 创建资源包 {#create-a-package}

```shell
curl -u <user>:<password> -X POST http://localhost:4502/crx/packmgr/service/.json/etc/packages/mycontent.zip?cmd=create -d packageName=<name> -d groupName=<name>
```

#### 预览包 {#preview-a-package}

```shell
curl -u <user>:<password> -X POST http://localhost:4502/crx/packmgr/service/.json/etc/packages/mycontent.zip?cmd=preview
```

#### 列出包内容 {#list-package-content}

```shell
curl -u <user>:<password> -X POST http://localhost:4502/crx/packmgr/service/console.html/etc/packages/mycontent.zip?cmd=contents
```

#### 生成包 {#build-a-package}

```shell
curl -X POST http://localhost:4502/crx/packmgr/service/.json/etc/packages/mycontent.zip?cmd=build
```

#### 重新包装包 {#rewrap-a-package}

```shell
curl -u <user>:<password> -X POST http://localhost:4502/crx/packmgr/service/.json/etc/packages/mycontent.zip?cmd=rewrap
```

#### 重命名包 {#rename-a-package}

```shell
curl -u <user>:<password> -X POST -Fname=<New Name> http://localhost:4502/etc/packages/<Group Name>/<Package Name>.zip/jcr:content/vlt:definition
```

#### 上传包 {#upload-a-package}

```shell
curl -u <user>:<password> -F cmd=upload -F force=true -F package=@test.zip http://localhost:4502/crx/packmgr/service/.json
```

#### 安装包 {#install-a-package}

```shell
curl -u <user>:<password> -F cmd=install http://localhost:4502/crx/packmgr/service/.json/etc/packages/my_packages/test.zip
```

#### 卸载包 {#uninstall-a-package}

```shell
curl -u <user>:<password> -F cmd=uninstall http://localhost:4502/crx/packmgr/service/.json/etc/packages/my_packages/test.zip
```

#### 删除包 {#delete-a-package}

```shell
curl -u <user>:<password> -F cmd=delete http://localhost:4502/crx/packmgr/service/.json/etc/packages/my_packages/test.zip
```

#### 下载包 {#download-a-package}

```shell
curl -u <user>:<password> http://localhost:4502/etc/packages/my_packages/test.zip
```

#### 复制包 {#replicate-a-package}

```shell
curl -u <user>:<password> -X POST http://localhost:4502/crx/packmgr/service/.json/etc/packages/my_packages/test.zip?cmd=replicate
```

### 用户管理 {#user-management}

#### 创建新用户 {#create-a-new-user}

```shell
curl -u <user>:<password> -FcreateUser= -FauthorizableId=hashim -Frep:password=hashim http://localhost:4502/libs/granite/security/post/authorizables
```

#### 创建新组 {#create-a-new-group}

```shell
curl -u <user>:<password> -FcreateGroup=group1 -FauthorizableId=testGroup1 http://localhost:4502/libs/granite/security/post/authorizables
```

#### 向现有用户添加属性 {#add-a-property-to-an-existing-user}

```shell
curl -u <user>:<password> -Fprofile/age=25 http://localhost:4502/home/users/h/hashim.rw.html
```

#### 使用配置文件创建用户 {#create-a-user-with-a-profile}

```shell
curl -u <user>:<password> -FcreateUser=testuser -FauthorizableId=hashimkhan -Frep:password=hashimkhan -Fprofile/gender=male http://localhost:4502/libs/granite/security/post/authorizables
```

#### 创建新用户作为组成员 {#create-a-new-user-as-a-member-of-a-group}

```shell
curl -u <user>:<password> -FcreateUser=testuser -FauthorizableId=testuser -Frep:password=abc123 -Fmembership=contributor http://localhost:4502/libs/granite/security/post/authorizables
```

#### 将用户添加到组 {#add-a-user-to-a-group}

```shell
curl -u <user>:<password> -FaddMembers=testuser1 http://localhost:4502/home/groups/t/testGroup.rw.html
```

#### 从组中删除用户 {#remove-a-user-from-a-group}

```shell
curl -u <user>:<password> -FremoveMembers=testuser1 http://localhost:4502/home/groups/t/testGroup.rw.html
```

#### 设置用户的组成员资格 {#set-a-user-s-group-membership}

```shell
curl -u <user>:<password> -Fmembership=contributor -Fmembership=testgroup http://localhost:4502/home/users/t/testuser.rw.html
```

#### 删除用户 {#delete-a-user}

```shell
curl -u <user>:<password> -FdeleteAuthorizable= http://localhost:4502/home/users/t/testuser
```

#### 删除组 {#delete-a-group}

```shell
curl -u <user>:<password> -FdeleteAuthorizable= http://localhost:4502/home/groups/t/testGroup
```

### 备份 {#backup}

请参阅 [备份和恢复](/help/sites-administering/backup-and-restore.md#automating-aem-online-backup) 以了解详细信息。

### osgi {#osgi}

#### 启动捆绑包 {#starting-a-bundle}

```shell
curl -u <user>:<password> -Faction=start http://localhost:4502/system/console/bundles/<bundle-name>
```

#### 停止捆绑包 {#stopping-a-bundle}

```shell
curl -u <user>:<password> -Faction=stop http://localhost:4502/system/console/bundles/<bundle-name>
```

### Dispatcher {#dispatcher}

#### 使缓存失效 {#invalidate-the-cache}

```shell
curl -H "CQ-Action: Activate" -H "CQ-Handle: /content/test-site/" -H "CQ-Path: /content/test-site/" -H "Content-Length: 0" -H "Content-Type: application/octet-stream" http://localhost:4502/dispatcher/invalidate.cache
```

#### 逐出缓存 {#evict-the-cache}

```shell
curl -H "CQ-Action: Deactivate" -H "CQ-Handle: /content/test-site/" -H "CQ-Path: /content/test-site/" -H "Content-Length: 0" -H "Content-Type: application/octet-stream" http://localhost:4502/dispatcher/invalidate.cache
```

### 复制代理 {#replication-agent}

#### 检查代理的状态 {#check-the-status-of-an-agent}

```shell
curl -u <user>:<password> "http://localhost:4502/etc/replication/agents.author/publish/jcr:content.queue.json?agent=publish"
http://localhost:4502/etc/replication/agents.author/publish/jcr:content.queue.json?agent=publish
```

#### 删除代理 {#delete-an-agent}

```shell
curl -X DELETE http://localhost:4502/etc/replication/agents.author/replication99 -u <user>:<password>
```

#### 创建代理 {#create-an-agent}

```shell
curl -u <user>:<password> -F "jcr:primaryType=cq:Page" -F "jcr:content/jcr:title=new-replication" -F "jcr:content/sling:resourceType=/libs/cq/replication/components/agent" -F "jcr:content/template=/libs/cq/replication/templates/agent" -F "jcr:content/transportUri=http://localhost:4503/bin/receive?sling:authRequestLogin=1" -F "jcr:content/transportUser=admin" -F "jcr:content/transportPassword={DES}8aadb625ced91ac483390ebc10640cdf"http://localhost:4502/etc/replication/agents.author/replication99
```

#### 暂停代理 {#pause-an-agent}

```shell
curl -u <user>:<password> -F "cmd=pause" -F "name=publish"  http://localhost:4502/etc/replication/agents.author/publish/jcr:content.queue.json
```

#### 清除代理队列 {#clear-an-agent-queue}

```shell
curl -u <user>:<password> -F "cmd=clear" -F "name=publish"  http://localhost:4502/etc/replication/agents.author/publish/jcr:content.queue.json
```

### 社区 {#communities}

#### 分配和撤销徽章 {#assign-and-revoke-badges}

请参阅 [社区评分和徽章](/help/communities/implementing-scoring.md#assign-and-revoke-badges) 以了解详细信息。

请参阅 [评分和徽章要点](/help/communities/configure-scoring.md#example-setup) 以了解详细信息。

#### MSRP重新索引 {#msrp-reindexing}

请参阅 [MSRP - MongoDB存储资源提供程序](/help/communities/msrp.md#running-msrp-reindex-tool-using-curl-command) 以了解详细信息。

### 安全性 {#security}

#### 启用和禁用CRX DE Lite {#enabling-and-disabling-crx-de-lite}

请参阅 [在AEM中启用CRXDE Lite](/help/sites-administering/enabling-crxde-lite.md) 以了解详细信息。

### 数据存储垃圾收集 {#data-store-garbage-collection}

请参阅 [数据存储垃圾收集](/help/sites-administering/data-store-garbage-collection.md#automating-data-store-garbage-collection) 以了解详细信息。

### Analytics与Target集成 {#analytics-and-target-integration}

请参阅 [选择使用Adobe Analytics和Adobe Target](/help/sites-administering/opt-in.md#configuring-the-setup-and-provisioning-via-script) 以了解详细信息。

### 单点登录 {#single-sign-on}

#### 发送测试标头 {#send-test-header}

请参阅 [单点登录](/help/sites-deploying/single-sign-on.md) 以了解详细信息。

## 常见内容操作AEM cURL命令 {#common-content-manipulation-aem-curl-commands}

以下是用于内容操作的AEM cURL命令列表。

>[!NOTE]
>
>以下示例假定AEM运行于 `localhost` 在端口 `4502` 并使用用户 `admin` 包含密码 `admin`. 其他命令占位符设置在尖括号中。

### 页面管理 {#page-management}

#### 页面激活 {#page-activation}

```shell
curl -u <user>:<password> -X POST -F path="/content/path/to/page" -F cmd="activate" http://localhost:4502/bin/replicate.json
```

#### 页面停用 {#page-deactivation}

```shell
curl -u <user>:<password> -X POST -F path="/content/path/to/page" -F cmd="deactivate" http://localhost:4502/bin/replicate.json
```

#### 树激活 {#tree-activation}

```shell
curl -u <user>:<password> -F cmd=activate -F ignoredeactivated=true -F onlymodified=true -F path=/content/geometrixx http://localhost:4502/etc/replication/treeactivation.html
```

#### 锁定页面 {#lock-page}

```shell
curl -u <user>:<password> -X POST -F cmd="lockPage" -F path="/content/path/to/page" -F "_charset_"="utf-8" http://localhost:4502/bin/wcmcommand
```

#### 解锁页面 {#unlock-page}

```shell
curl -u <user>:<password> -X POST -F cmd="unlockPage" -F path="/content/path/to/page" -F "_charset_"="utf-8" http://localhost:4502/bin/wcmcommand
```

#### 复制页面 {#copy-page}

```shell
curl -u <user>:<password> -F cmd=copyPage -F destParentPath=/path/to/destination/parent -F srcPath=/path/to/source/location http://localhost:4502/bin/wcmcommand
```

### 工作流 {#workflows}

请参阅 [以编程方式与工作流交互](/help/sites-developing/workflows-program-interaction.md) 以了解详细信息。

### Sling内容 {#sling-content}

#### 创建文件夹 {#create-a-folder}

```shell
curl -u <user>:<password> -F jcr:primaryType=sling:Folder http://localhost:4502/etc/test
```

#### 删除节点 {#delete-a-node}

```shell
curl -u <user>:<password> -F :operation=delete http://localhost:4502/etc/test/test.properties
```

#### 移动节点 {#move-a-node}

```shell
curl -u <user>:<password> -F":operation=move" -F":applyTo=/sourceurl"  -F":dest=/target/parenturl/" https://localhost:4502/content
```

#### 复制节点 {#copy-a-node}

```shell
curl -u <user>:<password> -F":operation=copy" -F":applyTo=/sourceurl"  -F":dest=/target/parenturl/" https://localhost:4502/content
```

#### 使用Sling PostServlet上载文件 {#upload-files-using-sling-postservlet}

```shell
curl -u <user>:<password> -F"*=@test.properties"  http://localhost:4502/etc/test
```

#### 使用Sling PostServlet并指定节点名称上载文件 {#upload-files-using-sling-postservlet-and-specifying-node-name}

```shell
curl -u <user>:<password> -F"test2.properties=@test.properties"  http://localhost:4502/etc/test
```

#### 上载指定内容类型的文件 {#upload-files-specifying-a-content-type}

```shell
curl -u <user>:<password> -F "*=@test.properties;type=text/plain" http://localhost:4502/etc/test
```

### 资产操作 {#asset-manipulation}

请参阅 [资源HTTP API](/help/assets/mac-api-assets.md) 以了解详细信息。
