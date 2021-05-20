---
title: 为AEM Forms应用程序设置环境
seo-title: 为AEM Forms应用程序设置环境
description: 用于构建和部署AEM Forms应用程序的硬件、软件和许可证。
seo-description: 用于构建和部署AEM Forms应用程序的硬件、软件和许可证。
uuid: 4123a6b7-5766-476c-9afb-f57029b148ad
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: e6b01ade-7ea3-42a7-872d-cc35a3d2782a
docset: aem65
exl-id: 1d1f9db2-83cf-4612-ac8c-d2638c3bbaea
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---

# 为AEM Forms应用程序设置环境{#set-up-environment-for-aem-forms-app}

您需要以下硬件、软件和许可证才能构建和部署AEM Forms应用程序：

## 对于Windows设备{#for-windows-devices}

* Microsoft Windows 10
* Microsoft Visual Studio 2015
* 适用于Apache Cordova的Microsoft Visual Studio Tools

## 对于iOS设备{#for-ios-devices}

* 运行Mac OS X 10.9.5或更高版本的基于Intel的Apple Mac
* iOS SDK 8.4或更高版本
* Xcode版本：适用于OS X或更高版本的Xcode 6.4
* iOS开发人员企业计划的会员资格
* 用于分发内部iOS应用程序的企业证书
* 带iOS 8.4或更高版本的Apple iPad

## 对于Android设备{#for-android-devices}

* Android开发工具包（ADT包），可从[https://developer.android.com/sdk/index.html](https://developer.android.com/sdk/index.html)下载
* 如果在MAC系统上设置了环境，则应将ADT安装在Applications文件夹中。
* 如果ADT安装在MAC上的任何其他位置，或者如果环境是在Windows系统上设置的，则需要在`local.properties`文件中更新ADT SDK路径，该文件位于提取的源存档`mobileworkspace-src.zip`的`src\android`文件夹中。 在此文件中，将`sdk.dir`变量指向桌面上的ADT SDK位置。

>[!NOTE]
>
>adobe-lc-mobileworkspace-src.zip包含PhoneGap SDK 5.0。请确保未预安装PhoneGap SDK。
