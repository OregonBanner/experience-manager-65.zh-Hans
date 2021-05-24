---
title: AEM Brackets扩展
seo-title: AEM Brackets扩展
description: AEM Brackets扩展
seo-description: 'null'
uuid: 2f0dfa42-eb34-44ae-90eb-b5f321c03b79
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 8231a30a-dcb7-4156-bb45-c5a23e5b56ef
exl-id: 829d8256-b415-4a44-a353-455ac16950f3
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '931'
ht-degree: 1%

---

# AEM Brackets扩展{#aem-brackets-extension}

## 概述 {#overview}

AEM Brackets扩展提供了一个顺畅的工作流，用于编辑AEM组件和客户端库，并利用[Brackets](https://brackets.io/)代码编辑器的功能，该编辑器允许从代码编辑器中访问Photoshop文件和层。 扩展提供的轻松同步（不需要Maven或File Vault）提高了开发人员的效率，并且还帮助了解有限AEM的前端开发人员参与项目。 此扩展还为[HTML模板语言(HTL)](https://docs.adobe.com/content/help/zh-Hans/experience-manager-htl/using/overview.html)提供了一些支持，它消除了JSP的复杂性，使组件开发更加简单和安全。

![chlimage_1-53](assets/chlimage_1-53a.png)

### 功能 {#features}

AEM Brackets扩展的主要功能包括：

* 将更改的文件自动同步到AEM开发实例。
* 文件和文件夹的手动双向同步。
* 项目的完整内容包同步。
* 表达式和`data-sly-*`块语句的HTL代码完成。

此外，Brackets还为AEM字体端开发人员提供了许多有用功能：

* Photoshop文件支持从PSD文件中提取信息，如图层、测量、颜色、字体、文本等。
* 从PSD中提示代码，以便在代码中轻松重复使用此提取的信息。
* CSS预处理器支持，如LESS和SCSS。
* 另外还有数百个扩展，可满足更具体的需求。

## 安装 {#installation}

### 括号 {#brackets}

AEM Brackets扩展支持Brackets版本1.0或更高版本。

从[brackets.io](https://brackets.io/)下载最新的Brackets版本。

### 扩展{#the-extension}

要安装扩展，请按如下步骤继续操作：

1. 打开括号。 在菜单&#x200B;**File**&#x200B;中，选择&#x200B;**Extension Manager...**
1. 在搜索栏中输入&#x200B;**AEM**&#x200B;并查找&#x200B;**AEM Brackets Extension**。

   ![chlimage_1-54](assets/chlimage_1-54a.png)

1. 单击&#x200B;**安装**。
1. 安装完成后，关闭对话框和Extension Manager。

## 入门 {#getting-started}

### 内容包项目{#the-content-package-project}

安装扩展后，您可以通过从文件系统中使用Brackets打开内容包文件夹来开始开发AEM组件。

项目必须至少包含：

1. `jcr_root`文件夹(例如，`myproject/jcr_root`)

1. `filter.xml`文件(例如，`myproject/META-INF/vault/filter.xml`);有关`filter.xml`文件结构的更多详细信息，请参阅[工作区过滤器定义](https://jackrabbit.apache.org/filevault/filter.html)。

在“括号”的&#x200B;**文件**&#x200B;菜单中，选择&#x200B;**打开文件夹……** ，然后选择`jcr_root`文件夹或父项目文件夹。

>[!NOTE]
>
>如果您自己没有包含内容包的项目，则可以尝试使用[HTL TodoMVC示例](https://github.com/Adobe-Marketing-Cloud/aem-sightly-sample-todomvc)。 在GitHub上，单击&#x200B;**下载ZIP**，从本地解压文件，并按照上面的说明，在Brackets中打开`jcr_root`文件夹。 然后按照以下步骤设置&#x200B;**项目设置**，并最终按照完整内容包同步部分中的进一步说明，通过执行&#x200B;**导出内容包**，将整个包上传到AEM开发实例。
>
>完成这些步骤后，您应该能够访问AEM开发实例上的`/content/todo.html` URL，并且可以开始对Brackets中的代码进行修改，并查看在Web浏览器中刷新后如何将更改立即同步到AEM服务器。

### 项目设置{#project-settings}

要将内容同步到AEM开发实例和从开发实例同步内容，您需要定义项目设置。 可以通过转到&#x200B;**AEM**&#x200B;菜单并选择&#x200B;**项目设置……**&#x200B;来完成此操作

![chlimage_1-55](assets/chlimage_1-55a.png)

项目设置允许定义：

1. 服务器URL(例如`http://localhost:4502`)
1. 是否容忍没有有效HTTPS证书的服务器（如果需要，请取消选中）
1. 用于同步内容的用户名(例如，`admin`)
1. 用户的密码(例如`admin`)

## 正在同步内容{#synchronizing-content}

AEM Brackets扩展为`filter.xml`中定义的筛选规则所允许的文件和文件夹提供了以下类型的内容同步：

### 自动同步已更改的文件{#automated-synchronization-of-changed-files}

这将仅将Brackets中的更改同步到AEM实例，但绝不会相反。

### 手动双向同步{#manual-bidirectional-synchronization}

在项目资源管理器中，通过右键单击任何文件或文件夹来打开上下文菜单，并且可以访问&#x200B;**导出到服务器**&#x200B;或&#x200B;**从服务器**&#x200B;导入选项。

![chlimage_1-56](assets/chlimage_1-56a.png)

>[!NOTE]
>
>如果所选条目在`jcr_root`文件夹之外，则&#x200B;**导出到服务器**&#x200B;和&#x200B;**从服务器**&#x200B;导入上下文菜单条目将被禁用。

### 完全内容包同步{#full-content-package-synchronization}

在&#x200B;**AEM**&#x200B;菜单中，**导出内容包**&#x200B;或&#x200B;**导入内容包**&#x200B;选项允许将整个项目与服务器同步。

![chlimage_1-57](assets/chlimage_1-57a.png)

### 同步状态{#synchronization-status}

AEM Brackets扩展在Brackets窗口右侧的工具栏中显示一个通知图标，指示上次同步的状态：

* 绿色 — 已成功同步所有文件
* 蓝色 — 正在执行同步操作
* 黄色 — 某些文件未同步
* 红色 — 未同步任何文件

单击通知图标将打开同步状态报告对话框，其中列出了每个同步文件的所有状态。

![chlimage_1-58](assets/chlimage_1-58a.png)

>[!NOTE]
>
>无论使用何种同步方法，都只会同步被`filter.xml`的筛选规则中标记为包含的内容。
>
>此外，支持`.vltignore`文件，以排除与存储库进行同步和从存储库进行同步的内容。

## 编辑HTL代码{#editing-htl-code}

AEM Brackets扩展还具有一些自动完成功能，可简化HTL属性和表达式的编写。

### 属性自动完成{#attribute-auto-completion}

1. 在HTML属性中，键入`sly`。 该属性已自动完成到`data-sly-`。
1. 在下拉列表中选择HTL属性。

### 表达式自动完成{#expression-auto-completion}

在表达式`${}`中，将自动填写常用变量名称。

## 更多信息 {#more-information}

AEM Brackets扩展是一个开源项目，由[Adobe Marketing Cloud](https://github.com/Adobe-Marketing-Cloud)组织在GitHub上根据Apache许可证版本2.0托管：

* 代码存储库：[https://github.com/Adobe-Marketing-Cloud/aem-sightly-brackets-extension](https://github.com/Adobe-Marketing-Cloud/aem-sightly-brackets-extension)
* Apache许可证，版本2.0:[https://www.apache.org/licenses/LICENSE-2.0.html](https://www.apache.org/licenses/LICENSE-2.0.html)

Brackets代码编辑器也是一个开源项目，由[Adobe Systems Incorporated](https://github.com/adobe)组织在GitHub上托管：

* 代码存储库：[https://github.com/adobe/brackets](https://github.com/adobe/brackets)

请随时投稿！
