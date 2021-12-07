---
title: 安装和配置Designer
seo-title: Installing and configuring Designer
description: 'Designer可作为独立安装程序使用，并与Workbench捆绑在一起。 了解如何安装独立的Designer。  '
seo-description: Designer is available as a stand-alone installer and is also bundled with Workbench. Learn how to install stand-alone Designer.
uuid: c5b779d1-cb6a-48f4-87d6-48464753e516
contentOwner: gtalwar
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: designer
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: f3a5b5ce-2262-4d5d-a8ae-d59a3a4229e7
docset: aem65
role: Admin
exl-id: 90503d29-e079-43f4-a5dc-ce90ed7844c6
source-git-commit: a3cf926bde4a4b3a0810058e84ac01012a4a3a57
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 3%

---

# 安装和配置Designer{#installing-and-configuring-designer}

## 先决条件 {#pre-requisites}

AEM Forms Designer安装程序需要32位版本的 [Visual C++可再发行运行时包2012](https://support.microsoft.com/en-us/topic/the-latest-supported-visual-c-downloads-2647da03-1eea-4433-9aff-95f26a218cc0) 和 [Visual C++可再发行运行时包2013](https://support.microsoft.com/zh-cn/help/3179560/update-for-visual-c-2013-and-visual-c-redistributable-package). 在开始安装之前，请确保已安装之前提到的可再发行运行时包。

安装或卸载Designer需要管理员权限。

## 安装设计器 {#install-designer}

Designer可作为独立安装程序使用，并与WorkBench捆绑在一起。 如果您使用Designer的独立安装程序，请执行以下步骤：

1. 从Adobe下载Designer [许可网站](https://licensing.adobe.com/).

   >[!NOTE]
   >
   >如果安装了Designer的先前版本，请先卸载先前版本，然后再继续。

1. 通过双击setup.exe启动Designer安装程序。
1. 继续，并在“个性化”屏幕上提供您的详细信息和序列号。
1. 如果您接受许可协议，请单击“下一步”以继续。
1. （可选）如果要在所选位置安装Designer，请更改默认安装路径。 单击下一步。
1. 单击“上一步”以更改任何首选项。 要安装Designer，请单击“安装”。
1. 安装完成后，单击“完成”。

或者，也可以使用被动或静默模式通过命令行安装Designer。

* 被动命令行安装：安装程序显示一个进度条，指示安装正在进行，但未显示提示或错误消息。 启动后，将无法取消安装。

```shell
msiexec /i "<absolute path>\Designer.msi" /passive SERIALNUMBER=****-****-****-****-****-****
```

* 静默命令行安装：安装程序运行安装时不显示用户界面。 不显示提示、消息或对话框。 启动后，将无法取消安装。

```shell
msiexec /i "<absolute path>\Designer.msi" /quiet SERIALNUMBER=****-****-****-****-****-****
```


