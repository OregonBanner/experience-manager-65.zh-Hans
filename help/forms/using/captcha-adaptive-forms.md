---
title: 在自适应表单中使用CAPTCHA
seo-title: 在自适应表单中使用CAPTCHA
description: 了解如何在自适应表单中配置AEM CAPTCHA或Google reCAPTCHA服务。
seo-description: 了解如何在自适应表单中配置AEM CAPTCHA或Google reCAPTCHA服务。
uuid: 0e11e98a-12ac-484c-b77f-88ebdf0f40e5
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 4c53dfc0-25ca-419d-abfe-cf31fc6ebf61
docset: aem65
translation-type: tm+mt
source-git-commit: ebf3f34af7da6b1a659ac8d8843152b97f30b652
workflow-type: tm+mt
source-wordcount: '665'
ht-degree: 0%

---


# 在自适应表单中使用CAPTCHA{#using-captcha-in-adaptive-forms}

CAPTCHA(Completely Automated Public Turing test to tell Computers and Humans Apart)是在线交易中常用的项目，用于区分人和自动项目或机器人程序。 它提出了挑战并评估用户响应，以确定它是人还是机器人与站点交互。 它可防止用户在测试失败时继续操作，并防止蠕虫程序发布垃圾邮件或恶意用途，从而确保在线交易的安全。

AEM Forms支持自适应表单中的CAPTCHA。 您可以使用Google的reCAPTCHA服务来实施CAPTCHA。

>[!NOTE]
>
>* AEM Forms仅支持reCaptcha v2。 不支持任何其他版本。
>* 在AEM Forms应用程序的脱机模式下，不支持自适应表单中的CAPTCHA。

>



## 配置ReCAPTCHA服务（由Google提供） {#google-recaptcha}

表单作者可以使用Google的reCAPTCHA服务在自适应表单中实施CAPTCHA。 它优惠高级CAPTCHA功能来保护您的站点。 有关reCAPTCHA工作方式的更多信息，请 [参阅Google reCAPTCHA](https://developers.google.com/recaptcha/)。

![Recaptcha](assets/recaptcha_new.png)

要在AEM Forms中实施reCAPTCHA服务：

1. 从 [Google获取reCAPTCHA API密钥](https://www.google.com/recaptcha/admin) 对。 它包括一个站点密钥和一个秘密。
1. 创建云服务的配置容器。

   1. 转到“工 **[!UICONTROL 具”>“常规”>“配置浏览器”]**。
   1. 执行以下操作以启用云配置的全局文件夹，或跳过此步骤，为云服务配置创建和配置其他文件夹。

      1. 在配置浏览器中，选择全 **[!UICONTROL 局文]** 件夹并点 **[!UICONTROL 按属性]**。

      1. 在配置属性对话框中，启用 **[!UICONTROL 云配置]**。
      1. 点按 **[!UICONTROL 保存并关闭]** ，以保存配置并退出对话框。
   1. 在配置浏览器中，点按 **[!UICONTROL 创建]**。
   1. 在创建配置对话框中，指定文件夹的标题并启用云 **[!UICONTROL 配置]**。
   1. 点按 **[!UICONTROL 创建]** ，以创建为云服务配置启用的文件夹。


1. 为reCAPTCHA配置云服务。

   1. 在您的AEM作者实例中，转 ![到tools-1](assets/tools-1.png) > **Cloud Service**。
   1. 点击 **[!UICONTROL reCAPTCHA]**。 此时将打开“配置”页。 选择在上一步中创建的配置容器，然后点 **[!UICONTROL 按创建]**。
   1. 为reCAPTCHA服务指定名称、站点密钥和密钥，然后点 **[!UICONTROL 按创建]** ，以创建云服务配置。
   1. 在编辑组件对话框中，指定在步骤1中获取的站点和密钥。 点按 **保存设置** ，然后点 **按确** 定以完成配置。

   配置reCAPTCHA服务后，即可在自适应表单中使用。 有关详细信息，请参 [阅在自适应表单中使用CAPTCHA](#using-captcha)。

## 在自适应表单中使用CAPTCHA {#using-captcha}

要在自适应表单中使用CAPTCHA:

1. 在编辑模式下打开自适应表单。

   >[!NOTE]
   >
   >确保在创建自适应表单时选择的配置容器包含reCAPTCHA云服务。 您还可以编辑自适应表单属性以更改与表单关联的配置容器。

1. 从组件浏览器中，将Captcha组 **件拖** 放到自适应表单上。

   >[!NOTE]
   >
   >不支持在自适应表单中使用多个Captcha组件。 此外，不建议在标记为延迟加载的面板或片段中使用CAPTCHA。

   >[!NOTE]
   >
   >Captcha是时间敏感型的，约一分钟后过期。 因此，建议将Captcha组件放在自适应表单中“提交”按钮之前。

1. 选择您添加的Captcha组件，然后点 ![按](assets/cmppr.png) cmppr以编辑其属性。
1. 指定CAPTCHA构件的标题。 The default value is **Captcha**. 如果 **不希望显** 示标题，请选择隐藏标题。
1. 从Captcha **服务** 下拉框中，如果按Google的ReCAPTCHA服务中的说明对 **reCaptcha** 进行了配置，请选择 [reCaptcha以启用reCAPTCHA服务](#google-recaptcha)。 从设置下拉菜单中选择配置。 此外，为reCAPTCHA构件 **选择** “正常 **”或** “压缩”大小。

   >[!NOTE]
   >
   >不要从Captcha **[!UICONTROL 服务]** 下拉菜单中选择默认，因为默认的AEM CAPTCHA服务已弃用。

1. 保存属性。

reCAPTCHA服务在自适应表单上启用。 您可以预览表单并看到CAPTCHA正在运行。
