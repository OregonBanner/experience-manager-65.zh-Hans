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
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '931'
ht-degree: 1%

---


# AEM Brackets Extension{#aem-brackets-extension}

## 概述 {#overview}

AEM Brackets扩展提供了编辑AEM组件和客户端库的流畅工作流程，并利用了[Brackets](https://brackets.io/)代码编辑器的强大功能，该编辑器允许从代码编辑器中访问Photoshop文件和图层。 扩展提供的轻松同步（无需Maven或File Vault）提高了开发人员的效率，还有助于具有有限AEM知识的前端开发人员参与项目。 此扩展还提供对[HTML模板语言(HTL)](https://docs.adobe.com/content/help/zh-Hans/experience-manager-htl/using/overview.html)的一些支持，这消除了JSP的复杂性，使组件开发更简单、安全。

![chlimage_1-53](assets/chlimage_1-53a.png)

### 功能 {#features}

AEM Brackets扩展的主要功能有：

* 将更改的文件自动同步到AEM开发实例。
* 文件和文件夹的手动双向同步。
* 项目的完整内容包同步。
* 表达式和`data-sly-*`块语句的HTL代码完成。

此外，Brackets还为AEM字体端开发人员提供了许多有用的功能：

* Photoshop文件支持从PSD文件提取信息，如图层、度量、颜色、字体、文本等。
* PSD中的代码提示，以便轻松地在代码中重用提取的信息。
* CSS预处理器支持，如LESS和SCSS。
* 还有数百种其他扩展，可满足更具体的需求。

## 安装{#installation}

### 括号{#brackets}

AEM Brackets扩展支持Brackets 1.0或更高版本。

从[brackets.io](https://brackets.io/)下载最新的Brackets版本。

### 扩展{#the-extension}

要安装扩展，请按如下步骤继续：

1. 打开Bracket。 在菜单&#x200B;**文件**&#x200B;中，选择&#x200B;**Extension Manager...**
1. 在搜索栏中输入&#x200B;**AEM**&#x200B;并查找&#x200B;**AEM Brackets Extension**。

   ![chlimage_1-54](assets/chlimage_1-54a.png)

1. 单击&#x200B;**安装**。
1. 安装完成后关闭对话框和Extension Manager。

## 入门 {#getting-started}

### 内容包项目{#the-content-package-project}

安装扩展后，您可以通过使用Brackets从文件系统打开一个内容包文件夹来开始AEM组件的开发。

项目必须至少包含：

1. `jcr_root`文件夹(例如`myproject/jcr_root`

1. `filter.xml`文件(例如`myproject/META-INF/vault/filter.xml`);有关`filter.xml`文件结构的详细信息，请参阅[工作区过滤器定义](https://jackrabbit.apache.org/filevault/filter.html)。

在Brackets的&#x200B;**File**&#x200B;菜单中，选择&#x200B;**打开文件夹……**&#x200B;并选择`jcr_root`文件夹或父项目文件夹。

>[!NOTE]
>
>如果您没有包含内容包的项目，则可以尝试[HTL TodoMVC Example](https://github.com/Adobe-Marketing-Cloud/aem-sightly-sample-todomvc)。 在GitHub上，单击&#x200B;**下载ZIP**，在本地解压文件，然后按照上面的说明，在Brackets中打开`jcr_root`文件夹。 然后，按照以下步骤设置&#x200B;**项目设置**，最后按照完整内容包同步部分的进一步说明，通过执行&#x200B;**导出内容包**&#x200B;操作，将整个包上传到您的AEM开发实例。
>
>完成这些步骤后，您应可以访问AEM开发实例上的`/content/todo.html` URL，并可以开始对Brackets中的代码进行修改，并查看在Web浏览器中进行刷新后如何立即将更改同步到AEM服务器。

### 项目设置{#project-settings}

要与AEM开发实例同步内容，您需要定义项目设置。 要执行此操作，请转到&#x200B;**AEM**&#x200B;菜单并选择&#x200B;**“项目设置……**

![chlimage_1-55](assets/chlimage_1-55a.png)

项目设置允许定义：

1. 服务器URL(例如`http://localhost:4502`)
1. 是否容忍没有有效HTTPS证书的服务器（除非需要，否则不选中）
1. 用于同步内容的用户名(例如，`admin`)
1. 用户的密码(例如`admin`)

## 正在同步内容{#synchronizing-content}

AEM Brackets扩展为`filter.xml`中定义的过滤规则允许的文件和文件夹提供以下类型的内容同步：

### 自动同步更改的文件{#automated-synchronization-of-changed-files}

这将仅同步从Brackets到AEM实例的更改，但不会相反。

### 手动双向同步{#manual-bidirectional-synchronization}

在项目资源管理器中，通过右键单击任何文件或文件夹打开上下文菜单，可以访问&#x200B;**导出到Server**&#x200B;或&#x200B;**从Server**&#x200B;导入选项。

![chlimage_1-56](assets/chlimage_1-56a.png)

>[!NOTE]
>
>如果所选条目位于`jcr_root`文件夹之外，则禁用&#x200B;**导出到Server**&#x200B;和&#x200B;**从Server**&#x200B;导入上下文菜单条目。

### 完整内容包同步{#full-content-package-synchronization}

在&#x200B;**AEM**&#x200B;菜单中，**导出内容包**&#x200B;或&#x200B;**导入内容包**&#x200B;选项允许将整个项目与服务器同步。

![chlimage_1-57](assets/chlimage_1-57a.png)

### 同步状态{#synchronization-status}

AEM Brackets扩展功能在Brackets窗口右侧的工具栏中显示一个通知图标，它指示上次同步的状态：

* 绿色 — 所有文件已成功同步
* 蓝色 — 正在执行同步操作
* 黄色 — 某些文件未同步
* 红色 — 未同步任何文件

单击通知图标将打开“同步状态”报告对话框，其中列表了每个已同步文件的所有状态。

![chlimage_1-58](assets/chlimage_1-58a.png)

>[!NOTE]
>
>将只同步标记为`filter.xml`的筛选规则所包含的内容，而不管使用的同步方法。
>
>此外，支持`.vltignore`文件，以排除与存储库同步或从存储库同步的内容。

## 编辑HTL代码{#editing-htl-code}

AEM Brackets扩展还具有一些自动完成功能，可轻松编写HTL属性和表达式。

### 属性自动完成{#attribute-auto-completion}

1. 在HTML属性中，键入`sly`。 属性自动完成为`data-sly-`。
1. 在下拉列表中选择HTL属性。

### 表达式自动完成{#expression-auto-completion}

在表达式`${}`中，常用变量名称会自动完成。

## 更多信息 {#more-information}

AEM Brackets Extension是一个开放源项目，由[Adobe Marketing Cloud](https://github.com/Adobe-Marketing-Cloud)组织在GitHub上托管，位于Apache许可证版本2.0下：

* 代码存储库：[https://github.com/Adobe-Marketing-Cloud/aem-sightly-brackets-extension](https://github.com/Adobe-Marketing-Cloud/aem-sightly-brackets-extension)
* Apache License，版本2.0:[https://www.apache.org/licenses/LICENSE-2.0.html](https://www.apache.org/licenses/LICENSE-2.0.html)

Brackets代码编辑器也是一个开放源码项目，由[Adobe Systems Incorporated](https://github.com/adobe)组织在GitHub上托管：

* 代码存储库：[https://github.com/adobe/brackets](https://github.com/adobe/brackets)

请随时投稿！
