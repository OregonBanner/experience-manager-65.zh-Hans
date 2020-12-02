---
title: 在安装时配置管理员密码
seo-title: 在安装时配置管理员密码
description: 了解如何在AEM安装时更改管理员密码。
seo-description: 了解如何在AEM安装时更改管理员密码。
uuid: 06da9890-ed63-4fb6-88d5-fd0e16bc4ceb
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 00806e6e-3578-4caa-bafa-064f200a871f
translation-type: tm+mt
source-git-commit: 1c1ade947f2cbd26b35920cfd10b1666b132bcbd
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 0%

---


# 在安装时配置管理员密码{#configure-the-admin-password-on-installation}

## 概述 {#overview}

自6.3版起，AEM允许在安装新实例时使用命令行设置管理员密码。

在AEM的早期版本中，管理员帐户的口令以及各种其他控制台的口令必须在安装后进行更改。

此功能在安装AEM实例期间为存储库和Servlet引擎添加新管理员密码的工具，因此无需在安装后手动执行此操作。

>[!CAUTION]
>
>请注意，该功能不涵盖需要手动更改密码的Felix控制台。 有关详细信息，请参阅相关的[安全清单部分](/help/sites-administering/security-checklist.md#change-default-passwords-for-the-aem-and-osgi-console-admin-accounts)。

## 如何使用它？{#how-do-i-use-it}

如果您选择通过命令行安装AEM，则此功能将自动触发，而不是多次从文件系统资源管理器单击JAR。

从命令行运行AEM实例的常规合成是：

```shell
java -jar aem6.3.jar
```

从命令行运行实例时，您将在安装过程中看到更改管理员密码的选项：

![chlimage_1-116](assets/chlimage_1-116a.png)

>[!NOTE]
>
>更改管理员密码的提示仅在安装新AEM实例时显示。

## 使用-nointeractive标志{#using-the-nointeractive-flag}

您还可以选择从属性文件中指定密码。 这是通过使用与`-Dadmin.password.file`系统属性组合的`-nointeractive`标志来完成的。

以下是一个示例：

```shell
java -Dadmin.password.file =/path/to/passwordfile.properties -jar aem6.3.jar -nointeractive
```

`passwordfile.properties`文件中的口令必须采用以下格式：

```xml
admin.password = 12345678
```

>[!NOTE]
>
>如果您只使用`-nointeractive`参数而不使用`-Dadmin.password.file`系统属性，AEM将使用默认的管理员密码，而不要求您更改它，实际上是从先前版本复制行为。 此非交互式模式可用于使用安装脚本中的命令行进行自动安装。

