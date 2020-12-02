---
title: 如何使用IntelliJ IDEA开发AEM项目
seo-title: 如何使用IntelliJ IDEA开发AEM项目
description: 使用IntelliJ IDEA开发AEM项目
seo-description: 使用IntelliJ IDEA开发AEM项目
uuid: 382b5008-2aed-4e08-95be-03c48f2b549e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: df6410a2-794e-4fa2-ae8d-37271274d537
translation-type: tm+mt
source-git-commit: b3e1493811176271ead54bae55b1cd0cf759fe71
workflow-type: tm+mt
source-wordcount: '657'
ht-degree: 0%

---


# 如何使用IntelliJ IDEA{#how-to-develop-aem-projects-using-intellij-idea}开发AEM项目

## 概述 {#overview}

要开始在IntelliJ上进行AEM开发，需要执行以下步骤。

每项操作在本“操作方法”的其余部分中都有更详细的说明。

* 安装IntelliJ
* 根据Maven设置AEM项目
* 在Maven POM中为IntelliJ准备JSP支持
* 将Maven项目导入IntelliJ

>[!NOTE]
>
>本指南基于IntelliJ IDEA Ultimate Edition 12.1.4和AEM 5.6.1。

### 安装IntelliJ IDEA {#install-intellij-idea}

从[JetBrains](https://www.jetbrains.com/idea/download/index.html)的“下载”页下载IntelliJ IDEA。

然后，按照该页面上的安装说明操作。

### 根据Maven {#set-up-your-aem-project-based-on-maven}设置AEM项目

接下来，使用Maven设置项目，如[使用Apache Maven](/help/sites-developing/ht-projects-maven.md)构建AEM项目中所述。

要开始在IntelliJ IDEA中使用AEM项目，[5分钟入门](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html)中的基本设置已足够。

### 准备对IntelliJ IDEA {#prepare-jsp-support-for-intellij-idea}的JSP支持

IntelliJ IDEA还可以在使用JSP(例如，

* 标签库的自动完成
* 对由`<cq:defineObjects />`和`<sling:defineObjects />`定义的对象的感知

要使其正常工作，请按照[使用Apache Maven](/help/sites-developing/ht-projects-maven.md)构建AEM项目中[如何使用JSP](/help/sites-developing/ht-projects-maven.md#how-to-work-with-jsps)的说明操作。

### 导入Maven项目{#import-the-maven-project}

1. 通过&#x200B;****

   * 如果尚未打开任何项目，请在欢迎屏幕上选择&#x200B;**导入项目**
   * 从主菜单中选择&#x200B;**文件->导入项目**

1. 在“导入”对话框中，选择项目的POM文件。

   ![chlimage_1-45](assets/chlimage_1-45a.png)

1. 继续使用默认设置，如下面的对话框所示。

   ![chlimage_1-46](assets/chlimage_1-46a.png)

1. 单击&#x200B;**Next**&#x200B;和&#x200B;**Finish**，继续执行以下对话框。
1. 您现在已使用IntelliJ IDEA为AEM Development设置

   ![chlimage_1-47](assets/chlimage_1-47a.png)

### 使用IntelliJ IDEA {#debugging-jsps-with-intellij-idea}调试JSP

使用IntelliJ IDEA调试JSP时，必须执行以下步骤

* 在项目中设置Web彩块化
* 安装JSR45支持插件
* 配置调试用户档案
* 为调试模式配置AEM

#### 在项目{#set-up-a-web-facet-in-the-project}中设置Web Facet

IntelliJ IDEA需要了解在哪里可以找到用于调试的JSP。 由于IDEA无法解释`content-package-maven-plugin`设置，因此需要手动配置。

1. 转至&#x200B;**文件->项目结构**
1. 选择&#x200B;**Content**&#x200B;模块
1. 单击模块列表上方的&#x200B;**+**&#x200B;并选择&#x200B;**Web**
1. 作为Web资源目录，选择项目的`content/src/main/content/jcr_root subdirectory`，如下面的屏幕快照所示。

![chlimage_1-48](assets/chlimage_1-48a.png)

#### 安装JSR45支持插件{#install-the-jsr-support-plugin}

1. 转到IntelliJ IDEA设置中的&#x200B;**插件**&#x200B;窗格
1. 导航到&#x200B;**JSR45 Integration**&#x200B;插件并选中它旁边的复选框
1. 单击&#x200B;**应用**
1. 请求重新启动IntelliJ IDEA

![chlimage_1-49](assets/chlimage_1-49a.png)

#### 配置调试用户档案{#configure-a-debug-profile}

1. 转至&#x200B;**运行->编辑配置**
1. 点击&#x200B;**+**&#x200B;并选择&#x200B;**JSR45 Remote**
1. 在配置对话框中，选择&#x200B;**应用程序服务器**&#x200B;旁边的&#x200B;**配置**&#x200B;并配置通用服务器
1. 如果要在开始调试时打开浏览器，请将开始页设置为相应的URL
1. 如果使用vlt自动同步，请在启动&#x200B;**任务之前删除所有**&#x200B;任务，如果不使用vlt自动同步，则请配置相应的Maven
1. 在&#x200B;**启动／连接**&#x200B;窗格中，根据需要调整端口
1. 复制IntelliJ IDEA建议的命令行参数

![chlimage_1-50](assets/chlimage_1-50a.png) ![chlimage_1-51](assets/chlimage_1-51a.png)

#### 为调试模式{#configure-aem-for-debug-mode}配置AEM

最后一步是开始AEM使用IntelliJ IDEA提出的JVM选项。

为此，可以直接启动AEM jar文件并添加这些选项，例如使用以下命令行：

`java -Xdebug -Xrunjdwp:transport=dt_socket,address=58242,suspend=n,server=y -Xmx1024m -XX:MaxPermSize=256M -jar cq-quickstart-5.6.1.jar`

您还可以将这些选项添加到`crx-quickstart/bin/start`中的开始脚本，如下所示。

```shell
# ...

# default JVM options
if [ -z "$CQ_JVM_OPTS" ]; then
 CQ_JVM_OPTS='-server -Xmx1024m -XX:MaxPermSize=256M -Djava.awt.headless=true'
fi

CQ_JVM_OPTS="$CQ_JVM_OPTS -Xdebug -Xrunjdwp:transport=dt_socket,address=58242,suspend=n,server=y"

# ...
```

#### 开始调试{#start-debugging}

现在，您已全部设置为在AEM中调试JSP。

1. 选择&#x200B;**运行->调试->调试用户档案**
1. 在组件代码中设置断点
1. 在浏览器中访问页面

![chlimage_1-52](assets/chlimage_1-52a.png)

### 使用IntelliJ IDEA {#debugging-bundles-with-intellij-idea}调试捆绑包

可以使用标准通用远程调试连接调试捆绑包中的代码。 您可以按照远程调试](https://www.jetbrains.com/idea/webhelp/run-debug-configuration-remote.html)上的[Jetbrain文档操作。
