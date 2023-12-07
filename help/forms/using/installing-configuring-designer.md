---
title: 安装和配置设计器
description: Designer作为独立安装程序提供，并且与Workbench捆绑在一起。 了解如何安装独立设计器。
contentOwner: gtalwar
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: designer
geptopics: SG_AEMFORMS/categories/jee
docset: aem65
role: Admin
exl-id: 90503d29-e079-43f4-a5dc-ce90ed7844c6
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 0%

---

# 安装和配置设计器{#installing-and-configuring-designer}

## 先决条件 {#pre-requisites}

* 安装32位版本的  [Visual C++ 2019可再分发(x86)](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170). 在开始安装之前，请确保已安装前面提到的可再分发运行时包。
* 具有安装或卸载AEM Forms Designer管理员权限的用户。

## 安装AEM Forms Designer {#install-designer}

Designer作为独立安装程序提供，并且与WorkBench捆绑在一起。 如果您使用的是独立的AEM Forms Designer安装程序，请执行以下步骤：

1. 卸载以前版本的AEM Forms Designer（如果已安装）。
1. 下载设计器 [Adobe授权网站](https://licensing.adobe.com/).

   >[!NOTE]
   >
   > * 从Adobe Experience Manager 6.5 Forms Service Pack 15 (6.5.15.0)版本开始，Forms Designer版本还包含Service Pack版本。 例如，对于Service Pack 15，版本号为6.5.15.20221112.1.0。在此示例中，6.5.15是Service Pack版本。

1. 通过双击setup.exe启动AEM Forms Designer安装程序。
1. 继续，并在“个性化”屏幕上提供您的详细信息和序列号。
1. 如果您接受许可协议，请单击“下一步”继续。
1. （可选）如果要在所选位置安装Designer，请更改默认安装路径。 单击“下一步”。
1. 单击“上一步”以更改任何首选项。 要安装设计器，请单击“安装”。
1. 安装完成后，单击“完成”。

或者，您也可以使用被动模式或静默模式，通过命令行安装AEM Forms Designer。

* 被动命令行安装：安装程序显示进度条，指示安装正在进行，但不显示提示或错误消息。 启动后，无法取消安装。

```shell
msiexec /i "<absolute path>\Designer.msi" /passive SERIALNUMBER=****-****-****-****-****-****
```

* 静默命令行安装：安装程序运行安装时不显示用户界面。 不显示提示、消息或对话框。 启动后，无法取消安装。

```shell
msiexec /i "<absolute path>\Designer.msi" /quiet SERIALNUMBER=****-****-****-****-****-****
```

## 更新AEM Forms Designer {#update-forms-designer}

在更新AEM Forms Designer 6.5.16.0的最新版本时，有两种情况：

* **用例1**：当用户的AEM Forms Designer版本低于6.5.15.0时。
* **用例2**：用户具有6.5.15.0 AEM Forms Designer版本时。

+++**当用户的AEM Forms Designer版本低于6.5.15.0时。**

如果您使用的是独立的AEM Forms Designer安装程序，请执行以下步骤：

1. 安装之前 **AEM Forms Designer 6.5.16.0**，用户必须卸载任何以前的版本。
1. 下载并安装 [AEM Forms Designer 6.5.15.0](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) 从AEM Form Releases页面。
1. 成功安装后 **AEM Forms Designer 6.5.15.0**，下载并安装 [AEM Forms Designer 6.5.16.0](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) 通过双击下载的安装程序文件。

+++

+++**当用户具有6.5.15.0 AEM Forms Designer版本时**

如果您使用的是独立的AEM Forms Designer安装程序，请执行以下步骤：
1. 从下载最新版本的AEM Forms Designer [软件分发门户](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html).
1. 通过双击下载的安装程序文件来安装最新版本的AEM Forms Designer。

+++