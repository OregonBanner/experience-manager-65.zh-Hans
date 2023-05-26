---
title: 安装和配置Designer
seo-title: Installing and configuring Designer
description: Designer作为独立安装程序提供，并且还与Workbench捆绑在一起。 了解如何安装独立设计器。
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
source-git-commit: 1b2d743f8f2172c4e4663917d598734cb1ea1ea4
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 0%

---

# 安装和配置Designer{#installing-and-configuring-designer}

## 先决条件 {#pre-requisites}

* 安装32位版本的  [Visual C++ 2019可再分发(x86)](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170). 在开始安装之前，请确保已安装前面提到的可再发行运行时包。
* 具有安装或卸载AEM Forms Designer管理员权限的用户。

## 安装AEM Forms Designer {#install-designer}

Designer作为独立的安装程序提供，并且与WorkBench捆绑在一起。 如果您使用的是独立的AEM Forms Designer安装程序，请执行以下步骤：

1. 卸载以前版本的AEM Forms Designer（如果已安装）。
1. 从以下位置下载设计器 [Adobe授权网站](https://licensing.adobe.com/).

   >[!NOTE]
   >
   > * 从Adobe Experience Manager 6.5 Forms Service Pack 15 (6.5.15.0)版本开始，Forms Designer版本还包含Service Pack版本。 例如，对于Service Pack 15，版本号为6.5.15.20221112.1.0。在此示例中，6.5.15是Service Pack版本。


1. 通过双击setup.exe启动AEM Forms Designer安装程序。
1. 继续并在“个性化”屏幕上提供您的详细信息和序列号。
1. 如果您接受许可协议，请单击“下一步”继续。
1. （可选）如果要将Designer安装在所选的位置，请更改默认安装路径。 单击下一步。
1. 单击“上一步”以更改任何首选项。 要安装设计器，请单击“安装”。
1. 安装完成后，单击“完成”。

或者，您也可以使用被动模式或静默模式，通过命令行安装AEM Forms Designer。

* 被动命令行安装：安装程序显示一个进度条，指示安装正在进行，但不显示提示或错误消息。 启动后，无法取消安装。

```shell
msiexec /i "<absolute path>\Designer.msi" /passive SERIALNUMBER=****-****-****-****-****-****
```

* 静默命令行安装：安装程序运行安装时不显示用户界面。 不显示提示、消息或对话框。 启动后，无法取消安装。

```shell
msiexec /i "<absolute path>\Designer.msi" /quiet SERIALNUMBER=****-****-****-****-****-****
```

## 更新AEM Forms Designer {#update-forms-designer}

在更新最新版本的AEM Forms Designer 6.5.16.0时，有两种情况：

* **用例1**：用户使用的AEM Forms Designer版本低于6.5.15.0时。
* **用例2**：用户具有6.5.15.0版本的AEM Forms Designer时。

+++**用户使用的AEM Forms Designer版本低于6.5.15.0时。**

如果您使用的是独立的AEM Forms Designer安装程序，请执行以下步骤：

1. 安装之前 **AEM Forms Designer 6.5.16.0**，用户必须卸载任何以前的版本。
1. 下载并安装 [AEM Forms Designer 6.5.15.0](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) 从AEM Form版本页面。
1. 成功安装 **AEM Forms Designer 6.5.15.0**，下载并安装 [AEM Forms Designer 6.5.16.0](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) 双击下载的安装程序文件。

+++

+++**当用户具有6.5.15.0 AEM Forms Designer版本时**

如果您使用的是独立的AEM Forms Designer安装程序，请执行以下步骤：
1. 从下载最新版本的AEM Forms Designer [软件分发门户](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html).
1. 双击下载的安装程序文件，安装最新版本的AEM Forms Designer。

+++