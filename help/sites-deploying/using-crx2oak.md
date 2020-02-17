---
title: 使用CRX2Oak迁移工具
seo-title: 使用CRX2Oak迁移工具
description: 了解如何使用CRX2Oak迁移工具。
seo-description: 了解如何使用CRX2Oak迁移工具。
uuid: 9b788981-4ef0-446e-81f0-c327cdd3214b
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
discoiquuid: e938bdc7-f8f5-4da5-81f6-7f60c6b4b8e6
translation-type: tm+mt
source-git-commit: 24290b65a126822eb918fbecc978372394b5b655

---


# 使用CRX2Oak迁移工具{#using-the-crx-oak-migration-tool}

## 简介 {#introduction}

CRX2Oak是一款旨在在不同存储库之间迁移数据的工具。

它可用于将基于Apache Jackrabbit 2的旧版CQ数据迁移到Oak，还可用于在Oak存储库之间复制数据。

您可以从公共Adobe存储库下载最新版crx2oak，位置为：[https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/crx2oak/](https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/crx2oak/)

有关最新版本的更改和修复的列表，请参阅 [CRX2Oak发行说明](https://docs.adobe.com/content/help/en/experience-manager-64/release-notes/crx2oak.html)。

>[!NOTE]
>
>有关Apache Oak和AEM永久性的主要概念的详细信息，请参 [阅AEM平台简介](/help/sites-deploying/platform.md)。

## 迁移用例 {#migration-use-cases}

该工具可用于：

* 从旧版CQ 5迁移到AEM 6
* 在多个Oak存储库之间复制数据
* 在不同Oak MicroKernel实现之间转换数据。

支持使用外部Blob存储库（通常称为数据存储库）迁移存储库，这些支持采用不同的组合形式。 一个可能的迁移路径是从使用外部的CRX2存储库到 `FileDataStore` Oak存储库(使用 `S3DataStore`)。

下图说明了CRX2Oak支持的所有可能的迁移组合：

![chlimage_1-151](assets/chlimage_1-151.png)

## 功能 {#features}

CRX2Oak在AEM升级期间被调用，用户可以通过这种方式指定预定义的迁移配置文件，该配置文件可以自动重新配置持久性模式。 这称为快速启动模式。

还可以单独运行它，以防需要更多自定义。 但是，请注意，在此模式下，仅对存储库进行更改，并且需要手动执行AEM的任何其他重新配置。 这称为独立模式。

另外，在独立模式下使用默认设置时，将只迁移节点存储，而新存储库将重新使用旧的二进制存储。

### 自动快速启动模式 {#automated-quickstart-mode}

自AEM 6.3起，CRX2Oak能够处理用户定义的迁移配置文件，这些配置文件可以配置所有已可用的迁移选项。 这样，您既可以获得更高的灵活性，又可以自动配置AEM，这些功能在独立模式下使用时不可用。

要将CRX2Oak切换为快速启动模式，您需要通过以下操作系统环境变量定义AEM安装目录中crx-quickstart文件夹的路径：

**对于基于UNIX的系统和macOS:**

```shell
export SLING_HOME="/path/to/crx-quickstart"
```

**对于Windows:**

```shell
SET "SLING_HOME=/path/to/crx-quickstart"
```

#### 恢复支持 {#resume-support}

该迁移可随时中断，并且随后可恢复。

#### 可自定义的升级逻辑 {#customizable-upgrade-logic}

自定义Java逻辑也可使用实现 `CommitHooks`。 可以 `RepositoryInitializer` 实现自定义类，以便用自定义值初始化存储库。

#### 支持内存映射操作 {#support-for-memory-mapped-operations}

默认情况下，CRX2Oak还支持内存映射操作。 内存映射可大幅提高性能，应尽可能使用。

>[!CAUTION]
>
>但是，Windows平台不支持内存映射操作。 因此，建议在Windows上执 **行迁移时添加—disable-mmap** 参数。

#### 内容的选择性迁移 {#selective-migration-of-content}

默认情况下，该工具将整个存储库迁移到路径 `"/"` 下。 但是，您可以完全控制应迁移的内容。

如果新实例中不需要内容的任何部分，您可以使用该参 `--exclude-path` 数排除内容并优化升级过程。

#### 路径合并 {#path-merging}

如果需要在两个存储库之间复制数据，并且您的内容路径在两个实例上都不同，则可以在参数中定义该 `--merge-path` 数据。 一旦您这样做，CRX2Oak将仅将新节点复制到目标存储库，并保留旧节点。

![chlimage_1-152](assets/chlimage_1-152.png)

#### 版本支持 {#version-support}

默认情况下，AEM将创建每个被修改的节点或页面的一个版本，并将其存储在存储库中。 然后，这些版本可用于将页面恢复到较早状态。

但是，即使删除了原始页面，也不会清除这些版本。 在处理长期运行的存储库时，迁移可能需要处理由孤立版本导致的大量冗余数据。

对于这些类型的情况，一个有用的特征是添加了该参 `--copy-versions` 数。 它可用于在迁移或复制存储库期间跳过版本节点。

您还可以通过添加来选择是否复制孤立版本 `--copy-orphaned-versions=true`。

这两个参数还支持 `YYYY-MM-DD` 日期格式，以防复制版本不迟于特定日期。

![chlimage_1-153](assets/chlimage_1-153.png)

#### 开放源代码版本 {#open-source-version}

CRX2Oak的开放源版本以oak-upgrade的形式提供。 它支持除以下功能之外的所有功能：

* CRX2支持
* 迁移配置文件支持
* 支持自动AEM重新配置

See the [Apache Documentation](https://jackrabbit.apache.org/oak/docs/migration.html) for more information.

## 参数 {#parameters}

### 节点存储选项 {#node-store-options}

* `--cache`:缓存大小（以MB为单位）(默认为 `256`)

* `--mmap`:为区段存储启用内存映射文件访问
* `--src-password:` 源RDB数据库的口令

* `--src-user:` 源RDB的用户

* `--user`:目标RDB的用户

* `--password`:目标RDB的口令。

### 迁移选项 {#migration-options}

* `--early-shutdown`:在复制节点后和应用提交钩子之前关闭源JCR2存储库
* `--fail-on-error`:如果无法从源存储库读取节点，则强制执行迁移失败。
* `--ldap`:将LDAP用户从CQ 5.x实例迁移到基于Oak的实例。 为了使其正常工作，需要将Oak配置中的标识提供者命名为ldap。 For more information, see the [LDAP documentation](/help/sites-administering/ldap-config.md).

* `--ldap-config:` 将其与使用多个LDAP服 `--ldap` 务器进行身份验证的CQ 5.x存储库的参数结合使用。 您可以使用它指向CQ 5.x或配 `ldap_login.conf` 置 `jaas.conf` 文件。 格式为 `--ldapconfig=path/to/ldap_login.conf`。

### 版本存储选项 {#version-store-options}

* `--copy-orphaned-versions`:跳过复制孤立版本。 支持的参数有： `true`和 `false``yyyy-mm-dd`。 默认为 `true`.

* `--copy-versions:` 复制版本存储。 Parameters: `true`, `false`, `yyyy-mm-dd`. 默认为 `true`.

#### 路径选项 {#path-options}

* `--include-paths:` 复制过程中要包含的路径列表，以逗号分隔
* `--merge-paths`:复制过程中要合并的路径列表，以逗号分隔
* `--exclude-paths:` 复制过程中要排除的路径列表，以逗号分隔。

### 源Blob存储选项 {#source-blob-store-options}

* `--src-datastore:` 要用作源的数据存储目录 `FileDataStore`

* `--src-fileblobstore`:要用作源的数据存储目录 `FileBlobStore`

* `--src-s3datastore`:要用于源的数据存储目录 `S3DataStore`

* `--src-s3config`:源的配置文件 `S3DataStore`。

### 目标BlobStore选项 {#destination-blobstore-options}

* `--datastore:` 要用作目标的数据存储目录 `FileDataStore`

* `--fileblobstore:` 要用作目标的数据存储目录 `FileBlobStore`

* `--s3datastore`:要用于目标的数据存储目录 `S3DataStore`

* `--s3config`:目标的配置文件 `S3DataStore`。

### 帮助选项 {#help-options}

* `-?, -h, --help:` 显示帮助信息。

## 调试 {#debugging}

您还可以为迁移过程启用调试信息，以便对可能在迁移过程中出现的任何问题进行疑难解答。 根据您希望在以下位置运行工具的模式，您可以以不同方式执行此操作：

<table>
 <tbody>
  <tr>
   <td><strong>CRX2Oak模式</strong></td>
   <td><strong>操作</strong></td>
  </tr>
  <tr>
   <td>快速启动模式</td>
   <td>运行CRX2Oak时，可 <strong>以向命令行添</strong> 加日志级TRACE或日志级 <strong></strong>DEBUG选项。 在此模式下，日志会自动重定向到 <strong>upgrade.log文件</strong>。</td>
  </tr>
  <tr>
   <td>独立模式</td>
   <td><p>向CRX2Oak命令行添加 <strong>—trace选项</strong> ，以在标准输出中显示TRACE事件(您需要使用重定向字符重定向日志：“&gt;”或“tee”命令，供以后检查)。</p> </td>
  </tr>
 </tbody>
</table>

## 其他注意事项 {#other-considerations}

迁移到MongoDB复制副本集时，请确保在与Mongo数据库的所 `WriteConcern` 有连接 `2` 上都将该参数设置为。

可以通过在连接字符串 `w=2` 的末尾添加参数来执行此操作，如下所示：

```xml
java -Xmx4092m -XX:MaxPermSize=1024m -jar crx2oak.jar crx-quickstart/repository/ mongodb://localhost:27017/aem-author?replicaset=replica1&w=2
```

>[!NOTE]
>
>有关详细信息，请参阅MongoDB Connection String文档中的“写 [问题”](https://docs.mongodb.org/manual/reference/connection-string/#write-concern-options)。

