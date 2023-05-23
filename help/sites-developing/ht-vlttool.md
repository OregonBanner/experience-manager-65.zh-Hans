---
title: 如何使用VLT工具
seo-title: How to use the VLT Tool
description: Jackrabbit FileVault工具(VLT)由Apache Foundation開發，可將Jackrabbit/AEM執行個體的內容對應至您的檔案系統
seo-description: The Jackrabbit FileVault tool (VLT) is developed by The Apache Foundation that maps the content of a Jackrabbit/AEM instance to your file system
uuid: 579e7785-8b50-4366-b562-8e79b6451464
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: a76425e9-fd3b-4c73-80f9-0ebabb8fd94f
exl-id: efbba312-9fc8-4670-b8f1-d2a86162d075
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2718'
ht-degree: 1%

---

# 如何使用VLT工具 {#how-to-use-the-vlt-tool}

Jackrabbit FileVault工具(VLT)是由 [Apache Foundation](https://www.apache.org/) 將Jackrabbit/AEM例項的內容對應至您的檔案系統。 VLT工具具有類似原始檔控制系統使用者端(例如Subversion (SVN)使用者端)的功能，可提供一般入庫、出庫和管理操作，以及彈性表示專案內容的組態選項。

從命令列執行VLT工具。 本檔案說明如何使用該工具，包括如何開始使用及取得說明，以及所有內容的清單 [命令](#vlt-commands) 和可用 [選項](#vlt-global-options).

## 概念與架構 {#concepts-and-architecture}

請參閱 [Filevault概述](https://jackrabbit.apache.org/filevault/overview.html) 和 [儲存庫FS](https://jackrabbit.apache.org/filevault/vaultfs.html) 來自官方網站的頁面 [Apache Jackrabbit Filevault檔案](https://jackrabbit.apache.org/filevault/index.html) 以全面瞭解Filevault工具的概念和結構。

## VLT快速入門 {#getting-started-with-vlt}

若要開始使用VLT，您必須執行下列動作：

1. 安裝VLT、更新環境變數，以及更新全域忽略的subversion檔案。
1. 設定AEM存放庫（如果尚未這麼做的話）。
1. 檢視AEM存放庫。
1. 與存放庫同步。
1. 測試同步是否有效。

### 安裝VLT工具 {#installing-the-vlt-tool}

若要使用VLT工具，您必須先安裝它。 預設不會安裝，因為它是其他工具。 此外，您需要設定系統的環境變數。

1. 下載FileVault封存檔案(從 [Maven成品存放庫。](https://repo1.maven.org/maven2/org/apache/jackrabbit/vault/vault-cli/)
   >[!NOTE]
   >
   >VLT工具的來源為 [可在GitHub上取得。](https://github.com/apache/jackrabbit-filevault)
1. 擷取封存。
1. 新增 `<archive-dir>/vault-cli-<version>/bin` 至您的環境 `PATH` 讓命令檔案 `vlt` 或 `vlt.bat` 會適當地存取。 例如：

   `<aem-installation-dir>/crx-quickstart/opt/helpers/vault-cli-3.1.16/bin>`

1. 開啟命令列shell並執行 `vlt --help`. 確認輸出內容與下列說明畫面類似：

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

安裝之後，您需要更新全域忽略的subversion檔案。 編輯您的svn設定並新增下列專案：

```xml
[miscellany]
### Set global-ignores to a set of whitespace-delimited globs
### which Subversion will ignore in its 'status' output, and
### while importing or adding files and directories.
global-ignores = .vlt
```

### 設定行尾字元 {#configuring-the-end-of-line-character}

VLT會根據下列規則自動處理行尾(EOF)：

* 在Windows上出庫的檔案行結尾是 `CRLF`
* 在Linux/Unix上出庫的檔案行結尾是 `LF`
* 提交到存放庫的檔案行以 `LF`

為確保VLT和SVN組態相符，您應設定 `svn:eol-style` 屬性至 `native` 存放庫中儲存檔案的副檔名。 編輯您的svn設定並新增下列專案：

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

### 出庫存放庫 {#checking-out-the-repository}

使用原始檔控制系統出庫存放庫。 例如，在svn中，輸入以下內容（將URI和路徑替換為存放庫）：

```shell
svn co https://svn.server.com/repos/myproject
```

### 與存放庫同步 {#synchronizing-with-the-repository}

您需要將filevault與存放庫同步。 要执行此操作：

1. 在命令列中，導覽至 `content/jcr_root`.
1. 鍵入以下內容(將您的連線埠號碼替換為 **4502** 以及您的管理員密碼)：

   ```shell
   vlt --credentials admin:admin co --force http://localhost:4502/crx
   ```

   >[!NOTE]
   >
   >憑證只需在初次結帳時指定一次。 然後會儲存在內部的主目錄中 `.vault/auth.xml`.

### 測試同步是否有效 {#testing-whether-the-synchronization-worked}

簽出存放庫並同步化它後，您應該進行測試以確定所有專案皆正常運作。 一個簡單的方法是編輯 **.jsp** 並檢視確認變更後是否反映變更。

若要測試同步化：

1. 导航到 `.../jcr_content/libs/foundation/components/text`。
1. 在中編輯內容 `text.jsp`.
1. 透過輸入檢視修改的檔案 `vlt st`
1. 透過輸入檢視變更 `vlt diff text.jsp`
1. 提交變更： `vlt ci test.jsp`.
1. 重新載入包含文字元件的頁面，並檢視是否有變更。

## 使用VLT工具取得協助 {#getting-help-with-the-vlt-tool}

安裝VLT工具後，您可以從命令列存取其「說明」檔案：

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

如需特定命令的說明，請輸入help命令，後面接著命令的名稱。 例如：

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

## 在VLT中執行的常見工作 {#common-tasks-performed-in-vlt}

以下是VLT中執行的一些常見工作。 如需每個指令的詳細資訊，請參閱個別的 [命令](#vlt-commands).

### 出庫子樹狀結構 {#checking-out-a-subtree}

例如，如果您只想出庫存放庫的子樹狀結構， `/apps/geometrixx`，您可以輸入下列內容來完成此操作：

```shell
vlt co http://localhost:4502/crx/-/jcr:root/apps/geometrixx geo
```

這麼做會建立新的匯出根目錄 `geo` 搭配 `META-INF` 和 `jcr_root` 目錄，並將所有檔案放在下方 `/apps/geometrixx` 在 `geo/jcr_root`.

### 執行篩選的簽出 {#performing-a-filtered-checkout}

如果您有現有的工作區篩選器，而且想要將它用於出庫，您可以先建立 `META-INF/vault` 目錄，並將篩選條件放在該處，或在命令列上指定，如下所示：

```shell
$ vlt co --filter filter.xml http://localhost:4502/crx/-/jcr:root geo
```

範例篩選條件：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<workspaceFilter version="1.0">
    <filter root="/etc/designs/geometrixx" />
    <filter root="/apps/geometrixx"/>
</workspaceFilter>
```

### 使用匯入/匯出而不是.vlt控制項 {#using-import-export-instead-of-vlt-control}

您無需使用控制檔，即可在JCR存放庫與本機檔案系統之間匯入和匯出內容。

若要匯入和匯出內容而不使用 `.vlt` 控制：

1. 最初設定存放庫：

   ```shell
   $ cd /projects
   $ svn mkdir https://svn.server.com/repos/myproject
   $ svn co https://svn.server.com/repos/myproject
   $ vlt export -v http://localhost:4502/crx /apps/geometrixx geometrixx
   $ cd geometrixx/
   $ svn add META-INF/ jcr_root/
   $ svn ci
   ```

1. 變更遠端複製並更新JCR：

   ```shell
   $ cd /projects/geometrixx
   $ vlt -v import http://localhost:4502/crx . /
   ```

1. 變更遠端復本並更新檔案伺服器：

   ```shell
   $ cd /projects/geometrixx
   $ vlt export -v http://localhost:4502/crx /apps/geometrixx .
   $ svn st
   M      META-INF/vault/properties.xml
   M      jcr_root/apps/geometrixx/components/contentpage/.content.xml
   $ svn ci
   ```

## 使用VLT {#using-vlt}

若要在VLT中發出指令，請在指令行中輸入下列內容：

```shell
vlt [options] <command> [arg1 [arg2 [arg3] ..]]  
```

以下各節將詳細說明選項和指令。

## VLT全域選項 {#vlt-global-options}

以下列出可用於所有指令的VLT選項。 如需其他可用選項的資訊，請參閱個別命令。

|  |  |
|--- |--- |
| 选项 | 描述 |
| `-Xjcrlog <arg>` | 延伸的JcrLog選項 |
| `-Xdavex <arg>` | 延伸JCR遠端選項 |
| `--credentials <arg>` | 要使用的預設認證 |
| `--config <arg>` | 要使用的JcrFs設定 |
| `-v (--verbose)` | 詳細輸出 |
| `-q (--quiet)` | 儘可能減少列印 |
| `--version` | 列印版本資訊並結束VLT |
| `--log-level <level>` | 指示記錄層級，例如log4j記錄層級。 |
| `-h (--help) <command>` | 列印該特定命令的說明 |

## VLT指令 {#vlt-commands}

下表說明所有可用的VLT指令。 如需語法、可用選項和範例的詳細資訊，請參閱個別命令。

|  |  |  |
|--- |--- |--- |
| 命令 | 縮寫命令 | 描述 |
| `export` |  | 從JCR儲存庫（儲存庫檔案系統）匯出至本機檔案系統，而不使用控制檔。 |
| `import` |  | 將本機檔案系統匯入至JCR存放庫（儲存庫檔案系統）。 |
| `checkout` | `co` | 出庫儲存庫檔案系統。 使用此項可將初始JCR存放庫用於本機檔案系統。 （注意：您必須先出庫subversion中的存放庫。） |
| `analyze` |  | 分析封裝。 |
| `status` | `st` | 列印工作復本檔案和目錄的狀態。 |
| `update` | `up` | 將變更從存放庫匯入至工作復本。 |
| `info` |  | 顯示本機檔案的相關資訊。 |
| `commit` | `ci` | 將工作復本中的變更傳送至存放庫。 |
| `revert` | `rev` | 將工作復本檔案還原成原始狀態，並取消大部分的本機編輯。 |
| `resolved` | `res` | 移除工作復本檔案或目錄上的衝突狀態。 |
| `propget` | `pg` | 在檔案或目錄上列印屬性的值。 |
| `proplist` | `pl` | 列印檔案或目錄上的屬性。 |
| `propset` | `ps` | 設定檔案或目錄上的屬性值。 |
| `add` |  | 將檔案和目錄置於版本控制之下。 |
| `delete` | `del` 或 `rm` | 從版本控制中移除檔案和目錄。 |
| `diff` | `di` | 顯示兩個路徑之間的差異。 |
| `console` |  | 執行互動式主控台。 |
| `rcp` |  | 將節點樹從一個遠端存放庫複製到另一個存放庫。 |
| `sync` |  | 允許控制儲存庫同步服務。 |

### 导出 {#export}

匯出掛載於 &lt;uri> 至本機檔案系統，位於 &lt;local-path>. 選填 &lt;jcr-path> 可以指定以僅匯出子樹狀結構。

#### 語法 {#syntax}

```shell
export -v|-t <arg>|-p <uri> <jcr-path> <local-path>
```

#### 选项 {#options}

|  |  |
|--- |--- |
| `-v (--verbose)` | 詳細輸出 |
| `-t (--type) <arg>` | 指定匯出型別（platform或jar）。 |
| `-p (--prune-missing)` | 指定是否應該刪除遺失的本機檔案 |
| `<uri>` | 掛接點URI |
| `<jcrPath>` | JCR路徑 |
| `<localPath>` | 本機路徑 |

#### 示例 {#examples}

```shell
vlt export http://localhost:4502/crx /apps/geometrixx myproject
```

### 导入 {#import}

匯入本機檔案系統(從 `<local-path>` 至儲存庫檔案系統，位於 `<uri>`. 您可以指定 `<jcr-path>` 作為匯入根目錄。 若 `--sync` 指定後，匯入的檔案會自動置於儲存庫控制之下。

#### 語法 {#syntax-1}

```shell
import -v|-s <uri> <local-path> <jcr-path>
```

#### 选项 {#options-1}

|  |  |
|--- |--- |
| `-v (--verbose)` | 詳細輸出 |
| `-s (-- sync)` | 將本機檔案置於儲存庫控制之下 |
| `<uri>` | 掛接點URI |
| `<jcrPath>` | JCR路徑 |
| `<localPath>` | 本機路徑 |

#### 示例 {#examples-1}

```shell
vlt import http://localhost:4502/crx . /
```

### 結帳(co) {#checkout-co}

從JCR存放庫到本機檔案系統的初始簽出開始於 &lt;uri> 至本機檔案系統，位於 &lt;local-path>. 您也可以新增 &lt;jcrpath> 用來出庫遠端樹狀結構的子目錄的引數。 可以指定複製到META-INF目錄的工作區篩選器。

#### 語法 {#syntax-2}

```shell
checkout --force|-v|-q|-f <file> <uri> <jcrPath> <localPath>  
```

#### 选项 {#options-2}

|  |  |
|--- |--- |
| `--force` | 強制籤出以覆寫本機檔案（如果已經存在） |
| `-v (--verbose)` | 詳細輸出 |
| `-q (--quiet)` | 儘量少列印 |
| `-f (--filter) <file>` | 如果未定義任何專案，則指定自動篩選 |
| `<uri>` | 掛接點URI |
| `<jcrPath>` | （選擇性）遠端路徑 |
| `<localPath>` | （選用）本機路徑 |

#### 示例 {#examples-2}

使用JCR Remoting：

```shell
vlt --credentials admin:admin co http://localhost:8080/crx/server/crx.default/jcr_root/
```

使用預設工作區：

```shell
vlt --credentials admin:admin co http://localhost:8080/crx/server/-/jcr_root/
```

如果URI不完整，則會展開：

```shell
vlt --credentials admin:admin co http://localhost:8080/crx
```

### 分析 {#analyze}

分析封裝。

#### 語法 {#syntax-3}

```shell
analyze -l <format>|-v|-q <localPaths1> [<localPaths2> ...]
```

#### 选项 {#options-3}

|  |  |
|--- |--- |
| `-l (--linkFormat) <format>` | hotfix連結（名稱、id）的printf格式，例如 `[CQ520_HF_%s|%s]` |
| `-v (--verbose)` | 詳細輸出 |
| `-q (--quiet)` | 儘量少列印 |
| `<localPaths> [<localPaths> ...]` | 本機路徑 |

### 状态 {#status}

列印工作復本檔案和目錄的狀態。

若 `--show-update` 會指定，每個檔案都會根據遠端版本進行檢查。 第二個字母接著會指定更新操作將執行的動作。

#### 語法 {#syntax-4}

```shell
status -v|-q|-u|-N <file1> [<file2> ...]
```

#### 选项 {#options-4}

|  |  |
|--- |--- |
| `-v (--verbose)` | 詳細輸出 |
| `-q (--quiet)` | 儘量少列印 |
| `-u (--show-update)` | 顯示更新資訊 |
| `-N (--non-recursive)` | 在單一目錄中運作 |
| `<file> [<file> ...]` | 顯示狀態的檔案或目錄 |

### 更新 {#update}

將變更從存放庫複製到工作復本。

#### 語法 {#syntax-5}

```shell
update -v|-q|--force|-N <file1> [<file2> ...]
```

#### 选项 {#options-5}

|  |  |
|--- |--- |
| `-v (--verbose)` | 詳細輸出 |
| `-q (--quiet)` | 儘量少列印 |
| `--force` | 強制覆寫本機檔案 |
| `-N (--non-recursive)` | 在單一目錄中運作 |
| `<file> [<file> ...]` | 要更新的檔案或目錄 |

### 信息 {#info}

顯示本機檔案的相關資訊。

#### 語法 {#syntax-6}

```shell
info -v|-q|-R <file1> [<file2> ...]
```

#### 选项 {#options-6}

|  |  |
|--- |--- |
| `-v (--verbose)` | 詳細輸出 |
| `-q (--quiet)` | 儘量少列印 |
| `-R (--recursive)` | 操作遞回 |
| `<file> [<file> ...]` | 要顯示資訊的檔案或目錄 |

### 提交 {#commit}

將工作復本中的變更傳送至存放庫。

#### 語法 {#syntax-7}

```shell
commit -v|-q|--force|-N <file1> [<file2> ...]
```

#### 选项 {#options-7}

|  |  |
|--- |--- |
| `-v (--verbose)` | 詳細輸出 |
| `-q (--quiet)` | 儘量少列印 |
| `--force` | 即使遠端副本已修改，仍強制提交 |
| `-N (--non-recursive)` | 在單一目錄中運作 |
| `<file> [<file> ...]` | 要提交的檔案或目錄 |

### 还原 {#revert}

將工作復本檔案還原為原始狀態，並取消大部分的本機編輯。

#### 語法 {#syntax-8}

```shell
revert -q|-R <file1> [<file2> ...]
```

#### 选项 {#options-8}

|  |  |
|--- |--- |
| `-q (--quiet)` | 儘量少列印 |
| `-R (--recursive)` | 遞減遞減 |
| `<file> [<file> ...]` | 要提交的檔案或目錄 |

### 已解决 {#resolved}

移除 **衝突** 工作復本檔案或目錄的狀態。

>[!NOTE]
>
>這個指令不會從語義上解決衝突或移除衝突標籤；它只會移除與衝突相關的成品檔案，並允許再次提交PATH。

#### 語法 {#syntax-9}

```shell
resolved -q|-R|--force <file1> [<file2> ...]  
```

#### 选项 {#options-9}

|  |  |
|--- |--- |
| `-q (--quiet)` | 儘量少列印 |
| `-R (--recursive)` | 遞減遞減 |
| `--force` | 解析，即使有衝突標籤 |
| `<file> [<file> ...]` | 要解析的檔案或目錄 |

### Propget {#propget}

在檔案或目錄上列印屬性的值。

#### 語法 {#syntax-10}

```shell
propget -q|-R <propname> <file1> [<file2> ...]
```

#### 选项 {#options-10}

|  |  |
|--- |--- |
| `-q (--quiet)` | 儘量少列印 |
| `-R (--recursive)` | 遞減遞減 |
| `<propname>` | 屬性名稱 |
| `<file> [<file> ...]` | 要從中取得屬性的檔案或目錄 |

### Proplist {#proplist}

列印檔案或目錄上的屬性。

#### 語法 {#syntax-11}

```shell
proplist -q|-R <file1> [<file2> ...]
```

#### 选项 {#options-11}

|  |  |
|--- |--- |
| `-q (--quiet)` | 儘量少列印 |
| `-R (--recursive)` | 遞減遞減 |
| `<file> [<file> ...]` | 要列出其屬性的檔案或目錄 |

### Propset {#propset}

設定檔案或目錄上的屬性值。

>[!NOTE]
>
>VLT可辨識下列特殊版本化屬性：
>
>`vlt:mime-type`
>
>檔案的mimetype。 用於決定是否合併檔案。 以「text/」（或不存在mimetype）開頭的mimetype被視為文字。 任何其他專案都會視為二進位。

#### 語法 {#syntax-12}

```shell
propset -q|-R <propname> <propval> <file1> [<file2> ...]
```

#### 选项 {#options-12}

|  |  |
|--- |--- |
| `-q (--quiet)` | 儘量少列印 |
| `-R (--recursive)` | 遞減遞減 |
| `<propname>` | 屬性名稱 |
| `<propval>` | 屬性值 |
| `<file> [<file> ...]` | 要設定屬性的檔案或目錄 |

### 添加 {#add}

將檔案和目錄置於版本控制之下，並排程將其加入存放庫。 它們將在下次認可時新增。

#### 語法 {#syntax-13}

```shell
add -v|-q|-N|--force <file1> [<file2> ...]
```

#### 选项 {#options-13}

|  |  |
|--- |--- |
| `-v (--verbose)` | 詳細輸出 |
| `-q (--quiet)` | 儘量少列印 |
| `-N (--non-recursive)` | 在單一目錄中運作 |
| `--force` | 強制執行作業 |
| `<file> [<file> ...]` | 要新增的本機檔案或目錄 |

### 删除 {#delete}

從版本控制中移除檔案和目錄。

#### 語法 {#syntax-14}

```shell
delete -v|-q|--force <file1> [<file2> ...]
```

#### 选项 {#options-14}

|  |  |
|--- |--- |
| `-v (--verbose)` | 詳細輸出 |
| `-q (--quiet)` | 儘量少列印 |
| `--force` | 強制執行作業 |
| `<file> [<file> ...]` | 要刪除的本機檔案或目錄 |

### 差异 {#diff}

顯示兩個路徑之間的差異。

#### 語法 {#syntax-15}

```shell
diff -N <file1> [<file2> ...]
```

#### 选项 {#options-15}

|  |  |
|--- |--- |
| `-N (--non-recursive)` | 在單一目錄中運作 |
| `<file> [<file> ...]` | 要顯示差異的檔案或目錄 |

### 控制台 {#console}

執行互動式主控台。

#### 語法 {#syntax-16}

```shell
console -F <file>
```

#### 选项 {#options-16}

|  |  |
|--- |--- |
| `-F (--console-settings) <file>` | 指定主控台設定檔。 預設檔案為console.properties。 |

### Rcp {#rcp}

將節點樹從一個遠端存放庫複製到另一個存放庫。 `<src>` 指向來源節點和 `<dst>` 指定父節點必須存在的目的地路徑。 Rcp會透過串流資料來處理節點。

#### 語法 {#syntax-17}

```shell
rcp -q|-r|-b <size>|-t <seconds>|-u|-n|-e <arg1> [<arg2> ...] <src> <dst>
```

#### 选项 {#options-17}

|  |  |
|--- |--- |
| `-q (--quiet)` | 儘量少列印。 |
| `-r (--recursive)` | 遞回遞減。 |
| `-b (--batchSize) <size>` | 中繼儲存前要處理的節點數目。 |
| `-t (--throttle) <seconds>` | 中繼儲存後等待的秒數。 |
| `-u (--update)` | 覆寫/刪除現有節點。 |
| `-n (--newer)` | 遵守lastModified屬性以進行更新。 |
| `-e (--exclude) <arg> [<arg> ...]` | 排除的來源路徑的規則運算式。 |
| `<src>` | 來源樹狀結構的存放庫位址。 |
| `<dst>` | 目的地節點的存放庫位址。 |

#### 示例 {#examples-3}

```shell
vlt rcp http://localhost:4502/crx/-/jcr:root/content  https://admin:admin@localhost:4503/crx/-/jcr:root/content_copy  
```

>[!NOTE]
>
>此 `--exclude` 選項後面必須接著另一個選項，才能執行 `<src>` 和 `<dst>` 引數。 例如：
>
>`vlt rcp -e ".*\.txt" -r`

### 同步 {#sync}

允許控制儲存庫同步服務。 這個命令會嘗試將目前的工作目錄置於同步控制之下，而不使用任何引數。 如果在vlt簽出中執行，它會使用各自的篩選器和主機來設定同步。 如果在vlt出庫之外執行，則只有在目錄為空時，它才會註冊目前資料夾進行同步處理。

#### 語法 {#syntax-18}

```shell
sync -v|--force|-u <uri> <command> <localPath>
```

#### 选项 {#options-18}

|  |  |
|--- |--- |
| `-v (--verbose)` | 詳細輸出。 |
| `--force` | 強制執行某些指令。 |
| `-u (--uri) <uri>` | 指定同步處理主機的URI。 |
| `<command>` | 同步命令以執行。 |
| `<localPath>` | 要同步的本機資料夾。 |

### 狀態代碼 {#status-codes}

VLT使用的狀態代碼為：

* &#39; &#39;無修改
* &#39;A&#39;已新增
* &#39;C&#39;衝突
* &#39;D&#39;已刪除
* 已忽略&#39;I&#39;
* &#39;M&#39;已修改
* 已取代&#39;R&#39;
* &#39;？&#39; 專案不受版本控制
* &#39;!&#39; 專案遺失（由非svn命令移除）或不完整
* &#39;~&#39;版本化專案被其他型別的專案阻擋

## 設定FileVault同步 {#setting-up-filevault-sync}

儲存庫同步服務用於將存放庫內容與本機檔案系統表示進行同步，反之亦然。 這是透過安裝OSGi服務來達成，該服務將監聽存放庫變更並定期掃描檔案系統內容。 它使用與儲存庫相同的序列化格式將存放庫內容對應到磁碟。

>[!NOTE]
>
>儲存庫同步服務是一種開發工具，強烈建議不要將其用於高生產力的系統。 另請注意，此服務只能與本機檔案系統同步，不能用於遠端開發。

### 使用vlt安裝服務 {#installing-the-service-using-vlt}

此 `vlt sync install` 命令可用來自動安裝儲存庫同步服務套件和設定。

套件組合會安裝在底下 `/libs/crx/vault/install` 且設定節點建立於 `/libs/crx/vault/com.day.jcr.sync.impl.VaultSyncServiceImpl`. 最初啟用服務，但未設定同步處理根目錄。

以下範例會將同步服務安裝至特定URI可存取的CRX執行個體。

```shell
$ vlt --credentials admin:admin sync --uri http://localhost:4502/crx install
```

### 顯示服務狀態 {#displaying-the-service-status}

此 `status` 命令可用來顯示有關執行中同步服務的資訊。&quot;

```shell
$ vlt sync status --uri http://localhost:4502/crx
Connecting via JCR remoting to http://localhost:4502/crx/server
Listing sync status for http://localhost:4502/crx/server/-/jcr:root
- Sync service is enabled.
- No sync directories configured.
```

>[!NOTE]
>
>此 `status` 命令不會從服務擷取任何即時資料，而是讀取設定 `/libs/crx/vault/com.day.jcr.sync.impl.VaultSyncServiceImpl`.

### 新增同步資料夾 {#adding-a-sync-folder}

此 `register` 命令用於新增資料夾以同步至設定。

```shell
$ vlt sync register
Connecting via JCR remoting to http://localhost:4502/crx/server
Added new sync directory: /tmp/workspace/vltsync/jcr_root
```

>[!NOTE]
>
>此 `register` 命令不會觸發同步處理，直到您設定 `sync-once` 設定。

### 移除同步資料夾 {#removing-a-sync-folder}

此 `unregister` 命令用於從設定中移除要同步的資料夾。

```shell
$  vlt sync unregister
Connecting via JCR remoting to http://localhost:4502/crx/server
Removed sync directory: /tmp/workspace/vltsync/jcr_root
```

>[!NOTE]
>
>您必須先取消註冊同步資料夾，才能刪除資料夾本身。

### 設定同步 {#configuring-synchronization}

#### 服務設定 {#service-configuration}

服務執行後，可使用下列引數設定服務：

* `vault.sync.syncroots`：定義同步根的一或多個本機檔案系統路徑。

* `vault.sync.fscheckinterval`：應掃描檔案系統的變更頻率（以秒為單位）。 預設值為5秒。
* `vault.sync.enabled`：啟用/停用服務的一般標幟。

>[!NOTE]
>
>此服務可以使用Web主控台或 `sling:OsgiConfig` 節點(具有名稱 `com.day.jcr.sync.impl.VaultSyncServiceImpl`)。
>
>使用AEM時，有數種方法可管理此類服務的組態設定；請參閱 [設定OSGi](/help/sites-deploying/configuring-osgi.md) 以取得完整詳細資訊。

#### 同步資料夾設定 {#sync-folder-configuration}

每個同步資料夾都會將設定和狀態儲存在三個檔案中：

* `.vlt-sync-config.properties`：設定檔案。

* `.vlt-sync.log`：記錄檔，其中包含同步期間所執行操作的相關資訊。
* `.vlt-sync-filter.xml`：定義要同步存放庫哪些部分的篩選器。 此檔案的格式由 [執行篩選的簽出](#performing-a-filtered-checkout) 區段。

此 `.vlt-sync-config.properties` 檔案可讓您設定下列屬性：

**已停用** 開啟或關閉同步化。 預設情況下，此引數會設為false以允許同步。

**同步一次** 如果不為空，則下次掃描會以指定方向同步資料夾，然後清除引數。 支援兩個值：

* `JCR2FS`：匯出JCR存放庫中的所有內容，並寫入本機磁碟。
* `FS2JCR`：將所有內容從磁碟匯入至JCR存放庫。

**同步記錄** 定義記錄檔檔案名稱。 預設值為.vlt-sync.log

### 使用VLT同步進行開發 {#using-vlt-sync-for-development}

若要根據同步資料夾設定開發環境，請依照下列步驟進行：

1. 使用vlt命令列簽出您的存放庫：

   ```shell
   $ vlt --credentials admin:admin co --force http://localhost:4502/crx dev
   ```

   >[!NOTE]
   >
   >您可以使用篩選器來僅簽出適當的路徑。 請參閱 [執行篩選的簽出](#performing-a-filtered-checkout) 區段以取得資訊。

1. 前往工作復本的根資料夾：

   ```shell
   $ cd dev/jcr_root/
   ```

1. 將同步服務安裝至存放庫：

   ```xml
   $ vlt sync install
   Connecting via JCR remoting to http://localhost:4502/crx/server
   Preparing to install vault-sync-2.4.24.jar...
   Updated bundle: vault-sync-2.4.24.jar
   Created new config at /libs/crx/vault/config/com.day.jcr.sync.impl.VaultSyncServiceImpl
   ```

1. 初始化同步服務：

   ```shell
   $ vlt sync
   Connecting via JCR remoting to http://localhost:4502/crx/server
   Starting initialization of sync service in existing vlt checkout /Users/colligno/Applications/cq5/vltsync/sandbox/dev/jcr_root for http://localhost:4502/crx/server/-/jcr:root
   Added new sync directory: /Users/trushton/Applications/aem/vltsync/sandbox/dev/jcr_root
   
   The directory /Users/trushton/Applications/aem/vltsync/sandbox/dev/jcr_root is now enabled for syncing.
   You might perform a 'sync-once' by setting the
   appropriate flag in the /Users/trushton/Applications/aem/vltsync/sandbox/dev/jcr_root/.vlt-sync-config.properties file.
   ```

1. 編輯 `.vlt-sync-config.properties` 隱藏檔案並設定同步以同步存放庫的內容：

   ```xml
   sync-once=JCR2FS
   ```

   >[!NOTE]
   >
   >此步驟會根據您的篩選器設定下載整個存放庫。

1. 檢查記錄檔 `.vlt-sync.log` 若要檢視進度：

   ```xml
   ***
   30.04.2017 14:39:10 A file:///Users/trushton/Applications/aem/vltsync/sandbox/dev/jcr_root/apps/geometrixx-outdoors/src/core/src/main/java/info/geometrixx/outdoors/
   30.04.2017 14:39:10 A file:///Users/trushton/Applications/aem/vltsync/sandbox/dev/jcr_root/apps/geometrixx-outdoors/src/core/src/main/java/info/geometrixx/outdoors/core/
   30.04.2017 14:39:10 A file:///Users/trushton/Applications/aem/vltsync/sandbox/dev/jcr_root/apps/geometrixx-outdoors/src/core/src/main/java/info/geometrixx/outdoors/core/product/
   30.04.2017 14:39:10 A file:///Users/trushton/Applications/aem/vltsync/sandbox/dev/jcr_root/apps/geometrixx-outdoors/src/core/src/main/java/info/geometrixx/outdoors/core/product/GeoProduct.java
   ***
   ```

您的本機資料夾現在與存放庫同步。 同步是雙向的，因此來自存放庫的修改將套用至本機同步資料夾，反之亦然。

>[!NOTE]
>
>VLT同步功能僅支援簡單的檔案和資料夾，但會偵測特殊的儲存庫序列化檔案（.content.xml、dialog.xml等），並自動忽略它們。 因此，可以在預設vlt出庫中使用儲存庫同步。
