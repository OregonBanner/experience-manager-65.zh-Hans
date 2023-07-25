---
title: 在自适应表单中使用CAPTCHA
seo-title: Using CAPTCHA in adaptive forms
description: 了解如何在自适应表单中配置AEM验证码或Google reCAPTCHA服务。
seo-description: Learn how to configure AEM CAPTCHA or Google reCAPTCHA service in adaptive forms.
uuid: 0e11e98a-12ac-484c-b77f-88ebdf0f40e5
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: adaptive_forms, author
discoiquuid: 4c53dfc0-25ca-419d-abfe-cf31fc6ebf61
docset: aem65
feature: Adaptive Forms
exl-id: 9b4219b8-d5eb-4099-b205-d98d84e0c249
source-git-commit: 498fb5f6f923710a907e1cf525f56f49850e16b2
workflow-type: tm+mt
source-wordcount: '1995'
ht-degree: 0%

---

# 在自适应表单中使用CAPTCHA{#using-captcha-in-adaptive-forms}

|版本 |文章链接 | |青瓦-------- |青瓦---------------------------- | | AEMAS A CLOUD SERVICE |    [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/add-components-to-an-adaptive-form/captcha-adaptive-forms.html)                  | | AEM 6.5 |本文 |
=======
<span class="preview"> Adobe建议使用现代化的、可扩展的数据捕获 [核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html) 对象 [创建新的自适应Forms](/help/forms/using/create-an-adaptive-form-core-components.md) 或 [将自适应Forms添加到AEM Sites页面](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). 这些组件在创建自适应Forms方面实现了重大进步，确保了令人印象深刻的用户体验。 本文介绍了使用基础组件创作自适应Forms的旧方法。 </span>


CAPTCHA（完全自动化公共图灵测试，用于区分计算机和人类）是一种在线交易中常用的程序，用于区分人类和自动化程序或机器人。 它会提出挑战，并评估用户响应以确定是人类还是机器人与网站交互。 它可以在测试失败时阻止用户继续操作，并通过阻止机器人发送垃圾邮件或恶意目的，帮助确保在线交易的安全。

AEM Forms支持自适应表单中的验证码。 您可以使用Google的reCAPTCHA服务来实施CAPTCHA。

>[!NOTE]
>
>* AEM Forms支持reCAPTCHA v2和enterprise。 不支持任何其他版本。
>* AEM Forms应用程序在离线模式下不支持自适应表单中的验证码。

## 通过Google为自适应Forms配置reCAPTCHA服务 {#google-reCAPTCHA}

AEM Forms用户可以使用Google的reCAPTCHA服务在自适应表单中实施CAPTCHA。 它提供高级验证码功能以保护您的站点。 有关reCAPTCHA工作方式的更多信息，请参阅 [Google reCAPTCHA](https://developers.google.com/recaptcha/). reCAPTCHA服务（包括reCAPTCHA v2和reCAPTCHA Enterprise）集成到AEM Forms中。 根据要求，您可以配置reCAPTCHA服务以启用：

* [AEM Forms中的reCAPTCHA Enterprise](#steps-to-implement-reCAPTCHA-enterprise-in-forms)
* [AEM Forms中的reCAPTCHA v2](#steps-to-implement-reCAPTCHA-v2-in-forms)

![reCAPTCHA](/help/forms/using/assets/recaptcha_new.png)

### 配置reCAPTCHA Enterprise  {#steps-to-implement-reCAPTCHA-enterprise-in-forms}

1. 创建 [reCAPTCHA企业项目](https://cloud.google.com/recaptcha-enterprise/docs/set-up-non-google-cloud-environments-api-keys#before-you-begin) 启用方式 [reCAPTCHA Enterprise API](https://cloud.google.com/recaptcha-enterprise/docs/set-up-non-google-cloud-environments-api-keys#enable-the-recaptcha-enterprise-api).
1. [获取](https://support.google.com/googleapi/answer/7014113?hl=en#:~:text=To%20locate%20your%20project%20ID,a%20member%20of%20are%20displayed) 项目ID
1. 创建 [API密钥](https://cloud.google.com/recaptcha-enterprise/docs/set-up-non-google-cloud-environments-api-keys#create_an_api_key) 和 [网站的站点密钥](https://cloud.google.com/recaptcha-enterprise/docs/create-key#create-key).
1. 为云服务创建配置容器。

   1. 转到 **[!UICONTROL “工具”>“常规”>“配置浏览器”]**. 请参阅 [配置浏览器](/help/sites-administering/configurations.md) 文档，以了解更多信息。
   1. 执行以下操作可为云配置启用全局文件夹，或跳过此步骤为云服务配置创建和配置其他文件夹。
      1. 在配置浏览器中，选择 **[!UICONTROL 全局]** 文件夹并点按 **[!UICONTROL 属性]**.
      1. 在配置属性对话框中，启用 **[!UICONTROL 云配置]**.
      1. 点按 **[!UICONTROL 保存并关闭]** 保存配置并退出对话框。

   1. 在配置浏览器中，点按 **[!UICONTROL 创建]**.
   1. 在创建配置对话框中，指定文件夹的标题并启用 **[!UICONTROL 云配置]**.
   1. 点按 **[!UICONTROL 创建]** 以创建为云服务配置启用的文件夹。
1. 为reCAPTCHA Enterprise配置云服务。

   1. 在您的Experience Manager创作实例上，转到 ![tools-1](assets/tools-1.png) > **[!UICONTROL Cloud Services]**.
   1. 点按 **[!UICONTROL reCAPTCHA]**. 此时将打开“配置”页。 选择在上一步中创建的配置容器并点按 **[!UICONTROL 创建]**.
   1. 选择version作为reCAPTCHA Enterprise ，并为reCAPTCHA Enterprise服务指定名称、项目ID、站点密钥和API密钥（在步骤2和3中获得）。
   1. 选择密钥类型，则密钥类型应与在Google云项目中配置的站点密钥相同，例如， **复选框站点键** 或 **基于得分的网站密钥**.
   1. 指定介于0到1之间的阈值分数([单击以了解有关得分的更多信息](https://cloud.google.com/recaptcha-enterprise/docs/interpret-assessment#interpret_scores))。 分数大于或等于阈值分数标识人交互，否则被视为机器人交互。

      > 注意:
      >
      > * 表单作者可以在适合不间断表单提交的范围中指定一个分数。

   1. 点按 **[!UICONTROL 创建]** 以创建云服务配置。

   1. 在“编辑组件”对话框中，指定名称、项目ID、站点密钥、API密钥（在步骤2和3中获得），选择密钥类型，然后输入阈值分数。 点按 **[!UICONTROL 保存设置]** 然后点按 **[!UICONTROL 确定]** 以完成配置。

启用reCAPTCHA Enterprise服务后，就可以在自适应表单中使用。 参见 [在自适应表单中使用CAPTCHA](#using-reCAPTCHA).

![reCAPTCHA Enterprise](/help/forms/using/assets/recaptcha1-enterprise.png)


### 配置Google reCAPTCHA v2 {#steps-to-implement-reCAPTCHA-v2-in-forms}

1. 获取 [reCAPTCHA API密钥对](https://www.google.com/recaptcha/admin) 来自Google的。 它包括 **站点密钥** 和 **密钥**.
1. 为云服务创建配置容器。
   1. 转到 **[!UICONTROL “工具”>“常规”>“配置浏览器”]**. 请参阅 [配置浏览器](/help/sites-administering/configurations.md) 文档，以了解更多信息。
   1. 执行以下操作可为云配置启用全局文件夹，或跳过此步骤为云服务配置创建和配置其他文件夹。

      1. 在配置浏览器中，选择 **[!UICONTROL 全局]** 文件夹并点按 **[!UICONTROL 属性]**.

      1. 在配置属性对话框中，启用 **[!UICONTROL 云配置]**.
      1. 点按 **[!UICONTROL 保存并关闭]** 保存配置并退出对话框。

   1. 在配置浏览器中，点按 **[!UICONTROL 创建]**.
   1. 在创建配置对话框中，指定文件夹的标题并启用 **[!UICONTROL 云配置]**.
   1. 点按 **[!UICONTROL 创建]** 以创建为云服务配置启用的文件夹。

1. 为reCAPTCHA v2配置云服务。

   1. 在您的AEM创作实例上，转到 ![tools-1](assets/tools-1.png) > **Cloud Services**.
   1. 点按 **[!UICONTROL reCAPTCHA]**. 此时将打开“配置”页。 选择在上一步中创建的配置容器并点按 **[!UICONTROL 创建]**.
   1. 将version选择为reCAPTCHA v2，指定reCAPTCHA服务（在步骤1中获得）的名称、站点密钥和密钥，然后点击 **[!UICONTROL 创建]** 以创建云服务配置。
   1. 在“编辑组件”对话框中，指定在步骤1中获取的站点密钥和密钥。 点按 **[!UICONTROL 保存设置]** 然后点按 **确定** 以完成配置。

   配置reCAPTCHA服务后，便可在自适应表单中使用。 有关更多信息，请参阅 [在自适应表单中使用CAPTCHA](#using-captcha).

![reCAPTCHA v2](/help/forms/using/assets/recaptcha-v2.png)


## 在自适应表单中使用reCAPTCHA {#using-reCAPTCHA}

要在自适应表单中使用reCAPTCHA，请执行以下操作：

1. 在编辑模式下打开自适应表单。

   >[!NOTE]
   >
   >确保在创建自适应表单时选择的配置容器包含reCAPTCHA云服务。 您还可以编辑自适应表单属性，以更改与表单关联的配置容器。

1. 在组件浏览器中，拖放 **验证码** 组件到自适应表单上。

   >[!NOTE]
   >
   >不支持在自适应表单中使用多个验证码组件。 此外，不建议在标记为延迟加载的面板或片段中使用验证码。

   >[!NOTE]
   >
   >验证码对时间敏感，大约一分钟后过期。 因此，建议在自适应表单中将Captcha组件放在提交按钮之前。

1. 选择您添加的Captcha组件并点按 ![cmppr](assets/cmppr.png) 以编辑其属性。
1. 指定CAPTCHA小部件的标题。 默认值为 **验证码**. 选择 **隐藏标题** 如果您不想显示标题。
1. 从 **验证码服务** 下拉列表，选择 **reCAPTCHA** 启用reCAPTCHA服务（如果已按中的说明进行配置） [Google提供的reCAPTCHA服务](#google-reCAPTCHA).
1. 从“设置”下拉列表中选择一个配置。
1. **如果所选配置具有reCAPTCHA Enterprise版本**：
   1. 您可以通过选择reCAPTCHA云配置 **键类型** 作为 **复选框**. 在复选框键中，如果验证码验证失败，自定义错误消息将作为内联消息显示。 您可以选择大小为 **[!UICONTROL 普通]** 和 **[!UICONTROL 紧凑]**.
   1. 您可以通过选择reCAPTCHA云配置 **键类型** 作为 **基于得分**. 在基于得分的键类型中，如果captcha验证失败，自定义错误消息将显示为弹出消息。
   1. 当您选择 **[!UICONTROL 绑定引用]** 提交的数据是绑定的数据，否则就是未绑定的数据。 下面是提交表单时未绑定数据和绑定数据（将绑定引用作为SSN）的XML示例。

      ```xml
          <?xml version="1.0" encoding="UTF-8" standalone="no"?>
          <afData>
          <afUnboundData>
              <data>
                  <captcha16820607953761>
                      <captchaType>reCAPTCHAEnterprise</captchaType>
                      <captchaScore>0.9</captchaScore>
                  </captcha16820607953761>
              </data>
          </afUnboundData>
          <afBoundData>
              <Root
                  xmlns:xfa="http://www.xfa.org/schema/xfa-data/1.0/"
                  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
                  <PersonalDetails>
                      <SSN>371237912</SSN>
                      <FirstName>Sarah </FirstName>
                      <LastName>Smith</LastName>
                  </PersonalDetails>
                  <OtherInfo>
                      <City>California</City>
                      <Address>54 Residency</Address>
                      <State>USA</State>
                      <Zip>123112</Zip>
                  </OtherInfo>
              </Root>
          </afBoundData>
          <afSubmissionInfo>
              <stateOverrides/>
              <signers/>
              <afPath>/content/dam/formsanddocuments/captcha-form</afPath>
              <afSubmissionTime>20230608034928</afSubmissionTime>
          </afSubmissionInfo>
          </afData>
      ```


      ```xml
          <?xml version="1.0" encoding="UTF-8" standalone="no"?>
          <afData>
          <afUnboundData>
              <data/>
          </afUnboundData>
          <afBoundData>
              <Root
                  xmlns:xfa="http://www.xfa.org/schema/xfa-data/1.0/"
                  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
                  <PersonalDetails>
                      <SSN>
                          <captchaType>reCAPTCHAEnterprise</captchaType>
                          <captchaScore>0.9</captchaScore>
                      </SSN>
                      <FirstName>Sarah</FirstName>
                      <LastName>Smith</LastName>
                  </PersonalDetails>
                  <OtherInfo>
                      <City>California</City>
                      <Address>54 Residency</Address>
                      <State>USA</State>
                      <Zip>123112</Zip>
                  </OtherInfo>
              </Root>
          </afBoundData>
          <afSubmissionInfo>
              <stateOverrides/>
              <signers/>
              <afPath>/content/dam/formsanddocuments/captcha-form</afPath>
              <afSubmissionTime>20230608035111</afSubmissionTime>
          </afSubmissionInfo>
          </afData>
      ```


   **如果所选配置具有reCAPTCHA v2版本**：
   1. 选择大小为 **[!UICONTROL 普通]** 或 **[!UICONTROL 紧凑]** 用于reCAPTCHA构件。 您也可以选择 **[!UICONTROL 不可见]** 选项仅在可疑活动的情况下显示CAPTCHA质询。 此 **受reCAPTCHA保护** 徽章，如下所示，显示在受保护的表单上。

      ![受reCAPTCHA徽章保护的Google](/help/forms/using/assets/google-recaptcha-v2.png)


   已在自适应表单上启用reCAPTCHA服务。 您可以预览表单并查看验证码是否正常工作。

1. 保存属性。

>[!NOTE]
> 
> 不选择 **[!UICONTROL 默认]** 从Captcha服务下拉列表中，默认的AEM CAPTCHA服务已弃用。

### 根据规则显示或隐藏验证码组件 {#show-hide-captcha}

您可以选择根据应用于自适应表单中组件的规则显示或隐藏CAPTCHA组件。 点按组件，选择 ![编辑规则](assets/edit-rules-icon.svg)，然后点按 **[!UICONTROL 创建]** 创建规则。 有关创建规则的更多信息，请参阅 [规则编辑器](rule-editor.md).

例如，仅当表单中的货币值字段的值超过25000时，CAPTCHA组件才必须在自适应表单中显示。

点按 **[!UICONTROL 货币值]** 字段，并创建以下规则：

![显示或隐藏规则](assets/rules-show-hide-captcha.png)

>[!NOTE]
>
> * 如果选择reCAPTCHA v2配置且大小为 **[!UICONTROL 不可见]** 或reCAPTCHA基于企业得分的键值，则显示/隐藏选项不适用。

### 验证验证码 {#validate-captcha}

您可以在提交表单时验证自适应表单中的CAPTCHA，也可以根据用户操作和条件进行CAPTCHA验证。

#### 在提交表单时验证验证码 {#validation-form-submission}

要在提交自适应表单时自动验证验证码，请执行以下操作：

1. 点按CAPTCHA组件并选择 ![cmppr](assets/configure-icon.svg) 查看组件属性。
1. 在 **[!UICONTROL 验证验证码]** 部分，选择 **[!UICONTROL 在提交表单时验证验证码]**.
1. 点按 ![完成](assets/save_icon.svg) 以保存组件属性。

#### 在用户操作和条件上验证验证码 {#validate-captcha-user-action}

要根据条件和用户操作验证验证码，请执行以下操作：

1. 点按CAPTCHA组件并选择 ![cmppr](assets/configure-icon.svg) 查看组件属性。
1. 在 **[!UICONTROL 验证验证码]** 部分，选择 **[!UICONTROL 在用户操作时验证验证码]**.
1. 点按 ![完成](assets/save_icon.svg) 以保存组件属性。

   >[!NOTE]
   >
   >
   > 如果选择reCAPTCHA v2配置且大小为 **[!UICONTROL 不可见]** 或reCAPTCHA Enterprise基于得分的密钥，则用户操作上的“有效Captcha”不适用。

[!DNL Experience Manager Forms] 提供 `ValidateCAPTCHA` 用于使用预定义条件验证CAPTCHA的API。 您可以使用自定义提交操作或通过定义自适应表单中组件的规则来调用API。

以下示例为 `ValidateCAPTCHA` 用于使用预定义条件验证CAPTCHA的API：

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

此示例表明 `ValidateCAPTCHA` 仅当用户在填写表单时指定的数字框中的数字位数大于5时，API才会验证表单中的验证码。

**选项1：使用 [!DNL Experience Manager Forms] ValidateCAPTCHA API使用自定义提交操作验证验证码**

执行以下步骤以使用 `ValidateCAPTCHA` 使用自定义提交操作验证CAPTCHA的API：

1. 添加脚本以包含 `ValidateCAPTCHA` 用于自定义提交操作的API。 有关自定义提交操作的更多信息，请参阅 [为自适应Forms创建自定义提交操作](custom-submit-action-form.md).
1. 从中选择自定义提交操作的名称 **[!UICONTROL 提交操作]** 中的下拉列表 **[!UICONTROL 提交]** 自适应表单的属性。
1. 点按 **[!UICONTROL 提交]**. 验证码将根据 `ValidateCAPTCHA` 自定义提交操作的API。

**选项2：使用 [!DNL Experience Manager Forms] ValidateCAPTCHA API用于在提交表单之前对用户操作验证验证码**

您还可以调用 `ValidateCAPTCHA` API，方法是对自适应表单中的组件应用规则。

例如，您添加 **[!UICONTROL 验证验证码]** 按钮，并创建规则以在单击按钮时调用服务。

下图说明了在单击服务时如何调用服务 **[!UICONTROL 验证验证码]** 按钮：

![验证验证码](assets/captcha-validation1.gif)

您可以调用包含以下内容的自定义servlet `ValidateCAPTCHA` 使用规则编辑器的API，并根据验证结果启用或禁用自适应表单的提交按钮。

同样，您可以使用规则编辑器在自适应表单中包含用于验证验证码的自定义方法。

### 添加自定义验证码服务 {#add-custom-captcha-service}

[!DNL Experience Manager Forms] 提供reCAPTCHA作为CAPTCHA服务。 但是，您可以添加自定义服务以在 **[!UICONTROL CAPTCHA服务]** 下拉列表。

以下是向自适应表单添加其他CAPTCHA服务的界面的实现示例：

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

`captchaPropertyNodePath` 指Sling存储库中CAPTCHA组件的资源路径。 此属性用于包含特定于CAPTCHA组件的详细信息。 例如， `captchaPropertyNodePath` 包含有关在CAPTCHA组件上配置的reCAPTCHA云配置的信息。 云配置信息提供 **[!UICONTROL 站点密钥]** 和 **[!UICONTROL 密钥]** 用于实施reCAPTCHA服务的设置。

`userResponseToken` 是指 `g_reCAPTCHA_response` 在表单中求解验证码后生成的验证码。
