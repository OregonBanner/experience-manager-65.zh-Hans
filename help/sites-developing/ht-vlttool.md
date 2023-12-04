---
title: 如何使用VLT工具
description: Jackrabbit FileVault工具(VLT)由Apache Foundation开发，用于将Jackrabbit/AEM实例的内容映射到您的文件系统
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
exl-id: efbba312-9fc8-4670-b8f1-d2a86162d075
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '2687'
ht-degree: 1%

---

# 如何使用VLT工具 {#how-to-use-the-vlt-tool}

Jackrabbit FileVault工具(VLT)是由 [Apache Foundation](https://www.apache.org/) 将Jackrabbit/AEM实例的内容映射到您的文件系统。 VLT工具具有类似源代码控制系统客户端(如Subversion (SVN)客户端)的功能，可提供正常的签入、签出和管理操作，以及灵活呈现项目内容的配置选项。

从命令行运行VLT工具。 本文档介绍了如何使用该工具，包括如何开始使用并获得帮助，以及所有内容的列表 [命令](#vlt-commands) 和可用 [options](#vlt-global-options).

## 概念和架构 {#concepts-and-architecture}

请参阅 [Filevault概述](https://jackrabbit.apache.org/filevault/overview.html) 和 [保险库FS](https://jackrabbit.apache.org/filevault/vaultfs.html) 来自官方网站的网页 [Apache Jackrabbit Filevault文档](https://jackrabbit.apache.org/filevault/index.html) 全面概述Filevault工具的概念和结构。

## VLT快速入门 {#getting-started-with-vlt}

要开始使用VLT，您需要执行以下操作：

1. 安装VLT、更新环境变量和更新全局忽略的subversion文件。
1. 设置AEM存储库（如果尚未设置）。
1. 查看AEM存储库。
1. 与存储库同步。
1. 测试同步是否有效。

### 安装VLT工具 {#installing-the-vlt-tool}

要使用VLT工具，首先需要安装它。 默认情况下，不会安装此工具，因为它是一个附加工具。 此外，您需要设置系统的环境变量。

1. 从以下位置下载FileVault存档文件 [Maven工件存储库。](https://repo1.maven.org/maven2/org/apache/jackrabbit/vault/vault-cli/)
   >[!NOTE]
   >
   >VLT工具的来源为 [在GitHub上可用。](https://github.com/apache/jackrabbit-filevault)
1. 提取存档。
1. 添加 `<archive-dir>/vault-cli-<version>/bin` 到您的环境 `PATH` 这样命令文件 `vlt` 或 `vlt.bat` 会根据需要进行访问。 例如：

   `<aem-installation-dir>/crx-quickstart/opt/helpers/vault-cli-3.1.16/bin>`

1. 打开命令行外壳程序并执行 `vlt --help`. 确保输出与以下帮助屏幕类似：

   ```shell
   vlt --help
   -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
   Jackrabbit FileVault [version 3.1.16] Copyright 2013 by Apache Software Foundation. See LICENSE.txt for more information.
   -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
   Usage:
     vlt [options] <command> [arg1 [arg2 [arg3] ..]]
   -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
   
   Global options:
   
     -Xjcrlog <arg>           Extended JcrLog options (omit argument for help)
     -Xdavex <arg>            Extended JCR remoting options (omit argument for help)
     --credentials <arg>      The default credentials to use
     --update-credentials     if present the credentials-to-host list is updated in the ~/.vault/auth.xml
     --config <arg>           The JcrFs config to use
     -v (--verbose)           verbose output
     -q (--quiet)             print as little as possible
     --version                print the version information and exit
     --log-level <level>      the log4j log level
     -h (--help) <command>    print this help
   ```

安装之后，您需要更新全局忽略的subversion文件。 编辑您的svn设置并添加以下内容：

```xml
[miscellany]
### Set global-ignores to a set of whitespace-delimited globs
### which Subversion will ignore in its 'status' output, and
### while importing or adding files and directories.
global-ignores = .vlt
```

### 配置行尾字符 {#configuring-the-end-of-line-character}

VLT根据以下规则自动处理行尾(EOF)：

* 在Windows上签出的文件行以 `CRLF`
* 在Linux/Unix上签出的文件行以 `LF`
* 提交到存储库的文件行以 `LF`

为确保VLT和SVN配置匹配，您应该设置 `svn:eol-style` 属性至 `native` 存储库中存储的文件的扩展名。 编辑您的svn设置并添加以下内容：

```xml
[auto-props]
*.css = svn:eol-style=native
*.cnd = svn:eol-style=native
*.java = svn:eol-style=native
*.js = svn:eol-style=native
*.json = svn:eol-style=native
*.xjson = svn:eol-style=native
*.jsp = svn:eol-style=native
*.txt = svn:eol-style=native
*.html = svn:eol-style=native
*.xml = svn:eol-style=native
*.properties = svn:eol-style=native
```

### 签出存储库 {#checking-out-the-repository}

使用源代码管理系统签出存储库。 例如，在svn中，键入以下内容（将URI和路径替换为存储库）：

```shell
svn co https://svn.server.com/repos/myproject
```

### 与存储库同步 {#synchronizing-with-the-repository}

您需要将filevault与存储库同步。 要执行此操作：

1. 在命令行中，导航到 `content/jcr_root`.
1. 键入以下内容(将您的端口号替换为 **4502** 和管理员密码)：

   ```shell
   vlt --credentials admin:admin co --force http://localhost:4502/crx
   ```

   >[!NOTE]
   >
   >凭据只需在初始签出时指定一次。 然后，它们将存储在中的主目录中 `.vault/auth.xml`.

### 测试同步是否有效 {#testing-whether-the-synchronization-worked}

签出存储库并进行同步后，应进行测试以确保所有功能均可正常运行。 一个简单的方法是编辑 **.jsp** 文件，并查看在提交更改后是否反映更改。

要测试同步，请执行以下操作：

1. 导航到 `.../jcr_content/libs/foundation/components/text`。
1. 在中编辑内容 `text.jsp`.
1. 通过键入查看修改的文件 `vlt st`
1. 通过键入查看更改 `vlt diff text.jsp`
1. 提交更改： `vlt ci test.jsp`.
1. 重新加载包含文本组件的页面，并查看更改是否存在。

## 使用VLT工具获取帮助 {#getting-help-with-the-vlt-tool}

安装VLT工具后，可以从命令行访问其帮助文件：

```shell
vlt --help
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Jackrabbit FileVault [version 3.1.16] Copyright 2013 by Apache Software Foundation. See LICENSE.txt for more information.
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Usage:
  vlt [options] <command> [arg1 [arg2 [arg3] ..]]
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Global options:
  -Xjcrlog <arg>           Extended JcrLog options (omit argument for help)
  -Xdavex <arg>            Extended JCR remoting options (omit argument for help)
  --credentials <arg>      The default credentials to use
  --update-credentials     if present the credentials-to-host list is updated in the ~/.vault/auth.xml
  --config <arg>           The JcrFs config to use
  -v (--verbose)           verbose output
  -q (--quiet)             print as little as possible
  --version                print the version information and exit
  --log-level <level>      the log4j log level
  -h (--help) <command>    print this help
Commands:
  export                   Export the Vault filesystem
  import                   Import a Vault filesystem
  checkout (co)            Checkout a Vault file system
  status (st)              Print the status of working copy files and directories.
  update (up)              Bring changes from the repository into the working copy.
  info                     Displays information about a local file.
  commit (ci)              Send changes from your working copy to the repository.
  revert (rev)             Restore pristine working copy file (undo most local edits).
  resolved (res)           Remove 'conflicted' state on working copy files or directories.
  propget (pg)             Print the value of a property on files or directories.
  proplist (pl)            Print the properties on files or directories.
  propset (ps)             Set the value of a property on files or directories.
  add                      Put files and directories under version control.
  delete (del,rm)          Remove files and directories from version control.
  diff (di)                Display the differences between two paths.
  rcp                      Remote copy of repository content.
  sync                     Control vault sync service
  console                  Run an interactive console
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
```

要获取有关特定命令的帮助，请键入帮助命令，然后键入该命令的名称。 例如：

```shell
vlt --help export
Usage:
 export -v|-t <arg>|-p <uri> <jcr-path> <local-path>

Description:
  Export the Vault filesystem mounted at <uri> to the local filesystem at <local-path>. An optional <jcr-path> can be specified to export just a sub tree.
  Example:
    vlt export http://localhost:4502/crx /apps/geometrixx myproject

Options:
  -v (--verbose)          verbose output
  -t (--type) <arg>       specifies the export type. either 'platform' or 'jar'.
  -p (--prune-missing)    specifies if missing local files should be deleted.
  <uri>                   mountpoint uri
  <jcr-path>              the jcr path
  <local-path>            the local path
```

## 在VLT中执行的常见任务 {#common-tasks-performed-in-vlt}

以下是在VLT中执行的一些常见任务。 有关每个命令的详细信息，请参阅各个 [命令](#vlt-commands).

### 签出子树 {#checking-out-a-subtree}

例如，如果只想签出存储库的子树， `/apps/geometrixx`，您可以通过键入以下内容来完成此操作：

```shell
vlt co http://localhost:4502/crx/-/jcr:root/apps/geometrixx geo
```

执行此操作将创建新的导出根 `geo` 带有 `META-INF` 和 `jcr_root` 目录并将所有文件放在 `/apps/geometrixx` 在 `geo/jcr_root`.

### 执行过滤的签出 {#performing-a-filtered-checkout}

如果您已有工作区过滤器，并且要将其用于签出，则可以先创建 `META-INF/vault` 目录，并将筛选器放置在该处，或在命令行中指定该筛选器，如下所示：

```shell
$ vlt co --filter filter.xml http://localhost:4502/crx/-/jcr:root geo
```

示例筛选条件：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<workspaceFilter version="1.0">
    <filter root="/etc/designs/geometrixx" />
    <filter root="/apps/geometrixx"/>
</workspaceFilter>
```

### 使用导入/导出而不是.vlt控件 {#using-import-export-instead-of-vlt-control}

您无需使用控制文件即可在JCR存储库和本地文件系统之间导入和导出内容。

在不使用的情况下导入和导出内容 `.vlt` 控件：

1. 最初设置存储库：

   ```shell
   $ cd /projects
   $ svn mkdir https://svn.server.com/repos/myproject
   $ svn co https://svn.server.com/repos/myproject
   $ vlt export -v http://localhost:4502/crx /apps/geometrixx geometrixx
   $ cd geometrixx/
   $ svn add META-INF/ jcr_root/
   $ svn ci
   ```

1. 更改远程拷贝并更新JCR：

   ```shell
   $ cd /projects/geometrixx
   $ vlt -v import http://localhost:4502/crx . /
   ```

1. 更改远程副本并更新文件服务器：

   ```shell
   $ cd /projects/geometrixx
   $ vlt export -v http://localhost:4502/crx /apps/geometrixx .
   $ svn st
   M      META-INF/vault/properties.xml
   M      jcr_root/apps/geometrixx/components/contentpage/.content.xml
   $ svn ci
   ```

## 使用VLT {#using-vlt}

要在VLT中发出命令，请在命令行键入以下内容：

```shell
vlt [options] <command> [arg1 [arg2 [arg3] ..]]  
```

以下各节详细介绍了选项和命令。

## VLT全局选项 {#vlt-global-options}

以下是VLT选项的列表，这些选项可用于所有命令。 有关其他可用选项的信息，请参阅各个命令。

|  |  |
|--- |--- |
| 选项 | 描述 |
| `-Xjcrlog <arg>` | 扩展JcrLog选项 |
| `-Xdavex <arg>` | 扩展JCR远程选项 |
| `--credentials <arg>` | 要使用的默认凭据 |
| `--config <arg>` | 要使用的JcrFs配置 |
| `-v (--verbose)` | 详细输出 |
| `-q (--quiet)` | 尽可能少地打印 |
| `--version` | 打印版本信息并退出VLT |
| `--log-level <level>` | 指示日志级别，例如log4j日志级别。 |
| `-h (--help) <command>` | 打印该特定命令的帮助 |

## VLT命令 {#vlt-commands}

下表描述了所有可用的VLT命令。 有关语法、可用选项和示例的详细信息，请参阅各个命令。

|  |  |  |
|--- |--- |--- |
| 命令 | 缩写命令 | 描述 |
| `export` |  | 从JCR存储库（电子仓库文件系统）导出到本地文件系统，而不使用控制文件。 |
| `import` |  | 将本地文件系统导入到JCR存储库（保险库文件系统）。 |
| `checkout` | `co` | 签出Vault文件系统。 将此用于本地文件系统的初始JCR存储库。 （注意：请先在subversion中签出存储库。） |
| `analyze` |  | 分析包。 |
| `status` | `st` | 打印工作副本文件和目录的状态。 |
| `update` | `up` | 将更改从存储库导入工作副本。 |
| `info` |  | 显示有关本地文件的信息。 |
| `commit` | `ci` | 将更改从工作副本发送到存储库。 |
| `revert` | `rev` | 将工作副本文件恢复到其原始状态，并撤消大多数本地编辑。 |
| `resolved` | `res` | 删除工作副本文件或目录上的冲突状态。 |
| `propget` | `pg` | 在文件或目录上打印属性的值。 |
| `proplist` | `pl` | 打印文件或目录上的属性。 |
| `propset` | `ps` | 设置文件或目录上属性的值。 |
| `add` |  | 将文件和目录置于版本控制之下。 |
| `delete` | `del` 或 `rm` | 从版本控制中删除文件和目录。 |
| `diff` | `di` | 显示两个路径之间的差异。 |
| `console` |  | 运行交互式控制台。 |
| `rcp` |  | 将节点树从一个远程存储库复制到另一个远程存储库。 |
| `sync` |  | 允许您控制保险库同步服务。 |

### 导出 {#export}

导出安装在以下位置的Vault文件系统 &lt;uri> 到本地文件系统： &lt;local-path>. 可选 &lt;jcr-path> 可以指定以仅导出子树。

#### 语法 {#syntax}

```shell
export -v|-t <arg>|-p <uri> <jcr-path> <local-path>
```

#### 选项 {#options}

|  |  |
|--- |--- |
| `-v (--verbose)` | 详细输出 |
| `-t (--type) <arg>` | 指定导出类型，即platform或jar。 |
| `-p (--prune-missing)` | 指定是否应删除缺少的本地文件 |
| `<uri>` | 装入点URI |
| `<jcrPath>` | JCR路径 |
| `<localPath>` | 本地路径 |

#### 示例 {#examples}

```shell
vlt export http://localhost:4502/crx /apps/geometrixx myproject
```

### 导入 {#import}

导入本地文件系统(从 `<local-path>` 到Vault文件系统 `<uri>`. 您可以指定 `<jcr-path>` 作为导入根。 如果 `--sync` 指定后，导入的文件将自动置于电子仓库控制下。

#### 语法 {#syntax-1}

```shell
import -v|-s <uri> <local-path> <jcr-path>
```

#### 选项 {#options-1}

|  |  |
|--- |--- |
| `-v (--verbose)` | 详细输出 |
| `-s (-- sync)` | 将本地文件置于保险库控制下 |
| `<uri>` | 装入点URI |
| `<jcrPath>` | JCR路径 |
| `<localPath>` | 本地路径 |

#### 示例 {#examples-1}

```shell
vlt import http://localhost:4502/crx . /
```

### 结帐(co) {#checkout-co}

从JCR存储库到本地文件系统的初始签出开始于 &lt;uri> 到本地文件系统： &lt;local-path>. 您还可以添加 &lt;jcrpath> 用于签出远程树的子目录的参数。 可以指定复制到META-INF目录中的工作区筛选器。

#### 语法 {#syntax-2}

```shell
checkout --force|-v|-q|-f <file> <uri> <jcrPath> <localPath>  
```

#### 选项 {#options-2}

|  |  |
|--- |--- |
| `--force` | 如果本地文件已存在，则强制签出以覆盖这些文件 |
| `-v (--verbose)` | 详细输出 |
| `-q (--quiet)` | 尽量少打印 |
| `-f (--filter) <file>` | 如果未定义任何筛选器，则指定自动筛选器 |
| `<uri>` | 装入点URI |
| `<jcrPath>` | （可选）远程路径 |
| `<localPath>` | （可选）本地路径 |

#### 示例 {#examples-2}

使用JCR远程处理：

```shell
vlt --credentials admin:admin co http://localhost:8080/crx/server/crx.default/jcr_root/
```

在默认工作区中：

```shell
vlt --credentials admin:admin co http://localhost:8080/crx/server/-/jcr_root/
```

如果URI不完整，则将展开该URI：

```shell
vlt --credentials admin:admin co http://localhost:8080/crx
```

### 分析 {#analyze}

分析包。

#### 语法 {#syntax-3}

```shell
analyze -l <format>|-v|-q <localPaths1> [<localPaths2> ...]
```

#### 选项 {#options-3}

|  |  |
|--- |--- |
| `-l (--linkFormat) <format>` | 修补程序链接的printf格式（名称、id），例如， `[CQ520_HF_%s|%s]` |
| `-v (--verbose)` | 详细输出 |
| `-q (--quiet)` | 尽量少打印 |
| `<localPaths> [<localPaths> ...]` | 本地路径 |

### 状态 {#status}

打印工作副本文件和目录的状态。

如果 `--show-update` 指定时，每个文件都会根据远程版本进行检查。 然后，第二个字母指定更新操作将执行的操作。

#### 语法 {#syntax-4}

```shell
status -v|-q|-u|-N <file1> [<file2> ...]
```

#### 选项 {#options-4}

|  |  |
|--- |--- |
| `-v (--verbose)` | 详细输出 |
| `-q (--quiet)` | 尽量少打印 |
| `-u (--show-update)` | 显示更新信息 |
| `-N (--non-recursive)` | 在单个目录上运行 |
| `<file> [<file> ...]` | 文件或目录以显示状态 |

### 更新 {#update}

将更改从存储库复制到工作副本。

#### 语法 {#syntax-5}

```shell
update -v|-q|--force|-N <file1> [<file2> ...]
```

#### 选项 {#options-5}

|  |  |
|--- |--- |
| `-v (--verbose)` | 详细输出 |
| `-q (--quiet)` | 尽量少打印 |
| `--force` | 强制覆盖本地文件 |
| `-N (--non-recursive)` | 在单个目录上运行 |
| `<file> [<file> ...]` | 要更新的文件或目录 |

### 信息 {#info}

显示有关本地文件的信息。

#### 语法 {#syntax-6}

```shell
info -v|-q|-R <file1> [<file2> ...]
```

#### 选项 {#options-6}

|  |  |
|--- |--- |
| `-v (--verbose)` | 详细输出 |
| `-q (--quiet)` | 尽量少打印 |
| `-R (--recursive)` | 操作递归 |
| `<file> [<file> ...]` | 要显示信息的文件或目录 |

### 提交 {#commit}

将更改从工作副本发送到存储库。

#### 语法 {#syntax-7}

```shell
commit -v|-q|--force|-N <file1> [<file2> ...]
```

#### 选项 {#options-7}

|  |  |
|--- |--- |
| `-v (--verbose)` | 详细输出 |
| `-q (--quiet)` | 尽量少打印 |
| `--force` | 强制提交，即使远程副本被修改也是如此 |
| `-N (--non-recursive)` | 在单个目录上运行 |
| `<file> [<file> ...]` | 要提交的文件或目录 |

### 还原 {#revert}

将工作副本文件恢复为原始状态并撤消大多数本地编辑。

#### 语法 {#syntax-8}

```shell
revert -q|-R <file1> [<file2> ...]
```

#### 选项 {#options-8}

|  |  |
|--- |--- |
| `-q (--quiet)` | 尽量少打印 |
| `-R (--recursive)` | 递减递减 |
| `<file> [<file> ...]` | 要提交的文件或目录 |

### 已解决 {#resolved}

删除 **冲突** 工作副本文件或目录的状态。

>[!NOTE]
>
>此命令不会从语义上解决冲突或移除冲突标记；它仅会移除与冲突相关的工件文件，并允许PATH再次提交。

#### 语法 {#syntax-9}

```shell
resolved -q|-R|--force <file1> [<file2> ...]  
```

#### 选项 {#options-9}

|  |  |
|--- |--- |
| `-q (--quiet)` | 尽量少打印 |
| `-R (--recursive)` | 递减递减 |
| `--force` | 即使存在冲突标记也解析了 |
| `<file> [<file> ...]` | 要解析的文件或目录 |

### Propget {#propget}

在文件或目录上打印属性的值。

#### 语法 {#syntax-10}

```shell
propget -q|-R <propname> <file1> [<file2> ...]
```

#### 选项 {#options-10}

|  |  |
|--- |--- |
| `-q (--quiet)` | 尽量少打印 |
| `-R (--recursive)` | 递减递减 |
| `<propname>` | 属性名称 |
| `<file> [<file> ...]` | 从中获取属性的文件或目录 |

### proplist {#proplist}

打印文件或目录上的属性。

#### 语法 {#syntax-11}

```shell
proplist -q|-R <file1> [<file2> ...]
```

#### 选项 {#options-11}

|  |  |
|--- |--- |
| `-q (--quiet)` | 尽量少打印 |
| `-R (--recursive)` | 递减递减 |
| `<file> [<file> ...]` | 要从中列出属性的文件或目录 |

### 属性集 {#propset}

设置文件或目录上属性的值。

>[!NOTE]
>
>VLT可以识别以下特殊版本化属性：
>
>`vlt:mime-type`
>
>文件的mimetype。 用于确定是否合并文件。 以“text/”开头的mimetype（或不存在mimetype）被视为文本。 任何其他内容均被视为二进制。

#### 语法 {#syntax-12}

```shell
propset -q|-R <propname> <propval> <file1> [<file2> ...]
```

#### 选项 {#options-12}

|  |  |
|--- |--- |
| `-q (--quiet)` | 尽量少打印 |
| `-R (--recursive)` | 递减递减 |
| `<propname>` | 属性名称 |
| `<propval>` | 属性值 |
| `<file> [<file> ...]` | 要设置属性的文件或目录 |

### 添加 {#add}

将文件和目录置于版本控制之下，并计划将它们添加到存储库中。 它们将在下次提交时添加。

#### 语法 {#syntax-13}

```shell
add -v|-q|-N|--force <file1> [<file2> ...]
```

#### 选项 {#options-13}

|  |  |
|--- |--- |
| `-v (--verbose)` | 详细输出 |
| `-q (--quiet)` | 尽量少打印 |
| `-N (--non-recursive)` | 在单个目录上运行 |
| `--force` | 强制运行操作 |
| `<file> [<file> ...]` | 要添加的本地文件或目录 |

### 删除 {#delete}

从版本控制中删除文件和目录。

#### 语法 {#syntax-14}

```shell
delete -v|-q|--force <file1> [<file2> ...]
```

#### 选项 {#options-14}

|  |  |
|--- |--- |
| `-v (--verbose)` | 详细输出 |
| `-q (--quiet)` | 尽量少打印 |
| `--force` | 强制运行操作 |
| `<file> [<file> ...]` | 要删除的本地文件或目录 |

### 差异 {#diff}

显示两个路径之间的差异。

#### 语法 {#syntax-15}

```shell
diff -N <file1> [<file2> ...]
```

#### 选项 {#options-15}

|  |  |
|--- |--- |
| `-N (--non-recursive)` | 在单个目录上运行 |
| `<file> [<file> ...]` | 要显示差异的文件或目录 |

### 控制台 {#console}

运行交互式控制台。

#### 语法 {#syntax-16}

```shell
console -F <file>
```

#### 选项 {#options-16}

|  |  |
|--- |--- |
| `-F (--console-settings) <file>` | 指定控制台设置文件。 默认文件为console.properties。 |

### Rcp {#rcp}

将节点树从一个远程存储库复制到另一个远程存储库。 `<src>` 指向源节点并 `<dst>` 指定父节点必须存在的目标路径。 Rcp通过流式传输数据来处理节点。

#### 语法 {#syntax-17}

```shell
rcp -q|-r|-b <size>|-t <seconds>|-u|-n|-e <arg1> [<arg2> ...] <src> <dst>
```

#### 选项 {#options-17}

|  |  |
|--- |--- |
| `-q (--quiet)` | 尽量少打印。 |
| `-r (--recursive)` | 递减递减。 |
| `-b (--batchSize) <size>` | 在中间保存之前要处理的节点数。 |
| `-t (--throttle) <seconds>` | 中间保存后等待的秒数。 |
| `-u (--update)` | 覆盖/删除现有节点。 |
| `-n (--newer)` | 遵守lastModified属性以进行更新。 |
| `-e (--exclude) <arg> [<arg> ...]` | 排除的源路径的正则表达式。 |
| `<src>` | 源树的存储库地址。 |
| `<dst>` | 目标节点的存储库地址。 |

#### 示例 {#examples-3}

```shell
vlt rcp http://localhost:4502/crx/-/jcr:root/content  https://admin:admin@localhost:4503/crx/-/jcr:root/content_copy  
```

>[!NOTE]
>
>此 `--exclude` 选项后面必须跟有另一个选项，才能使用 `<src>` 和 `<dst>` 参数。 例如：
>
>`vlt rcp -e ".*\.txt" -r`

### 同步 {#sync}

允许您控制保险库同步服务。 如果没有参数，此命令尝试将当前工作目录置于同步控制下。 如果在vlt签出中运行，则它会使用相应的过滤器和主机来配置同步。 如果在vlt签出之外运行，则仅当目录为空时，它才会注册当前文件夹以进行同步。

#### 语法 {#syntax-18}

```shell
sync -v|--force|-u <uri> <command> <localPath>
```

#### 选项 {#options-18}

|  |  |
|--- |--- |
| `-v (--verbose)` | 详细输出。 |
| `--force` | 强制执行某些命令。 |
| `-u (--uri) <uri>` | 指定同步主机的URI。 |
| `<command>` | 要执行的同步命令。 |
| `<localPath>` | 要同步的本地文件夹。 |

### 状态代码 {#status-codes}

VLT使用的状态代码包括：

* &#39; &#39;无修改
* 已添加“A”
* “C”冲突
* 已删除“D”
* 已忽略“I”
* 已修改“M”
* 已替换“R”
* &#39;？&#39; 项目不受版本控制
* &#39;！&#39; 缺少项目（由非svn命令删除）或不完整
* &#39;~&#39;版本化项被其他类型的项阻塞

## 设置FileVault同步 {#setting-up-filevault-sync}

保险库同步服务用于将存储库内容与本地文件系统表示进行同步，反之亦然。 这是通过安装OSGi服务来实现的，该服务将侦听存储库更改并定期扫描文件系统内容。 它使用与Vault相同的序列化格式将存储库内容映射到磁盘。

>[!NOTE]
>
>保险库同步服务是一种开发工具，强烈建议不要将其用于生产系统。 此外，该服务只能与本地文件系统同步，不能用于远程开发。

### 使用vlt安装服务 {#installing-the-service-using-vlt}

此 `vlt sync install` 命令可用于自动安装保险库同步服务包和配置。

捆绑包安装在下面 `/libs/crx/vault/install` 并且配置节点创建于 `/libs/crx/vault/com.day.jcr.sync.impl.VaultSyncServiceImpl`. 最初启用该服务，但未配置同步根。

以下示例将同步服务安装到给定URI可访问的CRX实例。

```shell
$ vlt --credentials admin:admin sync --uri http://localhost:4502/crx install
```

### 显示服务状态 {#displaying-the-service-status}

此 `status` 命令可用于显示有关正在运行的同步服务的信息。&quot;

```shell
$ vlt sync status --uri http://localhost:4502/crx
Connecting via JCR remoting to http://localhost:4502/crx/server
Listing sync status for http://localhost:4502/crx/server/-/jcr:root
- Sync service is enabled.
- No sync directories configured.
```

>[!NOTE]
>
>此 `status` 命令不从服务获取任何实时数据，而是读取上的配置 `/libs/crx/vault/com.day.jcr.sync.impl.VaultSyncServiceImpl`.

### 添加同步文件夹 {#adding-a-sync-folder}

此 `register` 命令用于添加要同步到配置的文件夹。

```shell
$ vlt sync register
Connecting via JCR remoting to http://localhost:4502/crx/server
Added new sync directory: /tmp/workspace/vltsync/jcr_root
```

>[!NOTE]
>
>此 `register` 命令不会触发同步，直到您配置 `sync-once` 配置。

### 删除同步文件夹 {#removing-a-sync-folder}

此 `unregister` 命令用于从配置中删除要同步的文件夹。

```shell
$  vlt sync unregister
Connecting via JCR remoting to http://localhost:4502/crx/server
Removed sync directory: /tmp/workspace/vltsync/jcr_root
```

>[!NOTE]
>
>在删除同步文件夹本身之前，必须先注销该文件夹。

### 配置同步 {#configuring-synchronization}

#### 服务配置 {#service-configuration}

服务运行后，可以使用以下参数对其进行配置：

* `vault.sync.syncroots`：定义同步根的一个或多个本地文件系统路径。

* `vault.sync.fscheckinterval`：应扫描文件系统以查看更改的频率（以秒为单位）。 默认值为5秒。
* `vault.sync.enabled`：启用/禁用服务的常规标记。

>[!NOTE]
>
>该服务可以使用Web控制台或 `sling:OsgiConfig` 节点(具有名称 `com.day.jcr.sync.impl.VaultSyncServiceImpl`)。
>
>使用AEM时，可通过多种方法管理此类服务的配置设置；请参阅 [配置OSGi](/help/sites-deploying/configuring-osgi.md) 以了解全部详细信息。

#### 同步文件夹配置 {#sync-folder-configuration}

每个同步文件夹将配置和状态存储在三个文件中：

* `.vlt-sync-config.properties`：配置文件。

* `.vlt-sync.log`：日志文件，其中包含有关在同步期间执行的操作的信息。
* `.vlt-sync-filter.xml`：定义同步存储库哪些部分的过滤器。 此文件的格式由 [执行过滤的签出](#performing-a-filtered-checkout) 部分。

此 `.vlt-sync-config.properties` 文件允许您配置以下属性：

**已禁用** 打开或关闭同步。 默认情况下，此参数设置为false以允许同步。

**同步 — 一次** 如果不为空，则下次扫描将以给定方向同步文件夹，然后清除参数。 支持两个值：

* `JCR2FS`：导出JCR存储库中的所有内容并将内容写入本地磁盘。
* `FS2JCR`：将所有内容从磁盘导入JCR存储库。

**同步日志** 定义日志文件名。 默认情况下，该值为.vlt-sync.log

### 使用VLT同步进行开发 {#using-vlt-sync-for-development}

要基于同步文件夹设置开发环境，请执行以下操作：

1. 使用vlt命令行签出存储库：

   ```shell
   $ vlt --credentials admin:admin co --force http://localhost:4502/crx dev
   ```

   >[!NOTE]
   >
   >您可以使用过滤器仅签出适当的路径。 请参阅 [执行过滤的签出](#performing-a-filtered-checkout) 部分以了解相关信息。

1. 转到工作副本的根文件夹：

   ```shell
   $ cd dev/jcr_root/
   ```

1. 将同步服务安装到存储库：

   ```xml
   $ vlt sync install
   Connecting via JCR remoting to http://localhost:4502/crx/server
   Preparing to install vault-sync-2.4.24.jar...
   Updated bundle: vault-sync-2.4.24.jar
   Created new config at /libs/crx/vault/config/com.day.jcr.sync.impl.VaultSyncServiceImpl
   ```

1. 初始化同步服务：

   ```shell
   $ vlt sync
   Connecting via JCR remoting to http://localhost:4502/crx/server
   Starting initialization of sync service in existing vlt checkout /Users/colligno/Applications/cq5/vltsync/sandbox/dev/jcr_root for http://localhost:4502/crx/server/-/jcr:root
   Added new sync directory: /Users/trushton/Applications/aem/vltsync/sandbox/dev/jcr_root
   
   The directory /Users/trushton/Applications/aem/vltsync/sandbox/dev/jcr_root is now enabled for syncing.
   You might perform a 'sync-once' by setting the
   appropriate flag in the /Users/trushton/Applications/aem/vltsync/sandbox/dev/jcr_root/.vlt-sync-config.properties file.
   ```

1. 编辑 `.vlt-sync-config.properties` 隐藏的文件并配置同步以同步存储库的内容：

   ```xml
   sync-once=JCR2FS
   ```

   >[!NOTE]
   >
   >此步骤将根据您的过滤器配置下载整个存储库。

1. 检查日志文件 `.vlt-sync.log` 要查看进度，请执行以下操作：

   ```xml
   ***
   30.04.2017 14:39:10 A file:///Users/trushton/Applications/aem/vltsync/sandbox/dev/jcr_root/apps/geometrixx-outdoors/src/core/src/main/java/info/geometrixx/outdoors/
   30.04.2017 14:39:10 A file:///Users/trushton/Applications/aem/vltsync/sandbox/dev/jcr_root/apps/geometrixx-outdoors/src/core/src/main/java/info/geometrixx/outdoors/core/
   30.04.2017 14:39:10 A file:///Users/trushton/Applications/aem/vltsync/sandbox/dev/jcr_root/apps/geometrixx-outdoors/src/core/src/main/java/info/geometrixx/outdoors/core/product/
   30.04.2017 14:39:10 A file:///Users/trushton/Applications/aem/vltsync/sandbox/dev/jcr_root/apps/geometrixx-outdoors/src/core/src/main/java/info/geometrixx/outdoors/core/product/GeoProduct.java
   ***
   ```

您的本地文件夹现在与存储库同步。 同步是双向的，因此存储库中的修改将应用于本地同步文件夹，反之亦然。

>[!NOTE]
>
>VLT同步功能仅支持简单的文件和文件夹，但会检测特殊的vault序列化文件（.content.xml、dialog.xml等），并且静默地忽略它们。 因此，可以在默认的vlt签出中使用保险库同步。
