---
title: 在安装时配置管理员密码
seo-title: 在安装时配置管理员密码
description: 了解如何在AEM安装中更改管理员密码。
seo-description: 了解如何在AEM安装中更改管理员密码。
uuid: 06da9890-ed63-4fb6-88d5-fd0e16bc4ceb
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 00806e6e-3578-4caa-bafa-064f200a871f
exl-id: b55ff9d5-8139-4ecf-ba09-5cf88207c5c4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 0%

---

# 在安装{#configure-the-admin-password-on-installation}时配置管理员密码

## 概述 {#overview}

自版本6.3起，在安装新实例时，AEM允许使用命令行设置管理员密码。

对于AEM的早期版本，安装后必须更改管理员帐户的密码以及其他各种控制台的密码。

此功能添加了在安装AEM实例期间为存储库和Servlet引擎设置新管理员密码的功能，从而无需在安装后手动执行该操作。

>[!CAUTION]
>
>请注意，该功能未涵盖需要手动更改密码的Felix控制台。 有关更多信息，请参阅相关的[安全检查列表部分](/help/sites-administering/security-checklist.md#change-default-passwords-for-the-aem-and-osgi-console-admin-accounts)。

## 如何使用它？{#how-do-i-use-it}

如果您选择通过命令行安装AEM，而不是从文件系统资源管理器双击JAR，则此功能将自动触发。

从命令行运行AEM实例的常规合成是：

```shell
java -jar aem6.3.jar
```

从命令行运行实例时，您将看到在安装过程中更改管理员密码的选项：

![chlimage_1-116](assets/chlimage_1-116a.png)

>[!NOTE]
>
>只有在安装新AEM实例时，才会显示更改管理员密码的提示。

## 使用 — nointeractive标记{#using-the-nointeractive-flag}

您还可以选择从属性文件中指定密码。 这可以通过使用`-nointeractive`标记和`-Dadmin.password.file`系统属性来完成。

以下示例：

```shell
java -Dadmin.password.file =/path/to/passwordfile.properties -jar aem6.3.jar -nointeractive
```

`passwordfile.properties`文件内的密码需要具有以下格式：

```xml
admin.password = 12345678
```

>[!NOTE]
>
>如果您只是使用`-nointeractive`参数而不使用`-Dadmin.password.file`系统属性，则AEM将使用默认的管理员密码，而不要求您更改该密码，实际上就是复制早期版本中的行为。 此非交互式模式可用于使用安装脚本中的命令行进行自动安装。
