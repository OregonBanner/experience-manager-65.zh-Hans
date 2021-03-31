---
title: 在自适应表单中使用CAPTCHA
seo-title: 在自适应表单中使用CAPTCHA
description: 了解如何在自适应表单中配置AEM CAPTCHA或Google reCAPTCHA服务。
seo-description: 了解如何在自适应表单中配置AEM CAPTCHA或Google reCAPTCHA服务。
uuid: 0e11e98a-12ac-484c-b77f-88ebdf0f40e5
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: adaptive_forms, author
discoiquuid: 4c53dfc0-25ca-419d-abfe-cf31fc6ebf61
docset: aem65
feature: 自适应表单
translation-type: tm+mt
source-git-commit: 7a3f54d90769708344e6751756b2a12ac6c962d7
workflow-type: tm+mt
source-wordcount: '1291'
ht-degree: 0%

---


# 在自适应表单中使用CAPTCHA{#using-captcha-in-adaptive-forms}

CAPTCHA(Completely Automated Public Turing test to tell Computers and Humans Apart)是在线交易中常用的项目，用于区分人类和自动项目或机器人。 它提出了挑战并评估用户响应，以确定它是人还是机器人与站点交互。 它可防止用户在测试失败时继续操作，并通过阻止蠕虫程序发布垃圾邮件或恶意内容，帮助确保在线交易安全。

AEM Forms支持自适应表单中的CAPTCHA。 您可以使用Google的reCAPTCHA服务来实施CAPTCHA。

>[!NOTE]
>
>* AEM Forms仅支持reCaptcha v2。 不支持任何其他版本。
>* 在AEM Forms应用程序的脱机模式下，不支持自适应表单中的CAPTCHA。

>



## Google {#google-recaptcha}配置ReCAPTCHA服务

表单作者可以使用Google提供的reCAPTCHA服务在自适应表单中实现CAPTCHA。 它优惠高级CAPTCHA功能以保护您的站点。 有关reCAPTCHA工作方式的详细信息，请参阅[Google reCAPTCHA](https://developers.google.com/recaptcha/)。

![Recaptcha](assets/recaptcha_new.png)

要在AEM Forms中实施reCAPTCHA服务，请执行以下操作：

1. 从Google获取[reCAPTCHA API密钥对](https://www.google.com/recaptcha/admin)。 它包含一个站点密钥和一个秘密。
1. 为云服务创建配置容器。

   1. 转到&#x200B;**[!UICONTROL 工具>常规>配置浏览器]**。
      * 有关详细信息，请参阅[配置浏览器](/help/sites-administering/configurations.md)文档。
   1. 执行以下操作以启用云配置的全局文件夹，或跳过此步骤，为云服务配置创建和配置其他文件夹。

      1. 在配置浏览器中，选择&#x200B;**[!UICONTROL global]**&#x200B;文件夹，然后点按&#x200B;**[!UICONTROL 属性]**。

      1. 在“配置属性”对话框中，启用&#x200B;**[!UICONTROL 云配置]**。
      1. 点按&#x200B;**[!UICONTROL 保存并关闭]**&#x200B;以保存配置并退出对话框。
   1. 在配置浏览器中，点按&#x200B;**[!UICONTROL 创建]**。
   1. 在创建配置对话框中，指定文件夹的标题并启用&#x200B;**[!UICONTROL 云配置]**。
   1. 点按&#x200B;**[!UICONTROL 创建]**&#x200B;以创建为云服务配置启用的文件夹。


1. 为reCAPTCHA配置云服务。

   1. 在AEM作者实例中，转至![tools-1](assets/tools-1.png) > **Cloud Services**。
   1. 点按&#x200B;**[!UICONTROL reCAPTCHA]**。 此时将打开“配置”页。 选择在上一步中创建的配置容器，然后点按&#x200B;**[!UICONTROL 创建]**。
   1. 为reCAPTCHA服务指定名称、站点密钥和密钥，然后点按&#x200B;**[!UICONTROL 创建]**&#x200B;以创建云服务配置。
   1. 在“编辑组件”对话框中，指定在步骤1中获取的站点和密钥。 点按&#x200B;**保存设置**，然后点按&#x200B;**确定**&#x200B;以完成配置。

   配置reCAPTCHA服务后，即可在自适应表单中使用。 有关详细信息，请参阅[在自适应表单中使用CAPTCHA](#using-captcha)。

## 在自适应表单{#using-captcha}中使用CAPTCHA

要在自适应表单中使用CAPTCHA:

1. 在编辑模式下打开自适应表单。

   >[!NOTE]
   >
   >确保在创建自适应表单时选择的配置容器包含reCAPTCHA云服务。 您还可以编辑自适应表单属性以更改与表单关联的配置容器。

1. 从组件浏览器中，将&#x200B;**Captcha**&#x200B;组件拖放到自适应表单上。

   >[!NOTE]
   >
   >不支持在自适应表单中使用多个Captcha组件。 此外，不建议在标记为延迟加载的面板或片段中使用CAPTCHA。

   >[!NOTE]
   >
   >Captcha是时间敏感型的，约一分钟后过期。 因此，建议将Captcha组件放在自适应表单中“提交”按钮之前。

1. 选择您添加的Captcha组件，然后点按![cmpr](assets/cmppr.png)以编辑其属性。
1. 指定CAPTCHA Widget的标题。 默认值为&#x200B;**Captcha**。 如果不希望显示标题，请选择&#x200B;**隐藏标题**。
1. 从&#x200B;**Captcha服务**&#x200B;下拉列表中，如果按Google](#google-recaptcha)的[ ReCAPTCHA服务中所述配置reCAPTCHA服务，请选择&#x200B;**reCaptcha**&#x200B;以启用reCAPTCHA服务。 从设置下拉菜单中选择配置。 此外，为reCAPTCHA Widget选择&#x200B;**Normal**&#x200B;或&#x200B;**Compact**&#x200B;大小。

   >[!NOTE]
   >
   >请勿从Captcha服务下拉菜单中选择&#x200B;**[!UICONTROL Default]**，因为默认AEM CAPTCHA服务已弃用。

1. 保存属性。

reCAPTCHA服务在自适应表单上启用。 您可以预览表单并查看CAPTCHA的运行情况。

### 根据规则{#show-hide-captcha}显示或隐藏CAPTCHA组件

您可以根据您在自适应表单中对组件应用的规则选择显示或隐藏CAPTCHA组件。 点按组件，选择![编辑规则](assets/edit-rules-icon.svg)，然后点按&#x200B;**[!UICONTROL 创建]**&#x200B;以创建规则。 有关创建规则的详细信息，请参阅[规则编辑器](rule-editor.md)。

例如，仅当表单中的“货币值”字段的值超过25000时，CAPTCHA组件才必须显示在自适应表单中。

点按表单中的&#x200B;**[!UICONTROL 货币值]**&#x200B;字段并创建以下规则：

![显示或隐藏规则](assets/rules-show-hide-captcha.png)

### 验证验证码 {#validate-captcha}

在提交表单或根据用户操作和条件进行CAPTCHA验证时，您都可以在自适应表单中验证CAPTCHA。

#### 在表单提交{#validation-form-submission}时验证CAPTCHA

要在提交自适应表单时自动验证CAPTCHA，请执行以下操作：

1. 点按CAPTCHA组件并选择![cmppr](assets/configure-icon.svg)以视图组件属性。
1. 在&#x200B;**[!UICONTROL 验证CAPTCHA]**&#x200B;部分，选择&#x200B;**[!UICONTROL 验证表单提交时的CAPTCHA]**。
1. 点按![完成](assets/save_icon.svg)以保存组件属性。

#### 验证用户操作和条件{#validate-captcha-user-action}的CAPTCHA

要根据条件和用户操作验证CAPTCHA，请执行以下操作：

1. 点按CAPTCHA组件并选择![cmppr](assets/configure-icon.svg)以视图组件属性。
1. 在&#x200B;**[!UICONTROL 验证CAPTCHA]**&#x200B;部分，选择&#x200B;**[!UICONTROL 验证用户操作]**&#x200B;上的CAPTCHA。
1. 点按![完成](assets/save_icon.svg)以保存组件属性。

[!DNL Experience Manager Forms] 提 `ValidateCAPTCHA` 供API以使用预定义条件验证CAPTCHA。您可以使用自定义提交操作或通过定义自适应表单中组件的规则来调用API。

以下是使用预定义条件验证CAPTCHA的`ValidateCAPTCHA` API的示例：

```javascript
if (slingRequest.getParameter("numericbox1614079614831").length() >= 5) {
    	GuideCaptchaValidatorProvider apiProvider = sling.getService(GuideCaptchaValidatorProvider.class);
        String formPath = slingRequest.getResource().getPath();
        String captchaData = slingRequest.getParameter(GuideConstants.GUIDE_CAPTCHA_DATA);
        if (!apiProvider.validateCAPTCHA(formPath, captchaData).isCaptchaValid()){
            response.setStatus(400);
            return;
        }
    }
```

该示例表示，仅当填写表单时用户指定的数字框中的数字数大于5时，`ValidateCAPTCHA` API才验证表单中的CAPTCHA。

**选项1:使用 [!DNL Experience Manager Forms] ValidateCAPTCHA API使用自定义提交操作验证CAPTCHA**

请执行以下步骤以使用`ValidateCAPTCHA` API使用自定义提交操作验证CAPTCHA:

1. 将包含`ValidateCAPTCHA` API的脚本添加到自定义提交操作。 有关自定义提交操作的详细信息，请参阅[为自适应Forms创建自定义提交操作](custom-submit-action-form.md)。
1. 从自适应表单的&#x200B;**[!UICONTROL 提交]**&#x200B;属性中的&#x200B;**[!UICONTROL 提交操作]**&#x200B;下拉列表中选择自定义提交操作的名称。
1. 点按&#x200B;**[!UICONTROL 提交]**。 根据自定义提交操作的`ValidateCAPTCHA` API中定义的条件验证CAPTCHA。

**选项2:在提 [!DNL Experience Manager Forms] 交表单之前，使用ValidateCAPTCHA API验证用户操作的CAPTCHA**

您还可以通过对自适应表单中的组件应用规则来调用`ValidateCAPTCHA` API。

例如，您在自适应表单中添加&#x200B;**[!UICONTROL 验证CAPTCHA]**&#x200B;按钮，并在单击按钮时创建规则以调用服务。

下图说明了如何在单击&#x200B;**[!UICONTROL 验证CAPTCHA]**&#x200B;按钮时调用服务：

![验证验证码](assets/captcha-validation1.gif)

您可以使用规则编辑器调用包含`ValidateCAPTCHA` API的自定义servlet，并根据验证结果启用或禁用自适应表单的提交按钮。

同样，您也可以使用规则编辑器包含自定义方法来验证自适应表单中的CAPTCHA。

### 添加自定义CAPTCHA服务{#add-custom-captcha-service}

[!DNL Experience Manager Forms] 提供reCAPTCHA作为CAPTCHA服务。但是，可以添加自定义服务以在&#x200B;**[!UICONTROL CAPTCHA Service]**&#x200B;下拉列表中显示。

以下是该接口的示例实现，用于向自适应表单添加其他CAPTCHA服务：

```javascript
package com.adobe.aemds.guide.service;

import org.osgi.annotation.versioning.ConsumerType;

/**
 * An interface to provide captcha validation at server side in Adaptive Form
 * This interface can be used to provide custom implementation for different captcha services.
 */
@ConsumerType
public interface GuideCaptchaValidator {
    /**
     * This method should define the actual validation logic of the captcha
     * @param captchaPropertyNodePath path to the node with CAPTCHA configurations inside form container
     * @param userResponseToken  The user response token provided by the CAPTCHA from client-side
     *
     * @return  {@link GuideCaptchaValidationResult} validation result of the captcha
     */
     GuideCaptchaValidationResult validateCaptcha(String captchaPropertyNodePath, String userResponseToken);

    /**
     * Returns the name of the captcha validator. This should be unique among the different implementations
     * @return  name of the captcha validator
     */
     String getCaptchaValidatorName();
}
```

`captchaPropertyNodePath` 指Sling存储库中CAPTCHA组件的资源路径。使用此属性可包含特定于CAPTCHA组件的详细信息。 例如，`captchaPropertyNodePath`包含在CAPTCHA组件上配置的reCAPTCHA云配置的信息。 云配置信息提供用于实现reCAPTCHA服务的&#x200B;**[!UICONTROL 站点密钥]**&#x200B;和&#x200B;**[!UICONTROL 密钥]**&#x200B;设置。

`userResponseToken` 指在表 `g_recaptcha_response` 单中解析CAPTCHA后生成的。
