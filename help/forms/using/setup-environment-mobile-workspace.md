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
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# 为AEM Forms应用程序设置环境{#set-up-environment-for-aem-forms-app}

构建和部署AEM Forms应用程序需要以下硬件、软件和许可证：

## 对于Windows设备 {#for-windows-devices}

* Microsoft Windows 10
* Microsoft Visual Studio 2015
* 适用于Apache Cordova的Microsoft Visual Studio工具

## 对于iOS设备 {#for-ios-devices}

* 运行Mac OS X 10.9.5或更高版本的基于Intel的Apple Mac
* iOS SDK 8.4或更高版本
* Xcode版本：适用于OS X或更高版本的Xcode 6.4
* iOS开发人员企业项目的会员资格
* 用于分发内部iOS应用程序的企业证书
* 带有iOS 8.4或更高版本的Apple iPad

## 对于Android设备 {#for-android-devices}

* Android Development Toolkit（ADT捆绑包），可从https://developer.android.com/sdk/index.html下载 [它](https://developer.android.com/sdk/index.html)
* 如果环境是在MAC系统上设置的，则ADT应安装在“Applications”（应用程序）文件夹中。
* 如果ADT安装在MAC上的任何其他位置，或者环境在Windows系统上设置，则需要在解压缩的源归档文件中的文件夹中更新ADT SDK路径 `local.properties``src\android``mobileworkspace-src.zip`。 在此文件中，将变量指 `sdk.dir` 向桌面上的ADT SDK位置。

>[!NOTE]
>
>adobe-lc-mobileworkspace-src.zip包含PhoneGap SDK 5.0。确保未预安装PhoneGap SDK。
