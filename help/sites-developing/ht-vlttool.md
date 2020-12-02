---
title: 如何使用VLT工具
seo-title: 如何使用VLT工具
description: Jackrabbit FileVault工具(VLT)由Apache Foundation开发，它将Jackrabbit/AEM实例的内容映射到您的文件系统
seo-description: Jackrabbit FileVault工具(VLT)由Apache Foundation开发，它将Jackrabbit/AEM实例的内容映射到您的文件系统
uuid: 579e7785-8b50-4366-b562-8e79b6451464
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: a76425e9-fd3b-4c73-80f9-0ebabb8fd94f
translation-type: tm+mt
source-git-commit: 2da3da1a36f074593e276ddd15ed8331239ab70f
workflow-type: tm+mt
source-wordcount: '2748'
ht-degree: 1%

---


# 如何使用VLT工具{#how-to-use-the-vlt-tool}

Jackrabbit FileVault工具(VLT)是由[Apache Foundation](https://www.apache.org/)开发的工具，它将Jackrabbit/AEM实例的内容映射到您的文件系统。 VLT工具具有与源控制系统客户端(如Subversion(SVN)客户端)类似的功能，提供正常的登记、注销和管理操作，以及可灵活呈现项目内容的配置选项。

从命令行运行VLT工具。 本文档介绍如何使用该工具，包括如何开始和获取帮助，以及所有[命令](#vlt-commands)和可用[选项](#vlt-global-options)的列表。

## 概念和架构{#concepts-and-architecture}

有关Filevault工具的概念和结构的全面概述，请参阅官方[Apache Jackrabbit Filevault文档](https://jackrabbit.apache.org/filevault/index.html)中的[Filevault概述](https://jackrabbit.apache.org/filevault/overview.html)和[Vault FS](https://jackrabbit.apache.org/filevault/vaultfs.html)页。

## VLT {#getting-started-with-vlt}快速入门

要使用VLT进行开始，您需要执行以下操作：

1. 安装VLT、更新环境变量和更新全局忽略的subversion文件。
1. 设置AEM存储库（如果尚未设置）。
1. 查看AEM存储库。
1. 与存储库同步。
1. 测试同步是否有效。

### 安装VLT工具{#installing-the-vlt-tool}

要使用VLT工具，您首先需要安装它。 默认情况下，它不安装，因为它是一个附加工具。 此外，还需要设置系统的环境变量。

1. 从[Maven对象存储库下载FileVault归档文件。](https://repo1.maven.org/maven2/org/apache/jackrabbit/vault/vault-cli/)
   >[!NOTE]
   >
   >VLT工具的源代码在GitHub上可用。[](https://github.com/apache/jackrabbit-filevault)
1. 解压存档。
1. 将`<archive-dir>/vault-cli-<version>/bin`添加到环境`PATH`中，以便根据需要访问命令文件`vlt`或`vlt.bat`。 例如：

   `<aem-installation-dir>/crx-quickstart/opt/helpers/vault-cli-3.1.16/bin>`

1. 打开命令行shell并执行`vlt --help`。 确保输出类似于以下帮助屏幕：

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

安装后，您需要更新全局忽略的subversion文件。 编辑svn设置并添加以下内容：

```xml
[miscellany]
### Set global-ignores to a set of whitespace-delimited globs
### which Subversion will ignore in its 'status' output, and
### while importing or adding files and directories.
global-ignores = .vlt
```

### 配置行尾字符{#configuring-the-end-of-line-character}

VLT会根据以下规则自动处理行尾(EOF):

* 在Windows上签出的文件行以`CRLF`结尾
* 在Linux/Unix上签出的文件行以`LF`结尾
* 以`LF`结尾的文件行

为确保VLT和SVN配置匹配，应将`svn:eol-style`属性设置为`native`，以扩展存储库中存储的文件。 编辑svn设置并添加以下内容：

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

### 签出存储库{#checking-out-the-repository}

使用源控制系统签出存储库。 例如，在svn中，键入以下内容（将URI和路径替换为您的存储库）:

```shell
svn co https://svn.server.com/repos/myproject
```

### 与存储库{#synchronizing-with-the-repository}同步

您需要将文件与存储库同步。 要执行此操作：

1. 在命令行中，导航到`content/jcr_root`。
1. 通过键入以下内容（将端口号替换为&#x200B;**4502**&#x200B;和管理员密码），检查存储库：

   ```shell
   vlt --credentials admin:admin co --force http://localhost:4502/crx
   ```

   >[!NOTE]
   >
   >在初始结帐时，只能指定一次凭据。 然后，它们将存储在`.vault/auth.xml`的主目录中。

### 测试同步是否有效{#testing-whether-the-synchronization-worked}

在签出存储库并同步它后，应进行测试以确保所有内容都正常工作。 执行此操作的简单方法是编辑&#x200B;**.jsp**&#x200B;文件，并查看提交更改后是否反映了您所做的更改。

要测试同步，请执行以下操作：

1. 导航至 `.../jcr_content/libs/foundation/components/text`.
1. 在`text.jsp`中编辑内容。
1. 通过键入`vlt st`查看修改的文件
1. 键入`vlt diff text.jsp`查看更改
1. 提交更改：`vlt ci test.jsp`。
1. 重新加载包含文本组件的页面，并查看您所做的更改是否存在。

## 获取VLT工具帮助{#getting-help-with-the-vlt-tool}

安装VLT工具后，可以从命令行访问其“帮助”文件：

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

要获得特定命令的帮助，请键入help命令，后跟该命令的名称。 例如：

```shell
vlt --help export
Usage:
 export -v|-t <arg>|-p <uri> <jcr-path> <local-path>

Description:
  Export the Vault filesystem mounted at <uri> to the local filesystem at <local-path>. An optional <jcr-path> can be specified in order to export just a sub tree.
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

## 在VLT {#common-tasks-performed-in-vlt}中执行的常见任务

以下是在VLT中执行的一些常见任务。 有关每个命令的详细信息，请参见单个[命令](#vlt-commands)。

### 签出子树{#checking-out-a-subtree}

如果只想签出存储库的子树（例如`/apps/geometrixx`），可以通过键入以下内容来实现：

```shell
vlt co http://localhost:4502/crx/-/jcr:root/apps/geometrixx geo
```

这样做会创建一个新的导出根`geo`（带有`META-INF`和`jcr_root`目录），并将所有文件放在`geo/jcr_root`中的`/apps/geometrixx`下。

### 执行已过滤的签出{#performing-a-filtered-checkout}

如果您有现有的工作区过滤器，并且希望使用它进行签出，您可以先创建`META-INF/vault`目录并将过滤器放在该目录，或者按如下方式在命令行中指定它：

```shell
$ vlt co --filter filter.xml http://localhost:4502/crx/-/jcr:root geo
```

示例过滤器：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<workspaceFilter version="1.0">
    <filter root="/etc/designs/geometrixx" />
    <filter root="/apps/geometrixx"/>
</workspaceFilter>
```

### 使用导入／导出而不是。vlt控件{#using-import-export-instead-of-vlt-control}

无需使用控制文件，即可在JCR存储库和本地文件系统之间导入和导出内容。

要导入和导出内容而不使用`.vlt`控件，请执行以下操作：

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

1. 更改远程副本并更新JCR:

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

要在VLT中发出命令，请在命令行中键入以下内容：

```shell
vlt [options] <command> [arg1 [arg2 [arg3] ..]]  
```

选项和命令在以下各节中有详细介绍。

## VLT全局选项{#vlt-global-options}

以下是VLT选项的列表，所有命令都可用。 有关其他可用选项的信息，请参阅各个命令。

|  |  |
|--- |--- |
| 选项 | 描述 |
| `-Xjcrlog <arg>` | 扩展的JcrLog选项 |
| `-Xdavex <arg>` | 扩展的JCR远程处理选项 |
| `--credentials <arg>` | 要使用的默认凭据 |
| `--config <arg>` | 要使用的JcrFs配置 |
| `-v (--verbose)` | 详细输出 |
| `-q (--quiet)` | 尽可能少地打印 |
| `--version` | 打印版本信息并退出VLT |
| `--log-level <level>` | 指示日志级别，例如log4j日志级别。 |
| `-h (--help) <command>` | 打印该特定命令的帮助 |

## VLT命令{#vlt-commands}

下表描述了所有可用的VLT命令。 有关语法、可用选项和示例的详细信息，请参阅各个命令。

|  |  |  |
|--- |--- |--- |
| Command | 缩写命令 | 描述 |
| `export` |  | 从JCR存储库（保存库文件系统）导出到本地文件系统，而无控制文件。 |
| `import` |  | 将本地文件系统导入JCR存储库（保险存储文件系统）。 |
| `checkout` | `co` | 检出Vault文件系统。 将它用于本地文件系统的初始JCR存储库。 (注：必须首先在subversion中签出库。) |
| `analyze` |  | 分析包。 |
| `status` | `st` | 打印工作副本文件和目录的状态。 |
| `update` | `up` | 将更改从存储库导入工作副本。 |
| `info` |  | 显示有关本地文件的信息。 |
| `commit` | `ci` | 将工作副本中的更改发送到存储库。 |
| `revert` | `rev` | 将工作副本文件恢复到其原始状态并取消大多数本地编辑。 |
| `resolved` | `res` | 删除工作副本文件或目录的冲突状态。 |
| `propget` | `pg` | 在文件或目录上打印属性的值。 |
| `proplist` | `pl` | 打印文件或目录的属性。 |
| `propset` | `ps` | 设置文件或目录的属性值。 |
| `add` |  | 将文件和目录置于版本控制之下。 |
| `delete` | `del` 或 `rm` | 从版本控制中删除文件和目录。 |
| `diff` | `di` | 显示两个路径之间的差异。 |
| `console` |  | 运行交互式控制台。 |
| `rcp` |  | 将节点树从一个远程存储库复制到另一个远程存储库。 |
| `sync` |  | 允许控制保险库同步服务。 |

### 导出 {#export}

将装载在&lt;uri>的Vault文件系统导出到位于&lt;local-path>的本地文件系统。 可以指定可选的&lt;jcr-path>，以便仅导出子树。

#### 语法{#syntax}

```shell
export -v|-t <arg>|-p <uri> <jcr-path> <local-path>
```

#### 选项 {#options}

|  |  |
|--- |--- |
| `-v (--verbose)` | 详细输出 |
| `-t (--type) <arg>` | 指定导出类型，平台或jar。 |
| `-p (--prune-missing)` | 指定是否应删除缺少的本地文件 |
| `<uri>` | mountpoint uri |
| `<jcrPath>` | JCR路径 |
| `<localPath>` | 本地路径 |

#### 示例 {#examples}

```shell
vlt export http://localhost:4502/crx /apps/geometrixx myproject
```

### 导入 {#import}

将本地文件系统（从`<local-path>`开始）导入`<uri>`的电子仓库文件系统。 可以指定`<jcr-path>`作为导入根。 如果指定`--sync`，则导入的文件将自动置于保管库控制之下。

#### 语法{#syntax-1}

```shell
import -v|-s <uri> <local-path> <jcr-path>
```

#### 选项 {#options-1}

|  |  |
|--- |--- |
| `-v (--verbose)` | 详细输出 |
| `-s (-- sync)` | 将本地文件置于保险存储控制之下 |
| `<uri>` | mountpoint uri |
| `<jcrPath>` | JCR路径 |
| `<localPath>` | 本地路径 |

#### 示例 {#examples-1}

```shell
vlt import http://localhost:4502/crx . /
```

### 签出(co){#checkout-co}

从JCR存储库到本地文件系统执行初始签出，从&lt;uri>开始到&lt;local-path>的本地文件系统。 您还可以添加&lt;jcrPath>参数以签出远程树的子目录。 可以指定将其复制到META-INF目录中的工作区过滤器。

#### 语法{#syntax-2}

```shell
checkout --force|-v|-q|-f <file> <uri> <jcrPath> <localPath>  
```

#### 选项 {#options-2}

|  |  |
|--- |--- |
| `--force` | 强制签出，如果本地文件已存在，则覆盖它们 |
| `-v (--verbose)` | 详细输出 |
| `-q (--quiet)` | 打印尽可能少 |
| `-f (--filter) <file>` | 如果未定义自动过滤器，则指定自动 |
| `<uri>` | mountpoint uri |
| `<jcrPath>` | （可选）远程路径 |
| `<localPath>` | （可选）本地路径 |

#### 示例 {#examples-2}

使用JCR Remoting:

```shell
vlt --credentials admin:admin co http://localhost:8080/crx/server/crx.default/jcr_root/
```

使用默认工作区：

```shell
vlt --credentials admin:admin co http://localhost:8080/crx/server/-/jcr_root/
```

如果URI不完整，则将展开它：

```shell
vlt --credentials admin:admin co http://localhost:8080/crx
```

### 分析 {#analyze}

分析包。

#### 语法{#syntax-3}

```shell
analyze -l <format>|-v|-q <localPaths1> [<localPaths2> ...]
```

#### 选项 {#options-3}

|  |  |
|--- |--- |
| `-l (--linkFormat) <format>` | 修补程序链接（名称、id）的printf格式，例如`[CQ520_HF_%s|%s]` |
| `-v (--verbose)` | 详细输出 |
| `-q (--quiet)` | 打印尽可能少 |
| `<localPaths> [<localPaths> ...]` | 本地路径 |

### 状态 {#status}

打印工作副本文件和目录的状态。

如果指定`--show-update`，则根据远程版本检查每个文件。 第二个字母然后指定更新操作将执行什么操作。

#### 语法{#syntax-4}

```shell
status -v|-q|-u|-N <file1> [<file2> ...]
```

#### 选项 {#options-4}

|  |  |
|--- |--- |
| `-v (--verbose)` | 详细输出 |
| `-q (--quiet)` | 打印尽可能少 |
| `-u (--show-update)` | 显示更新信息 |
| `-N (--non-recursive)` | 在单个目录上运行 |
| `<file> [<file> ...]` | 显示状态的文件或目录 |

### 更新 {#update}

将更改从存储库复制到工作副本中。

#### 语法{#syntax-5}

```shell
update -v|-q|--force|-N <file1> [<file2> ...]
```

#### 选项 {#options-5}

|  |  |
|--- |--- |
| `-v (--verbose)` | 详细输出 |
| `-q (--quiet)` | 打印尽可能少 |
| `--force` | 强制覆盖本地文件 |
| `-N (--non-recursive)` | 在单个目录上运行 |
| `<file> [<file> ...]` | 要更新的文件或目录 |

### 信息 {#info}

显示有关本地文件的信息。

#### 语法{#syntax-6}

```shell
info -v|-q|-R <file1> [<file2> ...]
```

#### 选项 {#options-6}

|  |  |
|--- |--- |
| `-v (--verbose)` | 详细输出 |
| `-q (--quiet)` | 打印尽可能少 |
| `-R (--recursive)` | 递归 |
| `<file> [<file> ...]` | 显示信息的文件或目录 |

### 提交 {#commit}

将工作副本中的更改发送到存储库。

#### 语法{#syntax-7}

```shell
commit -v|-q|--force|-N <file1> [<file2> ...]
```

#### 选项 {#options-7}

|  |  |
|--- |--- |
| `-v (--verbose)` | 详细输出 |
| `-q (--quiet)` | 打印尽可能少 |
| `--force` | 即使修改了远程副本，也强制进行提交 |
| `-N (--non-recursive)` | 在单个目录上运行 |
| `<file> [<file> ...]` | 提交文件或目录 |

### 还原 {#revert}

将工作副本文件恢复为原始状态并取消大多数本地编辑。

#### 语法{#syntax-8}

```shell
revert -q|-R <file1> [<file2> ...]
```

#### 选项 {#options-8}

|  |  |
|--- |--- |
| `-q (--quiet)` | 打印尽可能少 |
| `-R (--recursive)` | 递归降 |
| `<file> [<file> ...]` | 提交文件或目录 |

### 已解决 {#resolved}

删除工作副本文件或目录的&#x200B;**冲突**&#x200B;状态。

>[!NOTE]
>
>此命令从语义上不解决冲突或删除冲突标记；它只删除与冲突相关的对象文件并允许再次提交PATH。

#### 语法{#syntax-9}

```shell
resolved -q|-R|--force <file1> [<file2> ...]  
```

#### 选项 {#options-9}

|  |  |
|--- |--- |
| `-q (--quiet)` | 打印尽可能少 |
| `-R (--recursive)` | 递归降 |
| `--force` | 解析，即使存在冲突标记 |
| `<file> [<file> ...]` | 要解析的文件或目录 |

### Propget {#propget}

在文件或目录上打印属性的值。

#### 语法{#syntax-10}

```shell
propget -q|-R <propname> <file1> [<file2> ...]
```

#### 选项 {#options-10}

|  |  |
|--- |--- |
| `-q (--quiet)` | 打印尽可能少 |
| `-R (--recursive)` | 递归降 |
| `<propname>` | 属性名称 |
| `<file> [<file> ...]` | 要获取属性的文件或目录 |

### Proplist {#proplist}

打印文件或目录的属性。

#### 语法{#syntax-11}

```shell
proplist -q|-R <file1> [<file2> ...]
```

#### 选项 {#options-11}

|  |  |
|--- |--- |
| `-q (--quiet)` | 打印尽可能少 |
| `-R (--recursive)` | 递归降 |
| `<file> [<file> ...]` | 文件或目录，以列表 |

### Propset {#propset}

设置文件或目录的属性值。

>[!NOTE]
>
>VLT可识别以下特殊版本控制属性：
>
>`vlt:mime-type`
>
>文件的mimetype。 用于确定是否合并文件。 以“text/”开头的mimetype（或缺少的mimetype）被视为文本。 任何其他内容均视为二进制。

#### 语法{#syntax-12}

```shell
propset -q|-R <propname> <propval> <file1> [<file2> ...]
```

#### 选项 {#options-12}

|  |  |
|--- |--- |
| `-q (--quiet)` | 打印尽可能少 |
| `-R (--recursive)` | 递归降 |
| `<propname>` | 属性名称 |
| `<propval>` | 属性值 |
| `<file> [<file> ...]` | 要将属性设置为的文件或目录 |

### 将 {#add}

将文件和目录置于版本控制之下，将它们安排为添加到存储库。 将在下次提交时添加它们。

#### 语法{#syntax-13}

```shell
add -v|-q|-N|--force <file1> [<file2> ...]
```

#### 选项 {#options-13}

|  |  |
|--- |--- |
| `-v (--verbose)` | 详细输出 |
| `-q (--quiet)` | 打印尽可能少 |
| `-N (--non-recursive)` | 在单个目录上运行 |
| `--force` | 迫使行动开始 |
| `<file> [<file> ...]` | 添加本地文件或目录 |

### 删除 {#delete}

从版本控制中删除文件和目录。

#### 语法{#syntax-14}

```shell
delete -v|-q|--force <file1> [<file2> ...]
```

#### 选项 {#options-14}

|  |  |
|--- |--- |
| `-v (--verbose)` | 详细输出 |
| `-q (--quiet)` | 打印尽可能少 |
| `--force` | 迫使行动开始 |
| `<file> [<file> ...]` | 删除本地文件或目录 |

### 差异 {#diff}

显示两个路径之间的差异。

#### 语法{#syntax-15}

```shell
diff -N <file1> [<file2> ...]
```

#### 选项 {#options-15}

|  |  |
|--- |--- |
| `-N (--non-recursive)` | 在单个目录上运行 |
| `<file> [<file> ...]` | 显示 |

### 控制台 {#console}

运行交互式控制台。

#### 语法{#syntax-16}

```shell
console -F <file>
```

#### 选项 {#options-16}

|  |  |
|--- |--- |
| `-F (--console-settings) <file>` | 指定控制台设置文件。 默认文件为console.properties。 |

### Rcp {#rcp}

将节点树从一个远程存储库复制到另一个远程存储库。 `<src>` 指向源节点并指 `<dst>` 定目标路径，其中必须存在父节点。Rcp通过流化数据处理节点。

#### 语法{#syntax-17}

```shell
rcp -q|-r|-b <size>|-t <seconds>|-u|-n|-e <arg1> [<arg2> ...] <src> <dst>
```

#### 选项 {#options-17}

|  |  |
|--- |--- |
| `-q (--quiet)` | 尽可能少地打印。 |
| `-r (--recursive)` | 递归降级。 |
| `-b (--batchSize) <size>` | 中间保存之前要处理的节点数。 |
| `-t (--throttle) <seconds>` | 中间保存后等待的秒数。 |
| `-u (--update)` | 覆盖／删除现有节点。 |
| `-n (--newer)` | 请遵循lastModified属性进行更新。 |
| `-e (--exclude) <arg> [<arg> ...]` | 排除的源路径的Regexp。 |
| `<src>` | 源树的存储库地址。 |
| `<dst>` | 目标节点的存储库地址。 |

#### 示例 {#examples-3}

```shell
vlt rcp http://localhost:4502/crx/-/jcr:root/content  https://admin:admin@localhost:4503/crx/-/jcr:root/content_copy  
```

>[!NOTE]
>
>`--exclude`选项后面必须有另一个选项，位于`<src>`和`<dst>`参数之前。 例如：
>
>`vlt rcp -e ".*\.txt" -r`

### 同步 {#sync}

允许控制保险库同步服务。 如果没有任何参数，此命令将尝试将当前工作目录置于同步控制下。 如果在vlt签出中执行，则它使用相应的过滤器和主机来配置同步。 如果在vlt签出之外执行，则仅当目录为空时，它才注册当前文件夹以进行同步。

#### 语法{#syntax-18}

```shell
sync -v|--force|-u <uri> <command> <localPath>
```

#### 选项 {#options-18}

|  |  |
|--- |--- |
| `-v (--verbose)` | 详细输出。 |
| `--force` | 强制执行某些命令。 |
| `-u (--uri) <uri>` | 指定同步主机的URI。 |
| `<command>` | 执行sync命令。 |
| `<localPath>` | 要同步的本地文件夹。 |

### 状态代码{#status-codes}

VLT使用的状态代码为：

* “ ”无修改
* “A”已添加
* “C”冲突
* “D”已删除
* “I”被忽略
* “M”已修改
* 已替换“R”
* &#39;? 项目未受版本控制
* &#39;!&#39; 项缺失（由非svn命令删除）或不完整
* “~”版本项被某种不同类型的项阻塞

## 设置FileVault同步{#setting-up-filevault-sync}

保管库同步服务用于将存储库内容与本地文件系统表示同步，反之亦然。 这是通过安装OSGi服务实现的，该服务将侦听存储库更改并将定期扫描文件系统内容。 它使用与存储库相同的序列化格式将存储库内容映射到磁盘。

>[!NOTE]
>
>保险存储同步服务是一种开发工具，我们强烈建议您在高效系统上使用它。 另请注意，该服务只能与本地文件系统同步，不能用于远程开发。

### 使用vlt {#installing-the-service-using-vlt}安装服务

`vlt sync install`命令可用于自动安装保险存储同步服务包和配置。

捆绑包安装在`/libs/crx/vault/install`下，配置节点创建在`/libs/crx/vault/com.day.jcr.sync.impl.VaultSyncServiceImpl`。 最初启用服务，但未配置同步根。

以下示例将同步服务安装到给定URI可访问的CRX实例。

```shell
$ vlt --credentials admin:admin sync --uri http://localhost:4502/crx install
```

### 显示服务状态{#displaying-the-service-status}

`status`命令可用于显示有关正在运行的同步服务的信息。&quot;

```shell
$ vlt sync status --uri http://localhost:4502/crx
Connecting via JCR remoting to http://localhost:4502/crx/server
Listing sync status for http://localhost:4502/crx/server/-/jcr:root
- Sync service is enabled.
- No sync directories configured.
```

>[!NOTE]
>
>`status`命令不从服务中提取任何活动数据，而是读取`/libs/crx/vault/com.day.jcr.sync.impl.VaultSyncServiceImpl`的配置。

### 添加同步文件夹{#adding-a-sync-folder}

`register`命令用于添加要与配置同步的文件夹。

```shell
$ vlt sync register
Connecting via JCR remoting to http://localhost:4502/crx/server
Added new sync directory: /tmp/workspace/vltsync/jcr_root
```

>[!NOTE]
>
>在配置`sync-once`配置之前，`register`命令不会触发同步。

### 删除同步文件夹{#removing-a-sync-folder}

`unregister`命令用于删除要从配置中同步的文件夹。

```shell
$  vlt sync unregister
Connecting via JCR remoting to http://localhost:4502/crx/server
Removed sync directory: /tmp/workspace/vltsync/jcr_root
```

>[!NOTE]
>
>必须先注销同步文件夹，然后才能删除文件夹本身。

### 配置同步{#configuring-synchronization}

#### 服务配置{#service-configuration}

运行服务后，可以使用以下参数配置它：

* `vault.sync.syncroots`:定义同步根的一个或多个本地文件系统路径。

* `vault.sync.fscheckinterval`:扫描文件系统的更改频率（以秒为单位）。默认为5秒。
* `vault.sync.enabled`:启用／禁用服务的常规标志。

>[!NOTE]
>
>服务可以使用Web控制台或存储库中的`sling:OsgiConfig`节点（名称为`com.day.jcr.sync.impl.VaultSyncServiceImpl`）进行配置。
>
>与AEM合作时，有多种方法管理此类服务的配置设置；有关详细信息，请参阅[配置OSGi](/help/sites-deploying/configuring-osgi.md)。

#### 同步文件夹配置{#sync-folder-configuration}

每个同步文件夹都将配置和状态存储在三个文件中：

* `.vlt-sync-config.properties`:配置文件。

* `.vlt-sync.log`:日志文件，其中包含有关同步过程中执行的操作的信息。
* `.vlt-sync-filter.xml`:过滤器，用于定义同步存储库的哪些部分。此文件的格式由[执行已过滤的签出](#performing-a-filtered-checkout)部分描述。

`.vlt-sync-config.properties`文件允许您配置以下属性：

**禁** 用打开或关闭同步。默认情况下，此参数设置为false以允许同步。

**sync-** once如果为非空，则下一个扫描将按给定方向同步文件夹，则将清除该参数。支持以下两个值：

* `JCR2FS`:导出JCR存储库中的所有内容并写入本地磁盘。
* `FS2JCR`:将磁盘中的所有内容导入JCR存储库。

**sync-log定** 义日志文件名。默认情况下，该值为。vlt-sync.log

### 使用VLT同步进行开发{#using-vlt-sync-for-development}

要根据同步文件夹设置开发环境，请按如下步骤进行：

1. 使用vlt命令行签出您的存储库：

   ```shell
   $ vlt --credentials admin:admin co --force http://localhost:4502/crx dev
   ```

   >[!NOTE]
   >
   >您可以使用过滤器仅检出相应的路径。 有关信息，请参见[执行已过滤的签出](#performing-a-filtered-checkout)部分。

1. 转到工作副本的根文件夹：

   ```shell
   $ cd dev/jcr_root/
   ```

1. 将同步服务安装到您的存储库：

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

1. 编辑`.vlt-sync-config.properties`隐藏文件并配置同步以同步存储库的内容：

   ```xml
   sync-once=JCR2FS
   ```

   >[!NOTE]
   >
   >此步骤根据您的筛选器配置下载整个存储库。

1. 检查日志文件`.vlt-sync.log`以查看进度：

   ```xml
   ***
   30.04.2017 14:39:10 A file:///Users/trushton/Applications/aem/vltsync/sandbox/dev/jcr_root/apps/geometrixx-outdoors/src/core/src/main/java/info/geometrixx/outdoors/
   30.04.2017 14:39:10 A file:///Users/trushton/Applications/aem/vltsync/sandbox/dev/jcr_root/apps/geometrixx-outdoors/src/core/src/main/java/info/geometrixx/outdoors/core/
   30.04.2017 14:39:10 A file:///Users/trushton/Applications/aem/vltsync/sandbox/dev/jcr_root/apps/geometrixx-outdoors/src/core/src/main/java/info/geometrixx/outdoors/core/product/
   30.04.2017 14:39:10 A file:///Users/trushton/Applications/aem/vltsync/sandbox/dev/jcr_root/apps/geometrixx-outdoors/src/core/src/main/java/info/geometrixx/outdoors/core/product/GeoProduct.java
   ***
   ```

您的本地文件夹现在与存储库同步。 同步是双向的，因此从存储库中进行的修改将应用于本地同步文件夹，反之亦然。

>[!NOTE]
>
>VLT同步功能仅支持简单的文件和文件夹，但检测到特殊的保险存储序列化文件（.content.xml、dialog.xml等）并以静默方式忽略它们。 因此，可以在默认vlt结帐时使用vault同步。
