---
title: 如何使用IntelliJ IDEA开发AEM项目
description: 了解如何使用IntelliJ IDEA开发Adobe Experience Manager项目。
uuid: 382b5008-2aed-4e08-95be-03c48f2b549e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: df6410a2-794e-4fa2-ae8d-37271274d537
exl-id: 5a79c79b-df65-4cb2-b9d4-eda994c992ec
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 0%

---

# 如何使用IntelliJ IDEA开发AEM项目{#how-to-develop-aem-projects-using-intellij-idea}

## 概述 {#overview}

要开始在IntelliJ上开发AEM，需要执行以下步骤。

本主题的其余部分将更详细地解释每个步骤。

* 安装IntelliJ
* 基于Maven设置您的AEM项目
* 在Maven POM中为IntelliJ准备JSP支持
* 将Maven项目导入IntelliJ

>[!NOTE]
>
>本指南基于IntelliJ IDEA Ultimate Edition 12.1.4和AEM 5.6.1。

### 安装IntelliJ IDEA {#install-intellij-idea}

下载IntelliJ IDEA [JetBrains的“下载”页面](https://www.jetbrains.com/idea/download/).

然后，按照该页面上的安装说明进行操作。

### 基于Maven设置您的AEM项目 {#set-up-your-aem-project-based-on-maven}

接下来，使用Maven设置项目，如中所述 [如何使用Apache Maven构建AEM项目](/help/sites-developing/ht-projects-maven.md).

要在IntelliJ IDEA中开始使用AEM项目，需了解 [5分钟后开始使用](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html) 就足够了。

### 为IntelliJ IDEA准备JSP支持 {#prepare-jsp-support-for-intellij-idea}

IntelliJ IDEA还可以在使用JSP时提供支持，例如：

* 自动完成标记库
* 感知由定义的对象 `<cq:defineObjects />` 和 `<sling:defineObjects />`

要使其生效，请按照 [如何使用JSP](/help/sites-developing/ht-projects-maven.md#how-to-work-with-jsps) 在 [如何使用Apache Maven构建AEM项目](/help/sites-developing/ht-projects-maven.md).

### 导入Maven项目 {#import-the-maven-project}

1. 打开 **导入** IntelliJ IDEA中的dialogue，作者：

   * 选择 **导入项目** 在欢迎屏幕上（如果尚未打开任何项目）
   * 选择 **文件>导入项目** 从主菜单

1. 在导入对话框中，选择项目的POM文件。

   ![chlimage_1-45](assets/chlimage_1-45a.png)

1. 继续使用默认设置，如下面的对话框中所示。

   ![chlimage_1-46](assets/chlimage_1-46a.png)

1. 通过单击继续下面的对话框 **下一个** 和 **完成**.
1. 现在，您已设置使用IntelliJ IDEA进行AEM开发

   ![chlimage_1-47](assets/chlimage_1-47a.png)

### 使用IntelliJ IDEA调试JSP {#debugging-jsps-with-intellij-idea}

使用IntelliJ IDEA调试JSP时，必须执行以下步骤

* 在项目中设置Web Facet
* 安装JSR45支持插件
* 配置调试配置文件
* 为调试模式配置AEM

#### 在项目中设置Web Facet {#set-up-a-web-facet-in-the-project}

IntelliJ IDEA必须了解在何处查找用于调试的JSP。 因为IDEA无法解释 `content-package-maven-plugin` 设置，则必须手动进行配置。

1. 转到 **文件>项目结构**
1. 选择 **内容** 模块
1. 单击 **+** 在模块列表上方并选择 **Web**
1. 作为Web资源目录，选择 `content/src/main/content/jcr_root subdirectory` ，如下面的屏幕快照所示。

![chlimage_1-48](assets/chlimage_1-48a.png)

#### 安装JSR45支持插件 {#install-the-jsr-support-plugin}

1. 转到 **插件** IntelliJ IDEA设置中的窗格
1. 导航至 **JSR45集成** 插件，然后选中它旁边的复选框
1. 单击 **应用**
1. 请求时重新启动IntelliJ IDEA

![chlimage_1-49](assets/chlimage_1-49a.png)

#### 配置调试配置文件 {#configure-a-debug-profile}

1. 转到 **运行>编辑配置**
1. 点击 **+** 并选择 **JSR45远程**
1. 在配置对话框中，选择 **配置** 旁边 **应用程序服务器** 并配置通用服务器
1. 如果要在开始调试时打开浏览器，请将起始页设置为适当的URL
1. 全部移除 **启动前** 任务（如果使用vlt自动同步），或配置相应的Maven任务（如果不使用）
1. 在 **启动/连接** 窗格，如有必要，调整端口
1. 复制IntelliJ IDEA建议的命令行参数

![chlimage_1-50](assets/chlimage_1-50a.png) ![chlimage_1-51](assets/chlimage_1-51a.png)

#### 为调试模式配置AEM {#configure-aem-for-debug-mode}

最后一步是使用IntelliJ IDEA提出的JVM选项启动AEM。

直接启动AEM jar文件并添加这些选项，例如，使用以下命令行：

`java -Xdebug -Xrunjdwp:transport=dt_socket,address=58242,suspend=n,server=y -Xmx1024m -jar cq-quickstart-6.5.0.jar`

您还可以将这些选项添加到中的启动脚本 `crx-quickstart/bin/start` 如下所示。

```shell
# ...

# default JVM options
if [ -z "$CQ_JVM_OPTS" ]; then
 CQ_JVM_OPTS='-server -Xmx1024m -Djava.awt.headless=true'
fi

CQ_JVM_OPTS="$CQ_JVM_OPTS -Xdebug -Xrunjdwp:transport=dt_socket,address=58242,suspend=n,server=y"

# ...
```

#### 开始调试 {#start-debugging}

现在，您已准备好在AEM中调试JSP。

1. 选择 **运行>调试>您的调试配置文件**
1. 在组件代码中设置断点
1. 访问浏览器中的页面

![chlimage_1-52](assets/chlimage_1-52a.png)

### 使用IntelliJ IDEA调试包 {#debugging-bundles-with-intellij-idea}

可以使用标准通用远程调试连接调试捆绑包中的代码。 您可以遵循 [关于远程调试的Jetbrain文档](https://www.jetbrains.com/help/idea/remote-debugging-with-product.html#remote-interpreter).
