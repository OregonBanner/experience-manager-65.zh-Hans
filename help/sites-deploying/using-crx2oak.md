---
title: 使用CRX2Oak迁移工具
seo-title: Using the CRX2Oak Migration Tool
description: 了解如何使用CRX2Oak迁移工具。
seo-description: Learn how to use the CRX2Oak migration tool.
uuid: 9b788981-4ef0-446e-81f0-c327cdd3214b
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
discoiquuid: e938bdc7-f8f5-4da5-81f6-7f60c6b4b8e6
feature: Upgrading
exl-id: ef3895b9-8d35-4881-8188-c864ae3f0b4c
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '1246'
ht-degree: 0%

---

# 使用CRX2Oak迁移工具{#using-the-crx-oak-migration-tool}

## 简介 {#introduction}

CRX2Oak是一种用于在不同存储库之间迁移数据的工具。

它可用于将数据从基于Apache Jackrabbit 2的较旧CQ版本迁移到Oak，它也可用于在Oak存储库之间复制数据。

您可以从公共Adobe存储库下载最新版本的crx2oak，位置如下：
[https://repo1.maven.org/maven2/com/adobe/granite/crx2oak/](https://repo1.maven.org/maven2/com/adobe/granite/crx2oak/)

最新版本的更改和修复列表可在 [CRX2Oak发行说明](https://experienceleague.adobe.com/docs/experience-manager-64/release-notes/crx2oak.html).

>[!NOTE]
>
>有关Apache Oak以及AEM持久性的关键概念的更多信息，请参阅 [AEM平台简介](/help/sites-deploying/platform.md).

## 迁移用例 {#migration-use-cases}

该工具可用于：

* 从旧版CQ 5迁移到AEM 6
* 在多个Oak存储库之间复制数据
* 在不同的Oak MicroKernel实施之间转换数据。

通过不同的组合支持使用外部Blob存储（通常称为数据存储）迁移存储库。 一个可能的迁移路径来自使用外部的CRX2存储库 `FileDataStore` 到Oak存储库 `S3DataStore`.

下图说明了CRX2Oak支持的所有可能的迁移组合：

![chlimage_1-151](assets/chlimage_1-151.png)

## 功能 {#features}

CRX2Oak在AEM升级期间以用户可指定预定义迁移配置文件的方式调用，该配置文件可自动重新配置持久性模式。 这称为快速启动模式。

如果需要进行更多自定义，也可以单独运行该函数。 但是，请注意，在此模式下，仅对存储库进行更改，并且需要手动执行任何额外的AEM重新配置。 这称为独立模式。

另外需要注意的是，在独立模式下使用默认设置时，将只迁移节点存储，而新存储库将重复使用旧的二进制存储。

### 自动快速启动模式 {#automated-quickstart-mode}

自AEM 6.3起，CRX2Oak能够处理用户定义的迁移配置文件，这些配置文件可使用所有可用的迁移选项进行配置。 这样既提高了灵活性，又能够自动配置AEM，在独立模式下使用该工具时，这些功能将不可用。

为了将CRX2Oak切换到快速启动模式，您需要通过此操作系统环境变量在AEM安装目录中定义crx-quickstart文件夹的路径：

**对于基于UNIX的系统和macOS：**

```shell
export SLING_HOME="/path/to/crx-quickstart"
```

**对于Windows：**

```shell
SET "SLING_HOME=/path/to/crx-quickstart"
```

#### 恢复支持 {#resume-support}

迁移可随时中断，之后可继续进行。

#### 可定制的升级逻辑 {#customizable-upgrade-logic}

自定义Java逻辑，也可以使用实施 `CommitHooks`. 自定义 `RepositoryInitializer` 可以实施类以使用自定义值初始化存储库。

#### 支持内存映射操作 {#support-for-memory-mapped-operations}

默认情况下，CRX2Oak还支持内存映射操作。 内存映射可大大提高性能，应尽可能使用。

>[!CAUTION]
>
>但请注意，Windows平台不支持内存映射操作。 因此，建议添加 **—disable-mmap** 在Windows上执行迁移时的参数。

#### 选择性迁移内容 {#selective-migration-of-content}

默认情况下，该工具会将整个存储库迁移到 `"/"` 路径。 但是，您可以完全控制应该迁移哪些内容。

如果新实例上有不需要的内容的任何部分，您可以使用 `--exclude-path` 用于排除内容并优化升级过程的参数。

#### 路径合并 {#path-merging}

如果需要在两个存储库之间复制数据，并且两个实例中的内容路径不同，则可以在以下位置定义该数据 `--merge-path` 参数。 执行此操作后，CRX2Oak将仅将新节点复制到目标存储库中，并将保留旧节点。

![chlimage_1-152](assets/chlimage_1-152.png)

#### 版本支持 {#version-support}

默认情况下，AEM会为每个要修改的节点或页面创建一个版本，并将其存储在存储库中。 然后，可以使用这些版本将页面还原到以前的状态。

但是，即使删除了原始页面，也不会清除这些版本。 在处理已运行多年的存储库时，迁移可能需要处理大量由孤立版本导致的冗余数据。

对于这些类型的情况，一个有用的功能是添加 `--copy-versions` 参数。 它可用于在迁移或复制存储库期间跳过版本节点。

您还可以通过添加以下内容来选择是否复制孤立版本 `--copy-orphaned-versions=true`.

这两个参数还支持 `YYYY-MM-DD` 日期格式（如果您希望在不晚于特定日期的情况下复制版本）。

![chlimage_1-153](assets/chlimage_1-153.png)

#### 开源版本 {#open-source-version}

CRX2Oak的开源版本以oak-upgrade的形式提供。 它支持所有功能，但以下功能除外：

* CRX2支持
* 迁移配置文件支持
* 支持自动AEM重新配置

请参阅 [Apache文档](https://jackrabbit.apache.org/oak/docs/migration.html) 了解更多信息。

## 参数 {#parameters}

### 节点存储选项 {#node-store-options}

* `--cache`：缓存大小(以MB为单位，默认值为 `256`)

* `--mmap`：为区段存储启用内存映射文件访问
* `--src-password:` 源RDB数据库的口令

* `--src-user:` 源RDB的用户

* `--user`：目标RDB的用户

* `--password`：目标RDB的密码。

### 迁移选项 {#migration-options}

* `--early-shutdown`：在复制节点之后和应用提交挂接之前关闭源JCR2存储库
* `--fail-on-error`：如果无法从源存储库中读取节点，则强制迁移失败。
* `--ldap`：将LDAP用户从CQ 5.x实例迁移到基于Oak的实例。 要使此功能正常工作，需要将Oak配置中的身份提供程序命名为ldap。 欲了解更多信息，请参见 [LDAP文档](/help/sites-administering/ldap-config.md).

* `--ldap-config:` 将此函数与 `--ldap` 使用多个LDAP服务器进行身份验证的CQ 5.x存储库的参数。 您可以使用它指向CQ 5.x `ldap_login.conf` 或 `jaas.conf` 配置文件。 格式为 `--ldapconfig=path/to/ldap_login.conf`.

### 版本存储选项 {#version-store-options}

* `--copy-orphaned-versions`：跳过复制孤立版本。 支持的参数包括： `true`， `false` 和 `yyyy-mm-dd`. 默认为 `true`.

* `--copy-versions:` 复制版本存储。 参数： `true`， `false`， `yyyy-mm-dd`. 默认为 `true`.

#### 路径选项 {#path-options}

* `--include-paths:` 复制期间要包含的以逗号分隔的路径列表
* `--merge-paths`：复制期间要合并的以逗号分隔的路径列表
* `--exclude-paths:` 复制期间要排除的以逗号分隔的路径列表。

### 源Blob存储选项 {#source-blob-store-options}

* `--src-datastore:` 用作源的数据存储目录 `FileDataStore`

* `--src-fileblobstore`：用作源的数据存储目录 `FileBlobStore`

* `--src-s3datastore`：用于源的数据存储目录 `S3DataStore`

* `--src-s3config`：源的配置文件 `S3DataStore`.

### 目标BlobStore选项 {#destination-blobstore-options}

* `--datastore:` 用作目标的数据存储目录 `FileDataStore`

* `--fileblobstore:` 用作目标的数据存储目录 `FileBlobStore`

* `--s3datastore`：用于目标的数据存储目录 `S3DataStore`

* `--s3config`：目标的配置文件 `S3DataStore`.

### 帮助选项 {#help-options}

* `-?, -h, --help:` 显示帮助信息。

## 调试 {#debugging}

您还可以为迁移过程启用调试信息，以便对迁移过程中可能出现的任何问题进行故障诊断。 根据您希望在其中运行工具的模式，您可以采用不同的方式执行此操作：

<table>
 <tbody>
  <tr>
   <td><strong>CRX2Oak模式</strong></td>
   <td><strong>操作</strong></td>
  </tr>
  <tr>
   <td>快速入门模式</td>
   <td>您可以添加 <strong> — 日志级别TRACE</strong> 或 <strong> — 日志级别调试 </strong>运行CRX2Oak时命令行选项。 在此模式下，日志会自动重定向到 <strong>upgrade.log文件</strong>.</td>
  </tr>
  <tr>
   <td>独立模式</td>
   <td><p>添加 <strong>—trace</strong> CRX2Oak命令行的选项，以在标准输出中显示TRACE事件（您需要使用重定向字符“&gt;”或“T”命令自行重定向日志，以供以后检查）。</p> </td>
  </tr>
 </tbody>
</table>

## 其他注意事项 {#other-considerations}

迁移到MongoDB复制副本集时，请确保设置 `WriteConcern` 参数至 `2` 所有与Mongo数据库的连接。

为此，您可以添加 `w=2` 连接字符串末尾的参数，如下所示：

```xml
java -Xmx4092m -jar crx2oak.jar crx-quickstart/repository/ mongodb://localhost:27017/aem-author?replicaset=replica1&w=2
```

>[!NOTE]
>
>有关详细信息，请参见MongoDB连接字符串文档，该文档位于 [编写关注点](https://docs.mongodb.org/manual/reference/connection-string/#write-concern-options).
