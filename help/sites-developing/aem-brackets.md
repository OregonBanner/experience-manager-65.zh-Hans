---
title: AEM Brackets扩展
seo-title: AEM Brackets扩展
description: 'null'
seo-description: 'null'
uuid: 2f0dfa42-eb34-44ae-90eb-b5f321c03b79
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 8231a30a-dcb7-4156-bb45-c5a23e5b56ef
translation-type: tm+mt
source-git-commit: 6d216e7521432468a01a29ad2879f8708110d970

---


# AEM Brackets扩展{#aem-brackets-extension}

## 概述 {#overview}

AEM Brackets扩展提供了一个顺畅的工作流，用于编辑AEM组件和客户端库，并利用 [Brackets](https://brackets.io/) 代码编辑器的强大功能，该编辑器允许从代码编辑器中访问Photoshop文件和图层。 该扩展提供的轻松同步（无需Maven或File Vault）提高了开发人员效率，并帮助AEM知识有限的前端开发人员参与项目。 此扩展还提供对 [HTML模板语言(HTL)的一些支持](https://docs.adobe.com/content/help/en/experience-manager-htl/using/overview.html)，它消除了JSP的复杂性，使组件开发更简单、安全。

![chlimage_1-53](assets/chlimage_1-53a.png)

### 功能 {#features}

AEM Brackets扩展的主要功能有：

* 将更改的文件自动同步到AEM开发实例。
* 手动双向同步文件和文件夹。
* 项目的完整内容包同步。
* 表达式和块语句的HTL代 `data-sly-*` 码完成。

此外，Brackets还为AEM字体端开发人员提供了许多有用的功能：

* Photoshop文件支持从PSD文件提取信息，如图层、度量、颜色、字体、文本等。
* PSD中的代码提示，以便在代码中轻松重复使用此提取的信息。
* CSS预处理器支持，如LESS和SCSS。
* 还有数百个附加扩展，它们涵盖更具体的需求。

## 安装 {#installation}

### 括号 {#brackets}

AEM Brackets扩展支持Brackets版本1.0或更高版本。

从brackets.io下载最 [新的Brackets版本](https://brackets.io/)。

### 扩展 {#the-extension}

要安装扩展，请按如下步骤继续：

1. 打开Brackets。 在菜单 **文件**，选择 **扩展管理器……**
1. 在搜 **索栏中输入AEM** ，然后查找 **AEM Brackets扩展**。

   ![chlimage_1-54](assets/chlimage_1-54a.png)

1. 单击&#x200B;**安装**。
1. 安装完成后，关闭对话框和Extension Manager。

## 入门 {#getting-started}

### 内容包项目 {#the-content-package-project}

安装扩展后，您可以通过使用Brackets从文件系统打开内容包文件夹，开始开发AEM组件。

项目必须至少包含：

1. 文 `jcr_root` 件夹(例如 `myproject/jcr_root`)

1. 文 `filter.xml` 件(例如， `myproject/META-INF/vault/filter.xml`);有关文件结构的更多详细 `filter.xml` 信息，请参阅工 [作区过滤器定义](https://jackrabbit.apache.org/filevault/filter.html)。

在Brackets的“ **文件** ”菜单中，选择“ **打开文件夹……** ”，然后选 `jcr_root` 择文件夹或父项目文件夹。

>[!NOTE]
>
>如果您没有包含内容包的项目，则可以试用 [HTL TodoMVC示例](https://github.com/Adobe-Marketing-Cloud/aem-sightly-sample-todomvc)。 在GitHub上，单击“ **下载ZIP**”，将文件解压到本地，然后按照上面的说明，在Brackets中 `jcr_root` 打开文件夹。 然后，按照以下步骤设置项目设置 **，最后，按照完整内容包同步部分的进一步说明，通过执行** Export Content Package **** （导出内容包），将整个包上传到AEM开发实例。
>
>完成这些步骤后，您应能够访问AEM开发实例上的 `/content/todo.html` URL，并可以开始对Brackets中的代码进行修改，并查看在Web浏览器中进行刷新后，更改如何立即同步到AEM服务器。

### 项目设置 {#project-settings}

要与AEM开发实例同步内容，您需要定义项目设置。 这可以通过转到 **AEM菜单** ，选择“项 **目设置……”来完成**

![chlimage_1-55](assets/chlimage_1-55a.png)

项目设置允许定义：

1. 服务器URL(例如， `http://localhost:4502`)
1. 是否允许没有有效HTTPS证书的服务器（不选中，除非需要）
1. 用于同步内容的用户名(例如， `admin`)
1. 用户的密码(例如 `admin`)

## 同步内容 {#synchronizing-content}

AEM Brackets扩展为中定义的筛选规则允许的文件和文件夹提供以下类型的内容同步 `filter.xml`:

### 已更改文件的自动同步 {#automated-synchronization-of-changed-files}

这将仅将Brackets中的更改同步到AEM实例，但绝不会相反。

### 手动双向同步 {#manual-bidirectional-synchronization}

在“项目资源管理器”中，通过右键单击任何文件或文件夹打开上下文菜单，并可以访问“导出到服 **务器** ”或“ **从服务器导入** ”选项。

![chlimage_1-56](assets/chlimage_1-56a.png)

>[!NOTE]
>
>如果选定条目在文件夹之外， `jcr_root` 则禁用“ **导出到服务器”和“从服** 务器导入 **** ”上下文菜单条目。

### 完全内容包同步 {#full-content-package-synchronization}

在 **AEM** 菜单中，“导出内容包 **”或“导** 入内容包 **** ”选项允许将整个项目与服务器同步。

![chlimage_1-57](assets/chlimage_1-57a.png)

### 同步状态 {#synchronization-status}

AEM Brackets扩展在Brackets窗口右侧的工具栏中显示一个通知图标，该图标指示上次同步的状态：

* 绿色——已成功同步所有文件
* 蓝色——同步操作正在进行中
* 黄色——部分文件未同步
* 红色——未同步任何文件

单击通知图标将打开“同步状态”报告对话框，其中列出了每个同步文件的所有状态。

![chlimage_1-58](assets/chlimage_1-58a.png)

>[!NOTE]
>
>无论使用何种同步方法，都将只同步标记为 `filter.xml` 包含在过滤规则中的内容。
>
>此外， `.vltignore` 支持将内容排除在与存储库同步之外的文件。

## 编辑HTL代码 {#editing-htl-code}

AEM Brackets扩展还具有一些自动完成功能，可轻松编写HTL属性和表达式。

### 属性自动完成 {#attribute-auto-completion}

1. 在HTML属性中，键入 `sly`。 属性将自动完成为 `data-sly-`。
1. 在下拉列表中选择HTL属性。

### 表达式自动完成 {#expression-auto-completion}

在表达式 `${}`中，公用变量名称是自动完成的。

## 更多信息 {#more-information}

AEM Brackets Extension是一个开放源项目，由 [Adobe Marketing Cloud](https://github.com/Adobe-Marketing-Cloud) Organization根据Apache许可证（版本2.0）在GitHub上托管：

* 代码存储库： [https://github.com/Adobe-Marketing-Cloud/aem-sightly-brackets-extension](https://github.com/Adobe-Marketing-Cloud/aem-sightly-brackets-extension)
* Apache License，版本2.0: [https://www.apache.org/licenses/LICENSE-2.0.html](https://www.apache.org/licenses/LICENSE-2.0.html)

Brackets代码编辑器也是一个开放源码项目，由 [Adobe Systems Incorporated组织在GitHub上托管](https://github.com/adobe) :

* 代码存储库： [https://github.com/adobe/brackets](https://github.com/adobe/brackets)

尽情贡献吧！
